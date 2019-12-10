# seahorse

[![crates.io](https://img.shields.io/crates/v/seahorse.svg)](https://crates.io/crates/seahorse)
![](https://img.shields.io/github/release/KeisukeToyota/seahorse.svg)
![](https://img.shields.io/github/issues/KeisukeToyota/seahorse.svg)
![](https://img.shields.io/github/forks/KeisukeToyota/seahorse.svg)
![](https://img.shields.io/github/license/KeisukeToyota/seahorse.svg)

A minimal CLI framework written in Rust

## Using

```toml
[dependencies]
seahorse = "0.2.1"
```

## Example

```rust
use std::env;
use seahorse::{App, Command, color};

fn main() {
    let args: Vec<String> = env::args().collect();
    let display_name = color::magenta("
     ██████╗██╗     ██╗
    ██╔════╝██║     ██║
    ██║     ██║     ██║
    ██║     ██║     ██║
    ╚██████╗███████╗██║
    ╚═════╝╚══════╝╚═╝");
    let command = Command {
        name: "hello",
        usage: "cli_tool hello user",
        action: |v: Vec<String>| println!("Hello, {:?}", v)
    };

    let mut app = App::new()
        .name("cli_tool")
        .display_name(display_name)
        .usage("cli_tool [command] [arg]")
        .version(env!("CARGO_PKG_VERSION"))
        .commands(vec![command]);

    app.run(args);
}
```