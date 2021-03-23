# cargo-lints

`cargo-lints` is a utility for running lints specified from files.

## Use Case

It is hard to share lint configuration in cargo workspace. Even more so as lint configuration in the form of:

``` rust
$ cat src/lib.rs
#![warn(clippy::all)]
...
```

will not affect tests and benchmark binaries in `./benches/` and `./tests` directories.

For now `cargo` and `clippy` don't provide convinient way to specify lints enabled for workspace and that is
why it is handy to have a utility such as this one.

## Installation

Install with:
```sh
$ cargo install --git https://github.com/soramitsu/iroha2-cargo_lints
```

## Example

You should set some lints in `lints.toml` file:

### `$ cat lints.toml`
```toml
#
# For all clippy lints please visit: https://rust-lang.github.io/rust-clippy/master/
#
deny = [
    'clippy::all',
    'clippy::cargo',
    'clippy::nursery',
    'clippy::pedantic',
]
allow = [
    'clippy::enum_glob_use',
]
```

After that you can run:

#### `$ cargo lint fmt`

to format the toml file.

#### `$ cargo lint clippy`

to run clippy (you don't have to have `lints.toml` file - in that case it will simply run `cargo clippy`).

## Options

On the top level you can supply `-f` option:
```sh
$ cargo lints -f custom_lints.toml clippy
```

Also all options after `cargo lints clippy` are forwarded to clippy:

```
$ cargo lints clippy --tests --benches --all-features --all
```
