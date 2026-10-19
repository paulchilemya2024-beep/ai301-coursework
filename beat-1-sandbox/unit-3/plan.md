# Plan: issue #72 — verify_password raises UnknownHashError on malformed stored hashes

## Diagnosis

`verify_password` in `core/security.py` calls `pwd_context.verify()` directly. If the
stored hash is not recognized, Passlib raises `UnknownHashError` instead of returning
a boolean, contrary to the function's documented behavior.

## Scope

- Update `verify_password` to return `False` for `UnknownHashError`.
- Remove the `xfail` marker from the malformed-hash regression test.
- Leave password hashing, JWT code, and other callers unchanged.

## Approach

Catch only `passlib.exc.UnknownHashError` around the existing verify call. This
handles unrecognized hashes without swallowing unrelated exceptions.

## Test plan

Run `tests/unit/test_security.py` to cover the malformed hash and existing valid,
incorrect, and other security behavior.

## Deviations

None; implementation and validation matched the plan.
