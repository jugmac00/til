# How can I find all repositories in a GitHub organization which do not follow the src layout?

Let's say, while not everybody is convinced, that the so-called `src layout` is a great idea, at least it is a trend in the Python eco system.

And, e.g. [Hynek has written about good reasons  to use the `src layout`](https://hynek.me/articles/testing-packaging/).

While my personal and work repositories (mostly) follow the `src layout`,
what about the almost 300 [Zope repositories](https://github.com/zopefoundation)?

## all-repos to the rescue

I really love to play with [all-repos](https://github.com/asottile/all-repos), 
an awesome tool to manage and manipulate a large amount of git repositories.

I even wrote a couple of [blog posts](https://jugmac00.github.io/blog/) about it.

Also this time **all-repos** seems to be perfect fit for this task.

While there is no direct command to get a "negative" list,
it is all possible with the help of `all-repos-list-repos` and some **bash magic**.

```
❯ all-repos-list-repos --output-paths -C all-repos-zope.json | xargs --replace bash -c 'ls {}/src >& /dev/null || echo {}'
output_zope/zopefoundation/BTrees
output_zope/zopefoundation/persistent
output_zope/zopefoundation/ZConfig
output_zope/zopefoundation/zc.zdaemonrecipe
output_zope/zopefoundation/zc.recipe.filestorage
output_zope/zopefoundation/Products.SQLAlchemyDA
output_zope/zopefoundation/zopetoolkit
output_zope/zopefoundation/Products.PluginRegistry
output_zope/zopefoundation/zc.zope3recipes
output_zope/zopefoundation/Products.CMFDefault
output_zope/zopefoundation/Products.CMFUid
output_zope/zopefoundation/Products.ExternalEditor
output_zope/zopefoundation/www.zope.org
output_zope/zopefoundation/zpt-docs
output_zope/zopefoundation/zopefoundation.github.io
output_zope/zopefoundation/meta
output_zope/zopefoundation/website-zope.de
output_zope/zopefoundation/.github
```

First, this is great - of the almost 300 active repositories, only a good dozen do not follow the `src layout` yet.
Also, some of the listed repositories are even no Python source code repositories, e.g. `www.zope.org`.

Second,... what does this command mean?

## analyzing the command

```
all-repos-list-repos --output-paths 
```
-> print the relative path for all repositories

```
-C all-repos-zope.json
```
-> only for the Zope repositories, not the repositories of my other organizations

```
| xargs --replace 
```
-> pipe the output to `xargs`, which replaces the output...

```
bash -c 'ls {}/src >& /dev/null || echo {}'
```
-> with the output again, but only if there is a `src` directory, otherwise with nothing.

## thanks

Once again, thanks to [Anthony Sottile](https://twitter.com/codewithanthony), who came up with this command.

I would have tried to write a for loop in bash, or even created a Python script...
