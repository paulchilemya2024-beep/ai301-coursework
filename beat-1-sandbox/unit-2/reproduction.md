# Unit 2 — Claim and Reproduce

## Your identity upstream

**GitHub username**

paulchilemya2024-beep

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5903305313

I'd like to work on issue #72, where `verify_password` raises `UnknownHashError` for malformed stored hashes instead of returning `False`. I'll first check how `verify_password` handles a malformed hash and run the focused wrong-hash-format test. I haven't tried it yet; I'll post my own report with the steps and output, whether or not I can reproduce the issue.

I used GitHub Copilot to help draft this comment; I'll verify the steps and report my own results.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5903594847

Reproduction report for [issue #72](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72)

**Result: reproduced.** The issue's malformed stored hash makes `verify_password` raise `passlib.exc.UnknownHashError` instead of returning `False`.

### Environment

- Windows (win32)
- Python 3.14.4, using the repository's `.venv`
- pytest 9.1.1
- passlib 1.7.4; bcrypt 4.3.0
- Repository: `codepath/pathreview-ai301-fa26-s3`, checked out locally

I followed the repository setup guide: copied `.env.example` to `.env`, started the Docker Compose services, and ran `make setup`, which installed the Python development dependencies and frontend packages, applied migrations, and seeded the database. The setup completed; the app's frontend loaded at `http://localhost:5173/login`. The focused security test itself does not require the app or database services, but I used the documented project environment.

### Steps

From the repository root, I ran the existing issue test with its `xfail` marker bypassed so pytest would show the underlying failure:

```powershell
.\.venv\Scripts\python.exe -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv --runxfail --tb=long
```

The test calls `verify_password("password", "not_a_valid_bcrypt_hash")`.

### Observed output

The test failed at the call to `verify_password`; the traceback ended with:

```text
>       result = verify_password("password", wrong_hash)
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

tests\unit\test_security.py:227:

>       return bool(pwd_context.verify(plain_password, hashed_password))
                    ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

core\security.py:37:

>           raise exc.UnknownHashError("hash could not be identified")
E           passlib.exc.UnknownHashError: hash could not be identified

.venv\Lib\site-packages\passlib\context.py:1132: UnknownHashError

=========================== short test summary info ===========================
FAILED tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - passlib.exc.UnknownHashError: hash could not be identified
======================== 1 failed, 1 warning in 3.84s =========================
EXIT_CODE=1
```

**Expected:** the test comment says the malformed hash should be handled gracefully and return `False`.

**Actual:** `passlib.exc.UnknownHashError: hash could not be identified` escaped from `pwd_context.verify()` through `core/security.py` line 37. This is the malformed-hash behavior described in issue #72, rather than a neighboring or unrelated error.

I used GitHub Copilot to help set up the environment and organize this report; I ran the test and checked the output myself.

## Eval iterations

**Run history**

1. Initial full eval run (rubric v1) against the Unit 2 packages → 13/20 agreement, all 7 disagreements false rejects on "Claim is a promise."
2. Diagnosed: the check was reading a completed reproduction *result* paired with a stated next step as an overclaim, when only asserting a finished diagnosis or fix should fail.
3. Rewrote the check's pass condition; ran a 10-package canary (7 fixed packages + 3 known-correct rejects) → 10/10 agreement.
4. Ran the confirming full eval → 18/20, but failed the category floor: disclosure scored 0/1 on pkg-20 (a repo requiring AI-use disclosure, with a non-disclosing comment that my rubric passed).
5. Rewrote "Comments respect repo rules" to explicitly fail an absent disclosure statement under a mandatory-disclosure policy; ran a 6-package canary (pkg-20 plus 5 known-correct accepts) → 6/6.
6. Ran the confirming full eval again → 20/20, all category floors met. Saved as eval-run.txt.
7. Reviewed the claim draft against the live-mode repro-check criteria → accept.
8. Reviewed the full package against the live-mode repro-check criteria → accept. Posted both comments.

**Package analysis**

pkg-20 (ghostty-org/ghostty#13604): gold label is reject, my rubric's first version said accept. Ghostty's AI_POLICY.md requires disclosing any AI usage, naming the tool and extent. The candidate claim comment said nothing about AI at all. My rubric's "Comments respect repo rules" check only failed a comment if it found language actively violating a rule, so a comment that stayed silent on AI passed by default. Since this course's workflow is AI-assisted, silence under a mandatory-disclosure policy is itself a missed disclosure, not a neutral case. I fixed this by adding an explicit rule: when a policy requires disclosure, the absence of any disclosure statement fails the check on its own, regardless of the rest of the comment's wording.

**Check rationale**

> | Comments respect repo rules | The candidate claim and repro comments, compared with the issue thread, repo-facts contribution-policy summary, and applicable repo instructions or templates | The comments do not violate an applicable contribution rule, including any required AI-use disclosure. They describe this student's own work and do not rely on another contributor's reproduction as their proof or claim priority without evidence. Repo-required wording or fields are followed when applicable; absent a stated requirement, a particular format is not required. When the repo-facts contribution policy requires AI-use disclosure (naming the tool and extent) for the type of comment posted, the candidate comment must contain an explicit disclosure statement meeting that requirement. Under this course's AI-assisted workflow, the absence of any disclosure statement in a comment posted to a repo whose policy mandates one is itself a failure of this check — do not infer that non-disclosure is acceptable merely because the comment's wording doesn't reference AI. | required |

I added this narrow rule after pkg-20 exposed the disclosure gap. It makes silence a failure only where the repo policy requires disclosure for the type of comment being graded.

**Trade-offs**

My rubric is tuned to distinguish an honest, evidenced claim or cannot-reproduce result (which should pass) from an unsupported diagnosis or fix asserted as fact (which should fail), rather than judging by tense or report length. The trade-off is that this requires each check's pass condition to be worded very specifically around *what is being asserted*, not just *what happened* — a looser wording on "Claim is a promise" initially let genuine overclaims blend in with honest progress reports, and required rewriting before the eval could tell the two apart. The disclosure check is similarly narrow: it only fires when a policy explicitly requires disclosure, so a repo with no stated AI policy, or one that explicitly waives disclosure for issue comments, is unaffected — meaning the rubric depends on the repo-facts block accurately capturing the policy text, and would miss a disclosure requirement stated somewhere the evidence guide doesn't map to.
