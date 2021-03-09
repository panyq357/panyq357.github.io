---
layout: post
title:  "博客搭建流程"
date:   2021-02-16 18:35:00 +0800
categories: 笔记
---

本文简要记录了在 WSL2 Ubuntu-20.04 下用 Jekyll 搭建 Github Pages 博客的过程。

> 注：由于作者懒得再弄一遍，本文主要靠记忆写成，可能有遗漏。

### 1、安装 Ruby、Jekyll 和 Bundler

按照 [Jekyll 的官方教程](https://jekyllrb.com/docs/installation/ubuntu/)，在 WSL2 Ubuntu-20.04 中安装 Ruby、Jekyll 和 Bundler。

```bash
# 安装 Ruby。
sudo apt-get install ruby-full build-essential zlib1g-dev
```

```bash
# 设置 Ruby Gems 的安装位置为家目录下的 gems 目录。
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

```bash
# （可选）使用 TUNA 的 Ruby Gems 镜像。
gem sources --add https://mirrors.tuna.tsinghua.edu.cn/rubygems/ --remove https://rubygems.org/
```

> 参考：<https://mirrors.tuna.tsinghua.edu.cn/help/rubygems/>

```bash
# 安装 Jekyll 和 Bundler。
gem install jekyll bundler
```

### 2、新建一个博客

按照 [Jekyll 的官方教程](https://jekyllrb.com/docs/)，新建一个博客。

```bash
jekyll new myblog
```

在运行完这行命令后，当前目录下会出现一个 ``myblog`` 目录，这就是一个模板博客了。

（模板博客套用了 Jekyll 官方的 [Minima 主题](https://github.com/jekyll/minima)）

### 3、启用 github-pages 插件

切换进博客目录。

```bash
cd myblog
```

修改这个目录下的 ``Gemfile`` 文件。按照其中注释的说明，将 ``gem "jekyll", "~> 4.2.0"`` 注释掉，并将 ``gem "github-pages", group: :jekyll_plugins`` 取消注释，最后变成这样。

```ruby
# （此前省略很多行……）
# This will help ensure the proper Jekyll version is running.
# Happy Jekylling!
# gem "jekyll", "~> 4.2.0"
# This is the default theme for new Jekyll sites. You may change this to anything you like.
gem "minima", "~> 2.5"
# If you want to use GitHub Pages, remove the "gem "jekyll"" above and
# uncomment the line below. To upgrade, run `bundle update github-pages`.
gem "github-pages", group: :jekyll_plugins
# If you have any plugins, put them here!
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
end
# （此后省略很多行……）
```

修改完并保存后，在博客目录下执行 ``bundle update``，使刚才在 ``Gemfile`` 中的改动生效。

### 4、推送至 Github

在 Github 上新建一个仓库，并命名为 ``<用户名>.github.io``。（过程可参考 [GitHub Pages 的官方教程](https://docs.github.com/en/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll#creating-a-repository-for-your-site)）

在博客目录下用 Git 初始化，然后连接远程仓库，并推送博客内容到远程仓库。

```bash
git init
git add --all
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:<用户名>/<用户名>.github.io.git # 这里换成自己的链接。
git push -u origin main
```

稍等片刻后，访问 ``<用户名>.github.io`` 即可看到更新好的模板博客。

### 5、修改博客的内容

有关 Jekyll 的基本知识，可参看 Jekyll 官网的 ["Step by Step Tutorial"](https://jekyllrb.com/docs/step-by-step/01-setup/)。

在掌握了基本知识后，可根据以下文档对模板博客进行修改。

- [Jekyll 官网上关于 Themes 的说明](https://jekyllrb.com/docs/themes/)
- [Minima 主题的 README](https://github.com/jekyll/minima)
