# How to install release candidates

Today on Twitter, one of the core maintainers of `pytest` announced the release of `pytest 6.0.0rc1` and also asked to install and run it, and report if there are any problems.
https://twitter.com/nicoddemus/status/1281385522422784005

Ok, but how do you install a release candidate?

If you just do a `pip install pytest`, the current latest release gets installed, which is `5.4.3` as the time of writing.

Turns out, there are a couple of options...

## pip 1

```
pip install pytest==6.0.0rc1
```

## pip 2

```
pip install --pre pytest
```

## pip 3

```
pip config set install.pre true
pip install pytest
```
https://twitter.com/pradyunsg/status/1281599545202208770

## tox 1

```
deps =
    pytest==6.0.0rc1
```

## tox 2

```
deps =
    pytest
pip_pre =
    True
```
https://twitter.com/pganssle/status/1281597323274067969

## tox 3

```
PIP_PRE=True tox -r
```
https://twitter.com/pganssle/status/1281598162755616769


## more infos about version identification

https://www.python.org/dev/peps/pep-0440/
