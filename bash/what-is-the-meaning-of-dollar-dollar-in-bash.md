# What is the meaning of $$ in bash?

I stumbled upon a colleague's bash script which contained the following line,
which in isolation, made not much sense to me.

```
WRKDIR=~/app/work$$
```

But after some googling and having a look at the complete scope of the script, I finally got it.

```
...
WRKDIR=~/app/work$$
...
mkdir $WRKDIR
...
...
...
...
rmdir $WRKDIR
```

- `$$` is a reference to the PID (process id)
- it was used to create a *unique* temporary file

## All good?

Well, there may be a couple of reasons why this is not good.

At first and foremost, it is a bit obscure - at least for people who do not work a lot with bash.

Consider the alternative: `mktemp`

No matter from which programming language you come, you will understand that.

Also, there are a [couple of hints](https://stackoverflow.com/questions/78493) out there,
why `mkdir foo$$` may be not a good idea:

- security problems
- race conditions
- other stuff

... but, no really good and detailed explanation. Can you bring light into the darkness?

Create a pull request or drop me a note via email or twitter, see https://jugmac00.github.io/
