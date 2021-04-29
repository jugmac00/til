# How to run a bash script in a sane way?

When you never had problems with running/debugging a bash script,
you might wonder what I am talking about.

Instead of introducing the possible problems, and then the way to counter them, let's start with the solution.

All your bash scripts should probably start with...

```
#!/usr/bin/env bash
```
... wait... it goes on...

```
set -euxo pipefail
```

## Wat?

Ok, let's go through the options, one by one.

### `set -e`

This makes a bash script to stop on error immediately, and exit.

Sound like it should be anyways,
and it is in Python,
but well,
in bash you need to activate this ``error mode``,
otherwise the bash script just continues with the next line and you will possibly receive something you did not expect!


### `set -u`

This makes the bash script error on uninitialized variables!

If you do not set this, `echo hello $name` just gives `hello ` - which you probably do not want.

### `set -o pipefail`

This makes bash fail when any of the commands in a pipe fail, not only when the last one fails.


### `set -x`

This makes bash print the commands before executing them, making debugging much, much easier.

You can also specify `-x` when executing the command like ...

```
❯ bash -x -c "echo hi"
+ echo hi
hi
```

## thanks

Once more, thanks to [Anthony Sottile](https://twitter.com/codewithanthony),
from whom I learned this in his [excellent video](https://www.youtube.com/watch?v=9fSkygQ-ZjI).
