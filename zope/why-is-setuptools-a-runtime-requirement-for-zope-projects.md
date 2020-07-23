# Why is setuptools a runtime requirement for Zope projects?

... or in other words...

Why is this snippet part of `setup.py` in all Zope projects?

```
install_requires = 'setuptools',
```

This sounds weird at first, but there is good reason.

`setuptools` provides `pkg_resources`, and the latter is used in `__init__.py`, in order to declare a namespace package.

```
__import__('pkg_resources').declare_namespace(__name__)
```

Still confused?

While no longer recommended for new projects, this approach was used to split large packages, and retrieve the contents from more than one location.


## examples from the wider Zope universe

- `zc.*`
- `z3c.*`
- `zope.*`
- `Products.*`
- `five.*`
- `grokcore.*`


## further reading

http://peak.telecommunity.com/DevCenter/setuptools#namespace-packages

https://packaging.python.org/guides/packaging-namespace-packages/#pkg-resources-style-namespace-packages

## thanks

While I stumbled upon namespace packages now and then, and I read about them a bit, it was Jason who connected the dots for me in

https://github.com/zopefoundation/zc.lockfile/issues/22
