[ Languages: [English](README.md), [Português](README-pt.md), [中文](README-zh.md) ]


# The Art of Command Line

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Meta](#meta)
- [Basics](#basics)
- [Everyday use](#everyday-use)
- [Processing files and data](#processing-files-and-data)
- [System debugging](#system-debugging)
- [One-liners](#one-liners)
- [Obscure but useful](#obscure-but-useful)
- [MacOS only](#macos-only)
- [More resources](#more-resources)
- [Disclaimer](#disclaimer)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

커맨드라인을 능숙하게 다루는것은 도외시되거나 신비스럽게 여겨집니다. 하지만 커맨드라인은 명백하고도 미묘한 방법으로 엔지니어가 하는 작업의 유연성과 생산성을 향상시십니다. 이 문서는 리눅스에서 작업을 하면서 찾은 노트와 팁들의 모음입니다. 몇 가지는 기초적이고, 몇가지는 상당히 구체적이며, 세련되고, 잘 알려지지 않은 것입니다. 이 문서는 그리 길지 않지만, 여기 있는 모든것을 사용할 수 있게 되고, 기억해낼 수 있게 된다면, 많은 것을 알게되는 것입니다.

여기있는 대부분의 것은
[원래](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[Quora에](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
 [올라온](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know) 것입니.
하지만 거기에 관심을 가지기보다, Github를 이용하는 것이 더 가치있는 것처럼 보입니다. 여기엔 더 재능있는 사람들이 손쉽게 개선안을 제안할 수 있는 곳이죠. 만약 문제가 있거나, 더 나아질 수 있는 내용이 보인다면, 이슈를 제출하거나 풀 리퀘스트를 보내주세요! (물론 meta 섹션과 이미 존재하는 풀 리퀘스트와 이슈를 봐주기를 바랍니다.)

## Meta

범위:

- 이 가이드는 초심자와 경험자 모두를 위한 것입니다. 목표는 범위(전부 다 중요합니다!), 구체성(대부분의 일반적인 케이스에 대한 구체적인 예제), 그리고 간결함(쉽게 마주치지 않는, 중요하지 않고, 지엽적인 것을 피함) 입니다. 모든 팁은 특정 상황에서 매우 중요하거나, 여러 대안들 사이에서의 시간을 확연하게 절약합니다.
- 이 문서는 리눅스를 위한것입니다. 일부는 MacOS에서 똑같이 적용되지 않습니다(Cygwin에서 조차 말이죠).
- 인터랙티브 Bash에 초점이 맞추어져있습니다만, 대부분의 팁은 다른 쉘이나, general Bash 스크립트에서도 동작합니다.
- 이 문서는 "스탠다드" 유닉스 커맨드와 특정 패키지 설치를 필요로 하는 것 둘 다 포함하고 있습니다. 여기서 다루는 스탠다드 커맨드와 특정 패키지에 대한 것은 포함될만큼 충분히 중요합니다.

노트:

- 이 문서를 한 파일로 유지하기 위해서, 컨텐츠들은 암시적인 레퍼런스 형태로 포함되어있습니다. 한 개념이나 명령어에 대해 알게 된 후에, 다른곳에서 그에대한 좀 더 자세한 정보를 찾을 수 있을만큼 당신은 똑똑할것입니다. `apt-get`, `yum`, `dnf`, `pacman`, `pip`, `brew` (혹은 적절한 다른 것)을 이용해 새 프로그램을 설치하세요.
- [Explainshell](http://explainshell.com/)을 이용해서 각각의 커맨드, 옵션, 파이프나 그 외 등등이 어떤것인지 알아보십시오.


## Basics

- 기본 Bash를 배우세요. 말하자면, 최소한 `man bash`를 실행하고, 전부를 훑어 보세요. 매뉴얼의 내용은 따라가기 쉬우며 그리 길지 않습니다. 다른 쉘들 또한 좋습니다만, Bash는 강력하고 언제나 사용가능합니다( *오직* zsh, fish, 그 외의 쉘만을 당신의 노트북에서 시도하면서 배우는 경우에는, 많은 경우 제한이 생길것입니다. 이미 존재하는 서버를 사용하는 것등의 일에서 말이죠).

- 텍스트 기반 에디터를 최소한 하나정도 다룰 수 있게 배우세요. Vim(`Vi`)가 이상적입니다. 터미널에서 온갖 작업을 하는데 다른 실질적인 경쟁자가 없기 때문이죠(Emacs, 대형 IDE 또는 모던 힙스터스러운 에디터를 대부분의 작업에 사용한다고 해도 말이죠).

- `man`을 이용해서 문서를 읽는 법을 배우세요(호기심 많은 사람을 위해서 하는 얘기입니다만, `man man`은 섹션 번호들의 목록을 표시합니다. 예를 들어 1은 "regular" 커맨드, 5는 files/conventions, 그리고 8은 administration이죠). `apropos`를 히용해서 man 페이지를 찾으세요. 몇몇 커맨드는 실행가능한 커맨드가 아니라는 것을 알아두세요. 하지만 Bash 빌트인 함수들은 `help`와 `help -d`를 이용해서 도움말을 볼 수 있습니다.

- `>`와 `<`, `|`를 이용한 파이프를 사용해서 입력과 출력의 리다이렉션을 배우세요. stdout(역주: 표준 출력)과 stderr(역주: 표준 에러 출력)에 대해서 배우세요. 

- `*`(그리고 아마도 `?`과 `{`...`}`)을 이용하는 파일 글롭(glob) 확장을 배우세요. 그리고 쌍따옴표`"`와 홑따옴표`'`의 차이를 배우세요. (변수 확장에 대해서 더 보려면 아래를 참조하세요)

- Bash 작업 관리에 익숙해지세요. `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill` 등등.

- `ssh`를 배우고, `ssh-agent`, `ssh-add`를 통해서 비밀번호 없는 인증 방식의 기본을 배우세요.

- 기본 파일 관리: `ls`와 `ls -l`(특별히, `ls -l`에서 각각의 열이 무슨 의미인지 배우세요), `less`, `head`, `tail` 그리고 `tail -f`(또는 더 좋은 `less +F`), `ln`과 `ln -s`(하드 링크와 소프트 링크의 차이와 각각의 장단점을 배우세요), `chown`, `chmod`, `du`( 디스크 사용량의 빠른 요약을 보려면 `du -hk *`). 파일 시스템 관리를 위해서는 `df`, `mount`, `fdisk`, `mkfs`, `lsblk`.

- 기본 네트워크 관리: `ip` 또는 `ifconfig`, `dig`.

- 정규표현식(regular expression)을 잘 알아두세요. 그리고 `grep`/`egrep`의 다양한 플래그도 알아두세요. `-i`, `-o`, `-A`와 `-B` 옵션은 알아둘 가치가 있습니다.

- `apt-get`, `yum`, `dnf` 또는 `pacman`을 이용하여 패키지를 찾고 설치하는 법을 배우세요. 그리고 `pip`가 설치되어있는지 확인해서, 파이선 기반의 커맨드 라인 도구를 설치할 수 있도록 하세요(밑에 설명된 것중 몇가지는 `pip`를 이용해 설치하는게 제일 쉽습니다.


## Everyday use

- Bash 에서 **Tab**을 쓰면 argument를 완성하고, **ctrl-r**을 쓰면 커맨드 히스토리에서 검색합니다.

- Bash에서 **ctrl-w**는 마지막 단어를 지웁니다. **ctrl-u**는 라인의 처음까지 전부다 지웁니다. **alt-b**와 **alt-f**를 이용해서 단어 단위로 이동할 수 있습니다. **ctrl-k**는 커서 위치부터 라인의 끝까지 지웁니다. **ctrl-l**은 화면을 깨끗하게 합니다. `man readline`을 이용해서 Bash의 기본 키 조합을 살펴보세요. 많은 것이 있습니다. 예를 들면 **alt-.**같은 경우, 이건 argument를 돌아가면서 나타내고 **alt-***는 글롭을 확장합니다.

- vi 스타일의 키  조합을 사랑한다면, `set -o vi`를 사용할수도 있습니다.

- 최근 사용한 커맨드를 보려면 `history`를 입력하세요. `!$`(마지막 argument), `!!`(마지막 커맨드)와 같은 약어들이 매우 많습니다. 비록 이런 것들이 **ctrl-r**이나 **alt-.**명령어로 자주 대체되기 쉽지만요.

- 이전에 작업하던 디렉토리로 돌아가려면 `cd -`를 사용하세요.

- 커맨드를 타이핑 하던 도중에 마음이 바뀌었다면, **alt-#**을 쳐서 시작점에 `#`을 삽입하고, 엔터를 쳐서 코멘트로 여겨지게 하세요(또는 **ctrl-a**, **#**, **enter**).  나중에 커맨드 히스토리에서 찾아서 타이핑 중이었던 커맨드로 돌아올 수 있습니다.

- `xargs`(혹은 `parallel`)를 사용하세요. 매우 강력합니다. 라인당 몇개의 아이템이 실행되게 할 것인지(`-L`) 그걸 병렬로 할 것인지(`-P`)를 제어할 수 있다는걸 기억하세요.  제대로 하고있는지 확신할 수 없다면 `xargs echo`를 먼저 실행해보세요. 또 `-I{}`도 간편합니다. 예시:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p`는 프로세스 트리를 표시하는데 도움이 됩니다.

- `pgrep`과 `pkill`을 사용해서 프로세스를 찾거나 시그널을 보내세요(`-f`가 유용합니다).

- 프로세스에 보낼 수 있는 다양한 시그널을 알아두세요. 예를 들어, 프로세스를 일시중지 할 때는 `kill -STOP [pid]`를 사용합니다. 전체 목록은 `man 7 signal`에서 볼 수 있습니다.

- 백그라운드 프로세스를 영원히 돌아가게 만들고 싶다면, `nohup`이나 `disown`을 사용하세요.

- 어떤 프로세스가 리스닝(역주: 특정 포트로 들어오는 패킷 리스닝)을 하고 있는지 알려면 `netstat -lntp`나 `ss -plat`을 사용해서 알 수 있습니다(TCP일 경우입니다. UDP의 경우 `-u`옵션을 추가하세요).

- `lsof`를 이용해서 열려있는 소켓과 파일을 볼 수 있습니다.

- Bash 스크립트에서 `set -x`를 사용하면 디버깅용 출력을 사용하게 됩니다. 스트릭트 모드(strict mode)가 가능할때면 사용하세요. `set -e`를 사용하면 에러가 났을때 중단시키게됩니다. `set -o pipefail`을 사용하면 에러에 대해서 강경한 기준을 적용합니다(이 주제가 조금 미묘하지만 말이죠). 더 복잡한 스크립트의 경우 `trap`또한 사용합니다.

- Bash 스크립트에서 (괄호로 둘러쌓여 작성된) 서브쉘은 커맨드를 그룹으로 묶는 편리한 방법입니다. 일반적인 예로, 임시로 다른 디렉토리로 이동하여 작업하는 것이 있습니다.
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- Bash 에는 여러가지 다양한 변수 확장이 있다는 것을 알아두세요. 변수가 존재하는지 확인하려면 `${name:?error message}`를 사용하세요. 예를 들어 Bash 스크립트가 하나의 argument를 요구한다면, `input_file=${1:?usage: $0 input_file}`를 사용하세요. 산술 확장은 `i=$(( (i + 1) % 5 ))` 처럼 사용합니다. 순열은 `{1...10}`처럼 사용합니다. 문자열 트리밍(trimmin)은 `${var%suffix}`이나 `${var#prefix}`처럼 사용할 수 있습니다. 예를들어 `var=foo.pdf`라면, `echo ${var$.pdf}.txt`는 `foo.txt`를 출력합니다.

- 커맨드의 실행 결과 출력물은 `<(some command)`처럼 이용해서 파일처럼 다뤄질 수 있습니다. 예를들어 로컬의 `/etc/hosts`를 리모트의 것과 비교하려면 다음처럼 하면 됩니다.
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- `cat << EOF...`같은 "here documents"에 대해서 알아두세요.

- Bash에서 표준 출력(standard output)과 표준 에러(standard error) 둘 다 `some-command > logfile 2>&1`같은 명령어로 리다이렉트할 수 있습니다. 종종, 커맨드가 열린 파일 핸들을 남기지 않는 것을 확실히 하기 위해, 현재 작업중인 터미널에서 명령어에 `</dev/null`을 덧붙이는 것은 좋은 습관입니다.

- `man ascii`를 사용해서 헥스값과 10진 값이 같이 있는 훌륭한 ASCII 테이블을 볼 수 있습니다. 일반적인 인코딩 정보를 보려면 `man unicode`, `man utf-8` 그리고 `man latin1`을 이용할 수 있습니다.

- `screen`을 이용하거나  [`tmux`](https://tmux.github.io/)를 이용해서 화면을 다중분할할 수 있습니다. 특히 리모트 ssh 세션을 떼어내고(detach) 다시 붙이는데(re-attach)하는데 유용합니다. 세션을 영구히 유지하는 최소한의 대안은 오직 `dtach`밖에 없습니다.

- ssh에서 `-L`이나 `-D`(가끔 `-R`)를 이용해서 포트 터널링하는 것을 알아두시면 유용합니다. 예를 들어 리모트 서버를 경유해서 웹사이트에 접속한다거나 할 때 말이죠.

- 몇가지 ssh 설정을 최적화하는 것은 유용할 수 있습니다. 예를들어 `~/.ssh/config`는 특정 네트워크 환경에서 연결이 끊기는 것을 회피하기 위해 압축을 사용하는 설정들을 담고 있습니다(특히 scp 명령어를 낮은 대역폭 연결에서 사용하는 경우에 도움이 됩니다. 그리고  로컬 제어 파일에서 같은 서버로 연결하는 채널을 다중화할 수 있습니다.

```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

-  ssh의 몇 가지 옵션들은 보안에 민감한 옵션이며 주의를 가지고 사용되어야합니다. 예를 들어 서브넷, 호스트 또는 신뢰되는 네트워크에서 `StrictHostKeyChecking=no`, `ForwardAgent=yes`을 사용하는 것 등입니다.

- 시스템 설정에 유용하지만 `ls`로 얻을 수 없고 쉽게 엉망이 되기 쉬운 파일의 권한을 8진법 형태로 얻으려면, 다음과 같은 커맨드를 사용하세요.
```sh
      stat -c '%A %a %n' /etc/timezone
```

- 다른 커맨드의 출력과 상호작용하면서 값을 선택하려면  [`percol`](https://github.com/mooz/percol)을 사용하세요.

- 다른 커맨드(예를 들면 `git`)의 출력에 기반하는 파일과 상호작용하려면, `fpp` ([PathPicker](https://github.com/facebook/PathPicker))를 사용하세요.

- 현재 네트워크에 있는 사용자들에게 현재 디렉토리에 있는 모든 파일(과 하위 디렉토리)를 위한 단순한 웹서버를 원한다면 다음을 사용하세요:
`python -m SimpleHTTPServer 7777` (7777포트, Python 2) 그리고 `python -m http.server 7777` (7777포트, Python 3).


## Processing files and data

- 현재 디렉토리에서 파일을 이름으로 찾으려면 `find . -iname '*something*'` (또는 비슷하게)를 사용하면 됩니다. 어느곳에 있든 파일을 이름으로 찾으려면 `locate something`을 사용하세요(하지만 인내를 가져야합니다. `updatedb`가 최근에 생성된 파일을 인덱싱하지 않았을 수 있습니다).

- 소스나 데이터 파일들에서 일반적인 검색을 할때는(`grep -r`보다 더 복잡할때), [`ag`](https://github.com/ggreer/the_silver_searcher)를 사용하세요.

- HTML을 텍스트로 변환할때는 `lynx -dump -stdin`를 사용하세요.

- 마크다운, HTML, 그리고 모든 종류의 문서 변환에는 [`pandoc`](http://pandoc.org/)을 시도해보세요.

- XML을 반드시 다뤄야한다면, `xmlstarlet`을 사용하세요. 오래되었지만 좋습니다.

- JSON에는 `jq`를 사용하세요.

- Excel이나 CSV파일에는 [csvkit](https://github.com/onyxfish/csvkit)가 `in2csv`, `csvcut`, `csvjoin`, `csvgrep`외 다른 도구들을 제공합니다..

- Amazon S3를 다룰때는 [`s3cmd`](https://github.com/s3tools/s3cmd)가 편리합니다. 그리고 [`s4cmd`](https://github.com/bloomreach/s4cmd)는 빠릅니다. Amazon의  [`aws`](https://github.com/aws/aws-cli)는 다른 AWS 관련 작업에 핵심적인 도구입니다.

- `sort`와 `uniq`에 대해서 알아두세요. uniq의 `-u`, `-d`옵션을 포함해서 말이죠. 하단의 one-liner를 보세요. 그리고 `comm`도 보세요.

- 텍스트 파일들을 다루는 `cut`, `paste` 그리고 `join`에 대해서 알아두세요. 많은 사람들이 `cut`을 사용하지만 `join`에 대해서는 잊고 있습니다.

- `wc`를 이용해서 행(`-l`), 캐릭터(`-m`), 단어(`-w`) 그리고 바이트(`-c`)를 세는 것을 알아두세요.

- `tee`를 이용해서 `ls -al | tee file.txt`처럼, 표준입력(stdin)에서 복사해서 파일로 보내거나, 표준 출력(stdout)으로 보내는 것을 알아두세요.

- 로케일이 커맨드라인 도구에 정렬 순서(collation)와 퍼포먼스를 포함해서 미묘하게 영향을 끼치는 것을 알아두세요. 대부분의 리눅스 설치는 `LANG`이나 다른 로케일 변수를 US English와 같은 로컬 세팅으로 설정합니다. 하지만 로케일을 바꿀 경우 정렬도 바뀔 것이라는 것에 주의하세요. 그리고 i18n 루틴들도 정렬이나 다른 커맨드들을 *몇 배* 느리게 할 수 있습니다. `export LC_ALL=C`를 사용하여, 어떤 상황에서는( 밑에 있는 집합(set) 작업이나, 유일성 작업등) i18n의 느린 루틴들을 통채로 안전하게 무시할 수 있습니다. 그리고 전통적인 바이트 기반의 정렬 순서를 사용할 수 있습니다.

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

- Know `sort`'s options. Know how keys work (`-t` and `-k`). In particular, watch out that you need to write `-k1,1` to sort by only the first field; `-k1` means sort according to the whole line. Stable sort (`sort -s`) can be useful. For example, to sort first by field 2, then secondarily by field 1, you can use `sort -k1,1 | sort -s -k2,2`. For handling human-readable numbers (e.g. from `du -h`) use `sort -h`.

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
- `sort`/`uniq`를 사용하여 텍스트 파일의 교차점, 조합, 차이점을 확인이 필요할때 상당한 도움이 될껍니다. 가령 `a`와 `b`가 유일한 텍스트 파일이라합시다. 이것이 임의의 크기인 파일을(그게 기가바이트라고 해도) 빠르게 작업할 수 있습니다. (Sort는 메모리 제한에 걸리지 않습니다만, 만약 루트 파티션이 작은 경우, `/tmp`를 사용하기위해 `-T`옵션을 사용하면됩니다.) 위의 `LC_ALL`에대한 내용은 `sort`의 `-u`옵션을 확인하십시오. (아래 예제에 집중하기 위해서 생략)
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

- `expr`: 산술적이거나 논리적인 작업을 수행하거나 정규표현식을 검증할때 사용합니다

- `m4`: 간단한 메크로 수행기를 실행합니다

- `yes`: 어떠한 한 문장을 매우 많이 출력합니다

- `cal`: 간단한 달력을 보여줍니다

- `env`: 어떤 한 커맨드를 실행합니다(스크립트를 만들때 유용합니다)

- `printenv`: 환경 변수들을 출력합니다(디버깅을 할때나 스크립트를 만들때 유용합니다)

- `look`: 어떤 문자열로 시작하는 영단어(혹은 파일의 어떤 한 줄)을 찾습니다

- `cut `과 `paste` 그리고 `join`: 데이터를 수정할때 사용합니다

- `fmt`: 문단의 서식을 지정합니다

- `pr`: 문서의 페이지나 컬럼 서식을 지정합니다

- `fold`: 문서의 각 라인들을 특정한 길이에 맞게 수정합니다

- `column`: 문서의 컬럼이나 테이블의 서식을 지정합니다

- `expand` and `unexpand`: 탭을 공백으로 바꾸어주거나 공백을 탭으로 바꾸어줍니다

- `nl`: 줄 번호를 추가해줍니다

- `seq`: 숫자들을 출력하는데 사용합니다

- `bc`: 간단한 계산기를 실행합니다

- `factor`: 정수들을 인수분해하는데 사용합니다

- `gpg`: 파일들을 암호화하고 서명하는데 사용합니다

- `toe`: terminfo 엔트리들의 테이블(table of terminfo entries)

- `nc`: 네트워크를 디버깅하거나 데이터를 전송할때 사용합니다

- `socat`: 소켓 릴레이나 TCP 포트로 내용을 전달할때 사용합니다(`netcat`과 비슷합니다)

- `slurm`: 네트워크 상황을 시각화하여 보여줍니다

- `dd`: 파일들이나 디바이스들 간에 데이터를 옮길때 사용합니다

- `file`: 파일의 종류를 알아내는데 사용합니다

- `tree`: 디렉토리들과 그 하위 디렉토리를 마치 ls를 반복적으로 입력한 것처럼 트리의 형태로 보여줍니다

- `stat`: 파일의 정보를 보여줍니다

- `tac`: 파일의 내용을 역순으로 출력합니다

- `shuf`: 파일의 각 줄들을 임의의 순서로 출력합니다

- `comm`: 정렬된 파일들을 각 라인별로 비교합니다

- `pv`: 파이프를 통해서 프로세스의 정보를 모니터링하는데 사용합니다

- `hd` and `bvi`: 바이너리 파일을 수정하거나 덤프를 얻어오는데 사용합니다

- `strings`: 바이너리 파일들에서 특정 문장을 추출하는데 사용합니다

- `tr`: 문자를 변환하거나 조작하는데 사용합니다

- `iconv` or `uconv`: 문서의 인코딩방식을 변환하는데 사용합니다

- `split `and `csplit`: 파일들을 쪼개는데 사용합니다

- `units`: 단위를 변환하거나 계산하는데 사용합니다 예를들어 furlongs/fortnight 단위를 twips/blink로 변환합니다 (`/usr/share/units/definitions.units`를 참고하세요)

- `7z`: 고효율의 파일 압축프로그램입니다

- `ldd`: 동적 라이브러리들의 정보를 보여줍니다

- `nm`: 오브젝트 파일들에 포함된 심볼정보를 얻어옵니다

- `ab`: 웹 서버를 벤치 마킹하는데 사용합니다

- `strace`: 시스템 콜을 디버깅할때 사용합니다

- `mtr`: 네트워크 디버깅시에 traceroute보다 더 낫습니다

- `cssh`: 쉘을 동시에 여러개 사용할때 사용합니다

- `rsync`: SSH를 통해서 파일과 폴더들을 동기화 할때 사용합니다

- `wireshark` and `tshark`: 패킷정보를 가져오며 네트워킹을 디버깅하는데 사용합니다

- `ngrep`: 네트워크 환경에서 grep과 같은 역할을 합니다

- `host` and `dig`: DNS 정보를 보여줍니다

- `lsof`: 프로세스 파일 디스크립터와 소켓의 정보를 보여줍니다

- `dstat`: 유용한 시스템 정보를 보여줍니다

- [`glances`](https://github.com/nicolargo/glances): 보다 고차원의 여러 서브시스템들의 정보를 한번에 보여줍니다

- `iostat`: CPU 나 디스크의 사용량 정보를 보여줍니다

- `htop`: 보다 개선된 형태의 top을 보여줍니다

- `last`: 로그인 했던 정보들을 보여줍니다

- `w`: 현재 누가 로그인했는지 보여줍니다

- `id`: 현재 유저나 그룹에 대한 식별 정보를 보여줍니다

- `sar`: 시스템 상태에 대한 정보를 보여줍니다

- `iftop` or `nethogs`: 소켓 또는 프로세스를 이용하여 네트워크를 정보를 보여줍니다

- `ss`: 소켓에 관한 통계자료들을 보여줍니다

- `dmesg`: 부팅 메시지와 시스템 에러 메시지들을 보여줍니다

- `hdparm`: SATA/ATA disk들의 정보를 수정하거나 그것들이 작동하도록 합니다.

- `lsb_release`: Linux 배포판의 정보를 보여줍니다

- `lsblk`: 블록 디바이스들의 목록을 보여줍니다 : 여러분의 디스크들이나 디스크파티션들을 트리의 형태로 보여줍니다

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: CPU, BIOS, RAID, graphics, devices 등의 하드웨어 정보를 보여줍니다

- `fortune`, `ddate`, 그리고 `sl`: 에... 증기기관차를 생각하고있고 그것을 인용하고 싶다면 이것은 "유용"합니다


## 맥용

*MacOS에서만* 해당되는 항목입니다.

- `brew` (Homebrew)나 `port` (MacPorts)를 패키지 메니저로 사용합니다. 보다 많은 명령어를 MacOS에 설치하여 사용할 수 있습니다.

- `pbcopy`를 이용하여 데스크탑 어플리케이션에 명령어 출력물을 복사하거나 `pbpaste`를 이용해 붙여넣기를 할 수 있습니다.

- 데스크탑 어플리케이션에서 파일을 열기위해, `open` 또는 `open -a /Applications/Whatever.app`을 사용하면 됩니다.

- Spotlight: `mdfind`를 이용해 파일을 찾고, `mdls`를 이용해 메타데이타 (사진 EXIF 정보와 같은) 목록을 볼 수 있습니다.

- MacOS는 BSD Unix 기반이며 많은 명령어들을 (예로 `ps`, `ls`, `tail`, `awk`, `sed`) 사용할 수 있으며, 이것들은 Linux 버전들과 미묘한 차이가 있습니다. 그리고 크게는 System V-style Unix와 GNU 도구들에 많은 영향을 받았습니다. 이런 내용들을 man 페이지 상단의 "BSD General Commands Manual." 라는 문구를 통해 알 수 있습니다. 가끔은 GNU 버전이 설치되기도합니다. (예로, GNU awk와 sed인 `gawk`와 `gsed`에서). 만약 이종 플랫폼간 Bash 스크립트를 작성하려면, 동일한 명령어 (예로, 파이썬이나 `perl`과 같은)나 테스트시 주의해야합니다.


## More resources

- [awesome-shell](https://github.com/alebcay/awesome-shell): 쉘에 대한 툴과 리소스들이 잘 정리되어 있는 리스트입니다.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/): 보다 나은 쉘스크립트를 작성하기 위한 정보글입니다.


## Disclaimer

매우 작은 작업을 제외한 코드들은 다른 사람이 읽을 수 있도록 작성됩니다. 그러니 이 내용은 작성자 전원에게 책임이 있습니다. Bash에서 뭔가를 *할 수 있다는* 것이 당신이 뭔가를 해야된다는 것을 강요하는 것이 아니다! ;)


## License

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/) 

이 저작물은 [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/)에 따라 이용할 수 있습니다.