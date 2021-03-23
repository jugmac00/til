# How to fix a broken rollback, caused by mixed Python environments, on Nixos via batou?

Today I tried to update a channel to 20.09.xxx, but the virtual machine was still running on 15.09, and seemingly the nix-version was pinned.

I got an error saying something like `the nix version is too low`.

I then tried to do a rollback, but then I got another following error:

```
ERROR: ./batou --help
Return code: 1
STDOUT
Running unclean installation from requirements.txt
Ensuring unclean install ...
.batou/unclean/bin/python -m pip install -r requirements.txt --upgrade returned with exit code 1
Traceback (most recent call last):
  File "/srv/s-custupload/.nix-profile/lib/python3.8/runpy.py", line 194, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/srv/s-custupload/.nix-profile/lib/python3.8/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/srv/s-custupload/deployment/.batou/unclean/lib/python3.8/site-packages/pip/__main__.py", line 23, in <module>
    from pip._internal.cli.main import main as _main  # isort:skip # noqa
  File "/srv/s-custupload/deployment/.batou/unclean/lib/python3.8/site-packages/pip/_internal/cli/main.py", line 10, in <module>
    from pip._internal.cli.autocompletion import autocomplete
  File "/srv/s-custupload/deployment/.batou/unclean/lib/python3.8/site-packages/pip/_internal/cli/autocompletion.py", line 9, in <module>
    from pip._internal.cli.main_parser import create_main_parser
  File "/srv/s-custupload/deployment/.batou/unclean/lib/python3.8/site-packages/pip/_internal/cli/main_parser.py", line 7, in <module>
    from pip._internal.cli import cmdoptions
  File "/srv/s-custupload/deployment/.batou/unclean/lib/python3.8/site-packages/pip/_internal/cli/cmdoptions.py", line 25, in <module>
    from pip._internal.cli.progress_bars import BAR_TYPES
  File "/srv/s-custupload/deployment/.batou/unclean/lib/python3.8/site-packages/pip/_internal/cli/progress_bars.py", line 8, in <module>
    from pip._vendor.progress.bar import Bar, FillingCirclesBar, IncrementalBar
  File "/srv/s-custupload/deployment/.batou/unclean/lib/python3.8/site-packages/pip/_vendor/progress/__init__.py", line 18, in <module>
    from datetime import timedelta
  File "/srv/s-custupload/.nix-profile/lib/python3.8/datetime.py", line 8, in <module>
    import math as _math
ImportError: /nix/store/wx1vk75bpdr65g6xwxbj4rw0pk04v5j3-glibc-2.27/lib/libm.so.6: version `GLIBC_2.29' not found (required by /srv/s-custupload/.nix-profile/lib/python3.8/lib-dynload/math.cpython-38-x86_64-linux-gnu.so)
```

The problem was caused by mixed packages, as the current `user package` containing Python 3.8.8 remains was not removed.

# the solution

```
# list installed user packages
nix-env -q

# delete user package
nix-env -e <package name>
```

And then repeat the deployment.
