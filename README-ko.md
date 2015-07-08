[ Languages: [English](README.md), [Español](README-es.md), [Português](README-pt.md), [中文](README-zh.md), [Русский](README-ru.md) ]


# The Art of Command Line
# 커멘드 라인 멋짐에 대해

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [메타](#메타)
- [기본](#기본)
- [자주 사용](#자주-사용)
- [파일과 데이터 처리](#파일과-데이터-처리)
- [시스템 디버깅](#시스템-디버깅)
- [한줄로](#한줄로)
- [유명하진 않지만 사용하면 편한](#유명하지-않지만-사용하면-편한)
- [맥용](#맥용)
- [더 많은 자료](#더-많은-자료)
- [면책 조항](#면책-조항)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

Fluency on the command line is a skill often neglected or considered arcane, but it improves your flexibility and productivity as an engineer in both obvious and subtle ways. This is a selection of notes and tips on using the command-line that I've found useful when working on Linux. Some tips are elementary, and some are fairly specific, sophisticated, or obscure. This page is not long, but if you can use and recall all the items here, you know a lot.

Much of this
[originally](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[appeared](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
on [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
but given the interest there, it seems it's worth using Github, where people more talented than I can readily suggest improvements. If you see an error or something that could be better, please submit an issue or PR! (Of course please review the meta section and existing PRs/issues first.)


## 메타

Scope:

- This guide is both for beginners and the experienced. The goals are *breadth* (everything important), *specificity* (give concrete examples of the most common case), and *brevity* (avoid things that aren't essential or digressions you can easily look up elsewhere). Every tip is essential in some situation or significantly saves time over alternatives.
- This is written for Linux, with the exception of the "[MacOS only](#macos-only)" section. Many of the other items apply or can be installed on other Unices or MacOS (or even Cygwin).
- The focus is on interactive Bash, though many tips apply to other shells and to general Bash scripting.
- It includes both "standard" Unix commands as well as ones that require special package installs -- so long as they are important enough to merit inclusion.

Notes:

- To keep this to one page, content is implicitly included by reference. You're smart enough to look up more detail elsewhere once you know the idea or command to Google. Use `apt-get`/`yum`/`dnf`/`pacman`/`pip`/`brew` (as appropriate) to install new programs.
- Use [Explainshell](http://explainshell.com/) to get a helpful breakdown of what commands, options, pipes etc. do.


## 기본

- Learn basic Bash. Actually, type `man bash` and at least skim the whole thing; it's pretty easy to follow and not that long. Alternate shells can be nice, but Bash is powerful and always available (learning *only* zsh, fish, etc., while tempting on your own laptop, restricts you in many situations, such as using existing servers).

- Learn at least one text-based editor well. Ideally Vim (`vi`), as there's really no competition for random editing in a terminal (even if you use Emacs, a big IDE, or a modern hipster editor most of the time).

- Know how to read documentation with `man` (for the inquisitive, `man man` lists the section numbers, e.g. 1 is "regular" commands, 5 is files/conventions, and 8 are for administration). Find man pages with `apropos`. Know that some commands are not executables, but Bash builtins, and that you can get help on them with `help` and `help -d`.

- Learn about redirection of output and input using `>` and `<` and pipes using `|`. Know `>` overwrites the output file and `>>` appends. Learn about stdout and stderr.

- Learn about file glob expansion with `*` (and perhaps `?` and `{`...`}`) and quoting and the difference between double `"` and single `'` quotes. (See more on variable expansion below.)

- Be familiar with Bash job management: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, etc.

- Know `ssh`, and the basics of passwordless authentication, via `ssh-agent`, `ssh-add`, etc.

- Basic file management: `ls` and `ls -l` (in particular, learn what every column in `ls -l` means), `less`, `head`, `tail` and `tail -f` (or even better, `less +F`), `ln` and `ln -s` (learn the differences and advantages of hard versus soft links), `chown`, `chmod`, `du` (for a quick summary of disk usage: `du -hk *`). For filesystem management, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`.

- Basic network management: `ip` or `ifconfig`, `dig`.

- Know regular expressions well, and the various flags to `grep`/`egrep`. The `-i`, `-o`, `-A`, and `-B` options are worth knowing.

- Learn to use `apt-get`, `yum`, `dnf` or `pacman` (depending on distro) to find and install packages. And make sure you have `pip` to install Python-based command-line tools (a few below are easiest to install via `pip`).


## 자주 사용

- In Bash, use **Tab** to complete arguments and **ctrl-r** to search through command history.

- In Bash, use **ctrl-w** to delete the last word, and **ctrl-u** to delete all the way back to the start of the line. Use **alt-b** and **alt-f** to move by word, **ctrl-k** to kill to the end of the line, **ctrl-l** to clear the screen. See `man readline` for all the default keybindings in Bash. There are a lot. For example **alt-.** cycles through previous arguments, and **alt-*** expands a glob.

- Alternatively, if you love vi-style key-bindings, use `set -o vi`.

- To see recent commands, `history`. There are also many abbreviations such as `!$` (last argument) and `!!` last command, though these are often easily replaced with **ctrl-r** and **alt-.**.

- To go back to the previous working directory: `cd -`

- If you are halfway through typing a command but change your mind, hit **alt-#** to add a `#` at the beginning and enter it as a comment (or use **ctrl-a**, **#**, **enter**). You can then return to it later via command history.

- Use `xargs` (or `parallel`). It's very powerful. Note you can control how many items execute per line (`-L`) as well as parallelism (`-P`). If you're not sure if it'll do the right thing, use `xargs echo` first. Also, `-I{}` is handy. Examples:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` is a helpful display of the process tree.

- Use `pgrep` and `pkill` to find or signal processes by name (`-f` is helpful).

- Know the various signals you can send processes. For example, to suspend a process, use `kill -STOP [pid]`. For the full list, see `man 7 signal`

- Use `nohup` or `disown` if you want a background process to keep running forever.

- Check what processes are listening via `netstat -lntp` or `ss -plat` (for TCP; add `-u` for UDP).

- See also `lsof` for open sockets and files.

- Use `alias` to create shortcuts for commonly used commands. For example, `alias ll='ls -latr'` creates a new alias `ll`.

- In Bash scripts, use `set -x` for debugging output. Use strict modes whenever possible. Use `set -e` to abort on errors. Use `set -o pipefail` as well, to be strict about errors (though this topic is a bit subtle). For more involved scripts, also use `trap`.

- In Bash scripts, subshells (written with parentheses) are convenient ways to group commands. A common example is to temporarily move to a different working directory, e.g.
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- In Bash, note there are lots of kinds of variable expansion. Checking a variable exists: `${name:?error message}`. For example, if a Bash script requires a single argument, just write `input_file=${1:?usage: $0 input_file}`. Arithmetic expansion: `i=$(( (i + 1) % 5 ))`. Sequences: `{1..10}`. Trimming of strings: `${var%suffix}` and `${var#prefix}`. For example if `var=foo.pdf`, then `echo ${var%.pdf}.txt` prints `foo.txt`.

- The output of a command can be treated like a file via `<(some command)`. For example, compare local `/etc/hosts` with a remote one:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Know about "here documents" in Bash, as in `cat <<EOF ...`.

- In Bash, redirect both standard output and standard error via: `some-command >logfile 2>&1`. Often, to ensure a command does not leave an open file handle to standard input, tying it to the terminal you are in, it is also good practice to add `</dev/null`.

- Use `man ascii` for a good ASCII table, with hex and decimal values. For general encoding info, `man unicode`, `man utf-8`, and `man latin1` are helpful.

- Use `screen` or [`tmux`](https://tmux.github.io/) to multiplex the screen, especially useful on remote ssh sessions and to detach and re-attach to a session. A more minimal alternative for session persistence only is `dtach`.

- In ssh, knowing how to port tunnel with `-L` or `-D` (and occasionally `-R`) is useful, e.g. to access web sites from a remote server.

- It can be useful to make a few optimizations to your ssh configuration; for example, this `~/.ssh/config` contains settings to avoid dropped connections in certain network environments, use compression (which is helpful with scp over low-bandwidth connections), and multiplex channels to the same server with a local control file:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- A few other options relevant to ssh are security sensitive and should be enabled with care, e.g. per subnet or host or in trusted networks: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- To get the permissions on a file in octal form, which is useful for system configuration but not available in `ls` and easy to bungle, use something like
```sh
      stat -c '%A %a %n' /etc/timezone
```

- For interactive selection of values from the output of another command, use [`percol`](https://github.com/mooz/percol) or [`fzf`](https://github.com/junegunn/fzf).

- For interaction with files based on the output of another command (like `git`), use `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- For a simple web server for all files in the current directory (and subdirs), available to anyone on your network, use:
`python -m SimpleHTTPServer 7777` (for port 7777 and Python 2) and `python -m http.server 7777` (for port 7777 and Python 3).

- For running a command with privileges, use `sudo` (for root) or `sudo -u` (for another user). Use `su` or `sudo bash` to actually run a shell as that user. Use `su -` to simulate a fresh login as root or another user.


## 파일과 데이터 처리

- To locate a file by name in the current directory, `find . -iname '*something*'` (or similar). To find a file anywhere by name, use `locate something` (but bear in mind `updatedb` may not have indexed recently created files).

- For general searching through source or data files (more advanced than `grep -r`), use [`ag`](https://github.com/ggreer/the_silver_searcher).

- To convert HTML to text: `lynx -dump -stdin`

- For Markdown, HTML, and all kinds of document conversion, try [`pandoc`](http://pandoc.org/).

- If you must handle XML, `xmlstarlet` is old but good.

- For JSON, use `jq`.

- For Excel or CSV files, [csvkit](https://github.com/onyxfish/csvkit) provides `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, etc.

- For Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) is convenient and [`s4cmd`](https://github.com/bloomreach/s4cmd) is faster. Amazon's [`aws`](https://github.com/aws/aws-cli) is essential for other AWS-related tasks.

- Know about `sort` and `uniq`, including uniq's `-u` and `-d` options -- see one-liners below. See also `comm`.

- Know about `cut`, `paste`, and `join` to manipulate text files. Many people use `cut` but forget about `join`.

- Know about `wc` to count newlines (`-l`), characters (`-m`), words (`-w`) and bytes (`-c`).

- Know about `tee` to copy from stdin to a file and also to stdout, as in `ls -al | tee file.txt`.

- Know that locale affects a lot of command line tools in subtle ways, including sorting order (collation) and performance. Most Linux installations will set `LANG` or other locale variables to a local setting like US English. But be aware sorting will change if you change locale. And know i18n routines can make sort or other commands run *many times* slower. In some situations (such as the set operations or uniqueness operations below) you can safely ignore slow i18n routines entirely and use traditional byte-based sort order, using `export LC_ALL=C`.

- Know basic `awk` and `sed` for simple data munging. For example, summing all numbers in the third column of a text file: `awk '{ x += $3 } END { print x }'`. This is probably 3X faster and 3X shorter than equivalent Python.

- To replace all occurrences of a string in place, in one or more files:
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- To rename many files at once according to a pattern, use `rename`. For complex renames, [`repren`](https://github.com/jlevy/repren) may help.
```sh
      # Recover backup files foo.bak -> foo:
      rename 's/\.bak$//' *.bak
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
```

- Use `shuf` to shuffle or select random lines from a file.

- Know `sort`'s options. For numbers, use `-n`, or `-h` for handling human-readable numbers (e.g. from `du -h`). Know how keys work (`-t` and `-k`). In particular, watch out that you need to write `-k1,1` to sort by only the first field; `-k1` means sort according to the whole line. Stable sort (`sort -s`) can be useful. For example, to sort first by field 2, then secondarily by field 1, you can use `sort -k1,1 | sort -s -k2,2`.

- If you ever need to write a tab literal in a command line in Bash (e.g. for the -t argument to sort), press **ctrl-v** **[Tab]** or write `$'\t'` (the latter is better as you can copy/paste it).

- The standard tools for patching source code are `diff` and `patch`. See also `diffstat` for summary statistics of a diff. Note `diff -r` works for entire directories. Use `diff -r tree1 tree2 | diffstat` for a summary of changes.

- For binary files, use `hd` for simple hex dumps and `bvi` for binary editing.

- Also for binary files, `strings` (plus `grep`, etc.) lets you find bits of text.

- For binary diffs (delta compression), use `xdelta3`.

- To convert text encodings, try `iconv`. Or `uconv` for more advanced use; it supports some advanced Unicode things. For example, this command lowercases and removes all accents (by expanding and dropping them):
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- To split files into pieces, see `split` (to split by size) and `csplit` (to split by a pattern).

- Use `zless`, `zmore`, `zcat`, and `zgrep` to operate on compressed files.


## 시스템 디버깅

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

- Check what OS you're on with `uname` or `uname -a` (general Unix/kernel info) or `lsb_release -a` (Linux distro info).

- Use `dmesg` whenever something's acting really funny (it could be hardware or driver issues).


## 한줄로

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


## 유명하진 않지만 사용하면 편한

- `expr`: 산술 또는 boolean 연산을 수행하거나 정규 표현식을 평가하는데 사용합니다.

- `m4`: 간단한 매크로 프로세서

- `yes`: 많은 양의 문자열 출력합니다.

- `cal`: 꽤 괜찮은 달력

- `env`: 명령어 실행합니다. (스크립트 작성시 유용함)

- `printenv`: 환경 변수 출력합니다. (디버깅하거나 스크립트 작성시 유용함)

- `look`: 문자열로 시작하는 영어 단어나 파일에 있는 라인을 찾습니다.

- `cut`, `paste`, `join`: 데이터를 조작합니다.

- `fmt`: 텍스트 구문 서식

- `pr`: 페이지 / 컬럼 텍스트 서식

- `fold`: 텍스트 줄 바꿈

- `column`: 열이나 테이블로 텍스트 서식 변경합니다.

- `expand`, `unexpand`: 탭에서 스페이스로, 스페이스에서 탭으로 변경

- `nl`: 줄번호를 추가합니다.

- `seq`: 숫자 출력를 출력합니다.

- `bc`: 계산기

- `factor`: 정수 인자

- `gpg`: 암호화한 서명 파일을 생성합니다.

- `toe`: terminfo 항목 표룰 나타냅니다.

- `nc`: 네트워크 디버깅과 데이터 변환합니다.

- `socat`: 소켓 릴레이 및 TCP 포트 전달자 (`netcat`과 유사)

- `slurm`: 네트워크 트래픽 시각화합니다.

- `dd`: 파일이나 장치간 데이터 이동합니다.

- `file`: 파일 유형 확인합니다.

- `tree`: 디렉토리와 하위 디렉토리를 중첩 트리로 표현. `ls`와 비슷하나 반복하여 보여줍니다.

- `stat`: 파일 정보를 표시합니다.

- `tac`: 역으로 파일을 출력합니다.

- `shuf`: 파일에서 줄을 무작위로 선택합니다.

- `comm`: 줄별로 정렬된 파일 줄을 비교합니다.

- `pv`: 파이프를 통해 처리되는 데이터를 감시합니다.

- `hd`, `bvi`: 바이너리 파일을 덤프하거나 수정합니다.

- `strings`: 바이너리 파일에서 텍스트를 추출합니다.

- `tr`: 문자를 변경하거나 조작합니다.

- `iconv`, `uconv`: 텍스트의 인코딩을 변경합니다.

- `split`, `csplit`: 파일을 분할합니다.

- `sponge`: 수정되는 내용을 읽어 입력합니다. 동일한 파일에 데이터를 변경하여 작성하기 유용합니다. 예로, `  grep -v something some-file | sponge some-file` 

- `units`: 단위를 계산하거나 변환합니다. 2주당 펄롱을 1깜박임당 트윕으로 변환합니다. (관련해서는 `/usr/share/units/definitions.units`를 확인하세요.)

- `7z`: 높은 비율을 자랑하는 파일 압축기

- `ldd`: 동적 라이브러리 정보를 나타냅니다.

- `nm`: 오브젝트 파일의 심볼을 나타냅니다.

- `ab`: 웹서버 벤치마킹에 사용합니다.

- `strace`: 시스템 콜을 디버깅합니다.

- `mtr`: 네트워크 디버깅을위한 더 나은 경로를 추적합니다.

- `cssh`: 동시에 여러 쉘 작업을 할 수 있습니다.

- `rsync`: SSH를 이용하여 파일이나 폴더를 동기화합니다.

- `wireshark`, `tshark`: 패킷 캡처하고 네트워크를 디버깅합니다.

- `ngrep`: 네트워크 레이어를 grep 합니다.

- `host`, `dig`: DNS를 조회합니다.

- `lsof`: 프로세스 파일 서술자(descriptor)와 소켓 정보를 나타냅니다.

- `dstat`: 시스템 통계를 내는대 유용합니다.

- [`glances`](https://github.com/nicolargo/glances): 높은 수준의 다중 서브시스템 모니터링 툴

- `iostat`: CPU, 디스크 사용량 상태를 나타냅니다.

- `htop`: top의 개선 버전

- `last`: 로그인 이력을 확인합니다.

- `w`: 지금 누가 로그인 되어있는지를 확인합니다.

- `id`: 사용자 / 그룹 계정 정보를 확인합니다.

- `sar`: 시스템 상태에 대한 이력을 확인하는 도구입니다.

- `iftop`, `nethogs`: 소켓이나 프로세스용 네트워크 유틸입니다.

- `ss`: 소켓 통계를 보여줍니다.

- `dmesg`: 부팅과 시스템 에러 메시지를 확인할 수 있습니다.

- `hdparm`: SATA/ATA 디스크 조작하거나 성능을 확인할 수 있습니다.

- `lsb_release`: 리눅스 배포판 정보를 확인할 수 있습니다.

- `lsblk`: 블록 장치 목록(List block devices): 디스크와 디스크 파티션에 대한 목록을 트리형식으로 보여줍니다.

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: CPU, BIOS, RAID, 그래픽, 장치 등이 포함되어있는 하드웨어 정보를 확인할 수 있습니다.

- `fortune`, `ddate`, `sl`: 음... 어떤 방식으로 사용하느냐에 따라 "유용하게" 사용할 수 있습니다.


## 맥용

*MacOS에서만* 해당되는 항목입니다.

- `brew` (Homebrew)나 `port` (MacPorts)를 패키지 메니저로 사용합니다. 보다 많은 명령어를 MacOS에 설치하여 사용할 수 있습니다.

- `pbcopy`를 이용하여 데스크탑 어플리케이션에 명령어 출력물을 복사하거나 `pbpaste`를 이용해 붙여넣기를 할 수 있습니다.

- 데스크탑 어플리케이션에서 파일을 열기위해, `open` 또는 `open -a /Applications/Whatever.app`을 사용하면 됩니다.

- Spotlight: `mdfind`를 이용해 파일을 찾고, `mdls`를 이용해 메타데이타 (사진 EXIF 정보와 같은) 목록을 볼 수 있습니다.

- MacOS는 BSD Unix 기반이며 많은 명령어들을 (예로 `ps`, `ls`, `tail`, `awk`, `sed`) 사용할 수 있으며, 이것들은 Linux 버전들과 미묘한 차이가 있습니다. 그리고 크게는 System V-style Unix와 GNU 도구들에 많은 영향을 받았습니다. 이런 내용들을 man 페이지 상단의 "BSD General Commands Manual." 라는 문구를 통해 알 수 있습니다. 가끔은 GNU 버전이 설치되기도합니다. (예로, GNU awk와 sed인 `gawk`와 `gsed`에서). 만약 이종 플랫폼간 Bash 스크립트를 작성하려면, 동일한 명령어 (예로, 파이썬이나 `perl`과 같은)나 테스트시 주의해야합니다.

## 더 많은 자료

- [awesome-shell](https://github.com/alebcay/awesome-shell): 쉘 도구와 리소스를 모아둔 목록
- 더 좋은 쉘 스크립트 작성을 위한 [Strict 모드](http://redsymbol.net/articles/unofficial-bash-strict-mode/)


## 면책 조항

매우 작은 작업을 제외한 코드들은 다른 사람이 읽을 수 있도록 작성됩니다. 그러니 이 내용은 작성자 전원에게 책임이 있습니다. Bash에서 뭔가를 *할 수 있다는* 것이 당신이 뭔가를 해야된다는 것을 강요하는 것이 아니다! ;)

## 라이센스

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

[Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/) 라이센스 하에 작성되었습니다.
