# How to install a Python package directly from a git branch from GitHub?

[Bernát Gábor](https://www.bernat.tech/) is currently working on a complete rewrite for [tox](https://github.com/tox-dev/tox).

I alpha-tested the latest release (4.0.0a2) and reported a couple of problems.

Within a day Bernát published some fixes on the `rewrite` branch, and asked me to test it.

That means there is no new package on `PyPI`, yet.

So, I had to install `tox` directly from Github, to be exact, from the `rewrite` branch:

```
pip install git+https://github.com/tox-dev/tox@rewrite
```

or more general

```
pip install git+https://github.com/username/repository@branch
```
