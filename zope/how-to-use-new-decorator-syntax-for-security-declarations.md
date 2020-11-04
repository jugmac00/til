# How to replace the old with the new decorator syntax for Zope's security declarations?

[Zope's](https://github.com/zopefoundation/Zope) security architecture is built upon security declarations, which scope can be either a method, several methods or even a complete class.

Until *recently* you usally declared the security for a method like this...

```
from AccessControl import getSecurityManager

class Suggestions(SomeBaseClass):
    security = ClassSecurityInfo()
    
    security.declareProtected("View", "all_suggestions")
    def all_suggestions():
        ...
```

Then, when accesssing this method, e.g. the logged in user's role or group was checked against the security declaration.

One big disadvantage was that you could easily introduce typos.
e.g. when you wrote `security.declareProtected("View", "all_sugestions")`,
the method was no longer protected again.

A couple of years ago, the new decorator syntax was introduced for security declarations.

Compare the old vs the new syntax - much nicer and less error prone...

```
security.declarePublic
# versus
@security.public
```

```
security.declareProtected("View", "method")
# versus
@security.protected("View")
def ...
```

```
security.declarePrivate("method")
# versus
@security.private
def ...
```

Ok, very nice. But what do you do when you have hundreds or thousands of declarations?

## search/replace over many files

While most IDEs have a comfortable search/replace function,
I will use **VS Code** to show what to do.

For all operations do the following...
- in the top right corner, click on **Edit** and then on **Replace in Files** (As keyboard shortcuts are very individual and also differ from OS to OS, I will not show mention them here.)
- activate the regex mode by clicking on the third icon besides the **Search** field

### replace security.declarePublic

Actually, I only had like 10 declarations of this kind,
so I reviewed and replaced them manually,
but the following search/replace should do it.

```
Search
security.declarePublic

Replace
@security.public
```

### replace security.declarePrivate("method_name")

This one is also trivial.
The regex matches both single and double quotes,
and also the method name, but the latter one can be dropped.

```
Search
security.declarePrivate\(['"].*\)$

Replace
@security.private
```

**Attention** As I had several methods marked with the `@staticmethod` decorator,
test collection failed after this search/replace operation,
as the order of decorators is important!

So I did another search/replace to fix the order...
```
Search
    @security.private
    @staticmethod

Replace
    @staticmethod
    @security.private
```

### replace security.declareProtected("permission_name", "method_name")

This one is a bit more evolved, as the permission name must be retained.

In order to make this work, 
you need to capture the permission name,
which can be achieved by using a group: `(.*).

You then can access the value of the group via the placeholder `$1`.

```
Search
security.declareProtected\('(.*)', '.*'\)$

Replace
@security.protected("$1")
```

**Attention** Again, the test runner showed some problems because of the wrong order of decorators.

## conclusion

Updating my code base, consisting of hundreds of files and security declarations only took a couple of minutes,
thanks to **VS Code** and a good test suite.
