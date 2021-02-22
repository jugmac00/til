# How can I update installed Rust packages?

[Rust](https://www.rust-lang.org/) is not only known for its memory safety,
but also for being (almost) on par with C, speed-wise.

In the last couple of years quite some interesting tools were created, 
which may replace common Linux command line tools,
e.g. [bat](https://github.com/sharkdp/bat) instead of `cat`,
[ripgrep](https://github.com/BurntSushi/ripgrep) instead of `grep`, ...

I installed a handful of them via `cargo`, Rust's package manager.

I can list all packages with `cargo install --list` ...

```
❯ cargo install --list
bat v0.16.0:
    bat
exa v0.9.0:
    exa
fd-find v7.4.0:
    fd
lok v0.1.1:
    lok
starship v0.46.0:
    starship
```

But I could not figure out how to update them :-/

For `cargo update` you need the source and a `Cargo.toml` file...

## disord to the rescue

As I wanted to update [starship](https://starship.rs/),
a super awesome prompt for any shell,
I asked on their discord channel and got a super quick answer:

```
cargo install starship
```

So, update and install commands are the same... unexpected but works out.

No more head scratching whether it is `update` or `upgrade` :-)
