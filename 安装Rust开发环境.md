# 前言

Rust 默认安装目录是 ~/.cargo，对于内存困难户来说很不友好（特别是 Windows C 盘困难户），所以我一般会修改默认安装位置。安装 Rust 环境时会读取两个环境变量： RUSTUP_HOME 和 CARGO_HOME，分别用于设置 rustup 和 cargo 安装目录（其中二进制可执行程序放在 $CARGO_HOME/bin 目录下）。

如果这两个环境变量不存在，就会默认安装在当前用户 .cargo 目录。所以，修改默认安装目录只需要创建两个文件夹并配置对应的环境变量即可，以 Linux 为例（Windows同理）：

创建目录：

```bash
sudo mkdir -p /usr/local/rust/rustup
sudo mkdir -p /usr/local/rust/cargo
```

配置环境变量：

```bash
export RUSTUP_HOME=/usr/local/rust/rustup
export CARGO_HOME=/usr/local/rust/cargo
export PATH=$PATH:$CARGO_HOME/bin
```

其中 $CARGO_HOME/bin 目录不存在，不过先配置到 PATH 中，稍后就不需要配置了。

对于 MacOS 用户来说，在 /usr/local 目录下创建的文件普通用户没有写和执行权限。因此最好使用 chmod 修改文件夹权限或使用 chown 修改文件夹所属用户，我比较倾向 chown 命令：

```bash
sudo chown -R [user][:group] /usr/local/rust
```

|**Note**|
|:-------|
|Linux 用户其实不需要修改权限，只需要使用超级管理员权限（`sudo` 或 `sh - -c "command"`）安装即可。|

# Linux 安装

官网提供的安装脚本命令（[https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install)）执行时会立即安装，比较推荐的做法是先将 shell 脚本下载下来，稍后选择自定义参数安装。

下载安装脚本：

```bash
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs -o rustup-init.sh

# 脚本增加执行权限
$ chmod +x rustup-init.sh
```

脚本提供了一些可选的安装参数，可以使用 help 命令输出帮助信息：

```bash
$ ./rustup-init.sh --help
```

不过我只需要使用 `--no-modify-path` 参数即可，该参数用于指定不自动配置环境变量（因为前面已经修改环境变量 PATH 了）。

```bash
$ bash rustup-init.sh --no-modify-path
```

之后会输出一些信息，包括 rustup 及 cargo 安装位置。如果没有设置环境变量（RUSTUP_HOME 和 CARGO_HOME）默认安装位置就会是 ~/.cargo：

```
info: downloading installer

Welcome to Rust!

This will download and install the official compiler for the Rust
programming language, and its package manager, Cargo.

Rustup metadata and toolchains will be installed into the Rustup
home directory, located at:

  /usr/local/rust/rustup

This can be modified with the RUSTUP_HOME environment variable.

The Cargo home directory is located at:

  /usr/local/rust/cargo

This can be modified with the CARGO_HOME environment variable.

The cargo, rustc, rustup and other commands will be added to
Cargo's bin directory, located at:

  /usr/local/rust/cargo/bin

This path needs to be in your PATH environment variable,
but will not be added automatically.

You can uninstall at any time with rustup self uninstall and
these changes will be reverted.

Current installation options:


   default host triple: x86_64-apple-darwin
     default toolchain: stable (default)
               profile: default
  modify PATH variable: no

1) Proceed with standard installation (default - just press enter)
2) Customize installation
3) Cancel installation
>
```

选择 1 或直接回车即可，安装完成后输出信息通常如下：

```
Rust is installed now. Great!

To get started you need Cargo's bin directory (/usr/local/rust/cargo/bin) in
your PATH
environment variable. This has not been done automatically.

To configure your current shell, you need to source
the corresponding env file under /usr/local/rust/cargo.

This is usually done by running one of the following (note the leading DOT):
. "/usr/local/rust/cargo/env"            # For sh/bash/zsh/ash/dash/pdksh
source "/usr/local/rust/cargo/env.fish"  # For fish
```

之后重新打开命令终端测试下安装是否 OK：

```bash
$ rustc -V
rustc 1.79.0 (129f3b996 2024-06-10)

$ cargo -V
cargo 1.79.0 (ffa9cf99a 2024-06-03)
```

# Windows 安装

直接到官网下载 Windows 安装程序即可（[https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install)），需要说明的是，做 Rust 开发需要 <u>Microsoft C++ Build Tools 环境</u>，否则安装时会提示类似如下信息：

```PowerShell
PS C:\Users\WINDOWS\Downloads> .\rustup-init.exe

Rust Visual C++ prerequisites

Rust requires a linker and Windows API libraries but they don't seem to be
available.

These components can be acquired through a Visual Studio installer.

1) Quick install via the Visual Studio Community installer
   (free for individuals, academic uses, and open source).

2) Manually install the prerequisites
   (for enterprise and advanced users).

3) Don't install the prerequisites
   (if you're targeting the GNU ABI).

>
```

你可以选择输入 1 进行快速安装或直接到 visualstudio 官网下载 [Microsoft C++ Build Tools](https://visualstudio.microsoft.com/zh-hans/visual-cpp-build-tools/) 安装程序。

下载完成后直接双击安装，安装时只需要勾选 **使用C++的桌面开发（Desktop development with C++）** 即可。另外还可以修改默认的安装位置（C盘内存困难户特别建议修改默认安装位置）。

之后重新 Rust 安装程序即可！

# 更新

```bash
rustup update
```

# 卸载

```bash
rustup self uninstall
```
