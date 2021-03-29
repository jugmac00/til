# How can you restrict `all-repos-grep` to specifc files?

Back at the end of 2020,
when Travis announced you need to move your open source projects from https://travis-ci.org to https://travis-ci.com,
I wanted to know in which **README** files I used the link to the org-site - of the many, many repositories I manage.

That is a textbook example what you can do with [all-repos](https://github.com/asottile/all-repos).

A naive way would be to grep in all repositories like ...

```
all-repos-grep travis-ci.org
```

Instead of grepping in all files,
it is a better idea to restrict the search only to **README** files.

As I was not sure,
whether they are all rst files, I kept my options open:

```
all-repos-grep travis-ci.org -- 'README*'
```

For more examples, see the [official documentation](https://github.com/asottile/all-repos#all-repos-grep-options-git_grep_options).

## Thanks

Thanks to [Anthony](https://twitter.com/codewithanthony) for providing [all-repos](https://github.com/asottile/all-repos), which is an insanely useful tool!
