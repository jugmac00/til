# How do you develop dependencies with buildout?

Given you have a decent sized project, with some dependencies...

How can you develop and test a dependency against your main project, when it is not yet published to PyPi?

Well, until recently, I relied on a strong test suite and mostly developed "blindly".

When I wanted to see the result, I used **Vim** to directly edit the dependency in my virtual env.

## There must be a better way

And actually, there is and has been for more than a decade.
Say hello to **mr.developer**.

While I heard of **mr.developer** on some of the Zope sprints, I never felt the urge to use it.

But the time has come.

## The task

I maintain a project called [Products.ZopeTree](https://github.com/jugmac00/Products.ZopeTree).

The plan is to delete a file which is not under test.

The easiest way - delete it and have a look whether the app is still running, right?

This is where **mr.developer** shines.

## Configure mr.developer via buildout

As I develop this one app via [zc.buildout](https://pypi.org/project/zc.buildout/), I just have to add a couple of lines:

```
[buildout]
extensions = mr.developer
auto-checkout = *

[sources]
Products.ZopeTree = git git@github.com:jugmac00/Products.ZopeTree.git
```

Then I run `bin/buildout` and instead of pulling the app from **PyPI**, it gets checked out from GitHub.

In hindsight... I could have tried this earlier :-)

## Thanks

.. to @tisto ( https://github.com/zopefoundation/Zope/issues/788#issuecomment-589782756 )

## Further resources

https://github.com/fschulze/mr.developer

