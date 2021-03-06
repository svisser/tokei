# Tokei ([時計](https://en.wiktionary.org/wiki/%E6%99%82%E8%A8%88))

[![Linux build status](https://img.shields.io/travis/Aaronepower/tokei.svg?branch=master)](https://travis-ci.org/Aaronepower/tokei)
[![Windows build status](https://ci.appveyor.com/api/projects/status/github/Aaronepower/tokei?svg=true)](https://ci.appveyor.com/project/Aaronepower/tokei)
[![](https://img.shields.io/crates/d/tokei.svg)](https://crates.io/crates/tokei)
[![](https://img.shields.io/github/issues-raw/Aaronepower/tokei.svg)](https://github.com/Aaronepower/tokei/issues)
[![](https://tokei.rs/b1/github/Aaronepower/tokei?category=code)](https://github.com/Aaronepower/tokei)

Tokei is a program that displays statistics about your code. Tokei will show number of files, total lines within those files and code, comments, and blanks grouped by language.

## Example Output
This is tokei running on it's own directory

```
$ tokei
-------------------------------------------------------------------------------
 Language            Files        Lines         Code     Comments       Blanks
-------------------------------------------------------------------------------
 BASH                    4          224          161           23           40
 JSON                    1         1263         1263            0            0
 Markdown                4          707          707            0            0
 Rust                   17         2367         1626          463          278
 TOML                    1           80           66            0           14
 YAML                    2          120           95           19            6
-------------------------------------------------------------------------------
 Total                  29         4761         3918          505          338
-------------------------------------------------------------------------------
```

## [Documentation](https://docs.rs/tokei)

## Table of Contents

- [Canonical Source](#canonical-source)
- [Installation](#installation)
    - [Automatic](#automatic)
        - [Arch Linux](#arch-linux)
        - [Cargo](#cargo)
        - [Fedora](#fedora)
    - [Manual](#manual)
- [How to use Tokei](#how-to-use-tokei)
- [Options](#options)
- [Badges](#badges)
- [Supported Languages](#supported-languages)
- [Changelog](CHANGELOG.md)
- [Common Issues](#common-issues)
- [Copyright](#copyright)


## Canonical Source
The canonical source of this repo is hosted on [GitHub](https://github.com/Aaronepower/tokei). If you have a GitHub account, please make your issues, and pull requests there.

## Installation

### Automatic

#### Arch Linux
```shell
$ pacman -S tokei
```

#### Cargo
```shell
$ cargo install tokei
```

#### Fedora 64 bit
```shell
$ dnf copr enable phnxrbrn/tokei
$ dnf install tokei
```

### Manual
You can download prebuilt binaries in the
[releases section](https://github.com/Aaronepower/tokei/releases), or create
from source.
```shell
$ git clone https://github.com/Aaronepower/tokei.git
$ cd tokei
$ cargo build --release
```
##### Linux
```
# sudo mv target/release/tokei /usr/local/bin
```
##### OSX
```
# sudo mv target/release/tokei /usr/local/bin/tokei
```
##### Windows
- Create a folder for tokei
- search for `env`
- open "edit your enviroment variables"
- edit `PATH`
- append folder path to the end of the string ie: `<path_stuff_here>;C:/tokei/;`

## How to use Tokei

#### Basic usage

This is the basic way to use tokei. Which will report on the code in `./foo`
and all subfolders.

```shell
$ tokei ./foo
```

#### Multiple folders
To have tokei report on multiple folders in the same call simply add a comma,
or a space followed by another path.

```shell
$ tokei ./foo ./bar ./baz
```
```shell
$ tokei ./foo, ./bar, ./baz
```

#### Excluding folders
Tokei will respect all `.gitignore` and `.ignore` files, and you can optionally
the `--exclude` option to exclude any addtional files. The `--exclude` flag has
the same semantics as `.gitignore`.

```shell
$ tokei ./foo --exclude *.rs
```

#### Sorting output
By default tokei sorts alphabetically by language name, however using `--sort`
tokei can also sort by any of the columns.

`blanks, code, comments, lines`

```shell
$ tokei ./foo --sort code
```

#### Outputing file statistics
By default tokei only outputs the total of the languages, and using `--files`
flag tokei can also output individual file statistics.

```shell
$ tokei ./foo --files
```

#### Outputting into different formats
Tokei normally outputs into a nice human readable format designed for terminals.
There is also using the `--output` option various other formats that are more
useful for bringing the data into another program.

**Currently supported formats**
- JSON `--output json`
- YAML `--output yaml`
- TOML `--output toml`
- CBOR `--output cbor`

```shell
$ tokei ./foo --output json
```

#### Reading in stored formats
Tokei can also take in the outputted formats added the previous results to it's
current run. Tokei can take either a path to a file, the format passed in as a
value to the option, or from stdin.

```shell
$ tokei ./foo --input ./stats.json
```

## Options

```
Tokei 4.5.3
Aaron P. <theaaronepower@gmail.com>
Count Code, Quickly.

USAGE:
    Tokei [FLAGS] [OPTIONS] <input>...

FLAGS:
    -f, --files        Will print out statistics on individual files.
    -h, --help         Prints help information
    -l, --languages    Prints out supported languages and their extensions.
    -V, --version      Prints version information
    -v, --verbose      Set verbose output level: 1: for unknown extensions

OPTIONS:
    -e, --exclude <exclude>     Ignore all files & directories containing the word.
    -i, --input <file_input>    Gives statistics from a previous tokei run. Can be given a file path, or "stdin" to read from stdin.
    -o, --output <output>       Outputs Tokei in a specific format. [values: cbor, json, toml, yaml]
    -s, --sort <sort>           Will sort based on column [values: files, lines, blanks, code, comments]

ARGS:
    <input>...    The input file(s)/directory(ies)
```

## Badges
Tokei has support for badges. For example
[![](https://tokei.rs/b1/github/Aaronepower/tokei)](https://github.com/Aaronepower/tokei).

```
[![](https://tokei.rs/b1/github/Aaronepower/tokei)](https://github.com/Aaronepower/tokei).
```

Tokei's URL scheme is as follows.

```
https://tokei.rs/{host: values: github|gitlab}/{Repo Owner eg: Aaronepower}/{Repo name eg: tokei}
```

By default the badge will show the repo's LoC(_Lines of Code_), you can also
specify for it to show a different category, by using the `?category=` query
string. It can be either `code`, `blanks`, `files`, `lines`, `comments`,
Example show total lines:

```
[![](https://tokei.rs/b1/github/Aaronepower/tokei?category=lines)](https://github.com/Aaronepower/tokei).
```

## Supported Languages

If there is a language that you want added, feel free to submit a pull request
with the following information. If you're unsure have a look at
[`languages.json`](./languages.json) to see how other languages are defined.

- Name of language
- File Extension(s)
- The comment syntax (_Does it have block comments? is it the same as C?_)
- The string literal syntax

```
ActionScript
Ada
ASP
ASP.NET
Assembly
Autoconf
BASH
Batch
C
C Header
C#
C Shell
Clojure
CoffeeScript
ColdFusion
ColdFusion CFScript
Coq
C++
C++ Header
CSS
D
Dart
Device Tree
Elixir
Elm
Erlang
Forth
FORTRAN Legacy
FORTRAN Modern
GLSL
Go
Handlebars
Haskell
HEX
HTML
Idris
Intel HEX
Isabelle
JAI
Java
JavaScript
JSON
JSX
Julia
Kotlin
Lean
LESS
LD Script
LISP
Lua
Makefile
Markdown
Mustache
Nim
OCaml
Objective C
Objective C++
Oz
Pascal
Perl
PHP
Polly
Prolog
Protocol Buffers
Python
QCL
R
Razor
ReStructuredText
Ruby
Ruby HTML
Rust
Sass
Scala
Standard ML
SQL
Swift
TCL
TeX
Plain Text
TOML
TypeScript
Unreal Script
Vim Script
Wolfram
XML
YAML
Zsh
```

## Common issues

### Tokei says I have a lot of D code, but I know there is no D code!
This is likely due to `gcc` generating `.d` files. Until the D people decide on
a different file extension, you can always exclude `.d` files using the
`-e --exclude` flag like so

```
$ tokei . -e *.d
```

## Copyright and License
(C) Copyright 2015 by Aaron Power and contributors

See CONTRIBUTORS.md for a full list of contributors.

Tokei is distributed under the terms of both the MIT license and the Apache License (Version 2.0).

See [LICENCE-APACHE](./LICENCE-APACHE), [LICENCE-MIT](./LICENCE-MIT) for more information.
