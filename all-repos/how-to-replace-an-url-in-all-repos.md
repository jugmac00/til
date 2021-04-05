# How to replace an URL in all repositories?

Recently Anthony Sottile, one of the maintainers of Flake8,
[announced on Twitter](https://twitter.com/codewithanthony/status/1378746934928699396)
that the source code repository of [Flake8](https://pypi.org/project/flake8/) was moved from GitLab to GitHub.

Those of us, who also use Anthony's `pre-commit`, now should update their `.pre-commit-config.yaml` file.

Though there is no hurry, as the repository on GitLab will stay as a mirror.

For one of my repos the `.pre-config-conig.yaml` looks like this:

```
repos:
...
-   repo: https://gitlab.com/pycqa/flake8
    rev: 3.9.0
    hooks:
    -   id: flake8
        additional_dependencies:
        - flake8-click==0.3.1
        - flake8-bugbear==20.1.4
...
```

I can easily replace the URL in the above configuration file, but what if you maintain 5, 10 or 300 repositories?

# all-repos

This is a prime example for using [all-repos](https://github.com/asottile/all-repos), with which you can clone and manipulate many, many repositories at once.

I have been using it intensively for the last six months, and I also wrote about using it a couple of times, but this time there is something new I learned.

While `all-repos` offers many command line tools, `all-repos-sed` is the one we need to use this time.

Imaging using `sed`, the stream editor, but not on one file or repository, but on all of them.

A usual sed command looks like this:

`$sed 's/unix/linux' hobbies.txt`

Which means
- search the file `hobbies.txt` the first occurence of `unix`
- and replace it with `linux`

Note, that the slash is used as delimiter.

# putting it all together

So, we need to use `all-repos-sed` and we have to replace an URL - with slashes!
Do we need to escape the slashes?

Turns out no - you can use any character as delimiter, it does not need to be a `#`.

```
all-repos-sed --commit-msg "Update repository URL for Flake8" s#https://gitlab.com/pycqa/flake8#https://github.com/PyCQA/flake8# -- '.pre-commit-config.yaml'
```

Let's break it down:
- `all-repos-sed` - like `sed` but applied on all repositories
- `--commit-msg "Update repository URL for Flake8"` - just a commit message for git
- `s#https://gitlab.com/pycqa/flake8#https://github.com/PyCQA/flake8#` - replace the old with the new URL
- '.pre-commit-config.yaml' - but only in the given configuration file


