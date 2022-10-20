# 介绍

本文参考[blog_os](https://os.phil-opp.com/zh-CN/freestanding-rust-binary/) 博客内容进行编写，学习和了解rust编写kernel os的知识点，供后面学习。

# 命令

- rustup update
- rustup target add thumbv7em-none-eabihf
- rustup override add nightly
- rustup component add llvm-tools-preview
- rustup component add rust-src 
- brew install qemu
- cargo install cargo-xbuild
- cargo xbuild --target x86_64-blog_os.json
- cargo xbuild
- cargo install bootimage
- cargo bootimage
- qemu-system-x86_64 -drive format=raw,file=bootimage-blog_os.bin

# bootloader bug

[github issues](https://github.com/phil-opp/blog_os/issues/403)

```markdown
Sevendaye commented on 27 May 2021
Starting from scratch and noticing this problem with bootloader 0.10.2 ― host OS is Fedora Rawhide and Rust version is 1.54.0-nightly (4de757209 2021-05-01):

Error: An error occured while trying to build the bootloader: The `bootloader` dependency has not the right format: No `package.metadata.bootloader.target` key found in Cargo.toml of bootloader
Particularly bizarre since I'm following this to the T and it worked fine last year. Oh, and obviously 0.10.2 > 0.5.1.

Hi,

I had the same problem, I was able to solve it by:

bootloader = "0.9.18" // In Cargo.toml
$cargo clean
$cargo bootimage --target .\x86_64-blog_os.json
$cargo run
It seems that there is a problem after version 0.9.18 of the bootlader crate

```