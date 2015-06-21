# 命令行的艺术

- [Meta](#meta)
- [Basics](#basics)
- [Everyday use](#everyday-use)
- [Processing files and data](#processing-files-and-data)
- [System debugging](#system-debugging)
- [One-liners](#one-liners)
- [Obscure but useful](#obscure-but-useful)
- [More resources](#more-resources)
- [Disclaimer](#disclaimer)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

熟练使用命令行是一种常常被忽视或被认为晦涩难懂，但实际上，它可以提高你作为工程师的灵活性以及生产力。本文是一份我在Linux上工作时发现的一些关于命令行的使用的小技巧的摘要。这些小技巧有基础的、相当复杂的甚至晦涩难懂的。这篇文章并不长，但当你能够熟练掌握这里列出的所有技巧时，你就学会了很多关于命令行的东西了。

这里的大部分内容
[首次](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[出现](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
于 [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
但考虑到这里的人们都具有学习的天赋且乐于接受别人的建议，使用Github来做这件事是更佳的选择。如果你在本文中发现了错误或者存在可以改善的地方，请果断提交Issue或Pull Request！（当然在提交前请看一下meta节和已有的issue/PR）。


## Meta

Scope:

- 这篇文章对刚接触命令行的新手以及具有命令行使用经验的人都有用处。The goals are *breadth* (everything important), *specificity* (give concrete examples of the most common case), and *brevity* (avoid things that aren't essential or digressions you can easily look up elsewhere). 每个小技巧在某个特定情境下都是基本的或能够显著地节约时间。
- 本文为Linux所写，但很多内容（并非所有的）同样适用于MacOS甚至Cygwin。
- 本文关注于交互式Bash，尽管很多技巧适用于其他shell或Bash脚本。
- 本文包括了"标准的"Unix命令和需要安装特定包的命令，只要它们足够重要。

Notes:

- To keep this to one page, content is implicitly included by reference. You're smart enough to look up more detail elsewhere once you know the idea or command to Google. 使用 `apt-get`/`yum`/`dnf`/`pip`/`brew` 来安装新程序。
- 使用 [Explainshell](http://explainshell.com/) 去获取相关命令、参数、管道等内容的解释。


## Basics

- 学习Bash的基础知识。具体来说, 输入 `man bash` 并至少全文浏览一遍; 它很简单并且不长。其他的shell可能很好用，但Bash功能强大且几乎所有情况下都是可用的 ( *只*学习 zsh, fish或其他的shell的话, 在你自己的电脑上会显得很方便, 但在很多情况下会限制你, 比如当你需要在服务器上工作时)。

- 学习并掌握至少一个基于文本的编辑器。通常 Vim (`vi`) 会是你最好的选择。

- 学会如何使用`man`命令去阅读文档。学会使用`apropos`去查找文档。了解有些命令并不对应可执行文件，而是Bash内置的，可以使用`help`和`help -d`命令获取帮助信息。

- 学会使用`>`和`<`来重定向输出和输入，学会使用`|`来重定向管道。了解标准输出stdout和标准错误stderr。

- 学会使用通配符`*` ( 若能`?`和`{`...`}`更好) 和引用以及引用中`'`和`"`的区别。

- 熟悉Bash任务管理工具: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill` 等。

- 了解`ssh`, 以及基本的无密码认证, `ssh-agent`, `ssh-add`等。

- 学会基本的文件管理: `ls` 和 `ls -l` (了解`ls -l`中每一列代表的意义), `less`, `head`, `tail`和`tail -f` (甚至 `less +F`), `ln` and `ln -s` (了解软连接和硬连接的区别), `chown`, `chmod`, `du` (硬盘使用情况概述: `du -sk *`)。 关于文件系统的管理,学习 `df`, `mount`, `fdisk`, `mkfs`。

- 学习基本的网络管理: `ip` 或 `ifconfig`, `dig`。

- 熟悉正则表达式，以及`grep`/`egrep`里不同参数的作用，例如`-i`, `-o`, `-A`,和 `-B`。

- 学会使用`apt-get`, `yum`, 或`dnf` (取决于你使用的Linux发行版)来查找或安装包。确保你的环境中有 `pip` 来安装基于Python的命令韩工具 (部分程序使用`pip`来安装会很简单)。


## Everyday use

- 在Bash中，可以使用**Tab**自动补全参数，使用**ctrl-r**搜索命令行历史。

- 在Bash中，使用**ctrl-w**删除你键入的最后一个单词，使用**ctrl-u**删除整行，使用**alt-b**和**alt-f**按单词移动， 使用**ctrl-k**从光标处删除到行尾，使用**ctrl-l**清屏。键入`man readline`查看Bash中的默认快捷键，内容很多。例如**alt-.** 循环地移向前一个参数, 以及**alt-***展开通配符。

- 你喜欢的话，可以键入`set -o vi`来使用vi风格的快捷键。

- 键入`history`查看命令行历史记录。其中有许多缩写， 例如`!$` (最后键入的参数)和`!!`（最后键入的命令），尽管通常被 **ctrl-r*和**alt-.**取代。

- 回到上一个工作路径: `cd -`

- 如果你输入命令的时候改变了注意，按下**alt-#**在行首添加`#`（将你输入的命令视为注释），并回车。这样做的话，之后你可以很方便的利用命令行历史回到你刚才输入到一半的命令。

- 使用`xargs` ( 或`parallel`)。他们非常给力。注意到你可以控制每行参数个数(`-L`)和最大并行数 (`-P`)。如果你不确定它们是否会按你想的那样工作，先使用`xargs echo`查看一下。此外, 使用`-I{}`会很方便。例如:
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

- 在Bash脚本中，使用`set -x`去调试输出，尽可能的使用严格模式，使用`set -e`令脚本在发生错误时退出而不是继续运行，使用`set -o pipefail`严谨地对待错误（尽管问题可能很微妙）。当牵扯到很多脚本时, 使用`trap`。

- 在Bash脚本中，子shell（使用括号`(...)`）是一种便捷的方式去组织参数。一个常见的例子是临时地移动工作路径，代码如下：
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- 在Bash中, 注意到其中有许多形式的扩展。检查变量是否存在: `${name:?error message}`。例如, 当Bash脚本需要一个参数时, 可以使用这样的代码`input_file=${1:?usage: $0 input_file}`。数学表达式: `i=$(( (i + 1) % 5 ))`。序列: `{1..10}`。 截断字符串: `${var%suffix}`和`${var#prefix}`。例如，假设`var=foo.pdf`, 那么`echo ${var%.pdf}.txt`将输出`foo.txt`。

- 通过使用`<(some command)`可以将输出视为文件。例如, 对比本地文件`/etc/hosts`和一个远程文件:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- 了解Bash中的"here documents", 例如`cat <<EOF ...`。

- 在Bash中，同时重定向标准输出和标准错误，`some-command >logfile 2>&1`。通常，为了保证命令不会在标准输入里残留一个打开了的文件句柄导致你当前所在的终端无法操作，添加`</dev/null`是一个好习惯。

- 使用`man ascii`查看具有十六进制和十进制值的ASCII表。`man unicode`, `man utf-8`,以及 `man latin1` 有助于你去了解通用的编码信息。

- 使用`screen`或`tmux`来使用多个屏幕, 当你在使用ssh时（保存session信息）将尤为有用。另一个轻量级的解决方案是`dtach`。

- ssh中, 了解如何使用`-L`或`-D`(偶尔需要用`-R`)去开启隧道是非常有用的，例如当你需要从一台远程服务器上访问web。

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

- 部分其他的关于ssh的选项是安全敏感且应当小心启用的。例如在可信任的网络中: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- 获取文件的八进制格式权限，使用类似如下的代码：
```sh
      stat -c '%A %a %n' /etc/timezone
```

- 使用[`percol`](https://github.com/mooz/percol)可以交互式地从另一个命令输出中选取值。

- 使用`fpp`([PathPicker](https://github.com/facebook/PathPicker))可以与基于另一个命令（例如`git`）输出的文件交互。

- 将web服务器上当前目录下所有的文件（以及子目录）暴露给你所处网络的所有用户，使用：
`python -m SimpleHTTPServer 7777` (使用端口7777和Python 2)或`python -m http.server 7777` (使用端口7777和Python 3)。


## Processing files and data

- 在当前路径下通过文件名定位一个文件，`find . -iname '*something*'`(或类似的)。在所有路径下通过文件名查找文件，使用 `locate something` (但请记住`updatedb`可能没有对最近新建的文件建立索引)。

- 使用[`ag`](https://github.com/ggreer/the_silver_searcher)在源或文件里检索（比`grep -r`更好）。

- 将HTML转为文本: `lynx -dump -stdin`

- Markdown, HTML, 以及所有文档格式之间的转换, 试试 [`pandoc`](http://pandoc.org/)。

- 如果你不得不处理XML， `xmlstarlet`宝刀未老。

- 使用`jq`处理json。

- Excel或CSV文件的处理, [csvkit](https://github.com/onyxfish/csvkit)提供了`in2csv`, `csvcut`, `csvjoin`, `csvgrep`等工具。

- 关于Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd)很方便而[`s4cmd`](https://github.com/bloomreach/s4cmd)更快。Amazon官方的[`aws`](https://github.com/aws/aws-cli)是其他AWS相关工作的基础。

- 了解如何使用`sort`和`uniq`，包括uniq的`-u`参数和`-d`参数，详见后文one-liners。

- 了解如何使用`cut`，`paste`和`join`来更改文件。大部分人都会使用`cut`但忘了`join`。

- 了解如何运用`wc`去计算新行数(`-l`), 字符数(`-m`),单词数(`-w`)以及字节数(`-c`)。

- 了解如何使用`tee`将标准输入复制到文件甚至标准输出，例如`ls -al | tee file.txt`。

- 了解语言环境对许多命令行工具的微妙影响，包括排序的顺序和性能。大多数Linux的安装过程会将`LANG`或其他有关的变量设置为符合本地的设置。意识到当你改变语言环境时，排序的结果可能会改变。明白国际化可能会时sort或其他命令运行效率下降*许多倍*。某些情况下（例如集合运算）你可以放心的使用`export LC_ALL=C`来忽略掉国际化并使用基于字节的顺序。

- 了解`awk`和`sed`关于数据的简单处理的用法。例如, 将文本文件中第三列的所有数字求和: `awk '{ x += $3 } END { print x }'`. 这可能比同等作用的Python代码块三倍且代码量少三倍。

- 替换一个或多个文件中出现的字符串:
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- 依据某种模式批量重命名多个文件，使用`rename`。对于复杂的重命名规则，[`repren`](https://github.com/jlevy/repren)或许有帮助。
```sh
      # Recover backup files foo.bak -> foo:
      rename 's/\.bak$//' *.bak
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
```

- 使用`shuf`从一个文件中随机选取行。

- 了解`sort`的参数。明白键的工作原理(`-t`和`-k`)。例如，注意到你需要`-k1,1`来仅按第一个域来排序，而`-k1`意味着按整行排序。

- 稳定排序(`sort -s`)在某些情况下很有用。例如,以第二个域为主关键字，第一个域为次关键字进行排序，你可以使用`sort -k1,1 | sort -s -k2,2`

- 如果你想在Bash命令行中写tab制表符，按下**ctrl-v** **[Tab]** 或键入`$'\t'`(后者可能更好，因为你可以复制粘贴它)。

- 对于二进制文件，使用`hd`使其以十六进制显示以及使用`bvi`来编辑二进制。

- 同样对于二进制文件，使用`strings`(包括`grep`等等)允许你查找一些文本。

- To convert text encodings, try `iconv`. Or `uconv` for more advanced use; it supports some advanced Unicode things. For example, this command lowercases and removes all accents (by expanding and dropping them):
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- 拆分文件，查看`split`(按大小拆分)和`csplit`(按模式拆分)。

- 使用`zless`, `zmore`, `zcat`和`zgrep`对压缩过的文件进行操作。


## System debugging

- For web debugging, `curl` and `curl -I` are handy, or their `wget` equivalents, or the more modern [`httpie`](https://github.com/jakubroztocil/httpie).

- To know disk/cpu/network status, use `iostat`, `netstat`, `top` (or the better `htop`), and (especially) `dstat`. Good for getting a quick idea of what's happening on a system.

- For a more in-depth system overview, use [`glances`](https://github.com/nicolargo/glances). It presents you with several system level statistics in one terminal window. Very helpful for quickly checking on various subsystems.

- To know memory status, run and understand the output of `free` and `vmstat`. In particular, be aware the "cached" value is memory held by the Linux kernel as file cache, so effectively counts toward the "free" value.

- Java system debugging is a different kettle of fish, but a simple trick on Oracle's and some other JVMs is that you can run `kill -3 <pid>` and a full stack trace and heap summary (including generational garbage collection details, which can be highly informative) will be dumped to stderr/logs.

- Use `mtr` as a better traceroute, to identify network issues.

- For looking at why a disk is full, `ncdu` saves time over the usual commands like `du -sh *`.

- To find which socket or process is using bandwidth, try `iftop` or `nethogs`.

- The `ab` tool (comes with Apache) is helpful for quick-and-dirty checking of web server performance. For more complex load testing, try `siege`.

- For more serious network debugging, `wireshark`, `tshark`, or `ngrep`.

- Know about `strace` and `ltrace`. These can be helpful if a program is failing, hanging, or crashing, and you don't know why, or if you want to get a general idea of performance. Note the profiling option (`-c`), and the ability to attach to a running process (`-p`).

- Know about `ldd` to check shared libraries etc.

- Know how to connect to a running process with `gdb` and get its stack traces.

- Use `/proc`. It's amazingly helpful sometimes when debugging live problems. Examples: `/proc/cpuinfo`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps`.

- When debugging why something went wrong in the past, `sar` can be very helpful. It shows historic statistics on CPU, memory, network, etc.

- For deeper systems and performance analyses, look at `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](http://en.wikipedia.org/wiki/Perf_(Linux)), and [`sysdig`](https://github.com/draios/sysdig).

- Confirm what Linux distribution you're using (works on most distros): `lsb_release -a`

- Use `dmesg` whenever something's acting really funny (it could be hardware or driver issues).


## One-liners

A few examples of piecing together commands:

- It is remarkably helpful sometimes that you can do set intersection, union, and difference of text files via `sort`/`uniq`. Suppose `a` and `b` are text files that are already uniqued. This is fast, and works on files of arbitrary size, up to many gigabytes. (Sort is not limited by memory, though you may need to use the `-T` option if `/tmp` is on a small root partition.) See also the note about `LC_ALL` above and `sort`'s `-u` option (left out for clarity below).
```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- Use `grep . *` to visually examine all contents of all files in a directory, e.g. for directories filled with config settings, like `/sys`, `/proc`, `/etc`.


- Summing all numbers in the third column of a text file (this is probably 3X faster and 3X less code than equivalent Python):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- If want to see sizes/dates on a tree of files, this is like a recursive `ls -l` but is easier to read than `ls -lR`:
```sh
      find . -type f -ls
```

- Use `xargs` or `parallel` whenever you can. Note you can control how many items execute per line (`-L`) as well as parallelism (`-P`). If you're not sure if it'll do the right thing, use xargs echo first. Also, `-I{}` is handy. Examples:
```sh
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- Say you have a text file, like a web server log, and a certain value that appears on some lines, such as an `acct_id` parameter that is present in the URL. If you want a tally of how many requests for each `acct_id`:
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- Run this function to get a random tip from this document (parses Markdown and extracts an item):
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```


## Obscure but useful

- `expr`: perform arithmetic or boolean operations or evaluate regular expressions

- `m4`: simple macro processor

- `yes`: print a string a lot

- `cal`: nice calendar

- `env`: run a command (useful in scripts)

- `look`: find English words (or lines in a file) beginning with a string

- `cut `and `paste` and `join`: data manipulation

- `fmt`: format text paragraphs

- `pr`: format text into pages/columns

- `fold`: wrap lines of text

- `column`: format text into columns or tables

- `expand` and `unexpand`: convert between tabs and spaces

- `nl`: add line numbers

- `seq`: print numbers

- `bc`: calculator

- `factor`: factor integers

- `gpg`: encrypt and sign files

- `toe`: table of terminfo entries

- `nc`: network debugging and data transfer

- `socat`: socket relay and tcp port forwarder (similar to `netcat`)

- `slurm`: network trafic visualization

- `dd`: moving data between files or devices

- `file`: identify type of a file

- `tree`: display directories and subdirectories as a nesting tree; like `ls` but recursive

- `stat`: file info

- `tac`: print files in reverse

- `shuf`: random selection of lines from a file

- `comm`: compare sorted files line by line

- `hd` and `bvi`: dump or edit binary files

- `strings`: extract text from binary files

- `tr`: character translation or manipulation

- `iconv` or `uconv`: conversion for text encodings

- `split `and `csplit`: splitting files

- `7z`: high-ratio file compression

- `ldd`: dynamic library info

- `nm`: symbols from object files

- `ab`: benchmarking web servers

- `strace`: system call debugging

- `mtr`: better traceroute for network debugging

- `cssh`: visual concurrent shell

- `rsync`: sync files and folders over SSH

- `wireshark` and `tshark`: packet capture and network debugging

- `ngrep`: grep for the network layer

- `host` and `dig`: DNS lookups

- `lsof`: process file descriptor and socket info

- `dstat`: useful system stats

- [`glances`](https://github.com/nicolargo/glances): high level, multi-subsystem overview

- `iostat`: CPU and disk usage stats

- `htop`: improved version of top

- `last`: login history

- `w`: who's logged on

- `id`: user/group identity info

- `sar`: historic system stats

- `iftop` or `nethogs`: network utilization by socket or process

- `ss`: socket statistics

- `dmesg`: boot and system error messages

- `hdparm`: SATA/ATA disk manipulation/performance

- `lsb_release`: Linux distribution info

- `lshw`: hardware information

- `fortune`, `ddate`, and `sl`: um, well, it depends on whether you consider steam locomotives and Zippy quotations "useful"


## More resources

- [awesome-shell](https://github.com/alebcay/awesome-shell): A curated list of shell tools and resources.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) for writing better shell scripts.


## Disclaimer

With the exception of very small tasks, code is written so others can read it. With power comes responsibility. The fact you *can* do something in Bash doesn't necessarily mean you should! ;)
