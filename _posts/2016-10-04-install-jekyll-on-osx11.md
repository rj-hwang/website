---
layout: blog
title: Jekyll + GitHub Pages 开发坏境配置 - Mac OS X El Capitan 10.11.6 篇
---

# {{page.title}}


## 1. 安装 Xcode Command-Line Tools

从 App Store 上下载 Xcode 后，默认是不会安装「Command Line Tools」的，「Command Line Tools」是 Xcode 中的一款工具，使可以在命令行中运行 C 程序。执行如下命令安装：

```shell
$ xcode-select -v
xcode-select version 2343.
$ xcode-select --install
```

`xcode-select --install` 实际上是启动了 /System/Library/CoreServices/Install Command Line Developer Tools.app 应用，从 Apple 服务器上下载安装「Command Line Tools」：

![图1]({{ site.github.url }}/images/apple/xcode-select-install.jpg){:style="max-width:100%"}

成功安装后，「Command Line Tools」将安装在 `/Library/Developer/CommandLineTools` 目录下。可以通过重复执行命令 `xcode-select --install` 来验证是否已经安装成功：

```shell
$ xcode-select --install
xcode-select: error: command line tools are already installed, use "Software Update" to install updates
```

## 2. 安装 [NodeJS]

到 [NodeJS] 官网下载安装最新的稳定版即可，安装后通过 `node -v` 和 `npm -v` 查看版本信息：

```shell
$ node -v
v6.2.1
$ npm -v
3.9.3
```

## 3. 升级 [Ruby] 到当前最新版并设置国内镜像源

请移步：[升级 Mac OS X El Capitan 10.11.6 的 Ruby 到最新版并设置国内镜像源]。安装好之后如下查看一下版本信息：

```shell
$ ruby -v
ruby 2.3.1p112 (2016-04-26 revision 54768) [x86_64-darwin15]
$ gem -v
2.5.1
```

## 4. 安装 Bundler 和配置 bundler 使用国内镜像

```shell
$ gem install bundler // 如果 bundler 已经安装，这个命令会将其升级到最新版本
$ bundle config mirror.https://rubygems.org https://gems.ruby-china.org
$ bundler -v
Bundler version 1.13.2
```

注：如遇 SSL 问题又懒得解决，将后面的 https 替换为 http 即可。

## 5. 安装 [Jekyll] 及 GitHub Pages 支持
创建 Gemfile 文件（无扩展名），内容为如下两行：

```
source 'https://rubygems.org'
gem 'github-pages'
```

在 Gemfile 文件所在目录下执行如下命令安装 Jekyll + GitHub Pages 支持：

```
$ bundler install
```

到此 [Jekyll] 的 Blog 开发环境就配置完毕！

`bundler install` 命令输出的结果纪录如下：

```shell
Fetching gem metadata from https://gems.ruby-china.org/............
Fetching version metadata from https://gems.ruby-china.org/..
Resolving dependencies...
Installing i18n 0.7.0
Using json 1.8.3
Installing minitest 5.9.1
Installing thread_safe 0.3.5
Installing addressable 2.4.0
Installing coffee-script-source 1.10.0
Installing execjs 2.7.0
Installing colorator 1.1.0
Installing ffi 1.9.14 with native extensions
Installing multipart-post 2.0.0
Installing forwardable-extended 2.6.0
Installing gemoji 2.1.0
Installing net-dns 0.8.0
Installing public_suffix 1.5.3
Installing sass 3.4.22
Installing rb-fsevent 0.9.7
Installing kramdown 1.11.1
Installing liquid 3.0.6
Installing mercenary 0.3.6
Installing rouge 1.11.1
Installing safe_yaml 1.0.4
Installing jekyll-feed 0.5.1
Installing mini_portile2 2.1.0
Installing jekyll-paginate 1.1.0
Installing jekyll-sitemap 0.10.0
Installing minima 1.2.0
Installing unicode-display_width 1.1.1
Using bundler 1.13.2
Installing tzinfo 1.2.2
Installing coffee-script 2.4.1
Installing ethon 0.9.1
Installing rb-inotify 0.9.7
Installing faraday 0.9.2
Installing pathutil 0.14.0
Installing jekyll-sass-converter 1.3.0
Installing nokogiri 1.6.8.1 with native extensions
Installing terminal-table 1.7.3
Installing activesupport 4.2.7
Installing jekyll-coffeescript 1.0.1
Installing typhoeus 0.8.0
Installing listen 3.0.6
Installing sawyer 0.7.0
Installing html-pipeline 2.4.2
Installing jekyll-watch 1.5.0
Installing octokit 4.3.0
Installing jekyll 3.2.1
Installing github-pages-health-check 1.2.0
Installing jekyll-gist 1.4.0
Installing jekyll-github-metadata 2.0.2
Installing jekyll-mentions 1.2.0
Installing jekyll-redirect-from 0.11.0
Installing jekyll-seo-tag 2.0.0
Installing jemoji 0.7.0
Installing github-pages 96
Bundle complete! 1 Gemfile dependency, 54 gems now installed.
Use `bundle show [gemname]` to see where a bundled gem is installed.
Post-install message from html-pipeline:
-------------------------------------------------
Thank you for installing html-pipeline!
You must bundle Filter gem dependencies.
See html-pipeline README.md for more details.
https://github.com/jch/html-pipeline#dependencies
-------------------------------------------------
Post-install message from github-pages:
---------------------------------------------------
Thank you for installing github-pages!
GitHub Pages recently upgraded to Jekyll 3.0, which
includes some breaking changes. More information:
https://github.com/blog/2100-github-pages-jekyll-3
---------------------------------------------------
```

## 6. 注意事项

[Jekyll] 网站的文件应该全部使用 UTF8 无 BOM 格式，否则在生成网站的过程中会报 "Liquid Exception: Incompatible character encoding" 异常。

## 7. 参考

- [Complete guide to install Xcode Command Line Tools  for Mac OS X El Capitan](http://railsapps.github.io/xcode-command-line-tools.html) - 2016-08-25
- [Xcode 中 Command Line Tools 安装方法](http://blog.csdn.net/chenyufeng1991/article/details/47007979) - 2015-07-22
- Jekyll 官网：[英文](https://jekyllrb.com)、[中文](http://jekyllcn.com/)
- [Jekyll 创始人的示例库](https://github.com/mojombo/tpw)
- [搭建免费无限流量 Blog - GitHub Pages 和 Jekyll 入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html) - 阮一峰 2012-08-25

[Ruby]: https://www.ruby-lang.org/
[Jekyll]: https://jekyllrb.com
[升级 Mac OS X El Capitan 10.11.6 的 Ruby 到最新版并设置国内镜像源]: {{ site.github.url }}/2016/10/03/upgrade-ruby-on-osx11.html
[NodeJS]: https://nodejs.org/