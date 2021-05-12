# How to create an empty branch?

What do I mean by an **empty** branch?

Simply, a branch with no commits.

## Why on earth...

Why would one even need an empty branch?

There are not many reasons which come to my mind,
but imagine you start a rewrite of an existing project and want to start from scratch,
but you want to keep the rewrite in the same repository.

For example [tox](https://github.com/tox-dev/tox) does this:
- the current main version is on [master](https://github.com/tox-dev/tox/tree/master)
- the upcoming version 4, which is a complete rewrite, is on the [rewrite branch](https://github.com/tox-dev/tox/tree/rewrite)

## How

The [`git checkout`](https://git-scm.com/docs/git-checkout#Documentation/git-checkout.txt---orphanltnewbranchgt) subcommand has an `--orphan` option.

```bash
git checkout --orphan <new_branch>
```

This creates a new branch, with no commits, and the first commit will have no parents.
