🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*


# 命令行的艺术

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [前言](#前言)
- [基础](#基础)
- [日常使用](#日常使用)
- [文件及数据处理](#文件及数据处理)
- [系统调试](#系统调试)
- [单行脚本](#单行脚本)
- [冷门但有用](#冷门但有用)
- [仅限 OS X 系统](#仅限-os-x-系统)
- [仅限 Windows 系统](#仅限-windows-系统)
- [更多资源](#更多资源)
- [免责声明](#免责声明)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

熟练使用命令行是一种常常被忽视，或被认为难以掌握的技能，但实际上，它会提高你作为工程师的灵活性以及生产力。本文是一份我在 Linux 上工作时，发现的一些命令行使用技巧的摘要。有些技巧非常基础，而另一些则相当复杂，甚至晦涩难懂。这篇文章并不长，但当你能够熟练掌握这里列出的所有技巧时，你就学会了很多关于命令行的东西了。

这篇文章是[许多作者和译者](AUTHORS.md)共同的成果。
这里的部分内容
[首次](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[出现](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
于 [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know)，
但已经迁移到了 Github，并由众多高手做出了许多改进。
如果你在本文中发现了错误或者存在可以改善的地方，请[**贡献你的一份力量**](/CONTRIBUTING.md)。

## 前言

涵盖范围：

- 这篇文章对刚接触命令行的新手，以及具有命令行使用经验的人都有用处。本文致力于做到*覆盖面广*（尽量包括一切重要的内容），*具体*（给出最常见的具体的例子），以及*简洁*（避免不必要的，或是可以在其他地方轻松查到的细枝末节）。每个技巧在特定情境下或是基本的，或是能显著节约时间。
- 本文为 Linux 所写，除了[仅限 OS X 系统](#仅限-os-x-系统)和[仅限 Windows 系统](#仅限-windows-系统)的部分。其它节中的大部分内容都适用于其它 Unix 系统或 OS X，甚至 Cygwin。
- 本文关注于交互式 Bash，尽管很多技巧也适用于其他 shell 或 Bash 脚本。
- 本文包括了“标准的”Unix 命令和需要安装特定包的命令，只要它们足够重要。

注意事项：

- 为了能在一页内展示尽量多的东西，一些具体的信息会被间接地包含在引用页里。聪明机智的你，如果掌握了使用 Google 搜索引擎的基本思路与命令，那么你将可以查阅到更多的详细信息。使用 `apt-get`，`yum`，`dnf`，`pacman`，
`pip` 或 `brew`（以及其它合适的包管理器）来安装新程序。
- 使用 [Explainshell](http://explainshell.com/) 去获取相关命令、参数、管道等内容的解释。


## 基础

- 学习 Bash 的基础知识。具体来说，输入 `man bash` 并至少全文浏览一遍; 它很简单并且不长。其他的 shell 可能很好用，但 Bash 功能强大到几乎所有情况下都是可用的 （ *只*学习 zsh，fish 或其他的 shell 的话，在你自己的电脑上会显得很方便，但在很多情况下会限制你，比如当你需要在服务器上工作时）。

- 学习并掌握至少一个基于文本的编辑器。通常 Vim （`vi`） 会是你最好的选择，因为在终端里进行随机编辑，Vim 真的毫无敌手，哪怕是 Emacs、某大型 IDE 甚至时下非常流行的编辑器。

- 学会如何使用 `man` 命令去阅读文档。学会使用 `apropos` 去查找文档。了解有些命令并不对应可执行文件，而是Bash内置的，可以使用 `help` 和 `help -d` 命令获取帮助信息。你可以用 `type 命令` 来判断它到底是可执行文件、shell 内置命令、还是别名。

- 学会使用 `>` 和 `<` 来重定向输出和输入，学会使用 `|` 来重定向管道。明白 `>` 会覆盖了输出文件而 `>>` 是在文件末添加。了解标准输出 stdout 和标准错误 stderr。

- 学会使用通配符 `*` （或许再算上 `?` 和 `[`...`]`） 和引用以及引用中 `'` 和 `"` 的区别。

- 熟悉 Bash 任务管理工具：`&`，**ctrl-z**，**ctrl-c**，`jobs`，`fg`，`bg`，`kill` 等。

- 了解 `ssh`，以及学会通过使用 `ssh-agent`，`ssh-add` 等命令来实现基本的无密码认证。

- 学会基本的文件管理：`ls` 和 `ls -l` （了解 `ls -l` 中每一列代表的意义），`less`，`head`，`tail` 和 `tail -f` （甚至 `less +F`），`ln` 和 `ln -s` （了解硬链接与软链接的区别），`chown`，`chmod`，`du` （硬盘使用情况概述：`du -hs *`）。 关于文件系统的管理，学习 `df`，`mount`，`fdisk`，`mkfs`，`lsblk`。知道 inode 是什么（与 `ls -i` 和 `df -i` 等命令相关）。

- 学习基本的网络管理：`ip` 或 `ifconfig`，`dig`。

- 学习并使用一种版本控制管理系统，例如 `git`。

- 熟悉正则表达式，以及 `grep`／`egrep` 里不同参数的作用，例如 `-i`，`-o`，`-v`，`-A`，`-B` 和 `-C`，这些参数是值得学习并掌握的。

- 学会使用 `apt-get`，`yum`，`dnf` 或 `pacman` （取决于你使用的 Linux 发行版）来查找或安装软件包。并确保你的环境中有 `pip` 来安装基于 Python 的命令行工具 （接下来提到的部分程序使用 `pip` 来安装会很方便）。


## 日常使用

- 在 Bash 中，可以使用 **Tab** 自动补全参数，使用 **ctrl-r** 搜索命令行历史（在按下之后，键入便可以搜索，重复按下 **ctrl-r** 会在更多匹配中循环，按下 **Enter** 会执行找到的命令，按下右方向键会将结果放入当前行中，使你可以进行编辑）。

- 在 Bash 中，可以使用 **ctrl-w** 删除你键入的最后一个单词，使用 **ctrl-u** 删除整行，使用 **alt-b** 和 **alt-f** 以单词为单位移动光标，使用 **ctrl-a** 将光标移至行首，使用 **ctrl-e** 将光标移至行尾，使用 **ctrl-k** 删除光标至行尾的所有内容，使用 **ctrl-l** 清屏。键入 `man readline` 查看 Bash 中的默认快捷键，内容很多。例如 **alt-.** 循环地移向前一个参数，以及 **alt-*** 展开通配符。


- 你喜欢的话，可以键入 `set -o vi` 来使用 vi 风格的快捷键，而 `set -o emacs` 可以把它改回来。

- 为了方便地键入长命令，在设置你的编辑器后（例如 `export EDITOR=vim`），键入 **ctrl-x** **ctrl-e** 会打开一个编辑器来编辑当前命令。在 vi 模式下则键入 **escape-v** 实现相同的功能。

- 键入 `history` 查看命令行历史记录，再用 `!n`（`n` 是命令编号）就可以再次执行。其中有许多缩写，最有用的大概就是用 `!$` 指代上次键入的参数，以及用 `!!` 指代上次键入的命令了（参考 man 页面中的“HISTORY EXPANSION”）。不过这些通常被 **ctrl-r** 和 **alt-.** 取代。

- 要进入 home 目录可以用 `cd`。要访问你的 home 目录中的文件，可以使用前缀 `~`（例如 `~/.bashrc`）。在 `sh` 脚本里则用 `$HOME` 指代 home 目录。

- 回到上一个工作路径：`cd -`

- 如果你输入命令的时候改变了主意，按下 **alt-#** 在行首添加 `#`，或者依次按下 **ctrl-a**， **#**， **enter**。这样做的话，之后你可以很方便的利用命令行历史回到你刚才输入到一半的命令。

- 使用 `xargs` （ 或 `parallel`）。他们非常给力。注意到你可以控制每行参数个数（`-L`）和最大并行数（`-P`）。如果你不确定它们是否会按你想的那样工作，先使用 `xargs echo` 查看一下。此外，使用 `-I{}` 会很方便。例如：
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```


- `pstree -p` 有助于展示进程树。

- 使用 `pgrep` 和 `pkill` 根据名字查找进程或发送信号（`-f` 参数通常有用）。

- 了解你可以发往进程的信号的种类。比如，使用 `kill -STOP [pid]` 停止一个进程。使用 `man 7 signal` 查看详细列表。

- 使用 `nohup` 或 `disown` 使一个后台进程持续运行。

- 使用 `netstat -lntp` 或 `ss -plat` 检查哪些进程在监听端口（默认是检查 TCP 端口; 使用参数 `-u` 检查 UDP 端口）。

- 有关打开套接字和文件，请参阅 `lsof`。

- 使用 `uptime` 或 `w` 来查看系统已经运行多长时间。

- 使用 `alias` 来创建常用命令的快捷形式。例如：`alias ll='ls -latr'` 创建了一个新的命令别名 `ll`。

- 把别名、shell 选项和常用函数保存在 `~/.bashrc`，然后[安排登陆 shell 来读取](http://superuser.com/a/183980/7106)。这样你就可以在所有 shell 会话中使用你的设定。

- 把环境变量的设定以及登陆时要执行的命令保存在 `~/.bash_profile`。对于从图形界面启动的，以及 `cron` 工作的 shell，需要单独配置。

- 要在几台电脑中同步你的配置文件（例如 `.bashrc` 和 `.bash_profile`），可以用 Git。

- 当变量和文件名中包含空格的时候要格外小心。Bash 变量要用引号括起来，比如 `"FOO"`。尽量使用 `-0` 或 `-print0` 选项以便用空字符来分隔文件名，例如 `locate -0 pattern | xargs -0 ls -al` 或 `find / -print0 -type d | xargs -0 ls -al`。如果 for 循环中循环访问的文件名含有空格，只需用 `IFS=$'\n'` 把内部字段分隔符设为换行符。

- 在 Bash 脚本中，使用 `set -x` 去调试输出，尽可能地使用严格模式，使用 `set -e` 令脚本在发生错误时退出而不是继续运行，使用 `set -u` 来检查是否使用了未赋值的变量，使用 `set -o pipefail` 严谨地对待错误（尽管问题可能很微妙）。当牵扯到很多脚本时，使用 `trap`。一个好的习惯是在脚本文件开头这样写，这会使它检测一些错误，并在错误发生时中断程序并输出信息：
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- 在 Bash 脚本中，子 shell（使用括号 `(...)`）是一种组织参数的便捷方式。一个常见的例子是临时地移动工作路径，代码如下：
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- 在 Bash 中，要注意其中有许多形式的扩展。检查变量是否存在：`${name:?error message}`。例如，当 Bash 脚本需要一个参数时，可以使用这样的代码 `input_file=${1:?usage: $0 input_file}`。数学表达式：`i=$(( (i + 1) % 5 ))`。序列：`{1..10}`。截断字符串：`${var%suffix}` 和 `${var#prefix}`。例如，假设 `var=foo.pdf`，那么 `echo ${var%.pdf}.txt` 将输出 `foo.txt`。

- 使用括号扩展（`{`...`}`）来减少输入相似文本，并自动化文本组合。这在某些情况下会很有用，例如 `mv foo.{txt,pdf} some-dir`（同时移动两个文件），`cp somefile{,.bak}`（会被扩展成 `cp somefile somefile.bak`）或者 `mkdir -p test-{a,b,c}/subtest-{1,2,3}`（会被扩展成所有可能的组合，并创建一个目录树）。

- 通过使用 `<(some command)` 可以将输出视为文件。例如，对比本地文件 `/etc/hosts` 和一个远程文件：
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- 了解 Bash 中的“here documents”，例如 `cat <<EOF ...`。

- 在 Bash 中，同时重定向标准输出和标准错误，`some-command >logfile 2>&1`。通常，为了保证命令不会在标准输入里残留一个打开了的文件句柄导致你当前所在的终端无法操作，添加 `</dev/null` 是一个好习惯。

- 使用 `man ascii` 查看具有十六进制和十进制值的ASCII表。`man unicode`，`man utf-8`，以及 `man latin1` 有助于你去了解通用的编码信息。

- 使用 `screen` 或 [`tmux`](https://tmux.github.io/) 来使用多个屏幕，当你在使用 ssh 时（保存 session 信息）将尤为有用。另一个轻量级的解决方案是 [`dtach`](https://github.com/bogner/dtach)。

- ssh 中，了解如何使用 `-L` 或 `-D`（偶尔需要用 `-R`）去开启隧道是非常有用的，例如当你需要从一台远程服务器上访问 web。

- 对 ssh 设置做一些小优化可能是很有用的，例如这个 `~/.ssh/config` 文件包含了防止特定环境下断开连接、压缩数据、多通道等选项：
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- 部分其他的关于 ssh 的选项是安全敏感的，而且应当小心启用。例如在可信任的网络中：`StrictHostKeyChecking=no`，`ForwardAgent=yes`

- 考虑使用 [`mosh`](https://mosh.mit.edu/) 作为 ssh 的替代品，它使用 UDP 协议。

- 获取文件的八进制格式权限，使用类似如下的代码：
```sh
      stat -c '%A %a %n' /etc/timezone
```

- 使用 [`percol`](https://github.com/mooz/percol) 或者 [`fzf`](https://github.com/junegunn/fzf) 可以交互式地从另一个命令输出中选取值。

- 使用 `fpp`（[PathPicker](https://github.com/facebook/PathPicker)）可以与基于另一个命令(例如 `git`）输出的文件交互。

- 将 web 服务器上当前目录下所有的文件（以及子目录）暴露给你所处网络的所有用户，使用：
`python -m SimpleHTTPServer 7777` （使用端口 7777 和 Python 2）或`python -m http.server 7777` （使用端口 7777 和 Python 3）。

- 以某种权限执行命令，使用`sudo`（root 权限）或`sudo -u`（其他用户）。使用`su`或者`sudo bash`来启动一个以对应用户权限运行的 shell。使用`su -`模拟其他用户的登录。

- 了解命令行的 [128K 限制](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong)。使用通配符匹配大量文件名时，常会遇到“Argument list too long”的错误信息。（这种情况下换用 `find` 或 `xargs` 通常可以解决。）

- 要实现基本的计算器功能（或者一般地使用 Python），可以使用 `python` 解释器。例如：
```
>>> 2+3
5
```


## 文件及数据处理

- 在当前路径下通过文件名定位一个文件，`find . -iname '*something*'`（或类似的）。在所有路径下通过文件名查找文件，使用 `locate something` （但请记住 `updatedb` 可能没有对最近新建的文件建立索引）。

- 使用 [`ag`](https://github.com/ggreer/the_silver_searcher) 在源代码或数据文件里检索（比 `grep -r` 更好）。

- 将 HTML 转为文本：`lynx -dump -stdin`

- Markdown，HTML，以及所有文档格式之间的转换，试试 [`pandoc`](http://pandoc.org/)。

- 如果你不得不处理 XML，`xmlstarlet` 宝刀未老。

- 使用 [`jq`](http://stedolan.github.io/jq/) 处理 JSON。

- 使用 [`shyaml`](https://github.com/0k/shyaml) 处理 YAML。

- Excel 或 CSV 文件的处理，[csvkit](https://github.com/onyxfish/csvkit) 提供了 `in2csv`，`csvcut`，`csvjoin`，`csvgrep` 等工具。

- 关于 Amazon S3，[`s3cmd`](https://github.com/s3tools/s3cmd) 很方便而 [`s4cmd`](https://github.com/bloomreach/s4cmd) 更快。Amazon 官方的 [`aws`](https://github.com/aws/aws-cli) 以及  [`saws`](https://github.com/donnemartin/saws) 是其他 AWS 相关工作的基础。

- 了解如何使用 `sort` 和 `uniq`，包括 uniq 的 `-u` 参数和 `-d` 参数，详见后文单行脚本节。另外可以了解一下 `comm`。

- 了解如何使用 `cut`，`paste` 和 `join` 来更改文件。很多人都会使用 `cut`，但几乎都不会使用 `join`。

- 了解如何运用 `wc` 去计算新行数（`-l`），字符数（`-m`），单词数（`-w`）以及字节数（`-c`）。

- 了解如何使用 `tee` 将标准输入复制到文件甚至标准输出，例如 `ls -al | tee file.txt`。

- 了解语言环境对许多命令行工具的微妙影响，包括排序的顺序和性能。大多数 Linux 的安装过程会将 `LANG` 或其他有关的变量设置为符合本地的设置。意识到当你改变语言环境时，排序的结果可能会改变。明白国际化可能会使 sort 或其他命令运行效率下降*许多倍*。某些情况下（例如集合运算）你可以放心的使用 `export LC_ALL=C` 来忽略掉国际化并使用基于字节的顺序。

- 你可以单独指定某一条命令的环境，只需在调用时把环境变量设定放在前面，例如 `TZ=Pacific/Fiji date`。

- 了解 `awk` 和 `sed` 关于数据的简单处理的用法。例如，将文本文件中第三列的所有数字求和：`awk '{ x += $3 } END { print x }'`. 这可能比同等作用的 Python 代码快三倍且代码量少三倍。

- 替换一个或多个文件中出现的字符串：
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- 使用 [`repren`](https://github.com/jlevy/repren) 来批量重命名，或是在多个文件中搜索替换。（有些时候 `rename` 命令也可以批量重命名，但要注意，它在不同 Linux 发行版中的功能并不完全一样。）
```sh
      # 将文件、目录和内容全部重命名 foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # 还原所有备份文件 whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # 用 rename 实现上述功能（若可用）:
      rename 's/\.bak$//' *.bak
```

- 根据 man 页面的描述，`rsync` 真的是一个快速且非常灵活的文件复制工具。它通常被用于机器间的同步，但在本地也同样有用。在安全限制允许下，用 `rsync` 代替 `scp` 可以实现续传，而不用重新从头开始。它同时也是删除大量文件的[最快方法](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html)之一：
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- 使用 `shuf` 从一个文件中随机选取多行。

- 了解 `sort` 的参数。处理数字方面，使用 `-n` 或者 `-h` 来处理可读性数字（例如 `du -h` 的输出）。明白键的工作原理（`-t` 和 `-k`）。例如，注意到你需要 `-k1，1` 来仅按第一个域来排序，而 `-k1` 意味着按整行排序。稳定排序（`sort -s`）在某些情况下很有用。例如，以第二个域为主关键字，第一个域为次关键字进行排序，你可以使用 `sort -k1，1 | sort -s -k2，2`。

- 如果你想在 Bash 命令行中写 tab 制表符，按下 **ctrl-v** **[Tab]** 或键入 `$'\t'` （后者可能更好，因为你可以复制粘贴它）。

- 标准的源代码对比及合并工具是 `diff` 和 `patch`。使用 `diffstat` 查看变更总览数据。注意到 `diff -r` 对整个文件夹有效。使用 `diff -r tree1 tree2 | diffstat` 查看变更总览数据。

- 对于二进制文件，使用 `hd` 使其以十六进制显示以及使用 `bvi` 来编辑二进制。

- 同样对于二进制文件，`strings`（包括 `grep` 等等）允许你查找一些文本。

- 二进制文件对比（Delta 压缩），使用 `xdelta3`。

- 使用 `iconv` 更改文本编码。而更高级的用法，可以使用 `uconv`，它支持一些高级的 Unicode 功能。例如，这条命令将所有元音字母转为小写并移除了：
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- 拆分文件，查看 `split`（按大小拆分）和 `csplit`（按模式拆分）。

- 用 [`dateutils`](http://www.fresse.org/dateutils/) 中的 `dateadd`、`datediff`、`strptime` 等工具操作日期和时间表达式。

- 使用 `zless`、`zmore`、`zcat` 和 `zgrep` 对压缩过的文件进行操作。

- 文件属性可以通过 `chattr` 进行设置，它比文件权限更加底层。例如，为了保护文件不被意外删除，可以使用不可修改标记：`sudo chattr +i /critical/directory/or/file`

- 使用 `getfacl` 和 `setfacl` 以保存和恢复文件权限。例如：
```sh
   getfacl -R /some/path > permissions.txt
   setfacl --restore=permissions.txt
```

## 系统调试

- `curl` 和 `curl -I` 可以便捷地被应用于 web 调试中，它们的好兄弟 `wget` 也可以，或者是更潮的 [`httpie`](https://github.com/jkbrzt/httpie)。

- 使用 `iostat`、`netstat`、`top` （`htop` 更佳）和 `dstat` 去获取硬盘、cpu 和网络的状态。熟练掌握这些工具可以使你快速的对系统的当前状态有一个大概的认识。

- 使用 `netstat` 和 `ss` 查看网络连接的细节。

- 若要对系统有一个深度的总体认识，使用 [`glances`](https://github.com/nicolargo/glances)。它在一个终端窗口中向你提供一些系统级的数据。这对于快速的检查各个子系统非常有帮助。

- 若要了解内存状态，运行并理解 `free` 和 `vmstat` 的输出。尤其注意“cached”的值，它指的是 Linux 内核用来作为文件缓存的内存大小，因此它与空闲内存无关。

- Java 系统调试则是一件截然不同的事，一个可以用于 Oracle 的 JVM 或其他 JVM 上的调试的技巧是你可以运行 `kill -3 <pid>` 同时一个完整的栈轨迹和堆概述（包括 GC 的细节）会被保存到标准输出/日志文件。JDK 中的 `jps`，`jstat`，`jstack`，`jmap` 很有用。[SJK tools](https://github.com/aragozin/jvm-tools) 更高级.

- 使用 [`mtr`](http://www.bitwizard.nl/mtr/) 去跟踪路由，用于确定网络问题。

- 用 [`ncdu`](https://dev.yorhel.nl/ncdu) 来查看磁盘使用情况，它比常用的命令，如 `du -sh *`，更节省时间。

- 查找正在使用带宽的套接字连接或进程，使用 [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) 或 [`nethogs`](https://github.com/raboof/nethogs)。

- `ab` 工具（捆绑于 Apache）可以简单粗暴地检查 web 服务器的性能。对于更复杂的负载测试，使用 `siege`。

- [`wireshark`](https://wireshark.org/)，[`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) 和 [`ngrep`](http://ngrep.sourceforge.net/) 可用于复杂的网络调试。

- 了解 `strace` 和 `ltrace`。这俩工具在你的程序运行失败、挂起甚至崩溃，而你却不知道为什么或你想对性能有个总体的认识的时候是非常有用的。注意 profile 参数（`-c`）和附加到一个运行的进程参数 （`-p`）。

- 了解使用 `ldd` 来检查共享库。

- 了解如何运用 `gdb` 连接到一个运行着的进程并获取它的堆栈轨迹。

- 学会使用 `/proc`。它在调试正在出现的问题的时候有时会效果惊人。比如：`/proc/cpuinfo`，`/proc/meminfo`，`/proc/cmdline`，`/proc/xxx/cwd`，`/proc/xxx/exe`，`/proc/xxx/fd/`，`/proc/xxx/smaps`（这里的 `xxx` 表示进程的 id 或 pid）。

- 当调试一些之前出现的问题的时候，[`sar`](http://sebastien.godard.pagesperso-orange.fr/) 非常有用。它展示了 cpu、内存以及网络等的历史数据。

- 关于更深层次的系统分析以及性能分析，看看 `stap`（[SystemTap](https://sourceware.org/systemtap/wiki)），[`perf`](https://en.wikipedia.org/wiki/Perf_(Linux))，以及[`sysdig`](https://github.com/draios/sysdig)。

- 查看你当前使用的系统，使用 `uname` ， `uname -a` （Unix／kernel 信息） 或者 `lsb_release -a` （Linux 发行版信息）。

- 无论什么东西工作得很欢乐时试试 `dmesg`（可能是硬件或驱动问题）。

- 如果你删除了一个文件，但通过 `du` 发现没有释放预期的磁盘空间，请检查文件是否被进程占用：
`lsof | grep deleted | grep "filename-of-my-big-file"`


## 单行脚本

一些命令组合的例子：

- 当你需要对文本文件做集合交、并、差运算时，结合使用 `sort`/`uniq` 很有帮助。假设 `a` 与 `b` 是两内容不同的文件。这种方式效率很高，并且在小文件和上G的文件上都能运用 （`sort` 不被内存大小约束，尽管在 `/tmp` 在一个小的根分区上时你可能需要 `-T` 参数），参阅前文中关于 `LC_ALL` 和 `sort` 的 `-u` 参数的部分。
```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- 使用 `grep . *`（每行都会附上文件名）或者 `head -100 *`（每个文件有一个标题）来阅读检查目录下所有文件的内容。这在检查一个充满配置文件的目录（如 `/sys`、`/proc`、`/etc`）时特别好用。


- 计算文本文件第三列中所有数的和（可能比同等作用的 Python 代码快三倍且代码量少三倍）：
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- 如果你想在文件树上查看大小/日期，这可能看起来像递归版的 `ls -l` 但比 `ls -lR` 更易于理解：
```sh
      find . -type f -ls
```

- 假设你有一个类似于 web 服务器日志文件的文本文件，并且一个确定的值只会出现在某些行上，假设一个 `acct_id` 参数在URI中。如果你想计算出每个 `acct_id` 值有多少次请求，使用如下代码：
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- 要连续地监测变化，可以使用 `watch`，例如检查某个文件夹中文件的改变，可以用 `watch -d -n 2 'ls -rtlh | tail'`；或者在排查 WiFi 设置故障时要监测网络设置的更改，可以用 `watch -d -n 2 ifconfig`。

- 运行这个函数从这篇文档中随机获取一条技巧（解析 Markdown 文件并抽取项目）：
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README-zh.md|
          pandoc -f markdown -t html |
          iconv -f 'utf-8' -t 'unicode' |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```

## 冷门但有用

- `expr`：计算表达式或正则匹配

- `m4`：简单地宏处理器

- `yes`：多次打印字符串

- `cal`：漂亮的日历

- `env`：执行一个命令（脚本文件中很有用）

- `printenv`：打印环境变量（调试时或在使用脚本文件时很有用）

- `look`：查找以特定字符串开头的单词

- `cut`、`paste` 和 `join`：数据修改

- `fmt`：格式化文本段落

- `pr`：将文本格式化成页/列形式

- `fold`：包裹文本中的几行

- `column`：将文本格式化成多列或表格

- `expand` 和 `unexpand`：制表符与空格之间转换

- `nl`：添加行号

- `seq`：打印数字

- `bc`：计算器

- `factor`：分解因数

- [`gpg`](https://gnupg.org/)：加密并签名文件

- `toe`：terminfo entries 列表

- `nc`：网络调试及数据传输

- `socat`：套接字代理，与 `netcat` 类似

- [`slurm`](https://github.com/mattthias/slurm)：网络可视化

- `dd`：文件或设备间传输数据

- `file`：确定文件类型

- `tree`：以树的形式显示路径和文件，类似于递归的 `ls`

- `stat`：文件信息

- `time`：执行命令，并计算执行时间

- `timeout`：在指定时长范围内执行命令，并在规定时间结束后停止进程

- `lockfile`：使文件只能通过 `rm -f` 移除

- `logrotate`： 切换、压缩以及发送日志文件

- `watch`：重复运行同一个命令，展示结果并高亮有更改的部分

- `tac`：反向输出文件

- `shuf`：文件中随机选取几行

- `comm`：一行一行的比较排序过的文件

- `pv`：监视通过管道的数据

- `hd`，`hexdump`，`xxd`，`biew` 和 `bvi`：保存或编辑二进制文件

- `strings`：从二进制文件中抽取文本

- `tr`：转换字母

- `iconv` 或 `uconv`：简易的文件编码

- `split` 和 `csplit`：分割文件

- `sponge`：在写入前读取所有输入，在读取文件后再向同一文件写入时比较有用，例如 `grep -v something some-file | sponge some-file`

- `units`：将一种计量单位转换为另一种等效的计量单位（参阅 `/usr/share/units/definitions.units`）

- `apg`：随机生成密码

- `7z`：高比例的文件压缩

- `ldd`：动态库信息

- `nm`：提取 obj 文件中的符号

- `ab`：性能分析 web 服务器

- `strace`：系统调用调试

- [`mtr`](http://www.bitwizard.nl/mtr/)：更好的网络调试跟踪工具

- `cssh`：可视化的并发 shell

- `rsync`：通过 ssh 或本地文件系统同步文件和文件夹

- [`wireshark`](https://wireshark.org/) 和 [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html)：抓包和网络调试工具

- [`ngrep`](http://ngrep.sourceforge.net/)：网络层的 grep

- `host` 和 `dig`：DNS 查找

- `lsof`：列出当前系统打开文件的工具以及查看端口信息

- `dstat`：系统状态查看

- [`glances`](https://github.com/nicolargo/glances)：高层次的多子系统总览

- `iostat`：硬盘使用状态

- `mpstat`： CPU 使用状态

- `vmstat`： 内存使用状态

- `htop`：top 的加强版

- `last`：登入记录

- `w`：查看处于登录状态的用户

- `id`：用户/组 ID 信息

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/)：系统历史数据

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) 或 [`nethogs`](https://github.com/raboof/nethogs)：套接字及进程的网络利用

- `ss`：套接字数据

- `dmesg`：引导及系统错误信息

- `sysctl`： 在内核运行时动态地查看和修改内核的运行参数

- `hdparm`：SATA/ATA 磁盘更改及性能分析

- `lsblk`：列出块设备信息：以树形展示你的磁盘以及磁盘分区信息

- `lshw`，`lscpu`，`lspci`，`lsusb` 和 `dmidecode`：查看硬件信息，包括 CPU、BIOS、RAID、显卡、USB设备等

- `lsmod` 和 `modinfo`：列出内核模块，并显示其细节

- `fortune`，`ddate` 和 `sl`：额，这主要取决于你是否认为蒸汽火车和莫名其妙的名人名言是否“有用”


## 仅限 OS X 系统

以下是*仅限于* OS X 系统的技巧

- 用 `brew` （Homebrew）或者 `port` （MacPorts）进行包管理。这些可以用来在 OS X 系统上安装以上的大多数命令。

- 用 `pbcopy` 复制任何命令的输出到桌面应用，用 `pbpaste` 粘贴输入。

- 若要在 OS X 终端中将 Option 键视为 alt 键（例如在上面介绍的 **alt-b**、**alt-f** 等命令中用到），打开 偏好设置 -> 描述文件 -> 键盘 并勾选“使用 Option 键作为 Meta 键”。

- 用 `open` 或者 `open -a /Applications/Whatever.app` 使用桌面应用打开文件。

- Spotlight： 用 `mdfind` 搜索文件，用 `mdls` 列出元数据（例如照片的 EXIF 信息）。

- 注意 OS X 系统是基于 BSD UNIX 的，许多命令（例如 `ps`，`ls`，`tail`，`awk`，`sed`）都和 Linux 中有些微的不同，这些极大的被 System V-style Unix 和 GNU 工具影响。你可以通过标题为 "BSD General Commands Manual" 的 man 页面发现这些不同。在有些情况下 GNU 版本的命令也可能被安装（例如 `gawk` 和 `gsed` 对应 GNU 中的 awk 和 sed ）。如果要写跨平台的 Bash 脚本，避免使用这些命令（例如，考虑 Python 或者 `perl` ）或者经过仔细的测试。

- 用 `sw_vers` 获取 OS X 的版本信息。

## 仅限 Windows 系统

- 要在 Microsoft Windows 中使用 Unix shell，可以安装 [Cygwin](https://cygwin.com/)。本文档中介绍的大多数内容都将适用。

- 通过 Cygwin 的包管理器来安装额外的 Unix 程序。

- 使用 `mintty` 作为你的命令行窗口。

- 要访问 Windows 剪贴板，可以通过 `/dev/clipboard`。

- 运行 `cygstart` 以通过默认程序打开一个文件。

- 要访问 Windows 注册表，可以使用 `regtool`。

- 注意 Windows 驱动器路径 `C:\` 在 Cygwin 中用 `/cygdrive/c` 代表，而 Cygwin 的 `/` 在 Windows 中显示在 `C:\cygwin`。要转换 Cygwin 和 Windows 风格的路径可以用 `cygpath`。这在需要调用 Windows 程序的脚本里很有用。

- 学会使用 `wmic`，你就可以从命令行执行大多数 Windows 系统管理任务，并编成脚本。

## 更多资源

- [awesome-shell](https://github.com/alebcay/awesome-shell)：一份精心组织的命令行工具及资源的列表。
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line)：一份针对 OS X 命令行的更深入的指南。
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/)：为了编写更好的脚本文件。
- [shellcheck](https://github.com/koalaman/shellcheck)：一个静态 shell 脚本分析工具，本质上是 bash／sh／zsh 的 lint。
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html)：有关如何在 shell 脚本里正确处理文件名的细枝末节。
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools)：用于数据科学的一些命令和工具，摘自同名书籍。

## 免责声明

除去特别微小的任务，编写代码是出于方便阅读的目的。能力往往伴随着责任。你 *可以* 在 Bash 中做一些事并不意味着你应该去做！;)


## 授权条款

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

本文使用授权协议 [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/)。
