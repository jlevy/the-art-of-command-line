# The Linux Command Line

This is a selection of command-line tips that I've found useful over the years when working on Linux. It's organized as a bit of a journey, from command-line novice to expert. Some tips are elementary, and some sophisticated enough few people know them. The goal is broad coverage of important tips that a technical user will find useful or time-saving. It's a bit long, and users certainly don't need to know all of them, but I've done my best to review that each item is worth reading in terms of projected time savings, if you use Linux heavily.

I originally wrote this list as an answer [on Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know/answer/Joshua-Levy), but given the interest there it seems perhaps it's worth moving it to Github, where people more talented than I can more easily suggest improvements. If you see an error or something that could be better, please submit a PR! :)

The items are intentionally brief. For more information on a command, try man, aptitude/yum, or Google.

## Basics

- Learn basic Bash. Actually, read the whole bash man page; it's pretty easy to follow and not that long. Alternate shells can be nice, but bash is powerful and always available (learning mainly zsh or tcsh restricts you in many situations).
- Learn vim. There's really no competition for random Linux editing (even if you use Emacs or Eclipse most of the time).
- Know ssh, and the basics of passwordless authentication, via ssh-agent, ssh-add, etc.
- Be familiar with bash job management: &, Ctrl-Z, Ctrl-C, jobs, fg, bg, kill, etc.
- Basic file management: ls and ls -l (in particular, learn what every column in "ls -l" means), less, head, tail and tail -f, ln and ln -s (learn the differences and advantages of hard versus soft links), chown, chmod, du (for a quick summary of disk usage: du -sk *), df, mount.
- Basic network management: ip or ifconfig, dig.
- Know regular expressions well, and the various flags to grep/egrep. The -o, -A, and -B options are worth knowing.
- Learn to use apt-get or yum (depending on distro) to find and install packages.

## Everyday use

- In bash, use Ctrl-R to search through command history.
- In bash, use Ctrl-W to kill the last word, and Ctrl-U to kill the line. See man readline for default keybindings in bash. There are a lot. For example Alt-. cycles through prevous arguments, and Alt-* expands a glob.
- To go back to the previous working directory: cd -
- If you are halfway through typing a command but change your mind, hit Alt-# to add a # at the beginning and enter it as a comment (or use Ctrl-A, #, enter). You can then return to it later via command history.
- Use xargs (or parallel). It's very powerful. Note you can control how many items execute per line (-L) as well as parallelism (-P). If you're not sure if it'll do the right thing, use xargs echo first. Also, -I{} is handy. Examples:

      find . -name \*.py | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname

- pstree -p is a helpful display of the process tree.
- Use pgrep and pkill to find or signal processes by name (-f is helpful).
- Know the various signals you can send processes. For example, to suspend a process, use kill -STOP [pid].  For the full list, see man 7 signal
- Use nohup or disown if you want a background process to keep running forever.
- Check what processes are listening via netstat -lntp. See also lsof.
- In bash scripts, use set -x for debugging output. Use set -e to abort on errors. - Consider using set -o pipefail as well, to be strict about errors (though this topic is a bit subtle). For more involved scripts, also use trap.
- In bash scripts, subshells (written with parentheses) are convenient ways to group commands. A common example is to temporarily move to a different working directory, e.g.

      # do something in current dir
      (cd /some/other/dir; other-command)
      # continue in original dir

- In bash, note there are lots of kinds of variable expansion. Checking a variable exists: ${name:?error message}. For example, if a bash script requires a single argument, just write input_file=${1:?usage: $0 input_file}. Arithmetic expansion: i=$(( (i + 1) % 5 )). Sequences: {1..10}. Trimming of strings: ${var%suffix} and ${var#prefix}. For example if var=foo.pdf, then echo ${var%.pdf}.txt prints "foo.txt".
- The output of a command can be treated like a file via <(some command). For example, compare local /etc/hosts with a remote one: diff /etc/hosts <(ssh somehost cat /etc/hosts)
- Know about "here documents" in bash, as in cat <<EOF ....
- In bash, redirect both standard output and standard error via: some-command >logfile 2>&1. Often, to ensure a command does not leave an open file handle to standard input, tying it to the terminal you are in, it is also good practice to add "</dev/null".
- Use man ascii for a good ASCII table, with hex and decimal values.
- On remote ssh sessions, use screen or dtach to save your session, in case it is interrupted.
- In ssh, knowing how to port tunnel with -L or -D (and occasionally -R) is useful, e.g. to access web sites from a remote server.
- It can be useful to make a few optimizations to your ssh configuration; for example, this .ssh/config contains settings to avoid dropped connections in certain network environments, not require confirmation connecting to new hosts, forward authentication, and use compression (which is helpful with scp over low-bandwidth connections):

      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      StrictHostKeyChecking=no
      Compression=yes
      ForwardAgent=yes

- To get the permissions on a file in octal form, which is useful for system configuration but not available in "ls" and easy to bungle, use something like
stat -c '%A %a %n' /etc/timezone

## Data processing

- To convert HTML to text: lynx -dump -stdin
- If you must handle XML, xmlstarlet is old but good.
- For JSON, use jq.
- For Amazon S3, s3cmd is convenient (albeit immature, with occasional misfeatures).
- Know about sort and uniq (including uniq's -u and -d options).
- Know about cut, paste, and join to manipulate text files. Many people use cut but forget about join.
- It is remarkably helpful sometimes that you can do set intersection, union, and difference of text files via sort/uniq. Suppose a and b are text files that are already uniqued. This is fast, and works on files of arbitrary size, up to many gigabytes. (Sort is not limited by memory, though you may need to use the -T option if /tmp is on a small root partition.)

      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b

- Know that locale affects a lot of command line tools, including sorting order and performance. Most Linux installations will set LANG or other locale variables to a local setting like US English. This can make sort or other commands run many times slower. (Note that even if you use UTF-8 text, you can safely sort by ASCII order for many purposes.) To disable slow i18n routines and use traditional byte-based sort order, use export LC_ALL=C (in fact, consider putting this in your .bashrc).
Know basic awk and sed for simple data munging. For example, summing all numbers in the third column of a text file: awk '{ x += $3 } END { print x }'. This is probably 3X faster and 3X shorter than equivalent Python.
- To replace all occurrences of a string in place, in one or more files:
perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
- To rename many files at once according to a pattern, use rename. (Or if you want something more general, my own tool repren may help.)

      rename 's/\.bak$//' *.bak

- Use shuf to shuffle or select random lines from a file.
- Know sort's options. Know how keys work (-t and -k). In particular, watch out that you need to write -k1,1 to sort by only the first field; -k1 means sort according to the whole line.
- Stable sort (sort -s) can be useful. For example, to sort first by field 2, then secondarily by field 1, you can use sort -k1,1 | sort -s -k2,2
- If you ever need to write a tab literal in a command line in bash (e.g. for the -t argument to sort), press Ctrl-V <tab> or write $'\t' (the latter is better as you can copy/paste it).
- For binary files, use hd for simple hex dumps and bvi for binary editing.
- Also for binary files, strings (plus grep, etc.) lets you find bits of text.
- To convert text encodings, try iconv. Or uconv for more advanced use; it supports some advanced Unicode things. For example, this command lowercases and removes all accents (by expanding and dropping them):

      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt

- To split files into pieces, see split (to split by size) and csplit (to split by a pattern).

## System debugging

- For web debugging, curl and curl -I are handy, and/or their wget equivalents.
- To know disk/cpu/network status, use iostat, netstat, top (or the better htop), and (especially) dstat. Good for getting a quick idea of what's happening on a system.
- To know memory status, run and understand the output of free and vmstat. In particular, be aware the "cached" value is memory held by the Linux kernel as file cache, so effectively counts toward the "free" value.
- Java system debugging is a different kettle of fish, but a simple trick on Sun's and some other JVMs is that you can run kill -3 <pid> and a full stack trace and heap summary (including generational garbage collection details, which can be highly informative) will be dumped to stderr/logs.
- Use mtr as a better traceroute, to identify network issues.
- For looking at why a disk is full, ncdu saves time over the usual commands like "du -sk *".
- To find which socket or process is using bandwidth, try iftop or nethogs.
- The ab tool (comes with Apache) is helpful for quick-and-dirty checking of web server performance. For more complex load testing, try siege.
- For more serious network debugging, wireshark or tshark.
- Know strace and ltrace. These can be helpful if a program is failing, hanging, or crashing, and you don't know why, or if you want to get a general idea of performance. - Note the profiling option (-c), and the ability to attach to a running process (-p).
- Know about ldd to check shared libraries etc.
- Know how to connect to a running process with gdb and get its stack traces.
- Use /proc. It's amazingly helpful sometimes when debugging live problems. Examples: /proc/cpuinfo, /proc/xxx/cwd, /proc/xxx/exe, /proc/xxx/fd/, /proc/xxx/smaps.
- When debugging why something went wrong in the past, sar can be very helpful. It shows historic statistics on CPU, memory, network, etc.
- For deeper systems and performance analyses, look at stap (systemtap) and perf.
- Confirm what Linux distribution you're using (works on most distros): "lsb_release -a"
- Use dmesg whenever something's acting really funny (it could be hardware or driver issues).

Disclaimer: Just because you can do something in bash, doesn't necessarily mean you should. ;)
