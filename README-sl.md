[ Jeziki: [English](README.md), [Español](README-es.md), [Português](README-pt.md), [中文](README-zh.md) ]



# Umetnost ukazne vrstice

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Meta](#meta)
- [Osnove](#osnove)
- [Vsakodnevna uporaba](#vsakodnevna-uporaba)
- [Procesiranje datotek in podatkov](#procesiranje-datotek-in-podatkov)
- [Sistemsko razhroščevanje](#sistemsko-razhroscevanje)
- [V eni vrstici](#v-eni-vrstici)
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

- V Bash-u uporabite **Tab** za dokončanje argumentov in **ctrl-r**, da iščete skozi zgodovino ukazov.

- V Bash-u uporabite **ctrl-w**, da izbrišete zadnjo besedo in **ctrl-u**, da izbrišete vse do začetka vrstice. Uporabite **alt-b** in **alt-f**, da se premikate po besedah, **ctrl-k**, da ubijete do začetka vrstice, **ctrl-l**, da počistite zaslon. Glejte `man readline` za vse privzete vezave tipk v Bash-u. Na voljo jih je veliko. Na primer **alt-.** kroži skozi prejšnje argumente in **alt-*** razširi glob.

- Alternativno, če imate radi vi-stilske vezave tipk, uporabite `set -o vi`.

- Da vidite nedavne ukaze, `history`. Na voljo je tudi veliko okrajšav, kot je `!$` (zadnji argument) in `!!` zadnji ukaz, čeprav so te pogostokrat enostavno zamenjani s **ctrl-r** in **alt-.**.

- Da greste nazaj na prejšnji delovni dirketorij: `cd -`

- Če ste na pol poti skozi vpisovanje ukaza, vendar si premislite, vtipkajte **alt-#**, da dodate `#` na začetek in ga vnesete kot komentar (ali uporabite **ctrl-a**, **#**, **enter**). Nato se lahko vrnete k njemu kasneje preko zgodovine ukazov.

- Uporabite `xargs` (ali `parallel`). Je zelo močan. Bodite pozorni, da lahko kontrolirate, kolikokrat izvršite na vrstico (`-L`) kot tudi paralelnost (`-P`). Če niste prepričani, da bo naredilo pravilno stvar, uporabite najprej `xargs echo`. Tudi `-I{}` je priročen. Primeri:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` je priročen prikaz drevesa procesov.

- Uporabite `pgrep` in `pkill`, da najdete ali signalizirate procese po imenu (`-f` je v pomoč).

- Vedite različne signale, katerim lahko pošljete procese. Na primer, da suspendirate proces, uporabite `kill -STOP [pid]`. Za celotni seznam glejte `man 7 signal`

- Uporabite `nohup` ali `disown`, če želite proces iz ozadja, da vedno poteka.

- Preverite, kateri procesi se poslušajo preko `netstat -lntp` ali `ss -plat` (za TCP; dodajte `-u` za UDP).

- Glejte tudi `lsof` za odprte priključke in datoteke.

- Uporabite `alias`, da ustvarite bližnjice za pogosto uporabljene ukaze. Na primer, `alias ll='ls -latr'` ustvari nov alias `ll`.

- V skriptah Bash uporabite `set -x` za razhroščevanje izpisa. Uporabite striktni način, kadarkoli je možno. Uporabite `set -e`, da prekinete na napakah. Uporabite tudi `set -o pipefail`, da ste striktni glede napak (čeprav je ta tema nekoliko subtilna). Za bolj vključene skripte uporabite tudi `trap`.

- V skriptah Bash so podlupine (napisane z oklepaji) priročen način za grupiranje ukazov. Skupen primer je začasno premakniti na različen delovni direktorij, npr.
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- V Bash-u bodite pozorni, saj je veliko vrst razširjenih spremenljivk. Preverjanje, če spremenljivka obstaja: `${name:?error message}`. Na primer, če skripta Bash zahteva en argument, samo napišite `input_file=${1:?usage: $0 input_file}`. Aritmetična raširitev: `i=$(( (i + 1) % 5 ))`. Sekvence: `{1..10}`. Obrezovanje nizov: `${var%suffix}` in `${var#prefix}`. Na primer, če je `var=foo.pdf`, potem `echo ${var%.pdf}.txt` izpiše `foo.txt`.

- Izpis ukaza se lahko tretira kot datoteko preko `<(some command)`. Na primer, primerjajte lokalno `/etc/hosts` z oddaljeno:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Spoznajte "here dokumente" v Bash-u, kot pri `cat <<EOF ...`.

- V Bash-u je preusmeritev obeh standardov izpisa in standardnih napak preko: `some-command >logfile 2>&1`. Pogosto zagotavlja, da ukaz ne pusti ročaja odprte datoteke za standardni vnos, kar ga veže na terminal v katerem se nahajate, je tudi dobra praksa, da dodate `</dev/null`.

- Uporabite `man ascii` za dobro tabelo ASCII s heksadecimalnimi in decimalnimi vrednostmi. Za splošne informacije enkodiranja so priročni `man unicode`, `man utf-8` in `man latin1`.

- Uporabite `screen` ali [`tmux`](https://tmux.github.io/), da muliplicirate zaslon, posebej uporabno na oddaljenih sejah ssh in da odstranite in se ponovno pripnete k seji. Bolj minimalna alternativa za samo obstojnost sej je `dtach`.

- V ssh je poznavanje, kako usmeriti tunel z `-L` ali `-D` (in občasno `-R`) je uporaben, npr. za dostopanje do spletnih strani iz oddaljenega strežnika.

- Lahko je uporabno, da se naredi nekaj optimizacij na vaših nastavitvah ssh; na primer, ta `~/.ssh/config` vsebuje nastavitve za izogib padle povezave v določenih okoljih omrežja, uporabite kompresijo (ki je v pomoč s scp preko nizko pasovnih povezav) in multiplicirajte kanale na isti strežnik z lokalno krmilno datoteko:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Nekaj ostalih opcij relevantnih za ssh so varnostno občutljive in bi morale biti omogočene s pazljivostjo, npr. na subnet ali gostitelja ali v zaupljivih omrežjih: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- Da dobite pravice na datoteki v osmiškem zapisu, ki je uporaben za nastavitve sistema vendar ni na voljo pri `ls` in enostaven za mešanje, uporabite nekaj takega kot je
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Za interaktivno izbiro vrednosti iz izpisa drugega ukaza, uporabite [`percol`](https://github.com/mooz/percol) ali [`fzf`](https://github.com/junegunn/fzf).

- Za interakcijo z datotekami osnovanimi na izpisu drugega ukaza (kot je `git`), uporabite `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- Za enostaven spletni strežnik za vse datoteke v trenutnem direktoriju (in poddirektorijih), ki so na voljo komurkoli v vašem omrežju, uporabite:
`python -m SimpleHTTPServer 7777` (za port 7777 in Python 2) in `python -m http.server 7777` (za port 7777 in Python 3).

- Za poogn ukaza s privilegiji, uporabite `sudo` (za root) ali `sudo -u` (za drugega uporabnika). Uporabite `su` ali `sudo bash`, da dejansko poženete lupino kot ta uporabnik. Uporabite `su -`, da simulirate svežo prijavo kot root ali drug uporabnik.


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
