# How can you delete complete lines with the search/replace function?

For many years now, I had been using Jetbrain's IntelliJ Idea Ultimate happily also for my Python development.

Due to "legacy issues", I had to apply many `# noinspection` annotations to my source code.

Now, that I switched to VS Code, I want to get rid of actually 821 `# noinspection` annotations :-)

A simple search for `# noinspection.*` and a replacement with basically *nothing* would work,
but would leave many newlines. And then `flake8` would complain.

## simple solution

search for `^# noinspection.*$\n`, ie expand the match with the newline character,
and then replace with *nothing*


## thank you

https://stackoverflow.com/a/53287432/672833
