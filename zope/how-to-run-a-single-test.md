# How can I run only a single test from the Zope test suite?

While this seems to be no Zope specific question,
as we all know how to narrow down the test selection with `pytest` (e.g. `pytest -k pattern`),
Zope does not use `pytest`, but `zope.testrunner`.

Similar to `pytest`, also `zope testrunner` offers some command line options,
see https://zopetestrunner.readthedocs.io/en/latest/getting-started.html#some-useful-command-line-options-to-get-you-started

This means, in order to run a specific test, you can use the `-t` flag,
which takes one or more regexes as input, e.g. `-t some_test`.

When developing against Zope, you can use `tox`.

Via `--` it is possible to inject extra arguments into the command run by `tox`,
see https://tox.readthedocs.io/en/latest/example/general.html

e.g.
`tox -e py38 -- -t some_test`

## further information
https://pypi.org/project/zope.testrunner/
