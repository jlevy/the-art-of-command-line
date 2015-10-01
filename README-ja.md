﻿[ Languages: [English](README.md), [Español](README-es.md), [한국어](README-ko.md), [Português](README-pt.md), [Русский](README-ru.md), [Slovenščina](README-sl.md), [中文](README-zh.md) ]

原文のコミット [bb0c38c0899339e836c37eead4a9534b06c56662](https://github.com/jlevy/the-art-of-command-line/blob/bb0c38c0899339e836c37eead4a9534b06c56662/README.md)

# The Art of Command Line

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [メタ情報](#meta)
- [基本](#basics)
- [日常的に使うもの](#everyday-use)
- [ファイルとデータの処理](#processing-files-and-data)
- [システムのデバッグ](#system-debugging)
- [ワンライナー](#one-liners)
- [目立たないが便利なもの](#obscure-but-useful)
- [さらなるリソース](#more-resources)
- [免責事項](#disclaimer)

![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/cowsay.png)

コマンドラインで流れるように操作ができるということは、軽く見られたり他人から理解されないスキルだとみなされることもあるでしょう。しかしそのスキルは、明らかにかすぐ分かるようかは問わず、エンジニアとしてのあなたの柔軟性や生産性を改善してくれるものです。ここでは、Linuxでコマンドラインを使う上で便利だと思ったメモやTipsの数々を挙げてみます。あるものは基礎的ですが、非常に詳しいもの、洗練されたもの、曖昧なものもあります。このページはそんなに長いものではないですが、ここに書いてあることの全てを使ったり思い出すことができれば、かなり詳しくなれるでしょう。

ここに書いてあることの多くは、[元々](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)[Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know)に[書かれて](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)いたものが多いですが、私よりももっと優れた人たちがすぐに改善案を出すことができるGithubに置くのがよいのではと思ったのです(訳注 : 原文はGithub上にあります)。間違いやもっとこうした方がよいという点があれば、イシューを登録するかプルリクエストをください！(もちろん、メタ情報の項や既存のプルリクエスト、イシューをまず確認してください)

## メタ情報

対象 :

- このガイドは、初心者向けでも経験者向きでもあります。幅広く(書いてあることは全て重要)、かつ明確で(多くのケースに対して具体的な例を付ける)、そして簡潔(他の場所で見つけられるような重要でないことや脱線したことは省く)であることをゴールにしています。各項目は、多くの場面において必須であるか、他の方法に比べて劇的に時間を節約してくれるでしょう。
- Linux向けに書いています。多くはMacOS(あるいはCygwin)でも使えますが、全部ではありません。
- インタラクティブなBashを使うことを想定していますが、多くの項目は他のシェルやBashのスクリプトでも使えるでしょう。

注意 :

- 1ページ内に収めるために、内容には暗黙的に書かれていることがあります。ここで取りかかりを知ったりコマンドが分かれば、詳細をどこかで調べたりするくらいはできるでしょう。新しいプログラムをインストールするには、`apt-get`/`yum`/`dnf`/`pacman`/`pip`/`brew`(どれか適したもの)を使いましょう。
- コマンドやオプション、パイプを分解して理解する手助けに、[Explainshell](http://explainshell.com/)を使おう。

## 基本

- 基本的なBashを学ぼう。実際のところ、`man bash`は結構簡単に理解できるしそんなに長くないので、これで一通りのことは分かる。それ以外のシェルもよいが、Bashは強力だし、常に使用可能であるという利点もある(自分のPCに入れてしまったと言ってzshやfishなど*だけ*を学んでしまうと、既存のサーバを触らなくてはならない時などに制約が出てしまう)。

- テキストエディタのどれか最低1つに習熟しよう。ターミナル内で適当にものを書くにあたって他に全く代替品がないという点で、理想的にはVim(`vi`)がよいだろう(通常はEmacsや高機能なIDEや最新のかっこいいエディタをメインに使っていたとしても)。

- `man`でのドキュメントの読み方を知ろう(知りたがりのために書くと、`man man`でセクション番号が分かる。例えば1は「一般的な」コマンド、5はファイルやそのお作法、8は管理についてといった具合)。`apropos`でmanページを探そう。コマンドによっては実行可能ファイルではなくBashのビルトインコマンドであることを理解し、`help`や`help -d`でヘルプが見られることを知ろう。

- `>`や`<`、`|`を使ったパイプによる入出力のリダイレクションを学ぼう。stdout(標準出力)とstderr(標準エラー出力)を学ぼう。

- `*`(または`?`や`{`...`}`)を使ったファイルグロブ展開、クォーテーション、ダブルクォート`"`とシングルクォート`'`の違いを学ぼう(詳しくはこの後の変数展開の項を参照)。

- `&`、**ctrl-z**、**ctrl-c**、`jobs`、`fg`、`bg`、`kill`など、Bashのジョブ管理について詳しくなろう。

- `ssh`について知るとともに、`ssh-agent`や`ssh-add`を使ったパスワードなしの認証の基本について理解しよう。

- ファイル管理について。`ls`や`ls -l`(特に、`ls -l`の各列が何を意味するか理解)、`less`、`head`、`tail`、`tail -f`(または`less +F`)、`ln`と`ln -s`(ハードリンクとソフトリンクの違いとそれぞれの利点の理解)、`chown`と`chmod`、`du`(ディスク使用量まとめを簡単に見るなら`du -sk *`)。ファイルシステム管理については、`df`、`mount`、`fdisk`、`mkfs`、`lsblk`。

- 基本的なネットワーク管理について。`ip`あるいは`ifconfig`、`dig`。

- 正規表現について詳しく知ろう。`grep`や`egrep`の色々なフラグも合わせて。`-i`、`-o`、`-A`、`-B`といったオプションは知っておいて損はない。

- `apt-get`、`yum`、`dnf`、`pacman`(ディストリビューションによって違う)といったコマンドでパッケージを探したりインストールする方法を学ぼう。Pythonベースのコマンドラインツールをインストールするのに、`pip`も必要だ(後に出てくるいくつかのコマンドは`pip`でインストールするのが一番簡単)。


## 日常的に使うもの

- Bashでは、引数を補完するのに**タブ**を使い、コマンド履歴から検索するのに**ctrl-r**を使う。

- Bashでは、最後の単語を削除するのには**ctrl-w**、行頭まで全て削除するには**ctrl-u**を使う。単語ごとに移動するには**alt-b**または**alt-f**、行末まで削除するには**ctrl-k**、画面のクリアは**ctrl-l**。Bashにおけるデフォルトのキー割り当てを全て見るには``man readline`を参照。たくさん出てくる。例えば、**alt-.**は前の引数を順番に表示し、**alt-***はグロブを展開する。

- vi風のキー割り当てが好きなら、`set -o vi`を実行しよう。

- 最近実行したコマンドを確認するなら`history`。**ctrl-r**や**alt-.**で用は足りるだろうが、`!$`(直前の引数)や`!!`(直前のコマンド)といった省略形もたくさんある。

- 前のワーキングディレクトリに戻るなら`cd -`

- 途中までコマンドを入力したけれど心変わりした時は、**alt-#**を打つと行頭に`#`が挿入され、コメントとして入力される(**ctrl-a**、**#**、**enter**でも同じ)。これは後でコマンド履歴から検索できる。

- `xargs`(または`parallel`)を使おう。非常に強力。行ごとにいくつのアイテムを実行するか(`-L`)や、並列度(`-P`)も制御できる。正しく実行されるか定かでないなら、まず`xargs echo`してみればよい。`-I{}`も便利。例えば以下の通り。

 ```bash
    find . -name '*.py' | xargs grep some_function
    cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p`はプロセスツリーを表示するのに便利。

- `pgrep`や`pkill`で、プロセス名で検索したりシグナルを送れる(`-f`も便利)。

- プロセスに遅れる色々なシグナルを知っておこう。例えば、プロセスをサスペンドするには`kill -STOP [pid]`を使う。全種類見るなら、`man 7 signal`。

- バックグラウンドプロセスをずっと実行し続けたいなら`nohup`あるいは`disown`を使おう。

- `netstat -lntp`や`ss -plat`で、どんなプロセスがリッスンしているか確認しよう(UDPなら`-u`を付ける)。

- 開かれているソケットやファイルを見るには`lsof`も参照。

- Bashスクリプトでは、`set -x`でデバッグ出力を出せる。可能なら厳格モードを使い、エラーが起きたら強制終了するよう`set -e`する。パイプのエラーも厳格に扱うために`set -o pipefail`も使おう(これはちょっと微妙かも)。より複雑なスクリプトなら、`trap`も使おう。

- Bashスクリプトでは、コマンドのグループを作るのにサブシェル(丸括弧で囲まれた部分)が便利。一時的にワーキングディレクトリを移動するというよくある例。

```bash
      # カレントディレクトリで何か実行
      (cd /some/other/dir && other-command)
      # 元のディレクトリで作業続行
```

- Bashでは、たくさんの変数展開の種類があることを覚えておこう。変数が存在するかチェックするなら、`${name:?error message}`。例えば、Bashスクリプトが1つの引数を取る必要があるなら、`input_file=${1:?usage: $0 input_file}`とだけ書けばよい。算術式の展開は、`i=$(( (i + 1) % 5 ))`。シーケンスは`{1..10}`。文字列のトリミングは`${var%suffix}`と`${var#prefix}`。例えば`var=foo.pdf`の時、`echo ${var%.pdf}.txt`とすると`foo.txt`が出力に。

- コマンドの出力を`<(some command)`のようにしてファイルのように扱える。例えば、ローカルとリモートのの`/etc/hosts`を比較するなら以下のようになる。

```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- `cat <<EOF ...`のような、Bashの「ヒアドキュメント」を理解しよう。

- Bashでは、`some-command >logfile 2>&1`で標準出力と標準エラー出力の両方をリダイレクトできる。コマンドが標準入力に対してファイルハンドルを開きっぱなしにせず、ログインしているターミナルにひもづけておくため、`</dev/null`するのもよい習慣。

- 16進と10進のASCIIテーブルを見るのに`man ascii`を使おう。一般的なエンコードに関する情報は、`man unicode`や`man utf-8`、`man latin1`が便利。

- スクリーンの分割に`screen`や[`tmux`](https://tmux.github.io/)を使おう。特に、リモートのSSHセッションをデタッチしたりアタッチし直したりするのに有効。セッション永続化だけの簡単なものなら`dtach`。

- SSHで`-L`あるいは`-D`(まれに`-R`)を使ったポートトンネルのやり方を覚えておくと便利。例えばリモートのサーバからウェブサイトにアクセスする時など。

- SSHの設定を少しでも最適化しておくと便利。例えば以下の設定だと、ネットワーク環境による接続断を回避し、圧縮を使用し(帯域の細い回線を使ったscpなどで便利)、ローカルの制御ファイルを指定して同一サーバとのチャネルを多重化する。

```
       TCPKeepAlive=yes
       ServerAliveInterval=15
       ServerAliveCountMax=6
       Compression=yes
       ControlMaster auto
       ControlPath /tmp/%r@%h:%p
       ControlPersist yes
```

- これ以外のSSHオプションはセキュリティ上の問題がある可能性があるため、有効にするには、サブネットごとやホストごとに指定したり、信頼できるネットワーク内でのみ使用するなど注意が必要。`StrictHostKeyChecking=no`、`ForwardAgent=yes`など。

- 8進数表現のファイルパーミッションは、システム設定の際に便利だが`ls`の結果にも出てこず、間違いやすい。以下のようにして取得できる。

```sh
      stat -c '%A %a %n' /etc/timezone
```

- 何らかのコマンドの出力から、インタラクティブに値を選択したい場合は、 [`percol`](https://github.com/mooz/percol)を使おう。

- (gitを使うなど)何らかのコマンドの出力からファイルに関するやり取りをする場合は、`fpp` ([PathPicker](https://github.com/facebook/PathPicker))を使おう。

- カレントディレクトリ(とサブディレクトリ)全体を、ネットワーク内に公開されたWebサーバにするなら、`python -m SimpleHTTPServer 7777` (ポート7777で公開。Python 2の場合)あるいは`python -m http.server 7777` (Python 3の場合)。

## ファイルとデータの処理

- カレントディレクトリ以下のファイルをファイル名で探したいなら、`find . -iname '*something*'`。場所を指定せずにファイル名で検索したいなら、`locate something`をつかおう(ただし`updatedb`は最近作られたファイルはインデックスしていないであろうことに注意)。

- ソースやデータファイルの(`grep -r`よりも高度な)一般的な検索には、[`ag`](https://github.com/ggreer/the_silver_searcher)を使おう。

- HTMLをテキストに変換するなら、`lynx -dump -stdin`。

- MarkdownやHTMLなど様々な種類のドキュメントの変換には、[`pandoc`](http://pandoc.org/)を試してみるとよい。

- XMLを扱わなくてはならないなら、`xmlstartlet`は古いがいいツールだ。

- JSONには`jq`を使おう。

- ExcelやCSVファイルには、[csvkit](https://github.com/onyxfish/csvkit)で`in2csv`、`csvcut`、`csvjoin`、`csvgrep`などが使えるようになる。

- Amazon S3には、[`s3cmd`](https://github.com/s3tools/s3cmd)が便利で、[`s4cmd`](https://github.com/bloomreach/s4cmd)はさらに高速。AWS関連の処理にはAmazon公式の[`aws`](https://github.com/aws/aws-cli)が欠かせない。

- `sort`や`uniq`、さらにuniqの`-u`や`-d`オプションを知っておこう。後に出てくるワンライナーも参照。`comm`も確認しておこう。

- 複数のテキストファイルを操作するのには、`cut`と`paste`、`join`は知っておこう。`cut`はみんな使っているが、`join`は忘れられている。

- `wc`を理解し、改行(`-l`)、文字(`-m`)、単語(`-w`)、バイト(`-c`)それぞれの数え方も知っておこう。

- 標準入力をファイルと標準出力の両方に出す`tee`を理解しよう。`ls -al | tee file.txt`のように使う。

- ロケールは、ソートの順序(照合順序)やパフォーマンスなど、たくさんのコマンドラインツールに微妙なところで影響することを覚えておこう。多くのLinuxディストリビューションでは、`LANG`や他のロケール変数はUS Englishのようなローカルな設定になっている。ロケールを変更するとソート順序が変わることに注意しよう。また、国際化(i18n)対応のルーチンはソートやその他の処理を*何倍も*遅く実行するようになる点も知っておこう。場合(設定の処理や一意性を見つける処理など)によっては、`export LC_ALL=C`としてしまい遅いi18n対応の処理を完全に無視してしまうことも可能だ。

- 単純なデータ加工のために`awk`と`sed`の基礎を身につけよう。例えば、テキストファイルの3カラム目の合計を出すなら、`awk '{ x += $3 } END { print x }'`。これは、Pythonで同じことをやるより3倍速くかつ3分の1の長さで書ける。

- 1つあるいは複数のファイル内の文字列を直接置き換えてしまうには、

```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- パターンにしたがってたくさんのファイル名を書き換えるには`rename`を使おう。複雑なファイル名変更なら [`repren`](https://github.com/jlevy/repren)も便利だ。

```sh
      # バックアップファイルfoo.bakをfooに戻す
      rename 's/\.bak$//' *.bak
      # ファイル名、ディレクトリ名、ファイルの中身全てのfooをbarに置き換える
      repren --full --preserve-case --from foo --to bar .
```

- ファイルからランダムな行を抜き出すには`shuf`

- `sort`のオプションを理解しよう。キーがどのように処理されるのか(`-t`や`-k`)を知ろう。特に、最初の列だけでソートするには`-k1,1`とかく必要があり、`-k1`だと全行を見てソートされるという点に注意。

- stableな(安定した)ソート(`sort -s`)は便利。例えば、始めに1列目でソートし、それから2列目でソートするなら、`sort -k1,1 | sort -s -k2,2`とすればよい。

- Bashのコマンドライン上でタブを表現する必要がある場合、**ctrl-v** **[Tab]**を入力するか`$'\t'` (コピペするなら後者の方がいいかも)。

- ソースコードにパッチを当てる基本のツールは`diff`と`patch`。diffの統計情報を見るなら`diffstat`も参照しよう。`diff -r`だと、ディレクトリ全体に対して実行される。変更点の概要を見るなら`diff -r tree1 tree2 | diffstat`。

- バイナリファイルなら、単純な16進ダンプを見るのに`hd`、バイナリエディタには`bvi`。

- 同じくバイナリファイルに関して、テキストを抽出したいなら`strings`(と`grep`などの組み合わせ)。

- バイナリのdiff(デルタ圧縮)なら、`xdelta3`。

- テキストエンコーディングの変換は`iconv`を使おう。あるいはより高度なツールとして`uconv`もあり、こちらはUnicodeの高度な処理が可能。例えば以下のコマンドでは小文字に変換しアクセント記号を取り除く(展開してから削除)。

```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- ファイルを分割するなら`split`(サイズで分割)と`csplit`(パターンで分割)。

- 圧縮ファイルの操作は`zless`、`zmore`、`zcat`、`zgrep`。

## システムのデバッグ

- Webのデバッグなら`curl`や`curl -l`が便利で、`wget`も同様、よりモダンなのは[`httpie`](https://github.com/jakubroztocil/httpie)。

- ディスクやCPU、ネットワークのステータスを知るには`iostat`、`netstat`、`top`(あるいは`htop`の方がよい)、(一番は)`dstat`。システムで何が起きているのか素早く知るにはよい。

- 更に詳しいシステムの全体像を見るには、[`glances`](https://github.com/nicolargo/glances)を使おう。ひとつのターミナル内で、いくつかのシステムレベルの統計情報を表示してくれる。複数のサブシステムを素早くチェックするのに非常に便利。

- メモリのステータスを知るには、`free`あるいは`vmstat`を実行し、その出力の意味を理解しよう。特に、"cached"の値はLinuxカーネルにファイルキャッシュとして保持されているメモリ量であり、"free"の値を見る際に考慮すべきであることに注意しよう。

- Javaのシステムのデバッグはまた違う困ったところがあるが、Oracleあるいは他のJVMにも共通しているシンプルなトリックは、`kill -3 <pid>`でフルスタックトレースとヒープの概要が標準出力あるいはログにダンプされる(世代別GCの詳細も参考程度だが含まれている)。

- 改良版tracerouteとして`mtr`を使ってネットワークの問題を調査しよう。

- ディスクがいっぱいになっている理由を調べるには、`ncdu`を使うと`du -sh *`より時間が節約できる。

- 帯域を使っているのがどのソケットやプロセスなのかを見つけるには、`iftop`あるいは`nethogs`を試そう。

- `ab`(Apacheに付属)は、Webサーバのパフォーマンスをざっくりチェックするのに便利。より複雑なテストには`siege`を試そう。

- より確実なネットワークのデバッグは`wireshark`、`tshark`、`ngrep`。

- `strace`と`ltrace`について知っておこう。プログラムの実行に失敗したりハングしたりクラッシュしたりして、その理由が分からない、あるいはパフォーマンスに関する一般的情報を知りたいなら、このツールが役立つはずだ。プロファイリングのオプション(`-c`)や起動中のプロセスにアタッチする機能(`-p`)も覚えておこう。

- 共有ライブラリをチェックするなら`ldd`を覚えておこう。

- 起動中のプロセスに`gdb`で接続し、そのスタックトレースを取る方法を知ろう。

- `/proc`以下のファイルを使おう。今起こっている問題をデバッグするのには素晴らしく便利だ。例えば、`/proc/cpuinfo`、`/proc/xxx/cwd`、`/proc/xxx/ece`、`/proc/xxx/fd/`、`/proc/xxx/smaps`。

- 過去に何か問題が起きたことの原因を探るなら、`sar`がとても便利。CPUやメモリ、ネットワークなどの過去の統計情報を見られる。

- さらに深いシステムとパフォーマンスの分析には、`stap` ([SystemTap](https://sourceware.org/systemtap/wiki))、[`perf`](http://en.wikipedia.org/wiki/Perf_(Linux))、
[`sysdig`](https://github.com/draios/sysdig)。

- どのディストリビューションを使っているか確認しよう。多くのディストリビューションでは`lsb_release -a`

- 何かいつもと違うおかしなこと(大抵ハードウェアかドライバ関連の問題だ)が起きていたら、`dmesg`を実行しよう。

## ワンライナー

コマンドをまとめて使う例をいくつか。

- `sort`や`uniq`を使ってテキストファイルの共通部分、結合、差異を求める時に特に便利なのが以下のやり方。`a`と`b`はそれぞれ内容に重複のないテキストファイルとする。この方法は高速で、数GB程度までの任意のファイルサイズで動作する(`/tmp`が小さなルートパーティションにある場合は`-T`オプションをつける必要があるが、ソートはメモリ内で行われるとは限らない)。上述の`LC_ALL`と`sort`の`-u`オプションも参照のこと。

```sh
      cat a b | sort | uniq > c   # cはaとbの和集合
      cat a b | sort | uniq -d > c   # cはaとbの共通部分
      cat a b b | sort | uniq -u > c   # cはaとbの差異
```

- コンフィグが含まれている`/sys`や`/proc`や`/etc/`のようなディレクトリ内の全てのファイルの中身全部を確認するには`grep . *`を使おう。

- テキストファイルの3列目を全て足し合わせるには以下で(Pythonで同じことをやるに比べて3倍速く3分の1の長さで書ける)。

```sh
      awk '{ x += $3 } END { print x }' myfile
```

- ファイルツリーのサイズやデータを確認したいなら、以下は再帰的な`ls -l`と同じだが`ls -lR`より見やすい。

```sh
      find . -type f -ls
```

- 事情が許すなら`xargs`や`parallel`を使おう。行あたりいくつのアイテムを実行するか(`-L`)や並列度(`-P`)は制御できるのにも注意。正しく使えているか心配な時には、xargs echoをまずやってみよう。また、`-I{}`も便利だ。以下の例をみてみよう。

```sh
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- Webサーバのログのようなテキストファイルがあり、各行には例えばURLの中に出てくる`acct_id`のような特定の値が現れるとしよう。`acct_id`が何回リクエストされているかを集計するには、

```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- このドキュメントからランダムに項目を抜き出すには以下の関数を実行しよう(Markdownをパースし、アイテムを抽出する)。

```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```

## 目立たないが便利なもの

- `expr`: 算術演算、論理演算、または正規表現の評価を実行

- `m4`: シンプルなマクロプロセッサ

- `yes`: 文字列をたくさん表示

- `cal`: いい感じのカレンダー

- `env`: コマンドを実行(スクリプト内で重宝する)

- `printenv`: 環境変数を表示する(デバッグやスクリプト内での使用に便利)

- `look`: 文字列で始まる英単語(またはファイル内の行)を見つける

- `cut `、  `paste`、 `join`: データの操作

- `fmt`: テキストの段落をフォーマットする

- `pr`: テキストをページとカラムにフォーマットする

- `fold`: テキストの行を分割

- `column`: テキストをカラムあるいはテーブルにフォーマット

- `expand` と `unexpand`: タブとスペースの相互変換

- `nl`: 行数を表示

- `seq`: 数字を表示

- `bc`: 計算機

- `factor`: 整数を因数分解

- `gpg`: 暗号化とファイルのサイニング

- `toe`: terminfoのエントリのテーブルを表示

- `nc`: ネットワークのデバッグとデータ転送

- `socat`: ソケットリレーとTCPポートのフォワーダ(`netcat`と同等)

- `slurm`: ネットワークトラフィックの可視化

- `dd`: データをファイルあるいはデバイス間で移動

- `file`: ファイルの種類を特定

- `tree`: ディレクトリとサブディレクトリをツリーで表示。`ls`に似ているが再帰的に動く

- `stat`: ファイルの情報

- `tac`: ファイルを逆から表示

- `shuf`: ファイルからランダムに選んだ行を表示

- `comm`: ソート済みファイルの行を比較

- `pv`: パイプ経由でデータの進行状況をモニタリング

- `hd` および `bvi`: バイナリファイルのダンプと編集

- `strings`: バイナリファイルからテキストを抽出

- `tr`: 文字の置き換えと操作

- `iconv` あるいは `uconv`: 文字エンコーディングの変換

- `split ` と `csplit`: ファイルを分割

- `units`: 単位の変換と計算。2週間あたりのハロン(訳注 : 長さの単位)からまばたきごとのトゥウィップまで( `/usr/share/units/definitions.units`も参照のこと)

- `7z`: 圧縮率の高いファイル圧縮

- `ldd`: 動的ライブラリの情報

- `nm`: オブジェクトファイルからシンボルを表示

- `ab`: Webサーバのベンチーマーク

- `strace`: システムコールのデバッグ

- `mtr`: ネットワークデバッグのためのより高機能なtraceroute

- `cssh`: ビジュアルな並列シェル

- `rsync`: ファイルやフォルダをSSH経由で同期

- `wireshark` と `tshark`: パケットキャプチャとネットワークデバッギング

- `ngrep`: ネットワーク層のgrep

- `host` と `dig`: DNS名前解決

- `lsof`:プロセスのファイルディスクリプタとソケット情報

- `dstat`: 便利なシステム情報

- [`glances`](https://github.com/nicolargo/glances): 高レベルに複数のサブシステムの概要を把握

- `iostat`: CPUとディスクの使用状況

- `htop`: topの改良版

- `last`: ログイン履歴

- `w`: 誰がログインしているか

- `id`: ユーザやグループの情報

- `sar`: システム統計情報の履歴

- `iftop` または `nethogs`: ソケットあるいはプロセスごとのネットワーク使用量

- `ss`: ソケットの統計情報

- `dmesg`: 起動時とシステムのエラーメッセージ

- `hdparm`: SATA/ATAディスクの操作やパフォーマンス確認

- `lsb_release`: Linuxディストリビューション情報

- `lsblk`: ブロックデバイスの一覧。ディスクとディスクパーティションのツリービュー

- `lshw` と `lspci`: RAIDやグラフィックなどを含めたハードウェア情報

- `fortune`、 `ddate`、`sl`: んー、あー、これは蒸気機関車やZippyの引用句が「便利」だと思うかどうかによる

## さらなるリソース

- [awesome-shell](https://github.com/alebcay/awesome-shell): シェルのツールやリソースのまとめ
- よりよいシェルスクリプトを書くには[Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/)

## 免責事項

ごく一部の例外はありますが、コードは誰でも読めるように書かれています。力には責任が伴います。Bashで*できる*からといって、そうすべき必要があるという意味ではありません！ ;)

## ライセンス

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/) 

このドキュメントは[Creative Commons Attribution-ShareAlike 4.0 International Licene](http://creativecommons.org/licenses/by-sa/4.0/)でライセンスされます。
