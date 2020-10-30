# How to fix broken tests on Travis for pypy?

The **xenial** build of **pypy** on **Travis CI** links against **OpenSSL 1.0.2**,
which causes `pip install cryptography` to fail with

```
RuntimeError: You are linking against OpenSSL 1.0.2, which is no longer
supported by the OpenSSL project. To use this version of cryptography
you need to upgrade to a newer version of OpenSSL. For this version only
you can also set the environment variable CRYPTOGRAPHY_ALLOW_OPENSSL_102
to allow OpenSSL 1.0.2.
```

Marius found the solution, see https://github.com/zopefoundation/transaction/pull/96

## solution

Use a newer Ubuntu version, e.g. `focal`, but make sure to rename `pypy` to `pypy2`.

```
language: python
dist: focal
python:
    - 2.7
    - 3.5
    - 3.6
    - 3.7
    - 3.8
    - pypy2
    - pypy3
...
```
