# How to update all zopefoundation repositories at once?

Most or even all `zopefoundation` repositories use Travis for CI.

While Travis offered Python 3.9 as a dev version (`3.9-dev`) for quite some time,
support for `3.9 final` took a while.

That's why we decided to run Travis with Python `3.9-dev`.

Meanwhile Travis finally offers support for Python `3.9 final`,
so [we have to update all repositories](https://github.com/zopefoundation/meta/issues/37),
which would be super tedious by hand.

## all-repos to the rescue

`all-repos` by @asottile is a set of command line tools,
which help to work in bulk with many repositories at once.

In order to get started, you need to

- install `all-repos` ( https://pypi.org/project/all-repos/ )
- create a GitHub API token ( https://github.com/settings/tokens/new )
- create a configuration file
- clone all repos

### configuration

My configuration file for `zopefoundation`,
which I named `all-repos.json`, looks like so:

```
{
    "output_dir": "output",
    "source": "all_repos.source.github_org",
    "source_settings":  {
        "api_key": "xxx",
        "org": "zopefoundation"
    },
    "push": "all_repos.push.github_pull_request",
    "push_settings": {
        "api_key": "xxx",
        "username": "jugmac00"
    }
}
```

Where
- `output_dir` is the folder where the repositories are cloned into
- `source` is the way how to get hold of the repositories, in our case it is a GitHub organization
- `api_key` is needed in order to access / write to the repositories
- `org` is the corresponding GitHub organization
- `push` configures what should be done after applied changes, here it is "create a pull request at GitHub"
- `username` is the username which should be used for the pull request

### grepping all repos

Once this is set up, you can give it a try like the following:
```
❯ all-repos-grep --repos-with-matches 3.9-dev -- '.travis.yml'
output/zopefoundation/AccessControl
output/zopefoundation/Acquisition
...
```

Where
- `all-repos-grep` is the CLI tool we use => grep on all repositories
- `--repos-with-matches` => only show repositories with a match
- `3.9-dev` => the string we are looking for
- `.travis.yml` => only look in `.travis.yml`

### update all `.travis.yml` files

DO NOT TRY THIS AT HOME!

`all-repos-sed --commit-msg "Use Python 3.9 final" s/3.9-dev/3.9/g -- '.travis.yml'`

Where
- `all-repos-sed` is the CLI tool we use, => use sed on all repositories
- `--commit-msg "Use Python 3.9 final"` => use a custom commit message
- `s/3.9-dev/3.9/g` => replace `3.9-dev` with `3.9`
- `.travis.yml` => only look in `.travis.yml`

### result

That is one of the many pull requests which I did not have to create manually...

https://github.com/zopefoundation/zope.session/pull/15

## thanks

Thank you, @asottile, for providing this tool, which saved me some hours for this task, and many more in future!
