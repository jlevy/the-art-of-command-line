🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*

# 命令列的藝術

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [必讀](#必讀)
- [基礎](#基礎)
- [日常使用](#日常使用)
- [檔案及資料處理](#檔案及資料處理)
- [系統偵錯](#系統偵錯)
- [單行指令碼](#單行指令碼)
- [冷門但有用的指令](#冷門但有用的指令)
- [僅限 OS X 系統](#僅限-os-x-系統)
- [僅限 Windows 系統](#僅限-windows-系统)
- [更多資源](#更多資源)
- [免責聲明](#免責聲明)
- [授權條款](#授權條款)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

熟練使用命令列是一種常常被忽視，或被認為難以掌握的技能，但實際上，它會提高你作為工程師的靈活性以及生產力。本文是一份我在 Linux 上工作時，發現的一些命令列使用技巧的摘要。有些技巧非常基礎，而另一些則相當複雜，甚至晦澀難懂。這篇文章並不長，但當你能夠熟練掌握這裡列出的所有技巧時，你就學會了很多關於命令列的東西了。

這篇文章是[許多作者和譯者](AUTHORS.md)共同的成果。這裡的大部分內容
[首次](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[出現](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
於 [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know)，但考慮到這裡的人們都具有學習的天賦且樂於接受別人的建議，使用 Github 來做這件事是更佳的選擇。如果你在本文中發現了錯誤或者​​存在可以改善的地方，請果斷提交 Issue 或 Pull Request！ (當然在提交前請看一下必讀節和已有的 PR/issue）。


## 必讀

涵蓋範圍：

- 這篇文章對剛接觸命令列的新手以及具有命令列使用經驗的人都有用處。本文致力於做到*覆蓋面廣*（盡量包括一切重要的內容），*具體*（給出最常見的具體的例子）以及*簡潔*（避免不必要的，或是可以在其他地方輕鬆查到的細枝末節）。每個技巧都是在特定情境下必備的，或是能顯著減省時間的。
- 本文為 Linux 所寫，除了 [僅限OS X 系統](#僅限-os-x-系統) 和 [僅限 Windows 系統](#僅限-windows-系统) 章節外，其它章節中的大部分內容都適用於其它 Unix 系統或 MacOS 系統，甚至 Cygwin。
- 本文關注於互動式 Bash，儘管很多技巧也適用於其他 shell 或 Bash 指令碼。
- 本文包括了“標準的” Unix 命令和需要安裝特定套件的命令，只要它們足夠重要。

注意事項：

- 為了能在一頁內展示盡量多的東西，一些具體的資訊會被間接的包含在引用頁裡。聰明機智的你如果掌握了使用 Google 搜尋引擎的基本方法與命令，那麼你將可以查閱到更多的詳細資訊。使用`apt-get`，`yum`，`dnf`，`pacman`，`pip` 或`brew`（以及其它合適的包管理器）來安裝新程式。
- 使用 [Explainshell](http://explainshell.com/) 去獲取相關命令、參數、管道等解釋。


## 基礎

- 學習 Bash 的基礎知識。具體來說，輸入`man bash` 並至少全文瀏覽一遍; 它很簡單並且不長。其他的 shell 可能很好用，但 Bash 功能強大且幾乎所有情況下都是可用的（ *只*學習 zsh，fish 或其他的 shell 的話，在你自己的電腦上會顯得很方便，但在很多情況下會限制你，比如當你需要在伺服器上工作時）。

- 學習並掌握至少一個基於文字的編輯器。通常 Vim （`vi`） 會是你最好的選擇，因為在終端裡進行隨機編輯 Vim 真的毫無敵手，哪怕是Emacs、某大型IDE 甚至時下非常流行的編輯器。

- 學會如何使用`man` 命令去閱讀文件。學會使用 `apropos` 去查詢文件。瞭解有些命令是不可執行，而是Bash內建的，可以使用`help` 和`help -d` 命令獲取幫助資訊。

- 學會使用`>` 和`<` 來重定向輸出和輸入，學會使用`|` 來重定向管道。明白`>` 會覆蓋了輸出文件而`>>` 是在檔案末新增。瞭解標準輸出 stdout 和標準錯誤 stderr。

- 學會使用通配符`*` （或許再算上`?` 和`[`...`]`） 和引用以及引用中`'` 和`"` 的區別。

- 熟悉 Bash 任務管理工具：`&`，**ctrl-z**，**ctrl-c**，`jobs`，`fg`，`bg`，`kill` 等。

- 瞭解`ssh`，以及學會通過使用`ssh-agent`，`ssh-add` 等命令來實現基本的無密碼認證。

- 學會基本的檔案管理：`ls` 和`ls -l` （瞭解`ls -l` 中每一列代表的意義），`less`，`head`，`tail` 和`tail -f` （甚至`less +F`），`ln` 和`ln -s` （瞭解硬連結與軟連結的區別），`chown`，`chmod`，`du` （硬碟使用情況概述：`du -hs *` ）。關於檔案系統的管理，學習`df`，`mount`，`fdisk`，`mkfs`，`lsblk`。知道 inode 是什麼（與`ls -i` 和`df -i` 等命令相關）。

- 學習基本的網路管理：`ip` 或`ifconfig`，`dig`。

- 熟悉正規表示式，以及`grep`／`egrep` 裡不同參數的作用，例如`-i`，`-o`，`-v`，`-A`，`-B` 和`-C` ，這些參數是值得學習並掌握的。

- 學會使用`apt-get`，`yum`，`dnf` 或`pacman` （取決於你使用的 Linux 發行版）來查詢或安裝軟體包。並確保你的環境中有`pip` 來安裝基於 Python 的命令列工具（接下來提到的部分程式使用`pip` 來安裝會很方便）。


## 日常使用

- 在 Bash 中，可以使用 **Tab** 自動補全參數，使用 **ctrl-r** 搜尋命令列歷史（在按下之後，鍵入便可以搜尋，重複按下**ctrl-r**會在更多匹配中迴圈，按下 **Enter** 會執行找到的命令，按下右方向鍵會將結果放入當前行中，使你可以進行編輯）。

- 在 Bash 中，可以使用 **ctrl-w** 刪除你鍵入的最後一個單詞，使用 **ctrl-u** 刪除當前游標所在位置之前的內容，使用 **alt-b** 和 **alt-f**以單詞為單位移動游標，​​使用 **ctrl-a** 將游標移至行首，使用 **ctrl-e** 將游標移至行尾，使用 **ctrl-k** 刪除游標至行尾的所有內容，使用 **ctrl-l** 清屏。鍵入`man readline` 檢視 Bash 中的預設快捷鍵，內容很多。例如 **alt-.** 迴圈地移向前一個參數，以及 **alt-*** 展開通配符。

- 你喜歡的話，可以鍵入`set -o vi` 來使用vi 風格的快捷鍵，而`set -o emacs` 可以把它改回來。

- 為了方便地鍵入長命令，在設定你的編輯器後（例如`export EDITOR=vim`），鍵入 **ctrl-x** **ctrl-e** 會開啟一個編輯器來編輯當前命令。在 vi 模式下則鍵入 **escape-v** 實現相同的功能。

- 鍵入 `history` 檢視命令列歷史記錄。其中有許多縮寫，例如`!$`（最後鍵入的參數）和`!!`（最後鍵入的命令），儘管通常被 **ctrl-r** 和 **alt-.** 取代。

- 回到上一個工作路徑：`cd -`

- 如果你輸入命令的時候改變了主意，按下 **alt-#** 來在行首新增`#`，或者依次按下 **ctrl-a**， **#**， **enter**。這樣做的話，之後你可以很方便的利用命令列歷史回到你剛才輸入到一半的命令。

- 使用 `xargs` （ 或 `parallel`），他們非常強大。注意到你可以控制每行參數的個數（`-L`）和最大並行數（`-P`）。如果你不確定它們是否會按你想的那樣工作，先使用`xargs echo` 檢視一下。此外，使用 `-I{}` 會很方便。例如：
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` 有助於展示程序樹。

- 使用`pgrep` 和`pkill` 根據名字查詢程序或傳送訊號（`-f` 參數通常有用）。

- 瞭解你可以發往程序的訊號的種類。比如，使用`kill -STOP [pid]` 停止一個程序。使用 `man 7 signal` 檢視詳細列表。

- 使用`nohup` 或`disown` 使一個後臺程序持續運行。

- 使用`netstat -lntp` 或`ss -plat` 檢查哪些程序在監聽埠（預設是檢查 TCP 埠; 使用參數`-u` 檢查 UDP 埠）。

- 有關開啟 socket 和檔案，請參閱`lsof`。

- 使用`uptime` 或`w` 來檢視系統已經運行多長時間。

- 使用`alias` 來創建常用命令的快捷形式。例如：`alias ll='ls -latr'` 使你可以方便地執行`ls -latr`命令。

- 在 Bash 指令碼中，使用`set -x` 去偵錯輸出，盡可能的使用嚴格模式，使用`set -e` 令指令碼在發生錯誤時退出而不是繼續運行，使用`set -u` 來檢查是否使用了未賦值的變數，使用`set -o pipefail` 嚴謹地對待錯誤（儘管問題可能很微妙）。當牽扯到很多指令碼時，使用 `trap`。一個好的習慣是在指令碼檔案開頭這樣寫，這會使它檢測一些錯誤，並在錯誤發生時中斷程式並輸出資訊：
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- 在 Bash 指令碼中，子 shell（使用括號`(...)`）是一種組織參數的便捷方式。一個常見的例子是臨時地移動工作路徑，程式碼如下：
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- 在 Bash 中，要注意其中有許多形式的擴展。檢查變數是否存在：`${name:?error message}`。例如，當 Bash 指令碼需要一個參數時，可以使用這樣的程式碼`input_file=${1:?usage: $0 input_file}`。數學表示式：`i=$(( (i + 1) % 5 ))`。序列：`{1..10}`。截斷字元串：`${var%suffix}` 和`${var#prefix}`。例如，假設`var=foo.pdf`，那麼`echo ${var%.pdf}.txt` 將輸出`foo.txt`。

- 使用括號擴展（`{`...`}`）來減少輸入相似文字，並自動化文字組合。這在某些情況下會很有用，例如`mv foo.{txt,pdf} some-dir`（同時移動兩個檔案），`cp somefile{,.bak}`（會被擴展成`cp somefile somefile .bak`）或者`mkdir -p test-{a,b,c}/subtest-{1,2,3}`（會被擴展成所有可能的組合，並創建一個目錄樹）。

- 通過使用`<(some command)` 可以將輸出視為檔案。例如，對比本地檔案`/etc/hosts` 和一個​​遠端檔案：
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- 瞭解 Bash 中的“here documents”，例如`cat <<EOF ...`。

- 在 Bash 中，同時重定向標準輸出和標準錯誤，`some-command >logfile 2>&1`。通常，為了保證命令不會在標準輸入裡殘留一個開啟了的檔案控制代碼導致你當前所在的終端無法操作，新增`</dev/null` 是一個好習慣。

- 使用`man ascii` 檢視具有十六進位制和十進位制值的ASCII表。 `man unicode`，`man utf-8`，以及`man latin1` 有助於你去了解通用的編碼資訊。

- 使用`screen` 或[`tmux`](https://tmux.github.io/) 來使用多個螢幕，當你在使用 ssh 時（儲存session 資訊）特別有用。另一個輕量級的解決方案是 `dtach`。

- ssh 中，瞭解如何使用`-L` 或`-D`（偶爾需要用`-R`）去開啟通道是非常有用的，例如當你需要從一臺遠端伺服器上訪問 web。

- 對 ssh 設定做一些小優化可能是很有用的，例如這個`​​~/.ssh/config` 檔案包含了防止特定環境下斷開連線、壓縮資料、多通道等選項：
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- 部分其他的關於 ssh 的選項是安全敏感且應當小心啟用的。例如在可信任的網路中：`StrictHostKeyChecking=no`，`ForwardAgent=yes`

- 考慮使用[`mosh`](https://mosh.mit.edu/) 作為 ssh 的替代品，它使用 UDP 協議。

- 獲取檔案的八進位制格式許可權，使用類似如下的程式碼：
```sh
      stat -c '%A %a %n' /etc/timezone
```

- 使用[`percol`](https://github.com/mooz/percol) 或者[`fzf`](https://github.com/junegunn/fzf) 可以互動式地從另一個命令輸出中選取值。

- 使用`fpp`（[PathPicker](https://github.com/facebook/PathPicker)）可以與基於另一個命令(例如`git`）輸出的檔案互動。

- 要基於當前目錄(以及子目錄)建立一個簡易的 web 伺服器給所處網路的所有使用者，可以使用：`python -m SimpleHTTPServer 7777` （使用埠 7777 和 Python 2）或`python -m http.server 7777` （使用埠 7777 和 Python 3）。

- 以某種許可權執行命令，使用`sudo`（root 許可權）或`sudo -u`（其他使用者）。使用`su`或者`sudo bash`來啟動一個以對應使用者許可權運行的shell。使用`su -`模擬其他使用者的登入。

## 檔案及資料處理

- 在當前路徑下通過檔名定位一個檔案，`find . -iname '*something*'`（或類似的）。在所有路徑下通過檔名查詢檔案，使用`locate something` （但請記住`updatedb` 可能沒有對最近新建的檔案建立索引）。

- 使用[`ag`](https://github.com/ggreer/the_silver_searcher) 在原始碼或資料檔案裡檢索（比`grep -r` 更好）。

- 將 HTML 轉為文字：`lynx -dump -stdin`

- Markdown，HTML，以及所有文件格式之間的轉換，試試[`pandoc`](http://pandoc.org/)。

- 如果你不得不處理 XML，`xmlstarlet` 寶刀未老。

- 使用[`jq`](http://stedolan.github.io/jq/) 處理 JSON。

- 使用[`shyaml`](https://github.com/0k/shyaml) 處理 YAML。

- Excel 或 CSV 檔案的處理，[csvkit](https://github.com/onyxfish/csvkit) 提供了`in2csv`，`csvcut`，`csvjoin`，`csvgrep` 等工具。

- 關於 Amazon S3，[`s3cmd`](https://github.com/s3tools/s3cmd) 很方便，而[`s4cmd`](https://github.com/bloomreach/s4cmd) 更快。 Amazon 官方的[`aws`](https://github.com/aws/aws-cli) 以及[`saws`](https://github.com/donnemartin/saws) 是其他 AWS 相關工作的基礎。

- 瞭解如何使用`sort` 和`uniq`，包括 uniq 的`-u` 參數和`-d` 參數，詳見後文單行指令碼節。另外可以瞭解一下 `comm`。

- 瞭解如何使用`cut`，`paste` 和`join` 來更改檔案。很多人都會使用`cut`，但幾乎都不會使用`join`。

- 瞭解如何運用`wc` 去計算新行數（`-l`），字元數（`-m`），單詞數（`-w`）以及位位元數（`-c`）。

- 瞭解如何使用`tee` 將標準輸入複製到檔案甚至標準輸出，例如`ls -al | tee file.txt`。

- 瞭解語言環境對許多命令列工具的微妙影響，包括排序的順序和效能。大多數 Linux 的安裝過程會將`LANG` 或其他有關的變數設定為符合本地的設定。意識到當你改變語言環境時，排序的結果可能會改變。明白國際化可能會使 sort 或其他命令運行效率下降*許多倍*。某些情況下（例如集合運算）你可以放心的使用`export LC_ALL=C` 來忽略掉國際化並使用基於位元組的順序。

- 瞭解`awk` 和`sed` 關於資料的簡單處理的用法。例如，將文字檔案中第三列的所有數字求和：`awk '{ x += $3 } END { print x }'`. 這可能比同等作用的 Python 程式碼快三倍且程式碼量少三倍。

- 替換一個或多個檔案中出現的字元：
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- 使用[`repren`](https://github.com/jlevy/repren) 來批次重新命名，或是在多個檔案中搜索替換。（有些時候`rename` 命令也可以批次重新命名，但要注意，它在不同 Linux 發行版中的功能並不完全一樣。）
```sh
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Recover backup files whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Same as above, using rename, if available:
      rename 's/\.bak$//' *.bak
```

- 根據 man 頁面的描述，`rsync` 真的是一個快速且非常靈​​活的檔案複製工具。它通常被用於機器間的同步，但在本地也同樣有用。它同時也是刪除大量檔案的[最快方法](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove -huge-number-of-files.html)之一：
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- 使用`shuf` 從一個檔案中隨機選取多行。

- 瞭解 `sort` 的參數。處理數字方面，使用`-n` 或者`-h` 來處理可讀性數字（例如`du -h` 的輸出）。明白鍵的工作原理（`-t` 和 `-k`）。例如，注意到你需要`-k1，1` 來按照第一個欄位來排序，而`-k1` 意味著按照整行排序。穩定排序（`sort -s`）在某些情況下很有用。例如，以第二個欄位為主關鍵字，第一個欄位為次關鍵字進行排序，你可以使用`sort -k1，1 | sort -s -k2，2`。

- 如果你想在 Bash 命令列中寫 tab 製表符，按下**ctrl-v** **[Tab]** 或鍵入`$'\t'` （後者可能更好，因為你可以複製貼上它）。

- 標準的原始碼對比及合併工具是`diff` 和`patch`。使用 `diffstat` 檢視變更總覽資料。注意到 `diff -r` 對整個資料夾有效。使用`diff -r tree1 tree2 | diffstat` 檢視變更總覽資料。

- 對於二進制檔案，使用`hd` 使其以十六進位制顯示以及使用`bvi` 來編輯二進位制。

- 同樣對於二進制檔案，`strings`（包括`grep` 等等）允許你查詢一些文字。

- 二進制檔案對比（Delta 壓縮），使用`xdelta3`。

- 轉換文字編碼可使用 `iconv` 或 `uconv`，後者支援 Unicode 相關的進階用法。例如：
```sh
      # 顯示十六進制碼或字元標準名稱（有益於除錯）
      uconv -f utf-8 -t utf-8 -x '::Any-Hex;' < input.txt
      uconv -f utf-8 -t utf-8 -x '::Any-Name;' < input.txt
      # 將文字轉換為小寫並移除所有重音標記（展開字元並移除標記）：
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC;' < input.txt > output.txt
```

- 拆分檔案，檢視`split`（按大小拆分）和`csplit`（按模式拆分）。

- 用[`dateutils`](http://www.fresse.org/dateutils/) 中的`dateadd`, `datediff`, `strptime` 等工具操作日期和時間表示式。

- 使用`zless`，`zmore`，`zcat` 和`zgrep` 對壓縮過的檔案進行操作。


## 系統偵錯

- `curl` 和`curl -I` 可以便捷地被應用於 web 偵錯，它們的好兄弟`wget` 也可以，或者是更潮的[`httpie`](https://github.com/jakubroztocil /httpie)。

- 使用`iostat`、`netstat`、`top` （`htop` 更佳）和`dstat` 去獲取硬碟、cpu 和網路的狀態。熟練掌握這些工具可以使你快速的對系統的當前狀態有一個大概的認識。

- 使用`netstat` 和`ss` 檢視網路連線的細節。

- 若要對系統有一個深度的總體認識，使用[`glances`](https://github.com/nicolargo/glances)。它在一個終端視窗中向你提供一些系統層級的資料。這對於快速的檢查各個子系統非常有幫助。

- 若要了解記憶體狀態，運行並理解`free` 和`vmstat` 的輸出。尤其注意 “cached” 的值，它指的是 Linux 核心用來作為檔案快取的記憶體大小，因此它與空閒記憶體無關。

- Java 系統偵錯則是一件截然不同的事，一個可以用於 Oracle 的 JVM 或其他 JVM 上的偵錯的技巧是你可以運行`kill -3 <pid>` 同時一個完整的棧軌跡和堆概述（包括 GC 的細節）會被儲存到標準輸出/日誌檔案。 JDK 中的`jps`，`jstat`，`jstack`，`jmap` 很有用。 [SJK tools](https://github.com/aragozin/jvm-tools) 更高階.

- 使用[`mtr`](http://www.bitwizard.nl/mtr/) ​​去跟蹤路由，用於確定網路問題。

- 用[`ncdu`](https://dev.yorhel.nl/ncdu) 來檢視磁碟使用情況，它比常用的命令，如`du -sh *`，更節省時間。

- 查詢正在使用頻寬的 socket 連線或程序，使用[`iftop`](http://www.ex-parrot.com/~pdw/iftop/) 或[`nethogs`](https://github.com/raboof/nethogs)。

- `ab` 工具（內建於Apache）可以簡單粗暴地檢查 web 伺服器的效能。對於更複雜的負載測試，使用`siege`。

- [`wireshark`](https://wireshark.org/)，[`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) 和[`ngrep`](http://ngrep.sourceforge.net/) 可用於復雜的網路偵錯。

- 瞭解 `strace` 和 `ltrace`。這倆工具在你的程式運行失敗、掛起甚至崩潰，而你卻不知道為什麼或你想對效能有個總體的認識的時候是非常有用的。注意 profile 參數（`-c`）和附加到一個運行的程序參數（`-p`）。

- 瞭解使用 `ldd` 來檢查共享庫。

- 瞭解如何運用`gdb` 連線到一個運行著的程序並獲取它的堆棧軌跡。

- 學會使用 `/proc`。它在偵錯正在出現的問題的時候有時會效果驚人。比如：`/proc/cpuinfo`，`/proc/meminfo`，`/proc/cmdline`，`/proc/xxx/cwd`，`/proc/xxx/exe`，`/proc/xxx/fd/` ，`/proc/xxx/smaps`（這裡的`xxx` 表示程序的 id 或 pid）。

- 當偵錯一些之前出現的問題的時候，[`sar`](http://sebastien.godard.pagesperso-orange.fr/) 非常有用。它展示了 cpu、記憶體以及網路等的歷史資料。

- 關於更深層次的系統分析以及效能分析，看看`stap`（[SystemTap](https://sourceware.org/systemtap/wiki)），[`perf`](http://en.wikipedia.org /wiki/Perf_(Linux))，以及[`sysdig`](https://github.com/draios/sysdig)。

- 檢視你當前使用的系統，使用`uname` ， `uname -a` （Unix／kernel 資訊） 或者`lsb_release -a` （Linux 發行版資訊）。

- 無論什麼東西工作得很歡樂時試試`dmesg`（可能是硬體或驅動問題）。


## 單行指令碼

一些命令組合的例子：

- 當你需要對文字檔案做集合交、並、差運算時，結合使用`sort`/`uniq` 很有幫助。假設 `a` 與 `b` 是兩內容不同的檔案。這種方式效率很高，並且在小檔案和上G的檔案上都能運用（`sort` 不被記憶體大小約束，儘管在`/tmp` 在一個小的根分區上時你可能需要`-T ` 參數），參閱前文中關於`LC_ALL` 和`sort` 的`-u` 參數的部分。
```sh
      cat a b | sort | uniq > c # c is a union b
      cat ab | sort | uniq -d > c # c is a intersect b
      cat abb | sort | uniq -u > c # c is set difference a - b
```

- 使用`grep . *`（每行都會附上檔名）或者`head -100 *`（每個檔案有一個標題）來閱讀檢查目錄下所有檔案的內容。這在檢查一個充滿配置檔案的目錄（如`/sys`、`/proc`、`/etc`）時特別好用。

- 計算文字檔案第三列中所有數的和（可能比同等作用的Python 程式碼快三倍且程式碼量少三倍）：
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- 如果你想在檔案樹上檢視大小/日期，這可能看起來像遞迴版的`ls -l` 但比`ls -lR` 更易於理解：
```sh
      find . -type f -ls
```

- 假設你有一個類似於 web 伺服器日誌檔案的文字檔案，並且一個確定的值只會出現在某些行上，假設一個`acct_id` 參數在URI中。如果你想計算出每個`acct_id` 值有多少次請求，使用如下程式碼：
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- 運行這個函數從這篇文件中隨機獲取一條技巧（解析 Markdown 檔案並抽取項目）：
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```


## 冷門但有用的指令

- `expr`：計算表示式或正規表示法

- `m4`：簡易的巨集處理器

- `yes`：列印多次字串

- `cal`：漂亮的日曆

- `env`：執行一個命令（指令碼中很有用）

- `printenv`：列印環境變數（偵錯時或在使用指令碼時很有用）

- `look`：查詢以特定字元串開頭的單詞

- `cut`、`paste` 和 `join`：資料操作

- `fmt`：格式化文字段落

- `pr`：將文字格式化成頁/列形式

- `fold`：包裹文字中的幾行

- `column`：將文字格式化成多列或表格

- `expand` 和`unexpand`：在 tab 與空格之間轉換

- `nl`：新增行號

- `seq`：列印數字

- `bc`：計算機

- `factor`：分解因數

- [`gpg`](https://gnupg.org/)：加密並針對檔案簽章

- `toe`：terminfo entries 列表

- `nc`：網路偵錯及資料傳輸

- `socat`：socket 代理，與 `netcat` 類似

- [`slurm`](https://github.com/mattthias/slurm)：網路流量視覺化

- `dd`：在檔案或裝置間傳輸資料

- `file`：確定檔案類型

- `tree`：以樹的形式顯示路徑和檔案，類似於遞迴的`ls`

- `stat`：檔案資訊

- `time`：執行命令，同時計算執行時間

- `lockfile`：使檔案只能通過`rm -f` 移除

- `logrotate`: 切換、壓縮以及傳送日誌檔案

- `watch`：重複運行同一個命令，展示結果並 highlight 有更改的部分

- `tac`：反向輸出文件

- `shuf`：檔案中隨機選取幾行

- `comm`：一行一行的比較排序過的檔案

- `pv`：監視通過 pipe 的資料

- `hd`，`hexdump`，`xxd`，`biew` 和`bvi`：儲存或編輯二進位檔案

- `strings`：從二進位檔案中抽取文字

- `tr`：轉換字母

- `iconv` 或 `uconv`：簡易的檔案編碼

- `split` 和 `csplit`：分割檔案

- `sponge`：在寫入前讀取所有輸入，在讀取檔案後再向同一檔案寫入時比較有用，例如`grep -v something some-file | sponge some-file`

- `units`：將一種計量單位轉換為另一種等效的計量單位（參閱`/usr/share/units/definitions.units`）

- `apg`：隨機生成密碼

- `7z`：高比例的檔案壓縮

- `ldd`：動態庫資訊

- `nm`：提取 obj 檔案中的符號

- `ab`：效能分析 web 伺服器

- `strace`：系統呼叫偵錯

- [`mtr`](http://www.bitwizard.nl/mtr/)：更好的網路偵錯跟蹤工具

- `cssh`：視覺化的並發 shell

- `rsync`：通過ssh 或本地檔案系統同步檔案和資料夾

- [`wireshark`](https://wireshark.org/) 和[`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html)：抓包和網路偵錯工具

- [`ngrep`](http://ngrep.sourceforge.net/)：網路層的 grep

- `host` 和 `dig`：DNS 查詢

- `lsof`：列出當前系統開啟檔案的工具以及檢視埠資訊

- `dstat`：系統狀態檢視

- [`glances`](https://github.com/nicolargo/glances)：高層次的多子系統總覽

- `iostat`：硬碟使用狀態

- `mpstat`: CPU 使用狀態

- `vmstat`: 記憶體使用狀態

- `htop`：top 的加強版

- `last`：登入記錄

- `w`：檢視處於登入狀態的使用者

- `id`：使用者/組 ID 資訊

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/)：系統歷史資料

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) 或[`nethogs`](https://github.com/raboof/nethogs)：套接字及程序的網路利用

- `ss`：socket 資料

- `dmesg`：引導及系統錯誤資訊

- `sysctl`: 在核心運行時動態地檢視和修改內核的運行參數

- `hdparm`：SATA/ATA 磁碟更改及效能分析

- `lsblk`：列出塊裝置資訊：以樹形展示你的磁碟以及磁碟分區資訊

- `lshw`，`lscpu`，`lspci`，`lsusb` 和`dmidecode`：檢視硬體資訊，包括CPU、BIOS、RAID、顯示卡、USB裝置等

- `lsmod` 和`modinfo`：列出核心模組，並顯示其細節

- `fortune`，`ddate` 和`sl`：額，這主要取決於你是否認為蒸汽火車和莫名其妙的名人名言是否“有用”

## 僅限 OS X 系統

以下是*僅限於* MacOS 系統的技巧

- 用`brew` （Homebrew）或者`port` （MacPorts）進行套件管理。這些可以用來在 Mac 系統上安裝以上的大多數命令。

- 用`pbcopy` 複製任何命令的輸出到桌面應用，用`pbpaste` 貼上輸入。

- 若要在 Mac OS 終端中將 Option 鍵視為 alt 鍵（例如在上面介紹的**alt-b**, **alt-f** 等命令中用到），開啟偏好設定-> 描述檔案-> 鍵盤並勾選“使用 Option 鍵作為 Meta 鍵”。

- 用`open` 或者`open -a /Applications/Whatever.app` 使用桌面應用開啟檔案。

- Spotlight： 用`mdfind` 搜尋檔案，用`mdls` 列出後設資料（例如照片的EXIF 資訊）。

- 注意 MacOS 系統是基於BSD UNIX 的，許多命令（例如`ps`，`ls`，`tail`，`awk`，`sed`）都和 Linux 中有些微的不同，這些指令主要是被 System V -style Unix 和 GNU 工具影響。你可以透過標題為"BSD General Commands Manual" 的 man 頁面發現這些不同。在有些情況下 GNU 版本的命令也可能被安裝（例如`gawk` 和`gsed` 對應GNU 中的awk 和sed ）。如果要寫跨平臺的 Bash 指令碼，避免使用這些命令（例如，考慮 Python 或者`perl` ）或者經過仔細的測試。

- 用 `sw_vers` 獲取 MacOS 的版本資訊。


## 僅限 Windows 系统

- 要在 Microsoft Windows 中使用 Unix shell，可以安装 [Cygwin](https://cygwin.com/)。本文件中介绍的大多數内容都將適用。

- 透過 Cygwin 的套件管理器來安裝額外的 Unix 指令。

- 使用 `mintty` 作為你的命令列視窗。

- 要訪問 Windows 剪貼簿，可以透過 `/dev/clipboard`。

- 執行 `cygstart` 以透過預設程式打開一個文件。

- 要訪問 Windows 登錄檔，可以使用 `regtool`。

- 注意 Windows 磁碟機路徑 `C:\` 在 Cygwin 中用 `/cygdrive/c` 代表，而 Cygwin 的 `/` 在 Windows 中顯示在 `C:\cygwin`。要轉換 Cygwin 和 Windows 風格的路徑可以用 `cygpath`。這在需要使用 Windows 指令的脚本裡很有用。

- 學會使用 `wmic`，你就可以從命令列執行大多數 Windows 系統管理任務，並編成腳本。

## 更多資源

- [awesome-shell](https://github.com/alebcay/awesome-shell)：一份精美的命令列工具及資源的列表。
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line)：一份針對 Mac OS 命令列的更深入的指南。
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/)：為了編寫更好的指令碼檔案。
- [shellcheck](https://github.com/koalaman/shellcheck)：一個靜態shell 指令碼分析工具，本質上是 bash／sh／zsh 的lint。
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html)：有關如何在 shell 腳本里正確處理檔名的細枝末節。


## 免責聲明

除去特別微小的任務，編寫程式碼是出於方便閱讀的目的。能力往往伴隨著責任。你 *可以* 在 Bash 中做一些事並不意味著你應該去做！ ;)


## 授權條款

[![創作共用License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

本文使用授權協議 [知識共享署名 - 相同方式共享 4.0 國際許可](http://creativecommons.org/licenses/by-sa/4.0/)。
