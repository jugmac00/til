# How to configure git to be used in tests?

[batou](https://batou.readthedocs.io/en/stable/) is a configuration management and deployment tool,
comparable to **Ansible**.

With **batou** you can deploy applications, also from **git** repositories.

For this **batou** uses the **git** binary - so this has to be tested somehow.

One test looks like this...
```
def test_git_remote_init_pull(tmpdir):
    source = tmpdir.mkdir("source")
    dest = tmpdir.mkdir("dest")
    with source.as_cwd():
        remote_core.cmd("git init")
        source.join("foo.txt").write("bar")
        remote_core.cmd("git add foo.txt")
        remote_core.cmd("git commit -m bar")

        remote_core.ensure_repository(str(dest), "git-bundle")
        remote_core.git_pull_code(str(source), "master")
        remote_core.git_update_working_copy("master")

    assert "bar" == dest.join("foo.txt").read()
```

... and worked in some environments,
even on **Travis**,
but failed on my Ubuntu box, and later also on GH Actions:

```
batou.remote_core.CmdError: ('git commit -m bar', 128, b'', b'Author identity unknown\n\n*** Please tell me who you are.\n\nRun\n\n  git config --global user.email "you@example.com"\n  git config --global user.name "Your Name"\n\nto set your account\'s default identity.\nOmit --global to set the identity only in this repository.\n\nfatal: empty ident name (for <runner@fv-az18-857.2cpogp2qopau1j0uik42oh12ub.cx.internal.cloudapp.net>) not allowed\n')
```

While this puzzled me for some time,
there is a simple solution.

**git** pulls its configuration from various places,
also from the environment!

## git needs to be configured properly

In order to use git, you need to configure it properly, ie set up a user / email address.

### one solution

Basically, you need to both setup a committer and an author ([difference](https://stackoverflow.com/q/18750808/672833)).

This resulted in code like this...

```
@mock.patch.dict(
    os.environ,
    {
        "GIT_AUTHOR_EMAIL": "test@example.com",
        "GIT_COMMITTER_EMAIL": "test@example.com",
    },
)
def test_git_remote_init_pull(tmpdir):
   ...
```

While this is ok for one or two tests, you could convert this into a fixture.

```
@pytest.fixture
def ensure_git_config(monkeypatch):
    monkeypatch.setitem(os.environ, "GIT_AUTHOR_EMAIL", "test@example.com")
    monkeypatch.setitem(os.environ, "GIT_COMMITTER_EMAIL", "test@example.com")
```

So you can write your test as ...

```
def test_git_remote_init_pull(tmpdir, ensure_git_config):
    ...
```

or, if you want the configuration be set for all tests you can use `autouse`...

```
@pytest.fixture(autouse=True)
def ensure_git_config(monkeypatch):
    ....
```

## bonus: use `git` in CI

If you directly use `git` e.g. in your CI pipeline,
you can use the following command:

```
git -c user.name ... -c user.email ... commit ...
```

## Thanks

Thanks to [Anthony Sottile](https://twitter.com/codewithanthony/status/1327661351230050304) - once again! 
