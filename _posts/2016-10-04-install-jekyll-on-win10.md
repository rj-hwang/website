---
layout: blog
title: Jekyll + GitHub Pages 开发坏境配置 - Win10 篇
---

# {{page.title}}

## 1. 安装 [Ruby]
我下载的版本是 [rubyinstaller-2.3.1-x64.exe]，安装完毕后用 `'ruby -v'` 确认安装成功：

```
> ruby -v
ruby 2.3.1p112 (2016-04-26 revision 54768) [x64-mingw32]
> gem -v
2.5.1
```

## 2. 更换 [Ruby] 镜像源为国内源
[Ruby] 默认的镜像源地址是 <https://rubygems.org>, 众所周知在国内访问是龟速，国内可选的镜像源基本上就是 [Ruby China 镜像源] 和 [Ruby 淘宝镜像源]。

Ruby China 镜像源的地址是：<https://gems.ruby-china.org/>  
Ruby 淘宝镜像源的地址是：<https://ruby.taobao.org/>

社区现在好像都推荐使用 [Ruby China 镜像源]，因此如下命令就是直接更换为使用 [Ruby China 镜像源]：

```shell
> gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
```

> 如果遇到 SSL 证书问题又无法解决，可直接用 <http://gems.ruby-china.org> 避免 SSL 的问题。

最后确保只有 gems.ruby-china.org，不要同时使用两个或以上的镜像源。使用如下命令可以查看当前正在使用的源：

```shell
> gem sources -l
*** CURRENT SOURCES ***

https://gems.ruby-china.org/
```

如果不小心添加了多个源，使用如下命令移除不需要的源地址：

```shell
> gem sources --remove https://rubygems.org/
```

## 3. 安装 [Ruby DevKit] - DEVELOPMENT KIT
我下载的是 [DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe]，下载后解压到指定目录，进入解压后的目录执行如下命令即安装完毕：

```shell
> ruby dk.rb init
> ruby dk.rb install
```

## 4. 安装 bundler 和配置 bundler 镜像

```shell
> gem install bundler
> bundle config mirror.https://rubygems.org https://gems.ruby-china.org
```

> 如果遇到 SSL 证书问题又无法解决，可直接用 <http://gems.ruby-china.org> 避免 SSL 的问题。

## 5. 安装 [Jekyll] 及 GitHub Pages 支持
创建 Gemfile 文件（无扩展名），内容为如下两行：

```
source 'https://rubygems.org'
gem 'github-pages'
```

在 Gemfile 文件所在目录下执行如下命令安装 Jekyll + GitHub Pages 支持：

```
> bundler install
```

到此 [Jekyll] 的 Blog 开发环境就配置完毕！

> 如果要安装 [Jekyll] 文档则执行 `'gem install jekyll-docs'` 进行安装，运行 `'jekyll docs'` 启动。

## 6. 注意事项

[Jekyll] 网站的文件应该全部使用 UTF8 无 BOM 格式，否则在生成网站的过程中会报 "Liquid Exception: Incompatible character encoding" 异常；在Windows平台，在终端可以通过 "chcp 65001" 命令切换到 UTF8 编码。

## 7. 参考

- Jekyll 官网：[英文](https://jekyllrb.com)、[中文](http://jekyllcn.com/)
- [Jekyll 创始人的示例库](https://github.com/mojombo/tpw)
- [关于 Windows 下证书无法验证问题 (certificate verify failed)](https://github.com/ruby-china/rubygems-mirror/wiki#关于-windows-下证书无法验证问题-certificate-verify-failed) - 2016-08-31
- [搭建免费无限流量 Blog - GitHub Pages 和 Jekyll 入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html) - 阮一峰 2012-08-25


[Jekyll]: https://jekyllrb.com
[Ruby]: https://www.ruby-lang.org/
[Ruby China 镜像源]: https://gems.ruby-china.org/
[Ruby 淘宝镜像源]: https://ruby.taobao.org/
[Ruby DevKit]: http://rubyinstaller.org/downloads/
[rubyinstaller-2.3.1-x64.exe]: http://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-2.3.1-x64.exe
[DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe]: http://dl.bintray.com/oneclick/rubyinstaller/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe