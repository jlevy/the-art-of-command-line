🌍
*[Čeština](README-cs.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [中文](README-zh.md) ∙ [العربية](README-ar.md)*


#  فنون أوامر وايعازات لنكس

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [المقدمة](#المقدمة)
- [الأوليات](#الأوليات)
- [الأستخدامات اليومية](#الأستخدامات-اليومية)
- [معالجة الملفات والمعلومات](#معالجة-الملفات-والمعلومات)
- [تصحيح النظام](#تصحيح-النظام)
- [أوامر السطر الواحد](#أوامر-السطر-الواحد)
- [أومر غامضة ولكن مهمة](#أومر-غامضة-ولكن-مهمة)
- [OS X أوامر خاصة بنظام](#OS-X-أوامر-خاصة-بنظام)
- [مصادر اضافية](#مصادر-اضافية)
- [اخلاء مسؤولية](#اخلاء-مسؤولية)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)



اتقان اوامر نظام لنكس هي احدى المهارات التي لا تحظى بالأهتمام الذي تستحقة. يراها الكثيرون على انها شيء مبهم. ولكنها في حقيقة الامر ليست كذلك. وجدت هذة الاوامر والايعازات لتساعدك كمستخدم\مستخدمة على اتمام اعمالك بسرعة واتقان.
نقدم لك هنا بعض النصائح والارشادات في كيفية استخدام بعض اوامر نظام لنكس التي وجدناها مفيدة. بعض هذة الارشادات بدائية, والبعض الاخر متقدم وعلى درجة من التعقيد. هذة الصفحة ليست بالطويلة او الشاملة, ولكنك اذا تمكنت من اتقان الاوامر المذكروة هنا, فستكون\تكونين قد تعلمت الكثير.

هذا المحتوى هو نتيجة لعمل مشترك من قبل [الكثير من المحررين والمترجمين](AUTHORS.md). بعضه [نشر](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands) [لأول مرة](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix) على موقع [قورة](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know) ولكن تم نقله فيما بعد الى هنا حيث قام بعض المختصين والمحترفين بتطويرة والاضافة الية. [**الرجاء المشاركة**](/CONTRIBUTING.md) في حالة رؤيتك لخطأ ما وذلك بارسال رسالة.


## المقدمة
### الإطار:

- هذا الدليل هو للمبتدئين ولذوي الخبرة كذلك. اهدافة تشتمل على **الدقة**: عن طريق التركيز على المسائل والحالات   الشائعة. و**الإيجاز**: بتفادي الامور الثانوية، او تلك التي تدفع القارىء الى الخروج عن سياق الموضوع. كل ايعاز هنا هو اما اساسي للتعامل مع النظام في بعض الحالات، او انه (في حالات معينة) يوفر عليك الكثير من الوقت بالمقارنة مع البدائل.
- [OS X](#os-x-only)  يختص هذا الموضوع بنظام لنكس، ماعدا القسم الخاص باوامر نظام   
Unices, MacOS, Cygwin الكثير من الملاحظات يمكن تطبيقها او تثبيتها على انظمة اخرى مثل  
- bash shell يركز الموضوع على واجهة
ولكن مع ذلك، فالكثير من الملاحظات تعتبر عامة ويمكن استخدامها مع انواع اخرى
- يحتوي الموضوع على ايعازات نموذجية (تكون مبنية بالنظام) واخرى تستوجب تثبيت بعض الحزم\البرامج -- تم انتقاءها لأهميتها واستحقاقها لتكون من ضمن الايعازات المهمة.

### ملاحظات:

- لأبقاء الموضوع في صفحة واحدة، لم يتم ادراج تفصيل الايعازات والاوامر هنا, وانما تم الاشارة للروابط الخاصة. انت على درجة من الذكاء لتتمكن من ايجاد معلومات اكثر عن طريق محركات البحث. استخدم احدى الادوات ادناة لتثبيت بعض الحزم المشار اليها
 `apt-get`/`yum`/`dnf`/`pacman`/`pip`/`brew`

- [Explainshell](http://explainshell.com/) لشرح وافٍ حول تركيبة الاوامر والخصائص المشار اليها هنا, يمكنك التوجة الى  



## الأوليات



- <p dir="rtl" > لتعلم أوليات bash shell استخدم ايعاز <code>man bash</code> والقي نظرة سريعة على دليل الاستخدام. ستجد ان دليل الاستخدام بسيط  ومفيد في نفس الوقت. يوجد الكثير من البدائل لـ bash shell التي قد يبدو بعضها اكثر جاذبية ومرونة ولكن bash shell تعتبر الافضل والاكثر شيوعا. (قد يستهويك\تستهويك تعلم zshell, fish shell, الخ... ولكن هذة البدائل سوف تقيد قدراتك ومهاراتك في حالات عديدة مثل الدخول الى خادمserver من بعد)
</p>

- <p dir="rtl" > أتقن أوليات محرر نصي واحد على الأقل. يفضل ان تتعلم Vim (<code> vi</code>) كونه المحرر النصي الافضل والاكثر شيوعاُ، حيث ان جميع انظمة لنكس تدعمة بخلاف بقية برامج التحرير النصي مثل Emacs او اي نوع من المحررات التفاعلية IDE.
</p>
- <p dir="rtl" > مارس قراءة وثائق دليل الاستخدام باستخدام ايعاز <code>man</code> (لمحبي الاستطلاع -- الفضوليون -- :ايعاز <code>man man</code> يعرض قائمة بارقام الاقسام المختلفة التي يحتويها دليل الاستخدام كالرقم ١ الذي يمثل الايعازات "الاعتيادية"، والرقم ٥ الذي يمثل ايعازات الملفات والتسميات المتبعة، والرقم ٨ الذي يمثل الاوامر الادارية). يستخدم ايعاز <code>apropos</code> لعرض صفحات معينة من دليل الاستخدام. لاحظ ان بعض الايعازات غير تنفيذية بمعنى انه لايمكن استخدامها كأوامر مباشرة وانما هي ادوات خاصة بـ bash shell يمكنك الأستعانة بـ <code>help</code> و <code>help -d</code> للتعرف على هذة الادوات.
</p>
- <p dir="rtl" > تعلم كيفية تغيير وجهة النتائج(outputs) والمداخلات(inputs) باستخدام الرموز التالية: <code> < </code> ، <code> > </code> ،<code>|</code>. لاحظ ان الرمز <code> < </code> يقوم بمحو محتويات الملف الاصلية واستبدالها بالنتائج الجديدة، في حين استخدام <code> << </code> يقوم باصافة النتائج الجديدة الى المحتوى الاصلي للملف. يشار للنتائج  القياسية (standard output) بـ stdout وللأخطاء الاساسية (standard error) بـ stderr.
</p>
- <p dir="rtl" > تعلم الامتداد العام للملفات باستخدام رمز <code> * </code> (وغيره من الرموز مثل <code> ? </code> و<code>]</code>...<code>[</code> ورموز الاقتباس والفرق بين الاقتباس المزدوج <code>"</code> والفردي <code>'</code> -- ستتعرف ادناة على المزيد من امدادات الملفات)
</p>

- <p dir="rtl" >
كن على اطلاع بكيفية ادارة الاعمال bash shell job management مثل: <code>&</code>، <b>ctrl-z</b>، <b>ctrl-c</b>، <code>jobs</code>، <code>fg</code>، <code>bg</code>، <code>kill</code>، الخ...
</p>

- <p dir="rtl" >
تعلم كيفية ادارة النظام من بعد باستخدام <code>ssh</code> وكيفية الدخول للنظام بدون استخدام كلمة سر عن طريق  <code>ssh-add</code> ، <code>ssh-agent</code>، وغيرهما من الادوات. 
</p>

- <p dir="rtl" >
- مارس أوليات ادارة الملفات:  <code>ls</code>  و <code>ls -l</code>  (اعرف ماعية كل عمود في  <code>ls -l</code> )، <code>less</code> ،  <code>head</code> ،  <code>tail</code> ، و  <code>tail +F</code>  .
وان امكن <code>ln</code> و <code>ln -s</code>  كن ملما باختلافات وفوائد كل من الروابط "الرقيقة" والروابط "الصلبة"،  <code>chown</code> ،  <code>chmod</code> ،   <code>du</code>  للحصول على نبذة مختصرة عن القرص الصلب:  <code>du -sh *</code> .
لادارة ملفات النظام:  <code>df</code> ،  <code>mount</code> ،  <code>fdisk</code> ،  <code>mkfs</code> ،  <code>lsblk</code> .  تعلم ما تمثلة indone وانواعها المختلفة ( <code>ls -i</code> او  <code>df -i</code> ).

</p>

-  <p dir="rtl" >
مارس أوليات ادارة الشبكات: <code>ip</code>، <code>ifconfig</code>، <code>dig</code>.

</p>

- <p dir="rtl" >
اتقن التعابير التنظيمية (او مايعرف بـ regex)، ومختلف لوائح <code>grep</code>/<code>egrep</code>. الخيارات ادناة تسترعي الانتباه كونها شائعة الاستخدام:
<code>-i</code>، <code>-o</code>، <code>-v</code>، <code>-A</code>، <code>-B</code>،<code>-C</code>.
</p>

- <p dir="rtl" >
تعلم كيفية استخدام </code>apt-get</code>، <code>yum</code>، <code>dnf</code>، <code>pacman<code> (حسب نوعية نظامك). وتأكد من وجود مدير الحزم: </code>pip<code> على النظام ولذلك ليتسنى لك امكانية تثبيت البرامج والحزم المكتوبة بلغة بايثون (بعض البرامج ادناة يمكن تثبيتها بسهولة باستخدام </code>pip<code>).
</p>
## الأستخدامات اليومية

- In Bash, use **Tab** to complete arguments or list all available commands and **ctrl-r** to search through command history (after pressing, type to search, press **ctrl-r** repeatedly to cycle through more matches, press **Enter** to execute the found command, or hit the right arrow to put the result in the current line to allow editing).

- In Bash, use **ctrl-w** to delete the last word, and **ctrl-u** to delete all the way back to the start of the line. Use **alt-b** and **alt-f** to move by word, **ctrl-a** to move cursor to beginning of line,  **ctrl-e** to move cursor to end of line, **ctrl-k** to kill to the end of the line, **ctrl-l** to clear the screen. See `man readline` for all the default keybindings in Bash. There are a lot. For example **alt-.** cycles through previous arguments, and **alt-*** expands a glob.


- Alternatively, if you love vi-style key-bindings, use `set -o vi` (and `set -o emacs` to put it back).

- For editing long commands, after setting your editor (for example `export EDITOR=vim`), **ctrl-x** **ctrl-e** will open the current command in an editor for multi-line editing. Or in vi style, **escape-v**.

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

- See `uptime` or `w` to know the how long the system has been running.

- Use `alias` to create shortcuts for commonly used commands. For example, `alias ll='ls -latr'` creates a new alias `ll`.

- In Bash scripts, use `set -x` (or the variant `set -v`, which logs raw input, including unexpanded variables and comments) for debugging output. Use strict modes unless you have a good reason not to: Use `set -e` to abort on errors (nonzero exit code). Use `set -u` to detect unset variable usages. Consider `set -o pipefail` too, to on errors within pipes, too (though read up on it more if you do, as this topic is a bit subtle). For more involved scripts, also use `trap` on EXIT or ERR. A useful habit is to start a script like this, which will make it detect and abort on common errors and print a message:
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- In Bash scripts, subshells (written with parentheses) are convenient ways to group commands. A common example is to temporarily move to a different working directory, e.g.
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- In Bash, note there are lots of kinds of variable expansion. Checking a variable exists: `${name:?error message}`. For example, if a Bash script requires a single argument, just write `input_file=${1:?usage: $0 input_file}`. Arithmetic expansion: `i=$(( (i + 1) % 5 ))`. Sequences: `{1..10}`. Trimming of strings: `${var%suffix}` and `${var#prefix}`. For example if `var=foo.pdf`, then `echo ${var%.pdf}.txt` prints `foo.txt`.

- Brace expansion using `{`...`}` can reduce having to re-type similar text and automate combinations of items.  This is helpful in examples like `mv foo.{txt,pdf} some-dir` (which moves both files), `cp somefile{,.bak}` (which expands to `cp somefile somefile.bak`) or `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (which expands all possible combinations and creates a directory tree).

- The output of a command can be treated like a file via `<(some command)`. For example, compare local `/etc/hosts` with a remote one:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Know about "here documents" in Bash, as in `cat <<EOF ...`.

- In Bash, redirect both standard output and standard error via: `some-command >logfile 2>&1` or `some-command &>logfile`. Often, to ensure a command does not leave an open file handle to standard input, tying it to the terminal you are in, it is also good practice to add `</dev/null`.

- Use `man ascii` for a good ASCII table, with hex and decimal values. For general encoding info, `man unicode`, `man utf-8`, and `man latin1` are helpful.

- Use `screen` or [`tmux`](https://tmux.github.io/) to multiplex the screen, especially useful on remote ssh sessions and to detach and re-attach to a session. `byobu` can enhance screen or tmux providing more information and easier management. A more minimal alternative for session persistence only is `dtach`.

- In ssh, knowing how to port tunnel with `-L` or `-D` (and occasionally `-R`) is useful, e.g. to access web sites from a remote server.

- It can be useful to make a few optimizations to your ssh configuration; for example, this `~/.ssh/config` contains settings to avoid dropped connections in certain network environments, uses compression (which is helpful with scp over low-bandwidth connections), and multiplex channels to the same server with a local control file:
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

- Consider [`mosh`](https://mosh.mit.edu/) an alternative to ssh that uses UDP, avoiding dropped connections and adding convenience on the road (requires server-side setup).

- To get the permissions on a file in octal form, which is useful for system configuration but not available in `ls` and easy to bungle, use something like
```sh
      stat -c '%A %a %n' /etc/timezone
```

- For interactive selection of values from the output of another command, use [`percol`](https://github.com/mooz/percol) or [`fzf`](https://github.com/junegunn/fzf).

- For interaction with files based on the output of another command (like `git`), use `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- For a simple web server for all files in the current directory (and subdirs), available to anyone on your network, use:
`python -m SimpleHTTPServer 7777` (for port 7777 and Python 2) and `python -m http.server 7777` (for port 7777 and Python 3).

- For running a command with privileges, use `sudo` (for root) or `sudo -u` (for another user). Use `su` or `sudo bash` to actually run a shell as that user. Use `su -` to simulate a fresh login as root or another user.


## معالجة الملفات والمعلومات

- To locate a file by name in the current directory, `find . -iname '*something*'` (or similar). To find a file anywhere by name, use `locate something` (but bear in mind `updatedb` may not have indexed recently created files).

- For general searching through source or data files (more advanced than `grep -r`), use [`ag`](https://github.com/ggreer/the_silver_searcher).

- To convert HTML to text: `lynx -dump -stdin`

- For Markdown, HTML, and all kinds of document conversion, try [`pandoc`](http://pandoc.org/).

- If you must handle XML, `xmlstarlet` is old but good.

- For JSON, use [`jq`](http://stedolan.github.io/jq/).

- For YAML, use [`shyaml`](https://github.com/0k/shyaml).

- For Excel or CSV files, [csvkit](https://github.com/onyxfish/csvkit) provides `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, etc.

- For Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) is convenient and [`s4cmd`](https://github.com/bloomreach/s4cmd) is faster. Amazon's [`aws`](https://github.com/aws/aws-cli) and the improved [`saws`](https://github.com/donnemartin/saws) are essential for other AWS-related tasks.

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

- To rename multiple files and/or search and replace within files, try [`repren`](https://github.com/jlevy/repren). (In some cases the `rename` command also allows multiple renames, but be careful as its functionality is not the same on all Linux distributions.)
```sh
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Recover backup files whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Same as above, using rename, if available:
      rename 's/\.bak$//' *.bak
```

- As the man page says, `rsync` really is a fast and extraordinarily versatile file copying tool. It's known for synchronizing between machines but is equally useful locally. It also is among the [fastest ways](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) to delete large numbers of files:
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Use `shuf` to shuffle or select random lines from a file.

- Know `sort`'s options. For numbers, use `-n`, or `-h` for handling human-readable numbers (e.g. from `du -h`). Know how keys work (`-t` and `-k`). In particular, watch out that you need to write `-k1,1` to sort by only the first field; `-k1` means sort according to the whole line. Stable sort (`sort -s`) can be useful. For example, to sort first by field 2, then secondarily by field 1, you can use `sort -k1,1 | sort -s -k2,2`.

- If you ever need to write a tab literal in a command line in Bash (e.g. for the -t argument to sort), press **ctrl-v** **[Tab]** or write `$'\t'` (the latter is better as you can copy/paste it).

- The standard tools for patching source code are `diff` and `patch`. See also `diffstat` for summary statistics of a diff and `sdiff` for a side-by-side diff. Note `diff -r` works for entire directories. Use `diff -r tree1 tree2 | diffstat` for a summary of changes. Use `vimdiff` to compare and edit files.

- For binary files, use `hd`, `hexdump` or `xxd` for simple hex dumps and `bvi` or `biew` for binary editing.

- Also for binary files, `strings` (plus `grep`, etc.) lets you find bits of text.

- For binary diffs (delta compression), use `xdelta3`.

- To convert text encodings, try `iconv`. Or `uconv` for more advanced use; it supports some advanced Unicode things. For example, this command lowercases and removes all accents (by expanding and dropping them):
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- To split files into pieces, see `split` (to split by size) and `csplit` (to split by a pattern).

- To manipulate date and time expressions, use `dateadd`, `datediff`, `strptime` etc. from [`dateutils`](http://www.fresse.org/dateutils/).

- Use `zless`, `zmore`, `zcat`, and `zgrep` to operate on compressed files.


## تصحيح النظام

- For web debugging, `curl` and `curl -I` are handy, or their `wget` equivalents, or the more modern [`httpie`](https://github.com/jkbrzt/httpie).

- To know current cpu/disk status, the classic tools are `top` (or the better `htop`), `iostat`, and `iotop`. Use `iostat -mxz 15` for basic CPU and detailed per-partition disk stats and performance insight.

- For network connection details, use `netstat` and `ss`.

- For a quick overview of what's happening on a system, `dstat` is especially useful. For broadest overview with details, use [`glances`](https://github.com/nicolargo/glances).

- To know memory status, run and understand the output of `free` and `vmstat`. In particular, be aware the "cached" value is memory held by the Linux kernel as file cache, so effectively counts toward the "free" value.

- Java system debugging is a different kettle of fish, but a simple trick on Oracle's and some other JVMs is that you can run `kill -3 <pid>` and a full stack trace and heap summary (including generational garbage collection details, which can be highly informative) will be dumped to stderr/logs. The JDK's `jps`, `jstat`, `jstack`, `jmap` are useful. [SJK tools](https://github.com/aragozin/jvm-tools) are more advanced.

- Use `mtr` as a better traceroute, to identify network issues.

- For looking at why a disk is full, `ncdu` saves time over the usual commands like `du -sh *`.

- To find which socket or process is using bandwidth, try `iftop` or `nethogs`.

- The `ab` tool (comes with Apache) is helpful for quick-and-dirty checking of web server performance. For more complex load testing, try `siege`.

- For more serious network debugging, `wireshark`, `tshark`, or `ngrep`.

- Know about `strace` and `ltrace`. These can be helpful if a program is failing, hanging, or crashing, and you don't know why, or if you want to get a general idea of performance. Note the profiling option (`-c`), and the ability to attach to a running process (`-p`).

- Know about `ldd` to check shared libraries etc.

- Know how to connect to a running process with `gdb` and get its stack traces.

- Use `/proc`. It's amazingly helpful sometimes when debugging live problems. Examples: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (where `xxx` is the process id or pid).

- When debugging why something went wrong in the past, `sar` can be very helpful. It shows historic statistics on CPU, memory, network, etc.

- For deeper systems and performance analyses, look at `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_(Linux)), and [`sysdig`](https://github.com/draios/sysdig).

- Check what OS you're on with `uname` or `uname -a` (general Unix/kernel info) or `lsb_release -a` (Linux distro info).

- Use `dmesg` whenever something's acting really funny (it could be hardware or driver issues).


## أوامر السطر الواحد

A few examples of piecing together commands:

- It is remarkably helpful sometimes that you can do set intersection, union, and difference of text files via `sort`/`uniq`. Suppose `a` and `b` are text files that are already uniqued. This is fast, and works on files of arbitrary size, up to many gigabytes. (Sort is not limited by memory, though you may need to use the `-T` option if `/tmp` is on a small root partition.) See also the note about `LC_ALL` above and `sort`'s `-u` option (left out for clarity below).
```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- Use `grep . *` to quickly examine the contents of all files in a directory (so each line is paired with the filename), or `head -100 *` (so each file has a heading). This can be useful for directories filled with config settings like those in `/sys`, `/proc`, `/etc`.


- Summing all numbers in the third column of a text file (this is probably 3X faster and 3X less code than equivalent Python):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- To see sizes/dates on a tree of files, this is like a recursive `ls -l` but is easier to read than `ls -lR`:
```sh
      find . -type f -ls
```

- Say you have a text file, like a web server log, and a certain value that appears on some lines, such as an `acct_id` parameter that is present in the URL. If you want a tally of how many requests for each `acct_id`:
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- To continuously monitor changes, use `watch`, e.g. check changes to files in a directory with `watch -d -n 2 'ls -rtlh | tail'` or to network settings while troubleshooting your wifi settings with `watch -d -n 2 ifconfig`.

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


## أومر غامضة ولكن مهمة

- `expr`: perform arithmetic or boolean operations or evaluate regular expressions

- `m4`: simple macro processor

- `yes`: print a string a lot

- `cal`: nice calendar

- `env`: run a command (useful in scripts)

- `printenv`: print out environment variables (useful in debugging and scripts)

- `look`: find English words (or lines in a file) beginning with a string

- `cut`, `paste` and `join`: data manipulation

- `fmt`: format text paragraphs

- `pr`: format text into pages/columns

- `fold`: wrap lines of text

- `column`: format text fields into aligned, fixed-width columns or tables

- `expand` and `unexpand`: convert between tabs and spaces

- `nl`: add line numbers

- `seq`: print numbers

- `bc`: calculator

- `factor`: factor integers

- [`gpg`](https://gnupg.org/): encrypt and sign files

- `toe`: table of terminfo entries

- `nc`: network debugging and data transfer

- `socat`: socket relay and tcp port forwarder (similar to `netcat`)

- [`slurm`](https://github.com/mattthias/slurm): network traffic visualization

- `dd`: moving data between files or devices

- `file`: identify type of a file

- `tree`: display directories and subdirectories as a nesting tree; like `ls` but recursive

- `stat`: file info

- `time`: execute and time a command

- `timeout`: execute a command for specified amount of time and stop the process when the specified amount of time completes.

- `lockfile`: create semaphore file that can only be removed by `rm -f`

- `logrotate`: rotate, compress and mail logs.

- `watch`: run a command repeatedly, showing results and/or highlighting changes

- `tac`: print files in reverse

- `shuf`: random selection of lines from a file

- `comm`: compare sorted files line by line

- `pv`: monitor the progress of data through a pipe

- `hd`, `hexdump`, `xxd`, `biew` and `bvi`: dump or edit binary files

- `strings`: extract text from binary files

- `tr`: character translation or manipulation

- `iconv` or `uconv`: conversion for text encodings

- `split` and `csplit`: splitting files

- `sponge`: read all input before writing it, useful for reading from then writing to the same file, e.g., `grep -v something some-file | sponge some-file`

- `units`: unit conversions and calculations; converts furlongs per fortnight to twips per blink (see also `/usr/share/units/definitions.units`)

- `apg`: generates random passwords

- `7z`: high-ratio file compression

- `ldd`: dynamic library info

- `nm`: symbols from object files

- `ab`: benchmarking web servers

- `strace`: system call debugging

- `mtr`: better traceroute for network debugging

- `cssh`: visual concurrent shell

- `rsync`: sync files and folders over SSH or in local file system

- `wireshark` and `tshark`: packet capture and network debugging

- `ngrep`: grep for the network layer

- `host` and `dig`: DNS lookups

- `lsof`: process file descriptor and socket info

- `dstat`: useful system stats

- [`glances`](https://github.com/nicolargo/glances): high level, multi-subsystem overview

- `iostat`: Disk usage stats

- `mpstat`: CPU usage stats

- `vmstat`: Memory usage stats

- `htop`: improved version of top

- `last`: login history

- `w`: who's logged on

- `id`: user/group identity info

- `sar`: historic system stats

- `iftop` or `nethogs`: network utilization by socket or process

- `ss`: socket statistics

- `dmesg`: boot and system error messages

- `sysctl`: view and configure Linux kernel parameters at run time

- `hdparm`: SATA/ATA disk manipulation/performance

- `lsb_release`: Linux distribution info

- `lsblk`: list block devices: a tree view of your disks and disk paritions

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: hardware information, including CPU, BIOS, RAID, graphics, devices, etc.

- `lsmod` and `modinfo`: List and show details of kernel modules.

- `fortune`, `ddate`, and `sl`: um, well, it depends on whether you consider steam locomotives and Zippy quotations "useful"


## OS X أوامر خاصة بنظام

These are items relevant *only* on MacOS.

- Package management with `brew` (Homebrew) and/or `port` (MacPorts). These can be used to install on MacOS many of the above commands.

- Copy output of any command to a desktop app with `pbcopy` and paste input from one with `pbpaste`.

- To enable the Option key in Mac OS Terminal as an alt key (such as used in the commands above like **alt-b**, **alt-f**, etc.), open Preferences -> Profiles -> Keyboard and select "Use Option as Meta key".

- To open a file with a desktop app, use `open` or `open -a /Applications/Whatever.app`.

- Spotlight: Search files with `mdfind` and list metadata (such as photo EXIF info) with `mdls`.

- Be aware MacOS is based on BSD Unix, and many commands (for example `ps`, `ls`, `tail`, `awk`, `sed`) have many subtle variations from Linux, which is largely influenced by System V-style Unix and GNU tools. You can often tell the difference by noting a man page has the heading "BSD General Commands Manual." In some cases GNU versions can be installed, too (such as `gawk` and `gsed` for GNU awk and sed). If writing cross-platform Bash scripts, avoid such commands (for example, consider Python or `perl`) or test carefully.

- To get MacOS release information, use `sw_vers`.


## مصادر اضافية

- [awesome-shell](https://github.com/alebcay/awesome-shell): A curated list of shell tools and resources.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): A more in-depth guide for the Mac OS command line.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) for writing better shell scripts.
- [shellcheck](https://github.com/koalaman/shellcheck): A shell script static analysis tool. Essentially, lint for bash/sh/zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): The sadly complex minutiae on how to handle filenames correctly in shell scripts.


## اخلاء مسؤولية

With the exception of very small tasks, code is written so others can read it. With power comes responsibility. The fact you *can* do something in Bash doesn't necessarily mean you should! ;)


## License

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
