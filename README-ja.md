🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*

# The Art of Command Line

[![質問してみよう](https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg)](https://airtable.com/shrzMhx00YiIVAWJg)

[![https://gitter.im/jlevy/the-art-of-command-lineでチャットに参加しよう](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [メタ情報](#メタ情報)
- [基本](#基本)
- [日常的に使うもの](#日常的に使うもの)
- [ファイルとデータの処理](#ファイルとデータの処理)
- [システムのデバッグ](#システムのデバッグ)
- [ワンライナー](#ワンライナー)
- [目立たないが便利なもの](#目立たないが便利なもの)
- [OS X用のもの](#os-x用のもの)
- [Windows専用](#windows専用)
- [さらなるリソース](#さらなるリソース)
- [免責事項](#免責事項)

![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

コマンドラインで流れるように操作ができるということは、軽く見られたり他人から理解されないスキルだとみなされることもあるだろう。しかしそのスキルは、明らかにかすぐ分かるようかは問わず、エンジニアとしてのあなたの柔軟性や生産性を改善してくれるものだ。ここでは、Linuxでコマンドラインを使う上で便利だと思ったメモやTipsの数々を挙げてみる。あるものは基礎的だが、非常に詳しいもの、洗練されたもの、曖昧なものもある。このページはそんなに長いものではないが、ここに書いてあることの全てを使ったり思い出すことができれば、かなり詳しくなれるだろう。

このドキュメントは[多くの執筆者と翻訳者](AUTHORS.md)による成果である。
ここに書いてあることの多くは、[元々](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)[Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know)に[書かれて](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)いたものが多いが、より優れた人たちがすぐに改善案を出すことができるGitHubに置くのがよいのではと思った。
コマンドラインについて疑問があるなら[**質問してみよう**](https://airtable.com/shrzMhx00YiIVAWJg) エラーや改善点を見つけたら[**貢献してみよう**](/CONTRIBUTING.md)!

## メタ情報

対象 :

- このガイドは、初心者向けでも経験者向きでもある。幅広く(書いてあることは全て重要)、かつ明確で(多くのケースに対して具体的な例を付ける)、そして簡潔(他の場所で見つけられるような重要でないことや脱線したことは省く)であることをゴールにしている。各項目は、多くの場面において必須であるか、他の方法に比べて劇的に時間を節約してくれるだろう。
- [OS X用のもの](#os-x-only)を除き、Linux向けの内容となっており、その多くは各種LinuxおよびMacOS(あるいはCygwin)でも使えるだろう。
- インタラクティブなBashを使うことを想定しているが、多くの項目は他のシェルやBashのスクリプトでも使えるだろう。
- (このリポジトリへ)組み込むメリットがあるのであれば、標準Unixコマンドやパッケージインストールコマンドも含める。

注意 :

- 1ページ内に収めるために、内容には暗黙的に書かれていることがある。ここで取りかかりを知ったりコマンドが分かれば、詳細をどこかで調べたりするくらいはできるだろう。新しいプログラムをインストールするには、`apt-get`、`yum`、`dnf`、`pacman`、`pip`、`brew`(どれか適したもの)を使おう。
- コマンドやオプション、パイプを分解して理解する手助けに、[Explainshell](http://explainshell.com/)を使おう。

## 基本

- 基本的なBashを学ぼう。実際のところ、`man bash`は結構簡単に理解できるしそんなに長くないので、これで一通りのことは分かる。それ以外のシェルもよいが、Bashは強力だし、常に使用可能であるという利点もある(自分のPCに入れてしまったと言ってzshやfishなど*だけ*を学んでしまうと、既存のサーバを触らなくてはならない時などに制約が出てしまう)。

- テキストエディタのどれか最低1つに習熟しよう。`nano`エディタは編集の基本操作(開く、修正する、保存する、検索する)を学ぶ最もシンプルな方法のひとつだ。ターミナル内で適当にものを書くにあたって他に全く代替品がないという点で、理想的にはVim(`vi`)がよいだろう(通常はEmacsや高機能なIDEや最新のかっこいいエディタをメインに使っていたとしても)。

- `man`でのドキュメントの読み方を知ろう(知りたがりのために書くと、`man man`でセクション番号が分かる。例えば1は「一般的な」コマンド、5はファイルやそのお作法、8は管理についてといった具合)。`apropos`でmanページを探そう。コマンドによっては実行可能ファイルではなくBashのビルトインコマンドであることを理解し、`help`や`help -d`でヘルプが見られることを知ろう。

- `>`や`<`、`|`を使ったパイプによる入出力のリダイレクションを学ぼう。`>`は出力ファイルを上書き、`>>`は追記となる。stdout(標準出力)とstderr(標準エラー出力)を学ぼう。

- `*`(または`?`や`[`...`]`)を使ったファイルグロブ展開、クォーテーション、ダブルクォート`"`とシングルクォート`'`の違いを学ぼう(詳しくはこの後の変数展開の項を参照)。

- `&`、**ctrl-z**、**ctrl-c**、`jobs`、`fg`、`bg`、`kill`など、Bashのジョブ管理について詳しくなろう。

- `ssh`について知るとともに、`ssh-agent`や`ssh-add`を使ったパスワードなしの認証の基本について理解しよう。

- ファイル管理について。`ls`や`ls -l`(特に、`ls -l`の各列が何を意味するか理解)、`less`、`head`、`tail`、`tail -f`(または`less +F`)、`ln`と`ln -s`(ハードリンクとソフトリンクの違いとそれぞれの利点の理解)、`chown`と`chmod`、`du`(ディスク使用量まとめを簡単に見るなら`du -hs *`)。ファイルシステム管理については、`df`、`mount`、`fdisk`、`mkfs`、`lsblk`。inodeについては、`ls -i`(または `df -i`)。

- 基本的なネットワーク管理について。`ip`あるいは`ifconfig`、`dig`、`traceroute`、 `route`。

-  `git`のようなバージョン管理システムを学んで使ってみよう。

- 正規表現について詳しく知ろう。`grep`や`egrep`の色々なフラグも合わせて。`-i`、`-o`、`-v`、`-A`、`-B`、`-C`といったオプションは知っておいて損はない。

- `apt-get`、`yum`、`dnf`、`pacman`(ディストリビューションによって違う)といったコマンドでパッケージを探したりインストールする方法を学ぼう。Pythonベースのコマンドラインツールをインストールするのに、`pip`も必要だ(後に出てくるいくつかのコマンドは`pip`でインストールするのが一番簡単)。


## 日常的に使うもの

- Bashでは、引数を補完、または利用可能なコマンドを列挙するのに**タブ**を使い、コマンド履歴から検索するのに**ctrl-r**を使う。(検索キーを入力した後、**ctrl-r**を繰り返し入力することで次から次へと検索結果を送ることができる。**Enter**で見つかったコマンドの実行となり、**Enter**ではなく右カーソルキーを押した場合は見つかったコマンドが入力された状態になる。)

- Bashでは、最後の単語を削除するのには**ctrl-w**、行頭まで全て削除するには**ctrl-u**を使う。単語ごとに移動するには**alt-b**または**alt-f**、行頭に移動するには**ctrl-a**、行末に移動するには**ctrl-e**、行末まで削除するには**ctrl-k**、画面のクリアは**ctrl-l**である。Bashにおけるデフォルトのキー割り当てを全て見るには`man readline`を参照。たくさん出てくる。例えば、**alt-.**は前の引数を順番に表示し、**alt-***はグロブを展開する。

- vi風のキー割り当てが好きなら、`set -o vi`を実行しよう。(元に戻したいときは`set -o emacs`)

- 長いコマンドを編集するときに、エディタを設定した後で(例えば`export EDITOR=vim`)、**ctrl-x** **ctrl-e**によって編集中のコマンドが複数行の編集のために指定したエディタで開かれる。vi風の場合は、**escape-v**。

- 最近実行したコマンドを確認するなら`history`。`!n`と続けることで(nはコマンド横に表示される数字)再度実行できる。**ctrl-r**や**alt-.**で用は足りるだろうが、`!$`(直前の引数)や`!!`(直前のコマンド)といった省略形もたくさんある。

- `cd`でホームディレクトリへの移動。ホームディレクトリに関連するファイルにアクセスする場合はプレフィックス`~`をつける(例: `~/.bashrc`)。`sh`スクリプトの中では`$HOME`でホームディレクトリを表すことができる。

- 前のワーキングディレクトリに戻るなら`cd -`

- 途中までコマンドを入力したけれど心変わりした時は、**alt-#**を打つと行頭に`#`が挿入され、コメントとして入力される(**ctrl-a**、**#**、**enter**でも同じ)。これは後でコマンド履歴から検索できる。

- `xargs`(または`parallel`)を使おう。非常に強力。行ごとにいくつのアイテムを実行するか(`-L`)や、並列度(`-P`)も制御できる。正しく実行されるか定かでないなら、まず`xargs echo`してみればよい。`-I{}`も便利。例えば以下の通り。

 ```bash
    find . -name '*.py' | xargs grep some_function
    cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p`はプロセスツリーを表示するのに便利。

- `pgrep`や`pkill`で、プロセス名で検索したりシグナルを送れる(`-f`も便利)。

- プロセスに送れる色々なシグナルを知っておこう。例えば、プロセスをサスペンドするには`kill -STOP [pid]`を使う。全種類見るなら、`man 7 signal`。

- バックグラウンドプロセスをずっと実行し続けたいなら`nohup`あるいは`disown`を使おう。

- `netstat -lntp`や`ss -plat`で、どんなプロセスがリッスンしているか確認しよう(UDPなら`-u`を付ける)。

- 開かれているソケットやファイルを見るには`lsof`も参照。

- `uptime`や`w`によってシステムの稼働時間を調べられる。

- `alias`によってよく利用するコマンドのエイリアス(ショートカット)を作成できる。例えば、`alias ll='ls -latr'`では新しいエイリアスである`ll`が作成される.

- よく使うエイリアス、シェル設定、機能を`~/.bashrc`に保存し、[ログインシェルに反映しよう](http://superuser.com/a/183980/7106)。これで全てのセッションであなたの設定が利用できる。

- ログイン時に実行されてほしいコマンド、環境変数を`~/.bash_profile`に記載する。画面からのログインや`cron`ジョブで起動されるシェルには別の設定が必要だ。

- Gitで様々なマシンの設定ファイル(例:`.bashrc`や`.bash_profile`)を同期させよう。

- 空白を含む変数やファイル名には注意が必要だ。Bash変数にはクオートをつけよう、こんな風に`"$FOO"`。
ファイル名の区切りとしてヌル文字を指定する場合には`-0`や`-print0`オプションを付与しよう。例:  `locate -0 pattern | xargs -0 ls -al` or `find / -print0 -type d | xargs -0 ls -al`。空白を含んだファイル名を繰り返し実行するためには、IFS=$'\n'`を使ってIFSを改行のみにしよう。

- Bashスクリプトでは、`set -x`でデバッグ出力を出せる(`set -v`は、実行されるコマンドや変数名やコメントなどをそのまま出力する)。特別な理由がない限り厳格モード(strict mode)を使い、`set -e`でエラー時(0以外の終了コード時)に強制終了するように。`set -u`によって未定義の変数の利用を検知、パイプのエラーも厳格に扱うために`set -o pipefail`も使おう(これはちょっと微妙かも)。より複雑なスクリプトなら、EXITまたはERRシグナルに対して`trap`も使おう。使う場面としては以下の場合のようにエラーを検知してメッセージを出力するとき:

```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- Bashスクリプトでは、コマンドのグループを作るのにサブシェル(丸括弧で囲まれた部分)が便利。一時的にワーキングディレクトリを移動するというよくある例。

```bash
      # カレントディレクトリで何か実行
      (cd /some/other/dir && other-command)
      # 元のディレクトリで作業続行
```

- Bashでは、たくさんの変数展開の種類があることを覚えておこう。変数が存在するかチェックするなら、`${name:?error message}`。例えば、Bashスクリプトが1つの引数を取る必要があるなら、`input_file=${1:?usage: $0 input_file}`とだけ書けばよい。算術式の展開は、`i=$(( (i + 1) % 5 ))`。シーケンスは`{1..10}`。文字列のトリミングは`${var%suffix}`と`${var#prefix}`。例えば`var=foo.pdf`の時、`echo ${var%.pdf}.txt`とすると`foo.txt`が出力に。

- `{`...`}`を使った中括弧展開によって、似たようなコマンドを複数回入力しなくて済む。例えば、 `mv foo.{txt,pdf} some-dir` (両方のファイルを移動させる), `cp somefile{,.bak}` (`cp somefile somefile.bak` と展開される)、`mkdir -p test-{a,b,c}/subtest-{1,2,3}` (すべての可能な組み合わせでディレクトリが作られる).

- 展開の順序は括弧→チルダ、パラメータや変数、計算機号、コマンド置換(左から右)→文字の分割→ファイル名の順だ。(例えば、{1..20}のような範囲は{$a..$b}というようには表現できない。`seq`や`for`ループを使ってこんな風に表すことができる。`seq $a $b or for((i=a; i<=b; i++)); do ... ; done`)

- コマンドの出力を`<(some command)`のようにしてファイルのように扱える。例えば、ローカルとリモートのの`/etc/hosts`を比較するなら以下のようになる。

```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- スクリプトを書く時は全てのコードを中括弧で囲まなくてはいけない。もし閉じ括弧が欠けていたらシンタックスエラーで実行が妨げられる。これはあなたがスクリプトをダウンロードしたときに判明する。（不完全なスクリプトの）実行によって部分的にwebからダウンロードしてしまうのを防ぐためだ。
```bash
{
      # Your code here
}
```

- 「ヒアドキュメント」によって、ファイルからの[複数行のリダイレクト](https://www.tldp.org/LDP/abs/html/here-docs.html)のように振る舞うことができる。
```
cat <<EOF
input
on multiple lines
EOF
```

- Bashでは、`some-command >logfile 2>&1`または`some-command &>logfile`で標準出力と標準エラー出力の両方をリダイレクトできる。コマンドが標準入力に対してファイルハンドルを開きっぱなしにせず、ログインしているターミナルにひもづけておくため、`</dev/null`するのもよい習慣。

- 16進と10進のASCIIテーブルを見るのに`man ascii`を使おう。一般的なエンコードに関する情報は、`man unicode`や`man utf-8`、`man latin1`が便利。

- スクリーンの分割に`screen`や[`tmux`](https://tmux.github.io/)を使おう。特に、リモートのSSHセッションをデタッチしたりアタッチし直したりするのに有効。`byobu`はscreenやtmuxの情報をより多く提供してくれ、管理が容易になる。セッション永続化だけの簡単なものなら`dtach`。

- SSHで`-L`あるいは`-D`(まれに`-R`)を使ったポートトンネルのやり方を覚えておくと便利。例えばリモートのサーバからウェブサイトにアクセスする時など。

- SSHの設定を少しでも最適化しておくと便利。例えば以下の`~/.ssh/config`の設定だと、ネットワーク環境による接続断を回避し、圧縮を使用し(帯域の細い回線を使ったscpなどで便利)、ローカルの制御ファイルを指定して同一サーバとのチャネルを多重化する。

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

- [`mosh`](https://mosh.mit.edu/)はUDPを使ったsshの代替で、(サーバー側での設定は必要であるが) 断続的な接続時に便利。

- 8進数表現のファイルパーミッションは、システム設定の際に便利だが`ls`の結果にも出てこず、間違いやすい。以下のようにして取得できる。

```sh
      stat -c '%A %a %n' /etc/timezone
```

- 何らかのコマンドの出力から、インタラクティブに値を選択したい場合は、 [`percol`](https://github.com/mooz/percol) または [`fzf`](https://github.com/junegunn/fzf)を使おう。

- (gitを使うなど)何らかのコマンドの出力からファイルに関するやり取りをする場合は、`fpp` ([PathPicker](https://github.com/facebook/PathPicker))を使おう。

- カレントディレクトリ(とサブディレクトリ)全体を、ネットワーク内に公開されたWebサーバにするなら、`python -m SimpleHTTPServer 7777` (ポート7777で公開。Python 2の場合)あるいは`python -m http.server 7777` (Python 3の場合)。

- 特権レベルでコマンドを実行するとき、rootでの実行には`sudo`、他のユーザの場合は`sudo -u`を利用。`su` または `sudo bash`で、シェルがそのユーザで起動する。`su -`でrootまたは他のユーザで新たにログインした状態がシミュレートされる。

- 異なるユーザーのシェルに移りたいと時は`su username`や`su - username`を使おう。"-"を用いることでまるで他のユーザーがログインしたかのように環境を得ることができる。スイッチ先のユーザーのパスワードを求められる。

- コマンドラインの[128K 制限](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong)について知ろう。この"Argument list too long"エラーはワイルドカードに大量のファイルがマッチしてしまったときに出る一般的なものだ。(もしこれが起きたら`find` や `xargs`が代替として助けになるだろう。)

- 基本的な計算(もちろんPythonの利用が一般的だ)には`python` interpreterを使おう。例えばこんな風に。
```
>>> 2+3
5
```

## ファイルとデータの処理

- カレントディレクトリ以下のファイルをファイル名で探したいなら、`find . -iname '*something*'`。場所を指定せずにファイル名で検索したいなら、`locate something`をつかおう(ただし`updatedb`は最近作られたファイルはインデックスしていないであろうことに注意)。

- ソースやデータファイルの(`grep -r`よりも高度な)一般的な検索には、[`ack`](https://github.com/beyondgrep/ack2)、[`ag`](https://github.com/ggreer/the_silver_searcher) ("the silver searcher")、そして[`rg`](https://github.com/BurntSushi/ripgrep) (ripgrep)を使おう。

- HTMLをテキストに変換するなら、`lynx -dump -stdin`。

- MarkdownやHTMLなど様々な種類のドキュメントの変換には、[`pandoc`](http://pandoc.org/)を試してみるとよい。

- XMLを扱わなくてはならないなら、`xmlstartlet`は古いがいいツールだ。

- JSONには[`jq`](http://stedolan.github.io/jq/)を使おう。

- YAMLには[`shyaml`](https://github.com/0k/shyaml)を。

- ExcelやCSVファイルには、[csvkit](https://github.com/onyxfish/csvkit)で`in2csv`、`csvcut`、`csvjoin`、`csvgrep`などが使えるようになる。

- Amazon S3には、[`s3cmd`](https://github.com/s3tools/s3cmd)が便利で、[`s4cmd`](https://github.com/bloomreach/s4cmd)はさらに高速。AWS関連の処理にはAmazon公式の[`aws`](https://github.com/aws/aws-cli)と改善版の[`saws`](https://github.com/donnemartin/saws)が欠かせない。

- `sort`や`uniq`、さらにuniqの`-u`や`-d`オプションを知っておこう。後に出てくるワンライナーも参照。`comm`も確認しておこう。

- 複数のテキストファイルを操作するのには、`cut`と`paste`、`join`は知っておこう。`cut`はみんな使っているが、`join`は忘れられている。

- `wc`を理解し、改行(`-l`)、文字(`-m`)、単語(`-w`)、バイト(`-c`)それぞれの数え方も知っておこう。

- 標準入力をファイルと標準出力の両方に出す`tee`を理解しよう。`ls -al | tee file.txt`のように使う。

- グルーピング、フィールドを入れ替える、統計的な計算といったもっと複雑な作業は[`datamash`](https://www.gnu.org/software/datamash/)の利用を検討しよう。

- ロケールは、ソートの順序(照合順序)やパフォーマンスなど、たくさんのコマンドラインツールに微妙なところで影響することを覚えておこう。多くのLinuxディストリビューションでは、`LANG`や他のロケール変数はUS Englishのようなローカルな設定になっている。ロケールを変更するとソート順序が変わることに注意しよう。また、国際化(i18n)対応のルーチンはソートやその他の処理を*何倍も*遅く実行するようになる点も知っておこう。場合(設定の処理や一意性を見つける処理など)によっては、`export LC_ALL=C`としてしまい遅いi18n対応の処理を完全に無視してしまうことも可能だ。

- `TZ=Pacific/Fiji date`のように起動時に変数を前につけることで、特定のコマンドの環境変数をセットすることができる。

- 単純なデータ加工のために`awk`と`sed`の基礎を身につけよう。[ワンライナー](#ワンライナー)を参照。

- 1つあるいは複数のファイル内の文字列を直接置き換えてしまうには、

```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- 複数のファイル名の変更やファイル内の検索や置換には、[`repren`](https://github.com/jlevy/repren)を使ってみよう。(場合によっては`rename`コマンドでも複数のファイル名変更ができるが、すべてのLinuxディストリビューションで挙動が同じであるわけではないので注意が必要。)

```sh
      # foo -> barへとファイル名、ディレクトリ名、ファイルの中身を変更する:
      repren --full --preserve-case --from foo --to bar .
      # バックアップファイルを元に戻す whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # 上記と同じものをrenameを使って:
      rename 's/\.bak$//' *.bak
```

- マニュアルページにあるように `rsync` は非常に高速で万能なファイルコピーの道具である。マシーン間のファイルを同期させることでよく知られているが、ローカルの場合でも同様に有用である。また、大量のファイルを削除する[高速な方法](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html)としても利用できる:

```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- 実行ファイルの進捗を監視したい場合、[`pv`](http://www.ivarch.com/programs/pv.shtml)、[`pycp`](https://github.com/dmerejkowsky/pycp)、 [`pmonitor`](https://github.com/dspinellis/pmonitor)、[`progress`](https://github.com/Xfennec/progress)や`rsync --progress`を使おう。ブロックレベルバックアップは`dd status=progress`だ。

- ファイルからランダムな行を抜き出すには`shuf`

- `sort`のオプションを理解しよう。数値に対しては`-n`を使い、人間にとって読みやすい形式の数値の場合(例えば、`du -h`の出力)は`-h`を使おう。キーがどのように処理されるのか(`-t`や`-k`)を知ろう。特に、最初の列だけでソートするには`-k1,1`と書く必要があり、`-k1`だと全行を見てソートされるという点に注意。

- stableな(安定した)ソート(`sort -s`)は便利。例えば、始めに1列目でソートし、それから2列目でソートするなら、`sort -k1,1 | sort -s -k2,2`とすればよい。

- Bashのコマンドライン上でタブを表現する必要がある場合、**ctrl-v** **[Tab]**を入力するか`$'\t'` (コピペするなら後者の方がいいかも)。

- ソースコードにパッチを当てる基本のツールは`diff`と`patch`。`diff`や横並びの`sdiff`の統計情報を見るなら`diffstat`も参照しよう。`diff -r`だと、ディレクトリ全体に対して実行される。変更点の概要を見るなら`diff -r tree1 tree2 | diffstat`。`vimdiff`ではファイルの比較と編集が可能。

- バイナリファイルなら、単純な16進ダンプを見るのに`hd`、バイナリエディタには`bvi`。

- 同じくバイナリファイルに関して、テキストを抽出したいなら`strings`(と`grep`などの組み合わせ)。

- バイナリのdiff(デルタ圧縮)なら、`xdelta3`。

- テキストエンコーディングの変換は`iconv`を使おう。あるいはより高度なツールとして`uconv`もあり、こちらはUnicodeの高度な処理が可能。例えば以下のコマンドでは小文字に変換しアクセント記号を取り除く(展開してから削除)。

```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- ファイルを分割するなら`split`(サイズで分割)と`csplit`(パターンで分割)。

- 日時について。現在日時を取得するには[ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)が助けになる。`date -u +"%Y-%m-%dT%H:%M:%SZ"` を使おう。(他のオプションは[こちら](https://stackoverflow.com/questions/7216358/date-command-on-os-x-doesnt-have-iso-8601-i-option) [problematic](https://unix.stackexchange.com/questions/164826/date-command-iso-8601-option))。日付や時間の表現を扱うには、[`dateutils`](http://www.fresse.org/dateutils/)にあるように、`dateadd`、 `datediff`、 `strptime` などを使いましょう。

- 圧縮ファイルの操作は`zless`、`zmore`、`zcat`、`zgrep`。

- `chattr`でファイル権限に代わる低階層のファイル属性情報をセットできる。例えば、意図しないファイル削除を防ぐフラグはこうやって立てる。`sudo chattr +i /critical/directory/or/file`

- ファイルの権限を保存、リストアするには`getfacl`と`setfacl`を使おう。例は
```sh
   getfacl -R /some/path > permissions.txt
   setfacl --restore=permissions.txt
```
- 空ファイルを素早く作るには`truncate`([sparse file](https://en.wikipedia.org/wiki/Sparse_file)を作成)、`fallocate`(ext4, xfs, btrfs とocfs2ファイルシステム)、`xfs_mkfile`(xfsprogs packageにあるほぼ全てのファイルシステム)、`mkfile` (Solaris、Mac OSといったUnix関連システム)

## システムのデバッグ

- Webのデバッグなら`curl`や`curl -l`が便利で、`wget`も同様、よりモダンなのは[`httpie`](https://github.com/jkbrzt/httpie)。

- CPUやディスクのステータスを知るには、標準的なツールは`top` (または、より良い`htop`)、 `iostat`、 `iotop`。`iostat -mxz 15`を使って、基本的なCPUの情報やパーティッション単位でのディスクの詳細情報やパフォーマンスについて調べましょう。

- ネットワークの状態の監視には、`netstat`や`ss`。

- 手早くシステムで何が起きているのかを調べるには、`dstat`が便利。より詳しく見るには、[`glances`](https://github.com/nicolargo/glances)。

- メモリのステータスを知るには、`free`あるいは`vmstat`を実行し、その出力の意味を理解しよう。特に、"cached"の値はLinuxカーネルにファイルキャッシュとして保持されているメモリ量であり、"free"の値を見る際に考慮すべきであることに注意しよう。

- Javaのシステムのデバッグはまた違う困ったところがあるが、Oracleあるいは他のJVMにも共通しているシンプルなトリックは、`kill -3 <pid>`でフルスタックトレースとヒープの概要が標準出力あるいはログにダンプされる(世代別GCの詳細も参考程度だが含まれている)。JDKの `jps`、 `jstat`、 `jstack`、 `jmap` も便利で、[SJK tools](https://github.com/aragozin/jvm-tools)はより高度なツールである。

- 改良版tracerouteとして[`mtr`](http://www.bitwizard.nl/mtr/)を使ってネットワークの問題を調査しよう。

- ディスクがいっぱいになっている理由を調べるには、[`ncdu`](https://dev.yorhel.nl/ncdu)を使うと`du -sh *`より時間が節約できる。

- 帯域を使っているのがどのソケットやプロセスなのかを見つけるには、[`iftop`](http://www.ex-parrot.com/~pdw/iftop/)あるいは[`nethogs`](https://github.com/raboof/nethogs)を試そう。

- `ab`(Apacheに付属)は、Webサーバのパフォーマンスをざっくりチェックするのに便利。より複雑なテストには`siege`を試そう。

- より確実なネットワークのデバッグは[`wireshark`](https://wireshark.org/)、[`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html)、[`ngrep`](http://ngrep.sourceforge.net/)。

- `strace`と`ltrace`について知っておこう。プログラムの実行に失敗したりハングしたりクラッシュしたりして、その理由が分からない、あるいはパフォーマンスに関する一般的情報を知りたいなら、このツールが役立つはずだ。プロファイリングのオプション(`-c`)や起動中のプロセスにアタッチする機能(`-p`)も覚えておこう。

- 共有ライブラリをチェックするなら`ldd`を覚えておこう。でも[怪しいファイルを指定して実行しないように](http://www.catonmat.net/blog/ldd-arbitrary-code-execution/)

- 起動中のプロセスに`gdb`で接続し、そのスタックトレースを取る方法を知ろう。

- `/proc`以下のファイルを使おう。今起こっている問題をデバッグするのには素晴らしく便利だ。例えば、`/proc/cpuinfo`、`/proc/meminfo`、`/proc/cmdline`、`/proc/xxx/cwd`、`/proc/xxx/ece`、`/proc/xxx/fd/`、`/proc/xxx/smaps` (ここで、`xxx`はプロセスIDまたはPIDを意味する)。

- 過去に何か問題が起きたことの原因を探るなら、[`sar`](http://sebastien.godard.pagesperso-orange.fr/)がとても便利。CPUやメモリ、ネットワークなどの過去の統計情報を見られる。

- さらに深いシステムとパフォーマンスの分析には、`stap` ([SystemTap](https://sourceware.org/systemtap/wiki))、[`perf`](https://en.wikipedia.org/wiki/Perf_(Linux))、
[`sysdig`](https://github.com/draios/sysdig)。

- どのOSを利用しているかを`uname`や`uname -a` (Unixカーネル情報)で確認しよう。どのディストリビューションを使っているかは`lsb_release -a` (ディストリビューション情報)。

- 何かいつもと違うおかしなこと(大抵ハードウェアかドライバ関連の問題だ)が起きていたら、`dmesg`を実行しよう。

- `du`で表示されたディスクースペースがファイルを消しても空かなかった場合、そのファイルがプロセスに使われているかどうかこうやって確認しよう。`lsof | grep deleted | grep "filename-of-my-big-file"`

## ワンライナー

コマンドをまとめて使う例をいくつか。

- `sort`や`uniq`を使ってテキストファイルの共通部分、結合、差異を求める時に特に便利なのが以下のやり方。`a`と`b`はそれぞれ内容に重複のないテキストファイルとする。この方法は高速で、数GB程度までの任意のファイルサイズで動作する(`/tmp`が小さなルートパーティションにある場合は`-T`オプションをつける必要があるが、ソートはメモリ内で行われるとは限らない)。上述の`LC_ALL`と`sort`の`-u`オプションも参照のこと。

```sh
      cat a b | sort | uniq > c   # cはaとbの和集合
      cat a b | sort | uniq -d > c   # cはaとbの共通部分
      cat a b b | sort | uniq -u > c   # cはaとbの差異
```

- `grep . *`(各行にファイル名が付く)や、`head -100 *` (ファイル毎にヘッダーが付く)を使って手軽にディレクトリ内の全てのファイルの中身を確認できる。設定ファイルが含まれるような`/sys`や`/proc`や`/etc/`に対して非常に便利である。

- テキストファイルの3列目を全て足し合わせるには以下で(Pythonで同じことをやるに比べて3倍速く3分の1の長さで書ける)。

```sh
      awk '{ x += $3 } END { print x }' myfile
```

- ファイルツリーのサイズやデータを確認したいなら、以下は再帰的な`ls -l`と同じだが`ls -lR`より見やすい。

```sh
      find . -type f -ls
```

- Webサーバのログのようなテキストファイルがあり、各行には例えばURLの中に出てくる`acct_id`のような特定の値が現れるとしよう。`acct_id`が何回リクエストされているかを集計するには、
```sh
      egrep -o 'acct_id=[0-9]+' access.log | cut -d= -f2 | sort | uniq -c | sort -rn
```

- 継続的に変更を監視する場合 `watch`を使う。例えば、ディレクトリのファイルの変更を確認するには `watch -d -n 2 'ls -rtlh | tail'` となり、wifi設定などのネットワーク設定関係のトラブルシューティングでは `watch -d -n 2 ifconfig`。

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

- `cut `、 `paste`、`join`: データの操作

- `fmt`: テキストの段落をフォーマットする

- `pr`: テキストをページとカラムにフォーマットする

- `fold`: テキストの行を分割

- `column`: テキストをカラムあるいはテーブルにフォーマット

- `expand` と `unexpand`: タブとスペースの相互変換

- `nl`: 行数を表示

- `seq`: 数字を表示

- `bc`: 計算機

- `factor`: 整数を因数分解

- [`gpg`](https://gnupg.org/): ファイルの暗号化と署名

- `toe`: terminfoのエントリのテーブルを表示

- `nc`: ネットワークのデバッグとデータ転送

- `socat`: ソケットリレーとTCPポートのフォワーダ(`netcat`と同等)

- [`slurm`](https://github.com/mattthias/slurm): ネットワークトラフィックの可視化

- `dd`: データをファイルあるいはデバイス間で移動

- `file`: ファイルの種類を特定

- `tree`: ディレクトリとサブディレクトリをツリーで表示。`ls`に似ているが再帰的に動く

- `stat`: ファイルの情報

- `time`: コマンドを実行して処理時間を計測

- `timeout`: コマンドを実行し、指定時間経過後にプロセスを停止する

- `lockfile`: セマフォファイルを生成する。これは`rm -f`のみで削除可能。

- `logrotate`: ログをローテート、圧縮、メール送信

- `watch`: コマンドを繰り返し実行する。変更部分の強調表示もできる。

- `tac`: ファイルを逆から表示

- `shuf`: ファイルからランダムに選んだ行を表示

- `comm`: ソート済みファイルの行を比較

- `pv`: パイプ経由でデータの進行状況をモニタリング

- `sponge`: 書き込み前に全ての入力を読み込む。例えば、`grep -v something some-file | sponge some-file` のように、入力と同じファイルに書き込む際に便利。

- `hd`、`hexdump`、`xxd`、`biew`、`bvi`: バイナリファイルのダンプと編集

- `strings`: バイナリファイルからテキストを抽出

- `tr`: 文字の置き換えと操作

- `iconv` あるいは `uconv`: 文字エンコーディングの変換

- `split` と `csplit`: ファイルを分割

- `units`: 単位の変換と計算。2週間あたりのハロン(訳注 : 長さの単位)からまばたきごとのトゥウィップまで( `/usr/share/units/definitions.units`も参照のこと)

- `apg`: ランダムなパスワードを生成

- `7z`: 圧縮率の高いファイル圧縮

- `ldd`: 動的ライブラリの情報

- `nm`: オブジェクトファイルからシンボルを表示

- `ab`: Webサーバのベンチーマーク

- `strace`: システムコールのデバッグ

- [`mtr`](http://www.bitwizard.nl/mtr/): ネットワークデバッグのためのより高機能なtraceroute

- `cssh`: ビジュアルな並列シェル

- `rsync`: ファイルやフォルダをSSH経由またはローカルファイルシステム内で同期

- [`wireshark`](https://wireshark.org/) と [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): パケットキャプチャとネットワークデバッギング

- [`ngrep`](http://ngrep.sourceforge.net/): ネットワーク層のgrep

- `host` と `dig`: DNS名前解決

- `lsof`:プロセスのファイルディスクリプタとソケット情報

- `dstat`: 便利なシステム情報

- [`glances`](https://github.com/nicolargo/glances): 高レベルに複数のサブシステムの概要を把握

- `iostat`: ディスクの使用状況

- `mpstat`: CPUの使用状況

- `vmstat`: メモリの使用状況

- `htop`: topの改良版

- `last`: ログイン履歴

- `w`: 誰がログインしているか

- `id`: ユーザやグループの情報

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): システム統計情報の履歴

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) または [`nethogs`](https://github.com/raboof/nethogs): ソケットあるいはプロセスごとのネットワーク使用量

- `ss`: ソケットの統計情報

- `dmesg`: 起動時とシステムのエラーメッセージ

- `sysctl`: Linuxカーネルパラメータの確認および設定

- `hdparm`: SATA/ATAディスクの操作やパフォーマンス確認

- `lsblk`: ブロックデバイスの一覧。ディスクとディスクパーティションのツリービュー

- `lshw`、`lscpu`、`lspci`、`lsusb`、`dmidecode`: CPUやBIOS、RAID、グラフィック、その他デバイスなどのハードウェア情報

- `lsmod`、`modinfo`: カーネルのモジュールリストとモジュール情報

- `fortune`、 `ddate`、`sl`: んー、あー、これは蒸気機関車やZippyの引用句が「便利」だと思うかどうかによる

## OS X用のもの

これらは*MacOS用*の項目です。

- パッケージ管理は`brew` (Homebrew)や`port` (MacPorts)を使う。上記の多くのコマンドをMacOSにインストールできる。

- コマンドの出力をクリップボードにコピーする`pbcopy`とクリップボードから出力する`pbpaste`。

- OptionキーをaltキーとしてMac OSのターミナルで使う(上述の**alt-b**、**alt-f**などを使う場合)には、環境設定 -> 設定 -> キーボード で、"メタキーとしてoptionキーを使用"を選択。

- デスクトップアプリケーションでファイルを開くには、`open`、`open -a /Applications/Whatever.app`。

- Spotlight: `mdfind`でファイルを検索し、メタデータ(画像ファイルのEXIFの情報など)を`mdls`で表示。

- Mac OSはBSD Unixベースであるため、多くのコマンド(例えば、`ps`、`ls`、`tail`、`awk`、`sed`)では、Unix System VとGNUツールの違いに影響されて、Linuxのものと比べて微妙な違いが多く含まれている。違いがあるかについては、マニュアルページのタイトルに"BSD General Commands Manual"と書かれているかどうかで判断できる。場合によっては、GNUバージョンをインストール可能である(例えば、`gawk`や`gsed`で、GNUのawkとsedに対応)。クロスプラットフォームのbashスクリプトを書く場合には、そのようなコマンドは避ける(Pythonや`perl`の利用を検討)か十分なテストが必要である。

- Mac OSのリリース情報を取得するには、`sw_vers`。

## Windows専用

これらは*Windows用*の項目です。

### Windows下でUnixツールを手に入れる方法

- [Cygwin](https://cygwin.com/)をMicrosoft WindowsでインストールしてUnixシェルの力を手にしよう。このドキュメントで説明されている大部分はびっくり箱みたいに独創的だ。

- Windows10であれば[Windows Subsystem for Linux (WSL)](https://msdn.microsoft.com/commandline/wsl/about)を使える。Unixコマンドラインや親しみのあるBashを提供してくれる。

- windows上で、主にGNUデベロッパーツール(GCCなど)を使いたい場合、[MinGW](http://www.mingw.org/)や[MSYS](http://www.mingw.org/wiki/msys)を検討しよう。bash、gawk、make、grepを提供してくれる。MSYSはCygwinと比べると全ての機能を持っているわけではない。MinGWはUnixツールのネイティブWindowsポートを作成するのに特に有効だ。

- Windows配下でUnixの見た目と操作感を得るもう一つの方法は[Cash](https://github.com/dthree/cash)だ。本当に限られたUnixコマンドやコマンドラインオプションしかこの環境では利用できないので注意が必要だ。

### 使えるWindowsコマンドラインツール
- `wmic`を使って学ぶことで、Windowsシステム管理者タスクの大部分をコマンドラインで記述、実行することができる。

- `ping`、`ipconfig`、`tracert`、`netstat`などのWindows固有のコマンドラインも便利だと思えるはずだ。

- `Rundll32`を実行することによって[便利なWindowsタスク](http://www.thewindowsclub.com/rundll32-shortcut-commands-windows)を利用することができる。

### Cygwinの秘訣とコツ

- Cygwinのパッケージマネージャーで追加のUnixプログラムをインストールしよう。

- `mintty`をコマンドラインウィンドウとして使おう

- `/dev/clipboard`でWindowsのクリップボードにアクセスしてみよう。

- 登録されたアプリケーションで任意のファイルを開くためには`cygstart`を起動しよう。

- `regtool`でWindowsレジストリにアクセスしよう。

- `C:\`WindowsドライブのパスはCygwin下では`/cygdrive/c`なので注意が必要だ。また、Cygwinの`/`はWindowsの`C:\cygwin`だ。`cygpath`を使ってCygwinスタイルとWindowsスタイルのパスを切り替えられる。これはWindowsプログラムを実行するスクリプトでとても有効だ。

## さらなるリソース

- [awesome-shell](https://github.com/alebcay/awesome-shell): シェルのツールやリソースのまとめ
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): より詳しいMac OSのコマンドラインガイド
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/): よりよいシェルスクリプトを書くために
- [shellcheck](https://github.com/koalaman/shellcheck): シェルスクリプト(本来、bash/sh/zsh用)の静的解析ツール
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): シェルスクリプトでファイル名を正しく扱うために
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools): 同タイトルの書籍から引用されているデータサイエンスで役に立つコマンドやツール

## 免責事項

ごく一部の例外はありますが、コードは誰でも読めるように書かれている。力には責任が伴う。Bashで*できる*からといって、そうすべき必要があるという意味ではない！ ;)

## ライセンス

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

このドキュメントは[Creative Commons Attribution-ShareAlike 4.0 International Licene](http://creativecommons.org/licenses/by-sa/4.0/)でライセンスされる。
