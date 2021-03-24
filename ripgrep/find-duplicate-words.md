# How can you find duplicate words in a code base?

When contributing to a new opensource project,
from time to time I searched the codebase for occurences of `the the`.

This is a common mistake in comments in English codebases.

My friend [Miroslav](https://twitter.com/eumiro) came up with an even better way:

Use a regex to find duplicate words!

```
rg --pcre2 "\b(\w+)\s+\1\b"
```

`rg` stands for [ripgrep](https://github.com/BurntSushi/ripgrep),
which is a blazing fast implemenation of a regex command line tool,
written in Rust.

When trying to understand the above regex,
I found an interesting [stackoverflow](https://stackoverflow.com/questions/2823016) question,
where an alternative regex was mentioned,
which even handles words with apostrophes, hyphens...

```
rg --pcre2 "(\b\S+\b)\s+\b\1\b"
```
The above link to stackoverflow also explains those regexes.
