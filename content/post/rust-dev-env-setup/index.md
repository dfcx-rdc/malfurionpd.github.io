+++

title = "Rust开发环境搭建"
description = "介绍Rust开发环境搭建"
author = "adeng"
tags = [
    "rust",
    "vscode",
]
date = "2021-04-29"
categories = [
    "Rust"
]

image = "QQ20210429-094005@2x.png"



+++



# 初步认识

拜读了大佬关于Rust的这篇博客 [RUST语言的编程范式](https://coolshell.cn/articles/20845.html)，对这门语言有了大致的认识。没有GC，强大的编译检查，基本上来说，一旦编译通过，代码运行起来是安全的，bug也是很少的。

> **如果你对Rust的概念认识的不完整，你完全写不出程序，那怕就是很简单的一段代码**。

感觉还是很有必要得着，搭个环境感受下。

直接参考 [官网入门](https://www.rust-lang.org/zh-CN/learn/get-started) 。



# 安装

笔者在mac上执行安装命令：

```
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

info: downloading installer

Welcome to Rust!

This will download and install the official compiler for the Rust
programming language, and its package manager, Cargo.

Rustup metadata and toolchains will be installed into the Rustup
home directory, located at:

  /Users/adeng/.rustup

This can be modified with the RUSTUP_HOME environment variable.

The Cargo home directory located at:

  /Users/adeng/.cargo

This can be modified with the CARGO_HOME environment variable.

The cargo, rustc, rustup and other commands will be added to
Cargo's bin directory, located at:

  /Users/adeng/.cargo/bin

This path will then be added to your PATH environment variable by
modifying the profile files located at:

  /Users/adeng/.profile
  /Users/adeng/.zshenv

You can uninstall at any time with rustup self uninstall and
these changes will be reverted.

Current installation options:


   default host triple: x86_64-apple-darwin
     default toolchain: stable (default)
               profile: default
  modify PATH variable: yes

1) Proceed with installation (default)
2) Customize installation
3) Cancel installation
>1

info: profile set to 'default'
info: default host triple is x86_64-apple-darwin
info: syncing channel updates for 'stable-x86_64-apple-darwin'
676.1 KiB / 676.1 KiB (100 %) 675.9 KiB/s in  1s ETA:  0s
info: latest update on 2021-03-25, rust version 1.51.0 (2fd73fabe 2021-03-23)
info: downloading component 'cargo'
  4.3 MiB /   4.3 MiB (100 %) 943.4 KiB/s in  5s ETA:  0s
info: downloading component 'clippy'
  1.8 MiB /   1.8 MiB (100 %) 956.9 KiB/s in  2s ETA:  0s
info: downloading component 'rust-docs'
 15.0 MiB /  15.0 MiB (100 %) 940.0 KiB/s in 17s ETA:  0s
info: downloading component 'rust-std'
 23.6 MiB /  23.6 MiB (100 %) 917.5 KiB/s in 27s ETA:  0s
info: downloading component 'rustc'
 56.6 MiB /  56.6 MiB (100 %) 792.3 KiB/s in  1m  5s ETA:  0s
info: downloading component 'rustfmt'
  2.3 MiB /   2.3 MiB (100 %) 943.5 KiB/s in  2s ETA:  0s
info: installing component 'cargo'
info: using up to 500.0 MiB of RAM to unpack components
info: installing component 'clippy'
info: installing component 'rust-docs'
 15.0 MiB /  15.0 MiB (100 %)   6.3 MiB/s in  1s ETA:  0s
info: installing component 'rust-std'
 23.6 MiB /  23.6 MiB (100 %)  12.2 MiB/s in  4s ETA:  0s
info: installing component 'rustc'
 56.6 MiB /  56.6 MiB (100 %)  14.4 MiB/s in  4s ETA:  0s
info: installing component 'rustfmt'
info: default toolchain set to 'stable-x86_64-apple-darwin'

  stable-x86_64-apple-darwin installed - rustc 1.51.0 (2fd73fabe 2021-03-23)


Rust is installed now. Great!

To get started you need Cargo's bin directory ($HOME/.cargo/bin) in your PATH
environment variable. Next time you log in this will be done
automatically.

To configure your current shell, run:
source $HOME/.cargo/env

$ source $HOME/.cargo/env

$ cargo --version
cargo 1.51.0 (43b129a20 2021-03-16)

$ rustup --version
rustup 1.23.1 (3df2264a9 2020-11-30)
info: This is the version for the rustup toolchain manager, not the rustc compiler.
info: The currently active `rustc` version is `rustc 1.51.0 (2fd73fabe 2021-03-23)`
```



## Rustup：Rust安装器和版本管理工具

Rust 的升级非常频繁。如果您安装 Rustup 后已有一段时间，那么很可能您的 Rust 版本已经过时了。运行 `rustup update` 获取最新版本的 Rust。



## Cargo：Rust 的构建工具和包管理器

您在安装 Rustup 时，也会安装 Rust 构建工具和包管理器的最新稳定版，即 Cargo。Cargo 可以做很多事情：

- `cargo build` 可以构建项目
- `cargo run` 可以运行项目
- `cargo test` 可以测试项目
- `cargo doc` 可以为项目构建文档
- `cargo publish` 可以将库发布到 [crates.io](https://crates.io/)



# 新建项目

`cargo new hello-rust`会生成一个名为 `hello-rust` 的新目录，其中包含以下文件:

```
hello-rust
|- Cargo.toml
|- src
  |- main.rs
```

`Cargo.toml` 为 Rust 的清单文件。其中包含了项目的元数据和依赖库。

`src/main.rs` 为编写应用代码的地方。

`cargo run` 您应该会在终端中看到如下内容：

```
$ cargo run
   Compiling hello-rust v0.1.0 (/Users/adeng/_tmp/rust/hello-rust)
    Finished dev [unoptimized + debuginfo] target(s) in 2.20s
     Running `target/debug/hello-rust`
Hello, world!
```



# VSCode 

安装 `rust-lang.rust` 插件从 [the VSCode Marketplace](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust) (or by entering `ext install rust-lang.rust` at the command palette Ctrl+P)。

打开刚才创建的hello-rust项目 (`File > Add Folder to Workspace...`). Open the folder for the whole project (i.e., the folder containing `Cargo.toml`, not the `src` folder).



打开 `main.rs`时，会提示安装其他未安装的插件，同意后：

```
> Executing task in folder hello-rust: rustup component add rust-analysis --toolchain stable-x86_64-apple-darwin <

info: downloading component 'rust-analysis'
info: installing component 'rust-analysis'
info: using up to 500.0 MiB of RAM to unpack components

Terminal will be reused by tasks, press any key to close it.

> Executing task in folder hello-rust: rustup component add rust-src --toolchain stable-x86_64-apple-darwin <

info: downloading component 'rust-src'
info: installing component 'rust-src'
info: using up to 500.0 MiB of RAM to unpack components

Terminal will be reused by tasks, press any key to close it.

> Executing task in folder hello-rust: rustup component add rls --toolchain stable-x86_64-apple-darwin <

info: downloading component 'rls'
info: installing component 'rls'
info: using up to 500.0 MiB of RAM to unpack components

Terminal will be reused by tasks, press any key to close it.
```





编辑器使用   https://marketplace.visualstudio.com/items?itemName=rust-lang.rust

https://www.rust-lang.org/zh-CN/learn/get-started



