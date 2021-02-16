---
layout: post
title:  "Linux 入门小教程"
date:   2021-01-24 9:43:00 +0800
categories: 教程
---

## 前言

为什么要学习 Linux 呢？因为：

1. 我们要分析数据（比如测序数据）。
2. 但是数据太多太大，自己的小电脑装不下、跑不动。
3. 所以想用所以性能强大的计算集群来分析数据。
4. 然而计算集群的操作系统是 Linux，之前没学过。😥

所以学习 Linux 还是很有必要的。

Linux 是个操作系统，所以要想学习 Linux，肯定需要一台装着 Linux 的电脑。

但是在自己的电脑上装一个完整的 Linux 很麻烦，也不是所有人都有集群的账号，虚拟机又很笨重......

所幸微软在 Windows 10 中加入了 WSL (Windows Subsystem for Linux) 的功能，这使得我们可以在自己的电脑上想装 APP 一样装 Linux。

## 安装 WSL

> 如果您知识渊博，可参看极为详尽的微软的官方教程 -> [右键新标签页打开](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10)。

Win10 默认是没有开启 WSL 这项功能的，我们需要先启用这个功能。

首先，按 ``Windows 键 + Q 键`` 呼出 Win10 的搜索界面，搜索 ``启用或关闭 Windows 功能``。

然后，找到 ``适用于 Linux 的 Windows 子系统`` 勾选后确定，之后重启电脑，WSL 功能就开启了。

![启用 WSL 功能](/assets/images/linux-mini-tutorial/启用WSL功能.gif)

重启电脑之后，打开 Win10 自带的 Microsoft Store，搜索 Linux，就能找到许多 Linux 发行版，在这里，我们选择安装 Ubuntu。

![从 Microsoft Store 安装 Ubuntu](/assets/images/linux-mini-tutorial/从MicrosoftStore安装Ubuntu.gif)

> 什么是 Linux 发行版呢？简单来说，Linux 是个操作系统内核，但只有一个光秃秃的内核没法用呀。发行版不只有 Linux 内核，还包含着许多常用软件，使其能够“开箱即用”。

启动刚安装的 Ubuntu，它会自动开始安装。

````bash
Installing, this may take a few minutes...
````

安装完成后，你需要设置一下这个 “迷你操作系统” 的用户名和密码。（注意：处于安全原因，输入密码时屏幕上是不会显示密码的内容的，输入之后回车就好。）

（井号及其之后的部分是我添加的注释）

````bash
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: ZhangSan # 提示输入用户名
New password: # 输入过程不会显示东西
Retype new password: # 再输一遍确认
passwd: password updated successfully
# 后面内容略
````

输入完成后，你就拥有一个小型 Linux 操作系统啦。🎉

## Linux 初探

是的没错，这个黑框框（**终端**）就是大名鼎鼎 Linux 操作系统的界面。

刚才输入完用户名和密码后，系统会在屏幕上显示出一些系统信息，以及安装成功的提示信息。但最后，屏幕上会出现类似这样的东西：

````bash
ZhangSan@ZhangSanPC:~$
````

这是一种叫做提示符（prompt）的东西，它的出现告诉我们，系统正在等待你输入**命令**。

Linux 就是这样一种操作系统，用户通过在终端中输入命令（而不是用鼠标点点点）来指示电脑完成各种各样的工作。

接下来让我们学习一些基础命令。

## 目录相关操作

Linux 是个由文件和目录（Linux 的目录就是 Windows 的文件夹）组成的操作系统，而我们也正处在某个目录之下。

用户当前所在的目录有个特殊的名字，叫**工作目录**（Work Directory)。

我们可以用 ``pwd``（**P**rint **W**ork **D**irectory）命令查询我们当前所在的工作目录的**绝对路径**。

> 绝对路径：文件或目录在整个文件系统中所处的位置，如果用我国的邮政地址来比喻的话，就是像“中国北京市朝阳区北辰西路1号院2号”这样的地址。

````bash
ZhangSan@ZhangSanPC:~$ pwd # 回车
/home/ZhangSan # 我们所在目录的绝对路径
ZhangSan@ZhangSanPC:~$ # 提示符重新出现，等待用户输入新的命令
````

在路径 ``/home/ZhangSan`` 中，最左边的一条斜线（``/``）代表**根目录**，之后的 ``home`` 代表 home 目录，再之后的斜线（``/``）就只是分隔符了，最后的 ``ZhangSan`` 代表 ZhangSan 目录，在 Linux 中，每一个用户都有一个自己专属的目录。

> 根目录：用刚才的邮政地址来比喻的话，根目录就相当于“中国”这一级。

所以这个路径告诉我们，我们正处在根目录下的 home 目录下的 ZhangSan 目录下……

我们已经知道自己所处在那个目录下了，那么这个目录下有什么东西呢？我们可以用 ``ls`` 命令列出（**L**i**s**t）当前目录下的内容。

````bash
ZhangSan@ZhangSanPC:~$ ls
ZhangSan@ZhangSanPC:~$
````

终端中没有打印出新的东西，也就是说当前工作目录下没有东西。

既然如此，就让我们创建一点东西吧，``mkdir``（**M**a**k**e **Dir**ectory）命令可以用来创建文件夹。

````bash
ZhangSan@ZhangSanPC:~$ mkdir hello_dir # 注意中间有个空格
ZhangSan@ZhangSanPC:~$ ls # 再用 ls 命令
hello_dir # hello_dir 目录已创建
ZhangSan@ZhangSanPC:~$
````

刚才我们用 ``mkdir`` 命令在当前工作目录下创建了一个叫 ``hello_dir`` 的目录，那么如果我想在 ``hello_dir`` 里再创建一个目录，要怎么办呢？

我们可以用 ``cd``（**C**hange **D**irectory）命令改变工作目录，然后再用 ``mkdir`` 命令在新的工作目录下创建文件夹。

````bash
ZhangSan@ZhangSanPC:~$ cd hello_dir # 将工作目录切换至 hello_dir 目录下
ZhangSan@ZhangSanPC:~/hello_dir$ mkdir nihao_dir # 在 hello_dir 下新建 nihao_dir 目录
ZhangSan@ZhangSanPC:~/hello_dir$ ls # 列出 hello_dir 目录下的内容
nihao_dir
ZhangSan@ZhangSanPC:~/hello_dir$ cd nihao_dir # 将工作目录切换至 nihao_dir 目录下
ZhangSan@ZhangSanPC:~/hello_dir/nihao_dir$ mkdir konnichiwa_dir # 在 nihao_dir 下新建 konnichiwa_dir 目录
ZhangSan@ZhangSanPC:~/hello_dir/nihao_dir$ ls # 列出 nihao_dir 目录下的内容
konnichiwa_dir
ZhangSan@ZhangSanPC:~/hello_dir/nihao_dir$
````

> 输命令的时候一个字母一个字母地打字很麻烦？尝试先输入一两个字母，然后按一下 Tab 键。😉
> 自动补齐目录的名字时会多一个 ``/``？这不碍事的，有无最后一个 ``/`` 都一样。

不难发现，当我们切换工作目录时，终端的提示符也发生了改变。

以最后一个提示符 ``ZhangSan@ZhangSanPC:~/hello_dir/nihao_dir$`` 为例，这个提示符显示的信息有：

1. 当前用户名为 ``ZhangSan``。
2. 当前主机名为 ``ZhangSanPC``。（就是电脑的名字）
3. 当前所处的工作目录的路径为 ``~/hello_dir/nihao_dir``

``@``、``:`` 和 ``$`` 则是一些分隔符。

那么问题来了，这个 ``~/hello_dir/nihao_dir`` 中的波浪线 ``~`` 是什么呢？

让我们用 ``pwd`` 查看一下当前工作目录的绝对路径。

````bash
ZhangSan@ZhangSanPC:~/hello_dir/nihao_dir$ pwd
/home/ZhangSan/hello_dir/nihao_dir
ZhangSan@ZhangSanPC:~/hello_dir/nihao_dir$
````

``~`` 其实就是 ``/home/ZhangSan`` 的简写，也就是当前用户的专属目录的绝对路径简写。

像这样的路径简写还有很多，比如 ``.``（一个英语的句点）和 ``..``（两个英语的句点）。``.`` 是当前工作目录的简写，``..`` 是当前工作目录的上一层目录的简写。

让我们用 ``cd`` 命令来验证一下。

````bash
ZhangSan@ZhangSanPC:~/hello_dir/nihao_dir$ cd . # 原地踏步
ZhangSan@ZhangSanPC:~/hello_dir/nihao_dir$ cd .. # 返回上一层目录
ZhangSan@ZhangSanPC:~/hello_dir$ cd .. # 再返回上一层目录
ZhangSan@ZhangSanPC:~$ # 回到最开始的地方
````

现在我们回到了 ``~`` 目录（也就是 ``\home\ZhangSan`` 目录）下，如果我要重新返回 ``nihao_dir`` 目录下要怎么办呢？

我们当然可以像之前那样两次调用 ``cd`` 命令，但也可以这样做。

````bash
ZhangSan@ZhangSanPC:~$ cd hello_dir/nihao_dir
ZhangSan@ZhangSanPC:~/hello_dir/nihao_dir$ cd ~
ZhangSan@ZhangSanPC:~$
````

这次，我们在使用 ``cd`` 命令时，提供的不只是一个目录的名字了，而是一个**相对路径**了。

> 相对路径：文件或目录相对于当前工作目录的路径，可以形象地理解为“往北走50米，再往东走300米就是北餐厅了”这样的“地址”。

绝对路径和相对路径的主要区别就是路径的最左边的符号，绝对路径的最左侧为 ``/``（代表根目录）或 ``~``（另一个绝对路径的缩写），相对路径最左侧没有符号，或是像 ``.``（代表当前目录） 和 ``..``（代表上一层目录）这样的相对路径缩写。下面是一些例子。

````bash
/home/ZhangSan/hello_dir/nihao_dir # 绝对路径
~/hello_dir/nihao_dir # 带简写的绝对路径
hello_dir/nihao_dir # 相对路径
../ZhangSan/hello_dir/nihao_dir # 带简写的相对路径
````

单独的一个目录名是最简单的相对路径。

如果当前目录是 ``~``（``/home/ZhangSan``） 的话，上述四个路径是一样的。

回顾刚才的几个例子，不难发现，我们既给过 ``cd`` 命令绝对路径，也给过相对路径，只要路径是正确的，给那个都可以。

刚开始用 ``pwd``、``ls``、``cd`` 等命令就像学用筷子夹菜一样，需要适应一段时间。

但是觉得晕的话，也可以调用 Win10 的资源管理器，这是随 WSL 附赠的功能。

````bash
ZhangSan@ZhangSanPC:~$ explorer.exe . # 在当前目录（注意有个"."）打开 Win10 的资源管理器
ZhangSan@ZhangSanPC:~$ # 会自动弹出个窗口
````

![explorer.exe](/assets/images/linux-mini-tutorial/explorer.exe.png)

然后就可以用习惯的方式探索 Linux 的文件结构了…………

嗯？怎么除了我们刚创建的目录（``hello_dir`` 等）还有一些以点（``.``）开头的目录和文件？

原来，在 Linux 中，以点开头的目录和文件名代表它们是隐藏的（在 Windows 下则不会）。所以在刚才，我们只用 ``ls`` 命令没能看到它们。

要想看到它们，我们得为 ``ls`` 命令加一个 ``-a`` 选项，来显示所有的（**A**ll）内容。

````bash
ZhangSan@ZhangSanPC:~$ ls
hello_dir
ZhangSan@ZhangSanPC:~$ ls -a # 注意用空格隔开命令和选项
.  ..  .bash_logout  .bashrc  .landscape  .motd_shown  .profile  hello_dir
ZhangSan@ZhangSanPC:~$
````

加上 ``-a`` 选项之后，隐藏的目录和文件都被显示了出来。

``ls`` 也可用来列出指定目录下的内容。

````bash
ZhangSan@ZhangSanPC:~$ ls hello_dir
nihao_dir
ZhangSan@ZhangSanPC:~$ ls -a hello_dir
.  ..  nihao_dir # 这里也有 . 和 .. 目录
ZhangSan@ZhangSanPC:~$
````

原来，我们之所以能用 ``.`` 和 ``..`` 这样的简写来表示当前目录和上层目录，是因为每个目录下都有 ``.`` 和 ``..`` 这样的具有特殊跳转功能的隐藏目录呀。

在刚才的例子中，我们通过 ``ls -a hello_dir`` 这一串内容，列出了 ``hello_dir`` 目录下的所有内容（包括隐藏目录）。

在 Linux 中，命令的基本结构如下：

````bash
[命令的名字] [选项] [参数] # 中间用空格分开
````

以 ``ls -a hello_dir`` 为例，``ls`` 就是命令的名字，``-a`` 是选项的名字，``hello_dir`` 是参数的内容，在这里是一个我们想要列出其内容的目录的相对路径。

其中命令的名字必须写在开头，选项的名字一般都以 ``-``（一个减号） 或 ``--``（两个减号）开头，以和参数有所区分，而选项和参数之间**没有关联**的话，可以随意排序，比如刚才的命令还可以这样写。

````bash
ZhangSan@ZhangSanPC:~$ ls hello_dir -a # 调换了顺序
.  ..  nihao_dir
ZhangSan@ZhangSanPC:~$ ls hello_dir --all # --all 和 -a 是同一个选项的不同写法
.  ..  nihao_dir
ZhangSan@ZhangSanPC:~$
````

如何删掉刚才创建的练习用的文件夹呢？Linux 中用于删除的命令是 ``rm``。

````bash
ZhangSan@ZhangSanPC:~$ rm hello_dir
rm: cannot remove 'hello_dir': Is a directory
ZhangSan@ZhangSanPC:~$ ls
hello_dir
ZhangSan@ZhangSanPC:~$
````

``rm`` 命令默认删除的是文件，所以单独使用 ``rm`` 命令是无法删除目录的（防止一个误操作把所有东西都删了😉），需要加一个 ``-r`` 选项，这个选项不仅让 ``rm`` 命令能够删除目录，还能够循环地（**R**ecursive）删除目录里的所有子目录和文件。

````bash
ZhangSan@ZhangSanPC:~$ ls
hello_dir
ZhangSan@ZhangSanPC:~$ rm -r hello_dir
ZhangSan@ZhangSanPC:~$ ls
ZhangSan@ZhangSanPC:~$
````

## 文件相关操作

在 Linux 中，一切皆文件，所以让我们来创建一个文件。

创建空文件最简单的命令是 ``touch`` 命令。

（在接下来的教程中，提示符将用一个 ``$`` 替代）

````bash
$ touch abc.txt
$ ls
abc.txt
$
````

那么问题来了，``touch`` 和创建文件有什么关系呢？其实这个命令的另一个用途是用来更新一个文件的最后修改时间的（即，摸一下这个文件），当指定的文件不存在时，才会创建一个新的文件。

如何验证刚创建的文件是空的呢？我们可以用 ``cat`` 命令查看文件的内容。

````bash
$ cat abc.txt
$
````

什么输出都没有，确实是空的。但是问题又来了，``cat`` 跟打印文件内容有什么关系呢？原来，``cat`` 命令本来的用途是用来拼接（con**cat**enate）文件的内容，并将其输出到屏幕上，而我们只将一个文件的名字作为参数传给了它，所以它就直接将该文件的内容输出到了屏幕上。

空的文件可没什么意思，让我们往文件里添点内容吧。

就像 Windows 中有记事本一样，在 Linux 下也有 nano 这个简单易用的文本编辑器，我们可以用 ``nano`` 命令来调用这个文本编辑器。

````bash
$ nano abc.txt
# 回车后切换至 nano 的界面
````

然后就进入 nano 文本编辑器的界面了。

现在就可以随意输入一些内容了。（我输入了 ``abcdefg``）

![nano](/assets/images/linux-mini-tutorial/nano.png)

之所以说 nano 是一个简单易用的文本编辑器，就是因为 nano 把使用方法都列在屏幕的下方了。例如 ``M-U Undo`` 就告诉我们：按 Alt + U 键能撤销操作，而 ``^G Get Help`` 告诉我们：按 Ctrl + G 可查看更详细的帮助文档。

> 为什么用 ``M`` 和 ``^`` 表示 Alt 键和 Ctrl 键呢？主要是一些历史原因，两个参考文献 -> 【[M](https://stackoverflow.com/questions/26285791/unix-what-modifier-key-does-m-refer-to-e-g-m-c)】 【[\^](https://en.wikipedia.org/wiki/Caret_notation)】

输入完内容后，按 Ctrl + X 键即可；提示是否保存，按 Y 确定；提示让我们设置保存的文件名，这里不修改，直接按回车保存。

再用 ``cat`` 命令试试。

````bash
$ cat abc.txt
abcdefg
$ cat abc.txt abc.txt # 拼接同一个文件
abcdefg
abcdefg
$
````

嗯，内容确实被修改了，``cat`` 也确实可以拼接（con**cat**enate）文件的内容并输出。

现在让我们新建一个目录 ``alphabet``。

````bash
$ mkdir alphabet
$ ls
abc.txt  alphabet
$
````

如果我想把 ``abc.txt`` 放到 ``alphabet`` 目录下，该怎么做呢？

在 Windows 下，我们可以用鼠标把文件拖进文件夹，而在 Linux 下，得用 ``mv`` 命令将文件移动（**M**o**v**e）进目录。

````bash
$ ls
abc.txt  alphabet
$ mv abc.txt alphabet
$ ls
alphabet
$ ls alphabet
abc.txt
$
````

``mv`` 命令的结构如下：

````bash
mv [要移动的文件的路径] [移动的目的地路径]
````

这里，两个路径参数的顺序不能颠倒。

``mv`` 命令同样也可以移动目录。

````bash
$ mkdir upper
$ touch upper/ABC.TXT # 在 upper 目录下创建 ABC.TXT 空文件
$ mv upper alphabet
$ ls
alphabet
$ ls alphabet/
abc.txt  upper
$
````

``mv`` 命令不仅可以移动文件和目录，还能修改文件或目录的名字。

````bash
$ ls
alphabet
$ mv alphabet ALPHABET # 原地改名
$ ls
ALPHABET
$ ls ALPHABET/
abc.txt  upper
$ mv ALPHABET/abc.txt def.txt # 移动的同时改名
$ ls ALPHABET/
upper
$ ls
ALPHABET  def.txt
````

既然有用于“剪切/粘贴”的 ``mv``，自然也有用于“复制/粘贴”的 ``cp``（**C**o**p**y）了，``cp`` 的用法与 ``mv`` 类似。

````bash
$ ls
ALPHABET  def.txt
$ ls ALPHABET/
upper
$ cp def.txt ALPHABET/ghi.txt # 复制的同时改名
$ ls ALPHABET/
ghi.txt  upper
$
````

同样的 ``cp`` 也能复制目录，但要额外加一个 ``-r`` 选项（与 ``rm`` 命令的 ``-r`` 选项意思相同，防止一个误操作复制了个超大的文件把硬盘挤爆了😜）。

````bash
$ ls
ALPHABET  def.txt
$ cp ALPHABET/ alphabet_copy
cp: -r not specified; omitting directory 'ALPHABET/' # 报错，无法复制
$ ls
ALPHABET  def.txt
$ cp ALPHABET/ alphabet_copy -r
$ ls
ALPHABET  alphabet_copy  def.txt
$
````

好了，基础的内容就是这些了，让我们把刚创建的目录和文件都删了吧。

````bash
$ ls
ALPHABET  alphabet_copy  def.txt
$ rm -r * # 这是个星号
$ ls
$ # 删光了
````

这里 ``*`` 是一种叫做通配符的东西，它可以用来匹配一个或多个字符。在这里我们用它来代表这个目录下的所有文件和目录的相对路径，然后让 ``rm -r`` 把它们都删了。😉

## 最重要的命令

Linux 中的命令成千上万，每个命令都有各种各样的选项和用法，没有人能把它们都记下来。

``man``（**Man**ual）命令能够用来查询别的命令的用法。

````bash
$ man ls # 查询 ls 命令的用法
# 进到 man 的界面中
````

进到界面中后，按方向键即可上下翻阅，更详细的操作可按 ``h`` 查询。

具有类似的功能的命令还有 ``help`` 和 ``info``，三个命令的覆盖范围各不相同，当用一个不好用时可以试试另一个。

通过查询 ``ls`` 的用法可以得知，可通过添加 ``-l`` 选项，展示详细信息。

````bash
$ ls -al # -a 和 -l 两个选项可以合并起来写
total 8
drwxr-xr-x 1 ZhangSan ZhangSan 4096 Jan 23 18:34 .
drwxr-xr-x 1 root  root  4096 Jan 23 10:25 ..
-rw------- 1 ZhangSan ZhangSan 2128 Jan 23 18:49 .bash_history
-rw-r--r-- 1 ZhangSan ZhangSan  220 Jan 23 10:25 .bash_logout
-rw-r--r-- 1 ZhangSan ZhangSan 3771 Jan 23 10:25 .bashrc
drwxr-xr-x 1 ZhangSan ZhangSan 4096 Jan 23 10:25 .landscape
drwxr-xr-x 1 ZhangSan ZhangSan 4096 Jan 23 15:38 .local
-rw-r--r-- 1 ZhangSan ZhangSan    0 Jan 23 10:25 .motd_shown
-rw-r--r-- 1 ZhangSan ZhangSan  807 Jan 23 10:25 .profile
$
````

额，好像又多了很多需要进一步学习的东西，这就留到以后的教程吧（如果还有的话😉）。

## 参考

1. [鸟哥的 Linux 私房菜](https://linux.vbird.org/)
   台湾同胞撰写的 Linux 教程，文风幽默，相当经典。
2. [The Missing Semester of Your CS Education](https://missing.csail.mit.edu/)
   MIT 的大杂烩课程，什么都讲。
3. [网道 - Bash 脚本教程](https://wangdoc.com/bash/)
   阮一峰撰写的 Bash 脚本教程，实用性很强。