# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

paulchilemya2024-beep

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-6256559333

Plan for this one, building on my reproduction at
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-[https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-6256559333)]:
`verify_password` in `core/security.py` calls `pwd_context.verify()` with no
exception handling, so a malformed hash (like `not_a_valid_bcrypt_hash`)
makes passlib raise `UnknownHashError` instead of letting the function
return `False` as its own docstring promises.

Fix is a single change: wrap that call in a try/except for
`passlib.exc.UnknownHashError` and return `False`, plus removing the
`xfail` marker from the repo's own existing test for this
(`test_verify_with_wrong_hash_format`) now that it's fixed. Nothing
else in `verify_password` or elsewhere changes.

I haven't checked whether other malformed inputs (empty string, None)
raise a different exception type -- if so, that's likely a separate
follow-up, not part of this fix.

I'll confirm the fix against both the malformed-hash case and normal
valid/invalid password checks before opening the PR, and report back
with the before/after test output.

(This plan was drafted with AI assistance, checked against my own
Unit 2 reproduction evidence before posting.)

---

## Your branch

**Branch**

fix/issue-72-malformed-password-hash


**Evidence**

Before (Unit 2 reproduction, bypassing the xfail marker to surface the real failure):

Command:
```
pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv --runxfail --tb=long
```

Output:
```
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format FAILED [100%]

================================== FAILURES ===================================
_______________ TestSecurity.test_verify_with_wrong_hash_format _______________

    def test_verify_with_wrong_hash_format(self):
        """Test verify_password with non-bcrypt hash."""
        wrong_hash = "not_a_valid_bcrypt_hash"

        # Should handle gracefully, return False
>       result = verify_password("password", wrong_hash)

core\security.py:37: in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))

passlib\context.py:1132: in identify_record
    raise exc.UnknownHashError("hash could not be identified")
E   passlib.exc.UnknownHashError: hash could not be identified

======================== 1 failed, 1 warning in 3.84s =========================
```

After (post-fix, xfail marker removed, no bypass needed):

Command:
```
pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -vv --tb=long
```

Output:
```
tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED [100%]

================ 1 passed, 1 warning in 1.25s ================
```

Full suite also re-run post-fix: 25 passed.
