# 命令行的艺术

- [必读](#必读)
- [基础](#基础)
- [日常使用](#日常使用)
- [文件及数据处理](#文件及数据处理)
- [系统调试](#系统调试)
- [一行代码](#一行代码)
- [冷门但有用](#冷门但有用)
- [更多资源](#更多资源)
- [免责声明](#免责声明)
- [授权条款](#授权条款)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

熟练使用命令行是一种常常被忽视或被认为晦涩难懂，但实际上，它可以提高你作为工程师的灵活性以及生产力。本文是一份我在Linux上工作时发现的一些关于命令行的使用的小技巧的摘要。这些小技巧有基础的、相当复杂的甚至晦涩难懂的。这篇文章并不长，但当你能够熟练掌握这里列出的所有技巧时，你就学会了很多关于命令行的东西了。

这里的大部分内容
[首次](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[出现](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
于 [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know)，但考虑到这里的人们都具有学习的天赋且乐于接受别人的建议，使用Github来做这件事是更佳的选择。如果你在本文中发现了错误或者存在可以改善的地方，请果断提交Issue或Pull Request！(当然在提交前请看一下必读节和已有的issue/PR)。


## 必读

涵盖范围:

- 这篇文章对刚接触命令行的新手以及具有命令行使用经验的人都有用处。本文致力于做到覆盖面广(尽量包括一切重要的内容)，具体(给出最常见的具体的例子)以及简洁(避免一些不必要的东西以及一些偏题的可以在其他地方翻阅到文献的东西)。 每个小技巧在某个特定情境下都是基本的或能够显著地节约时间。
- 本文为Linux所写，但很多内容(并非所有的)同样适用于MacOS甚至Cygwin。
- 本文关注于交互式Bash，尽管很多技巧适用于其他shell或Bash脚本。
- 本文包括了"标准的"Unix命令和需要安装特定包的命令，只要它们足够重要。

注意事项:

- 为了能在一页内展示尽量多的东西，一些具体的信息会被间接的包含在引用页里。聪明机智的你如果掌握了使用 Google 搜索引擎的基本思路与命令，那么你将可以查阅到更多的详细信息。使用 `apt-get`/`yum`/`dnf`/`pacman`/`pip`/`brew`来安装新程序。
- 使用 [Explainshell](http://explainshell.com/) 去获取相关命令、参数、管道等内容的解释。


## 基础

- 学习Bash的基础知识。具体来说，输入 `man bash` 并至少全文浏览一遍; 它很简单并且不长。其他的shell可能很好用，但Bash功能强大且几乎所有情况下都是可用的 ( *只*学习 zsh，fish或其他的shell的话，在你自己的电脑上会显得很方便，但在很多情况下会限制你，比如当你需要在服务器上工作时)。

- 学习并掌握至少一个基于文本的编辑器。通常 Vim (`vi`) 会是你最好的选择。

- 学会如何使用`man`命令去阅读文档。学会使用`apropos`去查找文档。了解有些命令并不对应可执行文件，而是Bash内置的，可以使用`help`和`help -d`命令获取帮助信息。

- 学会使用`>`和`<`来重定向输出和输入，学会使用`|`来重定向管道。了解标准输出stdout和标准错误stderr。

- 学会使用通配符`*` ( 若能`?`和`{`...`}`更好) 和引用以及引用中`'`和`"`的区别。

- 熟悉Bash任务管理工具: `&`，**ctrl-z**，**ctrl-c**，`jobs`，`fg`，`bg`，`kill` 等。

- 了解`ssh`，以及基本的无密码认证，`ssh-agent`，`ssh-add`等。

- 学会基本的文件管理: `ls` 和 `ls -l` (了解`ls -l`中每一列代表的意义)，`less`，`head`，`tail`和`tail -f` (甚至 `less +F`)，`ln` and `ln -s` (了解软连接和硬连接的区别)，`chown`，`chmod`，`du` (硬盘使用情况概述: `du -sk *`)。 关于文件系统的管理，学习 `df`，`mount`，`fdisk`，`mkfs`，`lsblk`。

- 学习基本的网络管理: `ip` 或 `ifconfig`，`dig`。

- 熟悉正则表达式，以及`grep`/`egrep`里不同参数的作用，例如`-i`，`-o`，`-A`，和 `-B`。

- 学会使用 `apt-get`，`yum`，`dnf` 或 `pacman` (取决于你使用的Linux发行版)来查找或安装包。确保你的环境中有 `pip` 来安装基于Python的命令行工具 (部分程序使用`pip`来安装会很简单)。


## 日常使用

- 在Bash中，可以使用**Tab**自动补全参数，使用**ctrl-r**搜索命令行历史。

- 在Bash中，使用**ctrl-w**删除你键入的最后一个单词，使用**ctrl-u**删除整行，使用**alt-b**和**alt-f**按单词移动，使用**ctrl-k**从光标处删除到行尾，使用**ctrl-l**清屏。键入`man readline`查看Bash中的默认快捷键，内容很多。例如**alt-.** 循环地移向前一个参数，以及**alt-***展开通配符。

- 你喜欢的话，可以键入`set -o vi`来使用vi风格的快捷键。

- 键入`history`查看命令行历史记录。其中有许多缩写，例如`!$` (最后键入的参数)和`!!`(最后键入的命令)，尽管通常被 **ctrl-r**和**alt-.**取代。

- 回到上一个工作路径: `cd -`

- 如果你输入命令的时候改变了主意，按下**alt-#**在行首添加`#`(将你输入的命令视为注释)，并回车。这样做的话，之后你可以很方便的利用命令行历史回到你刚才输入到一半的命令。

- 使用`xargs` ( 或`parallel`)。他们非常给力。注意到你可以控制每行参数个数(`-L`)和最大并行数 (`-P`)。如果你不确定它们是否会按你想的那样工作，先使用`xargs echo`查看一下。此外，使用`-I{}`会很方便。例如:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p`有助于展示进程树。

- 使用`pgrep`和`pkill`根据名字查找进程或发送信号。

- 了解你可以发往进程的信号的种类。比如，使用`kill -STOP [pid]`停止一个进程。使用`man 7 signal`查看详细列表。

- 使用`nohup`或`disown`使一个后台进程持续运行。

- 使用`netstat -lntp`或`ss -plat`检查哪些进程在监听端口(默认是检查TCP端口; 使用参数`-u`检查UDP端口)。

- 有关打开套接字和文件，请参阅`lsof`。

- 在Bash脚本中，使用`set -x`去调试输出，尽可能的使用严格模式，使用`set -e`令脚本在发生错误时退出而不是继续运行，使用`set -o pipefail`严谨地对待错误(尽管问题可能很微妙)。当牵扯到很多脚本时，使用`trap`。

- 在Bash脚本中，子shell(使用括号`(...)`)是一种便捷的方式去组织参数。一个常见的例子是临时地移动工作路径，代码如下：
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- 在Bash中，注意到其中有许多形式的扩展。检查变量是否存在: `${name:?error message}`。例如，当Bash脚本需要一个参数时，可以使用这样的代码`input_file=${1:?usage: $0 input_file}`。数学表达式: `i=$(( (i + 1) % 5 ))`。序列: `{1..10}`。 截断字符串: `${var%suffix}`和`${var#prefix}`。例如，假设`var=foo.pdf`，那么`echo ${var%.pdf}.txt`将输出`foo.txt`。

- 通过使用`<(some command)`可以将输出视为文件。例如，对比本地文件`/etc/hosts`和一个远程文件:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- 了解Bash中的"here documents"，例如`cat <<EOF ...`。

- 在Bash中，同时重定向标准输出和标准错误，`some-command >logfile 2>&1`。通常，为了保证命令不会在标准输入里残留一个打开了的文件句柄导致你当前所在的终端无法操作，添加`</dev/null`是一个好习惯。

- 使用`man ascii`查看具有十六进制和十进制值的ASCII表。`man unicode`，`man utf-8`，以及 `man latin1` 有助于你去了解通用的编码信息。

- 使用`screen`或[`tmux`](https://tmux.github.io/)来使用多个屏幕，当你在使用ssh时(保存session信息)将尤为有用。另一个轻量级的解决方案是`dtach`。

- ssh中，了解如何使用`-L`或`-D`(偶尔需要用`-R`)去开启隧道是非常有用的，例如当你需要从一台远程服务器上访问web。

- 对ssh设置做一些小优化可能是很有用的，例如这个`~/.ssh/config`文件包含了防止特定环境下断开连接、压缩数据、多通道等选项：
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- 部分其他的关于ssh的选项是安全敏感且应当小心启用的。例如在可信任的网络中: `StrictHostKeyChecking=no`，`ForwardAgent=yes`

- 获取文件的八进制格式权限，使用类似如下的代码：
```sh
      stat -c '%A %a %n' /etc/timezone
```

- 使用[`percol`](https://github.com/mooz/percol)可以交互式地从另一个命令输出中选取值。

- 使用`fpp`([PathPicker](https://github.com/facebook/PathPicker))可以与基于另一个命令(例如`git`)输出的文件交互。

- 将web服务器上当前目录下所有的文件(以及子目录)暴露给你所处网络的所有用户，使用：
`python -m SimpleHTTPServer 7777` (使用端口7777和Python 2)或`python -m http.server 7777` (使用端口7777和Python 3)。


## 文件及数据处理

- 在当前路径下通过文件名定位一个文件，`find . -iname '*something*'`(或类似的)。在所有路径下通过文件名查找文件，使用 `locate something` (但请记住`updatedb`可能没有对最近新建的文件建立索引)。

- 使用[`ag`](https://github.com/ggreer/the_silver_searcher)在源或文件里检索(比`grep -r`更好)。

- 将HTML转为文本: `lynx -dump -stdin`

- Markdown，HTML，以及所有文档格式之间的转换，试试 [`pandoc`](http://pandoc.org/)。

- 如果你不得不处理XML，`xmlstarlet`宝刀未老。

- 使用`jq`处理json。

- Excel或CSV文件的处理，[csvkit](https://github.com/onyxfish/csvkit)提供了`in2csv`，`csvcut`，`csvjoin`，`csvgrep`等工具。

- 关于Amazon S3，[`s3cmd`](https://github.com/s3tools/s3cmd)很方便而[`s4cmd`](https://github.com/bloomreach/s4cmd)更快。Amazon官方的[`aws`](https://github.com/aws/aws-cli)是其他AWS相关工作的基础。

- 了解如何使用`sort`和`uniq`，包括uniq的`-u`参数和`-d`参数，详见后文一行代码节。另外可以了解一下`comm`。

- 了解如何使用`cut`，`paste`和`join`来更改文件。大部分人都会使用`cut`但忘了`join`。

- 了解如何运用`wc`去计算新行数(`-l`)，字符数(`-m`)，单词数(`-w`)以及字节数(`-c`)。

- 了解如何使用`tee`将标准输入复制到文件甚至标准输出，例如`ls -al | tee file.txt`。

- 了解语言环境对许多命令行工具的微妙影响，包括排序的顺序和性能。大多数Linux的安装过程会将`LANG`或其他有关的变量设置为符合本地的设置。意识到当你改变语言环境时，排序的结果可能会改变。明白国际化可能会时sort或其他命令运行效率下降*许多倍*。某些情况下(例如集合运算)你可以放心的使用`export LC_ALL=C`来忽略掉国际化并使用基于字节的顺序。

- 了解`awk`和`sed`关于数据的简单处理的用法。例如，将文本文件中第三列的所有数字求和: `awk '{ x += $3 } END { print x }'`. 这可能比同等作用的Python代码块三倍且代码量少三倍。

- 替换一个或多个文件中出现的字符串:
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- 依据某种模式批量重命名多个文件，使用`rename`。对于复杂的重命名规则，[`repren`](https://github.com/jlevy/repren)或许有帮助。
```sh
      # Recover backup files foo.bak -> foo:
      rename 's/\.bak$//' *.bak
      # Full rename of filenames，directories，and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
```

- 使用`shuf`从一个文件中随机选取行。

- 了解`sort`的参数。明白键的工作原理(`-t`和`-k`)。例如，注意到你需要`-k1，1`来仅按第一个域来排序，而`-k1`意味着按整行排序。

- 稳定排序(`sort -s`)在某些情况下很有用。例如，以第二个域为主关键字，第一个域为次关键字进行排序，你可以使用`sort -k1，1 | sort -s -k2，2`

- 如果你想在Bash命令行中写tab制表符，按下**ctrl-v** **[Tab]** 或键入`$'\t'`(后者可能更好，因为你可以复制粘贴它)。

- 标准的源代码对比及合并工具是`diff`和`patch`。使用`diffstat`查看变更总览数据。注意到`diff -r`对整个文件夹有效。使用`diff -r tree1 tree2 | diffstat`查看变更总览数据。

- 对于二进制文件，使用`hd`使其以十六进制显示以及使用`bvi`来编辑二进制。

- 同样对于二进制文件，使用`strings`(包括`grep`等等)允许你查找一些文本。

- 二进制文件对比(Delta压缩)，使用`xdelta3`。

- 使用`iconv`更改文本编码。而更高级的用法，可以使用`uconv`，它支持一些高级的Unicode功能。例如，这条命令将所有元音字母转为小写并移除了:
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- 拆分文件，查看`split`(按大小拆分)和`csplit`(按模式拆分)。

- 使用`zless`，`zmore`，`zcat`和`zgrep`对压缩过的文件进行操作。


## 系统调试

- `curl`和`curl -I`可以便捷地被应用于web调试中，它们的好兄弟`wget`也可以，或者是更潮流的[`httpie`](https://github.com/jakubroztocil/httpie)。

- 使用`iostat`、`netstat`、`top` (`htop`更佳) 和`dstat`去获取硬盘、cpu和网络的状态。熟练掌握这些工具可以使你快速的对系统的当前状态有一个大概的认识。

- 若要对系统有一个深度的总体认识，使用[`glances`](https://github.com/nicolargo/glances)。它在一个终端窗口中向你提供一些系统级的数据。这对于快速的检查各个子系统非常有帮助。

- 若要了解内存状态，运行并理解`free`和`vmstat`的输出。尤其注意"cached"的值，它指的是Linux内核用来作为文件缓存的内存大小，因此它与空闲内存无关。

- Java系统调试则是一件截然不同的事，一个可以用于Oracle的JVM或其他JVM上的调试的小技巧是你可以运行`kill -3 <pid>`同时一个完整的栈轨迹和堆概述(包括GC的细节)会被保存到标准输出/日志文件。

- 使用`mtr`去跟踪路由，用于确定网络问题。

- 用`ncdu`来查看磁盘使用情况，它比常用的命令，如`du -sh *`，更节省时间。

- 查找正在使用带宽的套接字连接或进程，使用`iftop`或`nethogs`。

- `ab`工具(捆绑于Apache)可以简单粗暴地检查web服务器的性能。对于更复杂的负载测试，使用`siege`。

- `wireshark`，`tshark`和`ngrep`可用于复杂的网络调试。

- 了解`strace`和`ltrace`。这俩工具在你的程序运行失败、挂起甚至崩溃，而你却不知道为什么或你想对性能有个总体的认识的时候是非常有用的。注意profile参数(`-c`)和附加到一个运行的进程参数 (`-p`)。

- 了解使用`ldd`来检查共享库。

- 了解如何运用`gdb`连接到一个运行着的进程并获取它的堆栈轨迹。

- 学会使用`/proc`。它在调试正在出现的问题的时候有时会效果惊人。比如: `/proc/cpuinfo`，`/proc/xxx/cwd`，`/proc/xxx/exe`，`/proc/xxx/fd/`，`/proc/xxx/smaps`。

- 当调试一些之前出现的问题的时候，`sar`非常有用。它展示了cpu、内存以及网络等的历史数据。

- 关于更深层次的系统分析以及性能分析，看看`stap` ([SystemTap](https://sourceware.org/systemtap/wiki))，[`perf`](http://en.wikipedia.org/wiki/Perf_(Linux))，以及[`sysdig`](https://github.com/draios/sysdig)。

- 查看你当前使用的Linux发型版(大部分发行版有效): `lsb_release -a`

- 无论什么东西工作得很欢乐时试试`dmesg`(可能是硬件或驱动问题)。


## 一行代码

一些命令组合的例子:

- 当你需要对文本文件做集合交、并、差运算时，结合使用`sort`/`uniq`很有帮助。假设`a`与`b`是两内容不同的文件。这种方式效率很高，并且在小文件和上G的文件上都能运用 (`sort`不被内存大小约束，尽管在`/tmp`在一个小的根分区上时你可能需要`-T`参数)，参阅前文中关于`LC_ALL`和`sort`的`-u`参数的部分。
```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- 使用`grep . *`来阅读检查目录下所有文件的内容，例如检查一个充满配置文件的目录比如`/sys`、`/proc`、`/etc`。

- 计算文本文件第三列中所有数的和(可能比同等作用的Python代码块三倍且代码量少三倍):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- 如果你想在文件树上查看大小\日期，这可能看起来像递归版的`ls -l`但比`ls -lR`更易于理解:
```sh
      find . -type f -ls
```

- 尽可能的使用`xargs`或`parallel`。注意到你可以控制每行参数个数(`-L`)和最大并行数 (`-P`)。如果你不确定它们是否会按你想的那样工作，先使用`xargs echo`查看一下。此外，使用`-I{}`会很方便。例如:
```sh
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- 假设你有一个类似于web服务器日志文件的文本文件，并且一个确定的值只会出现在某些行上，假设一个`acct_id`参数在URI中。如果你想计算出每个`acct_id`值有多少次请求，使用如下代码:
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- 运行这个函数从这篇文档中随机获取一条小技巧(解析Markdown文件并抽取项目):
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```


## 冷门但有用

- `expr`: 计算表达式或正则匹配

- `m4`: 简单地宏处理器

- `yes`: 多次打印字符串

- `cal`: 漂亮的日历

- `env`: 执行一个命令(脚本文件中很有用)

- `printenv`: 打印环境变量(调试时或在使用脚本文件时很有用)

- `look`: 查找以特定字符串开头的单词

- `cut`、`paste`和`join`: 数据修改

- `fmt`: 格式化文本段落

- `pr`: 将文本格式化成页/列形式

- `fold`: 包裹文本中的几行

- `column`: 将文本格式化成多列或表格

- `expand`和`unexpand`: 制表符与空格之间转换

- `nl`: 添加行号

- `seq`: 打印数字

- `bc`: 计算器

- `factor`: 分解因数

- `gpg`: 加密并签名文件

- `toe`: terminfo entries列表

- `nc`: 网络调试及数据传输

- `socat`: 套接字代理，与`netcat`类似

- `slurm`: 网络可视化

- `dd`: 文件或设备间传输数据

- `file`: 确定文件类型

- `tree`: 以树的形式显示路径和文件，类似于递归的`ls`

- `stat`: 文件信息

- `tac`: 反向输出文件

- `shuf`: 文件中随机选取几行

- `comm`: 一行一行的比较排序过的文件

- `pv`: 监视通过管道的数据

- `hd` 和 `bvi`: 保存或编辑二进制文件

- `strings`: 从二进制文件中抽取文本

- `tr`: 转换字母

- `iconv`或`uconv`: 简易的文件编码

- `split `和`csplit`: 分割文件

- `units`: 将一种计量单位转换为另一种等效的计量单位(参阅`/usr/share/units/definitions.units`)

- `7z`: 高比例的文件压缩

- `ldd`: 动态库信息

- `nm`: 提取obj文件中的符号

- `ab`: 性能分析web服务器

- `strace`: 系统调用调试

- `mtr`: 更好的网络调试跟踪工具

- `cssh`: 可视化的并发shell

- `rsync`: 通过ssh同步文件和文件夹

- `wireshark`和`tshark`:抓包和网络调试工具

- `ngrep`: 网络层的grep

- `host` 和 `dig`: DNS查找

- `lsof`: 列出当前系统打开文件的工具以及查看端口信息

- `dstat`: 系统状态查看

- [`glances`](https://github.com/nicolargo/glances): 高层次的多子系统总览

- `iostat`: CPU和硬盘状态

- `htop`: top的加强版

- `last`: 登入记录

- `w`: 查看处于登录状态的用户

- `id`: 用户/组ID信息

- `sar`: 系统历史数据

- `iftop` 或 `nethogs`: 套接字及进程的网络利用

- `ss`: 套接字数据

- `dmesg`: 引导及系统错误信息

- `hdparm`: SATA/ATA磁盘更改及性能分析

- `lsb_release`: Linux发行版信息

- `lsblk`: 列出块设备信息: 以树形展示你的磁盘以及磁盘分区信息

- `lshw` 及 `lspci`: 查看硬件信息，包括RAID、显卡等

- `fortune`，`ddate`和`sl`: 额，这主要取决于你是否认为蒸汽火车和莫名其妙的名人名言是否"有用"


## 更多资源

- [awesome-shell](https://github.com/alebcay/awesome-shell): 一份精心组织的命令行工具及资源的列表。
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/)： 为了编写更好的脚本文件。


## 免责声明

除去特别微小的任务，记录下这些代码以便他人查看。责任往往伴随着能力，*可以*做并不意味着应该做。


## 授权条款

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/) 

本文使用授权协议 [Creative Commons Attribution-ShareAlike 4.0 International Licene](http://creativecommons.org/licenses/by-sa/4.0/)。

