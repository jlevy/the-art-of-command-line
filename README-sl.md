[ Jeziki: [English](README.md), [Español](README-es.md), [Português](README-pt.md), [中文](README-zh.md) ]



# Umetnost ukazne vrstice

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Meta](#meta)
- [Osnove](#osnove)
- [Vsakodnevna uporaba](#everyday-use)
- [Procesiranje datotek in podatkov](#procesiranje-datotek-in-podatkov)
- [Sistemsko razhroščevanje](#system-debugging)
- [V eni vrstici](#one-liners)
- [Nepregledno vendar uporabno](#nejasno-vendar-uporabno)
- [Samo za MacOS](#samo-za-macos)
- [Več virov](#vec-virov)
- [Pogoji uporabe](#pogoji-uporabe)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

Jedrnatost v ukazni vrstici je znanje, ki je pogostokrat zanemarjeno ali smatrano za zastarelo, vendar izboljša vašo fleksibilnost in produktivnost kot inženir na očitne in neočitne načine. To so izbrani zapiski in nasveti glede uporabe ukazne vrstice, ki sem jo našel uporabno pri delu z Linux-om. Nekateri nasveti so elementarni in nekateri so precej določeni, sofisticirani ali nepregledni. Ta stran ni dolga, vendar če lahko uporabite in se spomnite vseh elementov tu, boste vedeli veliko.

Veliko tega
se [prvotno](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[pojavi](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
na [Quori](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
vendar glede na dani interes tu, izgleda vredno uporabe GitHub-a, kjer ljudje bolj talentirani kot jaz lahko bralno predlagajo izboljšave. Če opazite napako ali nekaj, kar je lahko bolje, prosim, pošljite težavo ali zahtevek potega (PR)! (Seveda, prosim preglejte meta sekcijo in obstoječe težave/zahtevke potega najprej.)


## Meta

Obseg:

- Ta vodič je tako za začetnike kot za poznavalce. Cilji so *širina* (vse pomembno), *specifičnost* (podaja konkretne primere najpogostejših primerov uporabe) in *kratkost* (izogiba se stvarem, ki niso bistvene ali se odmikajo, kar lahko enostavno pogledate drugje). Vsak nasvet je bistven v določeni situaciji ali bistveno prihrani čas pred alternativami.
- To je napisano za Linux z izjemo sekcije "[Samo za MacOS](#samo-za-macos)". Mnogi ostali elementi veljajo ali pa so lahko nameščeni na drugih Unix-ih ali MacOS (ali celo Cygwin).
- Poudarek je na interaktivnosti Bash-a, čeprav mnogo nasvetov velja za ostale lupine in splošno skriptanje Bash-a.
- Vključuje tako "standardne" ukaze Unix-a kot tudi tiste, ki zahtevajo namestitev posebnih paketov -- dokler so dovolj pomembni, da zaslužijo vključitev.

Opombe:

- Da se obdrži to na eni strani, je vsebina implicitno vključena z referencami. Ste dovolj pametni, da poiščete več podrobnosti drugje, ko enkrat veste idejo ali ukaz za iskanje na Google-u. Uporabite `apt-get`/`yum`/`dnf`/`pacman`/`pip`/`brew` (kot je ustrezno), da namestite nove programe.
- Uporabite [Explainshell](http://explainshell.com/), da dobite uporabne razčlenitve, kaj ukazi, opcije, cevi itd. naredijo.


## Osnove

- Naučite se osnovni Bash. Dejansko vtipkajte `man bash` in vsaj prelistajte celotno stvar; slediti je precej enostavno in ni tako dolgo. Alternativne lupine so lahko lepe, vendar Bash je močan in vedno na voljo (učenje *samo* zsh, fish itd., medtem ko poskušate na lastno pest na vašem prenosniku, vas omeji v mnogih situacijah, kot je uporaba obstoječih strežnikov).

- Naučite se tudi vsaj enega tekstovno osnovanega urejevalnika. Idealno Vim (`vi`) saj v realnosti ni konkurence za naključno urejanje v terminalu (tudi, če uporabljate Emacs, velik IDE, ali moderni hipsterski urejevalnik večino časa).

- Vedeti, kako brati dokumentacijo z `man` (za radovedne, `man man` izpiše številke sekcij, npr. 1 so "splošni" ukazi, 5 so datoteke/konvencije in 8 je za administracijo). Najdite strani man z `apropos`. Vedeti, da nekateri ukazi niso izvršljivi, vendar vgrajeni v Bash in pomoč zanje lahko dobite s `help` in `help -d`.

- Naučite se o preusmeritvi izpisa in vnosa z uporabo `>` in `<` ter uporabo cevi `|`. Vedite, da `>` prepiše izpis datoteke in `>>` ga pripne. Naučite se o stdout in stderr.

- Naučite se o razširitvi datotek glob z `*` (in mogoče `?` ter `{`...`}`) in citiranje ter razliko med dvojnim `"` in enojnim `'` citatom. (Poglejte več o razširitvi spremenljivk spodaj.)

- Seznanite se z upravljanjem nalog Bash-a: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill` itd.

- Spoznajte `ssh` in osnove avtentikacije brez gesla, preko `ssh-agent`, `ssh-add` itd.

- Osnovno upravljanje datotek: `ls` in `ls -l` (še posebej, se naučite, kaj vsak stolpec v `ls -l` pomeni), `less`, `head`, `tail` in `tail -f` (ali celo boljše, `less +F`), `ln` in `ln -s` (naučite se razlike in prednosti trdih in mehkih povezav), `chown`, `chmod`, `du` (za hiter povzetek uporabe diska: `du -hk *`). Za upravljanje datotečnega sistema, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`.

- Osnovno upravljanje omrežja: `ip` or `ifconfig`, `dig`.

- Vedite tudi splošne izraze in različne zastavice za `grep`/`egrep`. Opcije `-i`, `-o`, `-A` in `-B` so vredne znanja.

- Naučite se uporabljati `apt-get`, `yum`, `dnf` ali `pacman` (odvisno od distribucije), da najdete in namestite pakete. In zagotovite, da imate `pip`, da lahko nameščate orodja ukazne vrstice na osnovi Python-a (nekaj spodnjih je najenostavneje namestiti preko `pip`).


## Vsakodnevna uporaba

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


## Procesiranje datotek in podatkov

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


## Sistemsko razhroščevanje

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


## V eni vrstici

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


## Nepregledno vendar uporabno

- `expr`: perform arithmetic or boolean operations or evaluate regular expressions

- `m4`: simple macro processor

- `yes`: print a string a lot

- `cal`: nice calendar

- `env`: run a command (useful in scripts)

- `printenv`: print out environment variables (useful in debugging and scripts)

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

- `pv`: monitor the progress of data through a pipe

- `hd` and `bvi`: dump or edit binary files

- `strings`: extract text from binary files

- `tr`: character translation or manipulation

- `iconv` or `uconv`: conversion for text encodings

- `split `and `csplit`: splitting files

- `sponge`: read all input before writing it, useful for reading from then writing to the same file, e.g., `grep -v something some-file | sponge some-file`

- `units`: unit conversions and calculations; converts furlongs per fortnight to twips per blink (see also `/usr/share/units/definitions.units`)

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

- `lsblk`: List block devices: a tree view of your disks and disk paritions

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: hardware information, including CPU, BIOS, RAID, graphics, devices, etc.

- `fortune`, `ddate`, and `sl`: um, well, it depends on whether you consider steam locomotives and Zippy quotations "useful"


## Samo za MacOS

To so elementi pomembni *samo* za MacOS.

- Upravljanje paketov z `brew` (Homebrew) in/ali `port` (MacPorts). Te so lahko uporabljeni za namestitev na MacOS mnogih zgornjih ukazov.

- Kopirajte izpis katerega koli ukaza na namizno aplikacijo s `pbcopy` in prilepite vnos iz ene s `pbpaste`.

- Da oprete datoteko z namizno aplikacijo, uporabite `open` ali `open -a /Applications/Whatever.app`.

- Spotlight: Poiščite datoteke z `mdfind` in izpišite meta podatke (kot so EXIF informacije fotografije) z `mdls`.

- Bodite pozorni, saj je MacOS osnovan na BSD Unix in mnogi ukazi (na primer `ps`, `ls`, `tail`, `awk`, `sed`) imajo mnoge subtilne različice iz Linux-a, na katerega je večinoma vplival System V-style Unix in GNU tools. Pogostokrat lahko poveste razliko, da opazite, da ima stran man naslov "BSD General Commands Manual." V nekaterih primerih se lahko namestijo tudi GNU različice (kot so `gawk` in `gsed` za GNU awk in sed). Če pišete skripte Bash za vse platforme, se izogibajte takim ukazom (na primer, z upoštevanjem Python ali `perl`) ali pazljivo testirajte.


## Več virov

- [awesome-shell](https://github.com/alebcay/awesome-shell): A curated list of shell tools and resources.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) for writing better shell scripts.


## Pogoji uporabe

Z izjemo zelo majhnih opravil, je koda napisana tako, da jo lahko ostali berejo. Z močjo pride odgovornost. Dejstvo, da *lahko* naredite nekaj v Bash-u ne pomeni nujno, da bi morali! ;)


## Licenca

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

To delo je izdano pod [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
