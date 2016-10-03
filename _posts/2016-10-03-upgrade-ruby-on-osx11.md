---
layout: blog
title: 升级 Mac OS X El Capitan 10.11.6 的 Ruby 到最新版并设置国内镜像源
---

# {{page.title}}

默认情况下，Mac OS X 系统已经安装好 Ruby，安装在 `/System/Library/Frameworks/Ruby.framework/Versions/Current` 目录下。

我机器的版本是 OS X El Capitan 10.11.6，通过终端分别输入 `ruby -v` 和 `gem -v` 得到如下结果：

```shell
$ ruby -v
ruby 2.0.0p648 (2015-12-16 revision 53162) [universal.x86_64-darwin15]
$ gem -v
2.0.14.1
```

截止到写这篇 blog 的时间，Ruby 的最新稳定版是 2.3.1。在 Mac OS X 上推荐使用 [Homebrew] 来安装、管理 [Ruby] 的版本。以下为详细过程。

## 1. 安装 [Homebrew]

执行以下命令即可完成 [Homebrew] 的安装（安装过程需回车确认，视网络情况可能需要很长的时间）：

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

该命令将会从 [Homebrew] 的 [GitHub 仓库](https://github.com/Homebrew/brew) 抓取最新版本并自动完成安装。安装成功后，即可使用 `brew` 命令来安装 [Ruby] 的最新版本，以及其他工具。

> [Homebrew] 的默认安装目录为 `/usr/local`，所有通过 `brew` 安装的程序都会默认安装到 `/usr/local/Cellar/程序名/版本号/` 目录下

安装过程的命令输出纪录为：

```shell
==> This script will install:
/usr/local/bin/brew
/usr/local/share/doc/homebrew
/usr/local/share/man/man1/brew.1
/usr/local/share/zsh/site-functions/_brew
/usr/local/etc/bash_completion.d/brew
/usr/local/Homebrew
==> The following new directories will be created:
/usr/local/Homebrew

Press RETURN to continue or any other key to abort
==> /usr/bin/sudo /bin/mkdir -p /usr/local/Homebrew
==> /usr/bin/sudo /bin/chmod g+rwx /usr/local/Homebrew
==> /usr/bin/sudo /bin/chmod u+rwx share/zsh share/zsh/site-functions
==> /usr/bin/sudo /usr/sbin/chown dragon /usr/local/Homebrew
==> /usr/bin/sudo /usr/bin/chgrp admin /usr/local/Homebrew
==> Downloading and installing Homebrew...
remote: Counting objects: 1090, done.
remote: Compressing objects: 100% (975/975), done.
remote: Total 1090 (delta 109), reused 560 (delta 80), pack-reused 0
Receiving objects: 100% (1090/1090), 1.06 MiB | 9.00 KiB/s, done.
Resolving deltas: 100% (109/109), done.
From https://github.com/Homebrew/brew
 * [new branch]      master     -> origin/master
HEAD is now at f90f52d Merge pull request #1205 from MikeMcQuaid/help-external-commands

==> Homebrew has enabled anonymous aggregate user behaviour analytics
Read the analytics documentation (and how to opt-out) here:
  https://git.io/brew-analytics
==> Tapping homebrew/core
Cloning into '/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core'...
remote: Counting objects: 3728, done.
remote: Compressing objects: 100% (3619/3619), done.
remote: Total 3728 (delta 10), reused 358 (delta 1), pack-reused 0
Receiving objects: 100% (3728/3728), 3.00 MiB | 14.00 KiB/s, done.
Resolving deltas: 100% (10/10), done.
Checking connectivity... done.
Tapped 3607 formulae (3,755 files, 9.3M)
Already up-to-date.
==> Installation successful!
==> Next steps
Run `brew help` to get started
Further documentation: https://git.io/brew-docs
```

整个过程花了我不止半个小时，好漫长。

## 2. 通过 `brew` 命令安装 [Ruby] 最新版本

在命令行下依次执行以下命令，即可自动完成最新版本 [Ruby] 的安装：

```
$ brew update
$ brew install ruby
$ sudo reboot
```

说明：

1. `brew update` 将会从 GitHub 上更新 brew 所支持的所有软件的版本信息，保证能够安装到最新的版本
2. `brew install ruby` 将会从 Ruby 的 GitHub 仓库抓取最新版本的代码，并编译安装
3. `sudo reboot` 重启，使新安装的 `/usr/local/bin/ruby` 生效。因 Capitan 使用了 [Rootless 机制]，`/usr/bin` 不能修改，`/usr/bin/ruby` 依然是 2.0 版，新安装的`/usr/local/bin/ruby` 才是当前最新版。

安装过程的命令输出纪录为：

```shell
$ brew install ruby
==> Installing dependencies for ruby: readline, libyaml, openssl
==> Installing ruby dependency: readline
==> Downloading https://homebrew.bintray.com/bottles/readline-7.0.el_capitan.bottle.tar.gz
######################################################################## 100.0%
==> Pouring readline-7.0.el_capitan.bottle.tar.gz
==> Caveats
This formula is keg-only, which means it was not symlinked into /usr/local.

OS X provides the BSD libedit library, which shadows libreadline.
In order to prevent conflicts when programs look for libreadline we are
defaulting this GNU Readline installation to keg-only.


Generally there are no consequences of this for you. If you build your
own software and it requires this formula, you'll need to add to your
build variables:

    LDFLAGS:  -L/usr/local/opt/readline/lib
    CPPFLAGS: -I/usr/local/opt/readline/include

==> Summary
    /usr/local/Cellar/readline/7.0: 45 files, 2M
==> Installing ruby dependency: libyaml
==> Downloading https://homebrew.bintray.com/bottles/libyaml-0.1.7.el_capitan.bottle.tar.gz
#####################################                                     52.4%
curl: (56) SSLRead() return error -9806
Error: Failed to download resource "libyaml"
Download failed: https://homebrew.bintray.com/bottles/libyaml-0.1.7.el_capitan.bottle.tar.gz
Warning: Bottle installation failed: building from source.
==> Using the sandbox
==> Downloading http://pyyaml.org/download/libyaml/yaml-0.1.7.tar.gz

curl: (6) Could not resolve host: pyyaml.org
Trying a mirror...
==> Downloading https://mirrors.kernel.org/debian/pool/main/liby/libyaml/libyaml_0.1.7.ori
######################################################################## 100.0%
==> ./configure --prefix=/usr/local/Cellar/libyaml/0.1.7
==> make install
    /usr/local/Cellar/libyaml/0.1.7: 8 files, 306.5K, built in 2 minutes 1 second
==> Installing ruby dependency: openssl
==> Downloading https://homebrew.bintray.com/bottles/openssl-1.0.2j.el_capitan.bottle.tar.gz
######################################################################## 100.0%
==> Pouring openssl-1.0.2j.el_capitan.bottle.tar.gz
==> Caveats
A CA file has been bootstrapped using certificates from the system
keychain. To add additional certificates, place .pem files in
  /usr/local/etc/openssl/certs

and run
  /usr/local/opt/openssl/bin/c_rehash

This formula is keg-only, which means it was not symlinked into /usr/local.

Apple has deprecated use of OpenSSL in favor of its own TLS and crypto libraries

Generally there are no consequences of this for you. If you build your
own software and it requires this formula, you'll need to add to your
build variables:

    LDFLAGS:  -L/usr/local/opt/openssl/lib
    CPPFLAGS: -I/usr/local/opt/openssl/include

==> Summary
    /usr/local/Cellar/openssl/1.0.2j: 1,695 files, 12M
==> Installing ruby
==> Downloading https://homebrew.bintray.com/bottles/ruby-2.3.1_2.el_capitan.bottle.tar.gz
######################################################################## 100.0%
==> Pouring ruby-2.3.1_2.el_capitan.bottle.tar.gz
==> Caveats
Emacs Lisp files have been installed to:
  /usr/local/share/emacs/site-lisp/ruby
==> Summary
    /usr/local/Cellar/ruby/2.3.1_2: 1,261 files, 18.8M
```

安装成功后，重新执行 `ruby -v` 确认已成功安装了最新版本的 Ruby：

```shell
$ ruby -v
ruby 2.3.1p112 (2016-04-26 revision 54768) [x86_64-darwin15]
$ gem -v
2.5.1
```

## 3. 更换 [Ruby] 镜像源为国内源
[Ruby] 默认的镜像源地址是 <https://rubygems.org>, 众所周知在国内访问是龟速，国内可选的镜像源基本上就是 [Ruby China 镜像源] 和 [Ruby 淘宝镜像源]。

Ruby China 镜像源的地址是：<https://gems.ruby-china.org/>  
Ruby 淘宝镜像源的地址是：<https://ruby.taobao.org/>

社区现在好像都推荐使用 [Ruby China 镜像源]，因此如下命令就是直接更换为使用 [Ruby China 镜像源]：

```shell
$ gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
```

> 如果遇到 SSL 证书问题又无法解决，可直接用 http://gems.ruby-china.org 避免 SSL 的问题。

最后确保只有 gems.ruby-china.org，不要同时使用两个或以上的镜像源。使用如下命令可以查看当前正在使用的源：

```shell
$ gem sources -l
*** CURRENT SOURCES ***

https://gems.ruby-china.org/
```

如果不小心添加了多个源，使用如下命令移除不需要的源地址：

```shell
$ gem sources --remove https://rubygems.org/
```

## 4. 参考

- [ruby-china: Mac OS X 上安装 Ruby](https://github.com/ruby-china/ruby-china/wiki/Mac-OS-X-%E4%B8%8A%E5%AE%89%E8%A3%85-Ruby) - 2014-05-03
- [简书：Mac OS X 11中的/usr/bin 的“Operation not permitted”](http://www.jianshu.com/p/22b89f19afd6) - 2015-10-30
- [关于 Windows 下证书无法验证问题 (certificate verify failed)](https://github.com/ruby-china/rubygems-mirror/wiki#关于-windows-下证书无法验证问题-certificate-verify-failed) - 2016-08-31


[Ruby]: https://www.ruby-lang.org/
[Ruby China 镜像源]: https://gems.ruby-china.org/
[Ruby 淘宝镜像源]: https://ruby.taobao.org/
[Homebrew]: http://brew.sh/
[Rootless 机制]: http://www.jianshu.com/p/22b89f19afd6