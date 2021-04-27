# How to globally .gitignore VS Code configuration files?

Until today, I did not make up my mind about what to do with configuration files, created by e.g. VS Code.

Certainly, I do not want to commit them, but putting it into every's repository `.gitignore` file is also cumbersome - and sometimes it is not possible.

I always do a `git add -u` to avoid accidentally adding a `venv` or similar, so it did not really matter.

Except...

```
❯ ./batou deploy staging
Running unclean installation from requirements.txt
Ensuring unclean install ...
batou/2.2.2 (cpython 3.10.0-alpha7, Linux 5.4.0-72-generic x86_64)
======================================================= Preparing ========================================================
main: Loading environment `staging`...
main: Verifying repository ...
ERROR: Your repository has uncommitted changes.
I am refusing to deploy in this situation as the results will be unpredictable.
Please commit and push first.

?? .vscode/

============================================ DEPLOYMENT FAILED (during load) =============================================
```

I could not deploy, as [batou](https://batou.readthedocs.io/en/stable/) refuses to deploy from an unclean repository.

## globally ignore

So the solution was to globally ignore the `.vscode` folder.

```
echo .vscode/ >> ~/.gitignore
git config --global core.excludesfile ~/.gitignore
```

## but ...

But what if you want the configuration files to be committed.. just for this one repository?

```
git add --force ./vscode
```
