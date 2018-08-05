🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*


# The Art of Command Line

[![Ask a Question](https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg)](https://airtable.com/shrzMhx00YiIVAWJg)

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


- [Meta](#meta)
- [Basics](#basics)
- [Everyday use](#everyday-use)
- [Processing files and data](#processing-files-and-data)
- [System debugging](#system-debugging)
- [One-liners](#one-liners)
- [Obscure but useful](#obscure-but-useful)
- [macOS only](#macos-only)
- [Windows only](#windows-only)
- [More resources](#more-resources)
- [Disclaimer](#disclaimer)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

커맨드 라인을 능숙하게 다루는 기술은 종종 도외시되거나 신비스럽게 여겨집니다. 하지만 커맨드 라인은 명백하고도 미묘한 방법으로 엔지니어가 하는 작업의 유연성과 생산성을 향상시킵니다. 이 문서는 리눅스에서 커맨드 라인을 사용할 때 유용하게 활용할 수 있는 노트와 팁들의 모음입니다. 몇몇은 기초적인 것들이지만 몇몇은 상당히 구체적이고 세련되며 잘 알려지지 않은 것들입니다. 이 문서는 그리 길지 않지만 여기 있는 모든 것을 사용할 수 있고 기억해낼 수 있다면 당신은 많은 것을 알고 있다고 할 수 있습니다.

이 문서에는 [많은 저자와 번역가](AUTHORS.md)가 참여했습니다.
여기 중 일부 내용은
[원래](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[Quora에](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
[올라온](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know) 것이지만
후에 GitHub으로 옮겨졌고, 이 곳에서 원 저자들보다 더 재능있는 사람들이 무수히 많은 개선작업을 진행하였습니다.
커맨드 라인에 관해 궁금한 것이 있으면 [**질문해 주세요**.](https://airtable.com/shrzMhx00YiIVAWJg) 오류가 있거나 더 나아질 수 있는 내용이 보인다면 [**기여해 주세요**!](/CONTRIBUTING.md)

## Meta

범위:

- 이 가이드는 초보자와 경험자 모두를 위한 것 입니다. 이 가이드의 목표는 _폭넓은 지식을 제공하는 것_(전부 다 중요합니다), _구체적으로 제공하는 것_(가장 일반적인 사례에 대한 구체적인 예제를 제공합니다), 그리고 _간결하게 제공하는 것_(중요하지 않거나 다른 문서에서 쉽게 찾아볼 수 있는 지엽적인 것들을 피합니다)입니다. 모든 팁은 특정 상황에서 매우 중요하거나 여러 다른 대안들보다 시간을 확연하게 절약합니다.
- 이 문서는 리눅스를 위해 쓰였습니다. "[macOS only](#macos-only)", "[Windows only](#windows-only)" 섹션을 제외하고 말이죠. 그 밖의 대부분은 유닉스, macOS(심지어 Cygwin)에서도 적용하거나 설치할 수 있습니다.
- 인터랙티브 Bash에 초점이 맞추어져있습니다만, 대부분의 팁은 다른 쉘이나, general Bash 스크립트에서도 동작합니다.
- 이 문서는 "표준" 유닉스 커맨드와 특정 패키지 설치를 필요로 하는 것 둘 다 포함하고 있습니다 -- 여기서 다룰만큼 충분히 중요하다면요.

노트:

- 이 문서를 하나의 파일로 유지하기 위해서 콘텐츠들은 암시적인 레퍼런스 형태로 포함되어있습니다. 한 개념이나 명령어에 대해 알게 된 후에, 구글에서 그에 대한 좀 더 자세한 정보를 찾아보세요. `apt-get`, `yum`, `dnf`, `pacman`, `pip`, `brew` (혹은 적절한 다른 것)를 이용해 새 프로그램을 설치하세요.
- [Explainshell](http://explainshell.com/)을 이용해서 커맨드, 옵션, 파이프, 기타 등등이 어떤 기능을 하는지 분석하는데 도움을 받으세요.


## Basics

- Bash의 기초를 배우세요. 말하자면, `man bash`를 실행하고 최소한 전부 훑어보기라도 하세요. 매뉴얼의 내용은 따라가기 쉬우며 그리 길지 않습니다. 다른 쉘들 또한 좋습니다만, Bash는 강력하고 언제나 사용 가능합니다(zsh, fish, 혹은 그 외의 쉘*만* 배운다면 개인 노트북에서는 좋겠지만 많은 경우 제한이 생길 것입니다. 이미 존재하는 서버를 사용하는 것등의 일에서 말이죠).

- 텍스트 기반 에디터를 최소한 하나 정도는 잘 다룰 수 있게 배우세요. `nano` 에디터는 기본적인 편집기능(열기, 수정하기, 저장하기, 찾기)을 제공하는 가장 단순한 에디터 중 하나입니다. 그러나 텍스트 터미널을 이용하는 고급 이용자라면 Vim(`Vi`)을 대체할 수 있는 것은 없습니다. Vim은 사용법을 배우기는 어렵지만 믿음직하고 빠르며 풍부한 기능을 가졌습니다. 또한 고전적인 Emacs도 많이 사용됩니다. 특히 규모가 좀 더 큰 편집 작업에서요. (물론 요즘 같은 시대에 대형 프로젝트를 진행하고 있는 소프트웨어 개발자라면 순수한 텍스트 기반 에디터만 사용하지는 않을 것이고 최신의 그래픽 기반 IDE와 도구들에도 익숙해져야 합니다.)

- `man`을 이용해서 문서를 읽는 법을 배우세요(호기심 많은 사람을 위해서 하는 얘기입니다만, `man man`은 섹션 번호들의 목록을 표시합니다. 예를 들어 1은 "regular" 커맨드, 5는 files/conventions, 그리고 8은 administration이죠). `apropos`를 이용해서 man 페이지를 찾으세요. 몇몇 커맨드는 실행파일이 아니라 Bash 빌트인 명령어임을 알아두세요. Bash 빌트인 명령어들에 대한 도움을 받으려면 `help`와 `help -d`를 이용하세요. 어떤 커맨드가 실행파일, 쉘 빌트인 명령어인지, 아니면 별칭인지는 `type command`를 통해 확인할 수 있습니다.

- `>`와 `<`, `|`를 이용한 파이프를 사용해서 입력과 출력의 리다이렉션을 배우세요. `>`는 출력 파일을 덮어 씌우고, `>>`는 출력 파일 끝에 내용을 덧붙인다는 걸 알아두세요. stdout(역주: 표준 출력)과 stderr(역주: 표준 에러 출력)에 대해서 배우세요.

- `*`(그리고 아마도 `?`와 `[`...`]`)을 이용하는 파일 글롭(glob) 확장을 배우세요. 그리고 쌍따옴표`"`와 홑따옴표`'`의 차이를 배우세요. (변수 확장에 대해서 더 보려면 아래를 참조하세요)

- Bash 작업 관리에 익숙해지세요. `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill` 등등.

- `ssh`를 배우고, `ssh-agent`, `ssh-add`를 통해서 비밀번호 없는 인증 방식의 기본을 배우세요.

- 기본 파일 관리: `ls`와 `ls -l`(특별히, `ls -l`에서 각각의 열이 무슨 의미인지 배우세요), `less`, `head`, `tail` 그리고 `tail -f`(또는 더 좋은 `less +F`), `ln`과 `ln -s`(하드 링크와 소프트 링크의 차이와 각각의 장단점을 배우세요), `chown`, `chmod`, `du`( 디스크 사용량의 빠른 요약을 보려면 `du -hs *`). 파일 시스템 관리를 위해서는 `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. inode가 무엇인지 배우세요(`ls -i` 또는 `df -i`).

- 기본 네트워크 관리: `ip` 또는 `ifconfig`, `dig`, `traceroute`, `route`.

- `git` 같은 버전 관리 시스템을 배우고 사용하세요.

- 정규 표현식(regular expression)을 잘 알아두세요. 그리고 `grep`/`egrep`의 다양한 플래그도 알아두세요. `-i`, `-o`, `-v`,`-A`, `-B`와 `-C` 옵션은 알아둘 가치가 있습니다.

- `apt-get`, `yum`, `dnf` 또는 `pacman`(배포판마다 다릅니다)을 이용하여 패키지를 찾고 설치하는 법을 배우세요. 그리고 `pip`가 설치되어 있는지 확인해서 파이선 기반의 커맨드 라인 도구를 설치할 수 있도록 하세요(밑에 설명된 것 중 몇 가지는 `pip`를 이용해 설치하는 게 제일 쉽습니다).


## Everyday use

- Bash 에서 **Tab**을 쓰면 argument를 완성하고, **ctrl-r**을 쓰면 커맨드 히스토리에서 검색합니다(누른 다음, 검색할 것을 입력하고, **ctrl-r**를 계속 눌러 좀 더 맞는 것을 찾을 수 있습니다. **Enter**를 눌러 찾은 커맨드를 실행하고 오른쪽 화살표 키를 눌러 결과를 현재 라인에 복사해 수정할 수 있습니다).

- Bash에서 **ctrl-w**는 마지막 단어를 지웁니다. **ctrl-u**는 라인의 처음까지 전부다 지웁니다. **alt-b**와 **alt-f**를 이용해서 단어 단위로 이동할 수 있습니다. **ctrl-a**로 라인의 시작점으로 이동할 수 있고 **ctrl-e**로 라인의 끝으로 이동할 수 있습니다. **ctrl-k**는 커서 위치부터 라인의 끝까지 지웁니다. **ctrl-l**은 화면을 깨끗하게 합니다. `man readline`을 이용해서 Bash의 기본 키 조합을 살펴보세요. 많은 것이 있습니다. 예를 들면 **alt-.**같은 경우, 이건 argument를 돌아가면서 나타내고 **alt-***는 글롭을 확장합니다.


- vi 스타일의 키  조합을 사랑한다면, `set -o vi`를 사용할 수도 있습니다(`set -o emacs`로 되돌릴 수 있습니다).

- 긴 명령을 수정하려면 에디터를 설정한 다음(예를 들면, `export EDITOR=vim`) **ctrl-x** **ctrl-e**를 눌러 현재 명령을 에디터에서 열어 여러줄 편집을 할 수 있습니다. vi 스타일에서는 **escape-v**를 사용합니다.

- 최근 사용한 커맨드를 보려면 `history`를 입력하세요. 그 후 `!n`으로(여기서 `n`은 커맨드 번호를 뜻합니다) 다시 실행할 수 있습니다. `!$`(마지막 argument), `!!`(마지막 커맨드)와 같은 약어들이 매우 많습니다. 비록 이런 것들이 **ctrl-r**이나 **alt-.**명령어로 자주 대체되기 쉽지만요.

- `cd`로 홈 디렉터리로 갈 수 있습니다. 홈 디렉터리에서 상대적으로 파일을 접근하려면 `~` 접두사를 사용합니다(예: `~/.bashrc`). `sh` 스크립트에서는 `$HOME`로 홈 디렉터리를 참조합니다.

- 이전에 작업하던 디렉터리로 돌아가려면 `cd -`를 사용하세요.

- 커맨드를 타이핑하던 도중에 마음이 바뀌었다면, **alt-#**을 쳐서 시작점에 `#`을 삽입하고, 엔터를 쳐서 코멘트로 여겨지게 하세요(또는 **ctrl-a**, **#**, **enter**).  나중에 커맨드 히스토리에서 찾아서 타이핑 중이었던 커맨드로 돌아올 수 있습니다.

- `xargs`(혹은 `parallel`)를 사용하세요. 매우 강력합니다. 라인당 몇 개의 아이템이 실행되게 할 것인지(`-L`) 그걸 병렬로 할 것인지(`-P`)를 제어할 수 있다는 걸 기억하세요.  제대로 하고 있는지 확신할 수 없다면 `xargs echo`를 먼저 실행해보세요. 또 `-I{}`도 편리합니다. 예시:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p`는 프로세스 트리를 표시하는데 도움이 됩니다.

- `pgrep`과 `pkill`을 사용해서 프로세스를 찾거나 시그널을 보내세요(`-f`가 유용합니다).

- 프로세스에 보낼 수 있는 다양한 시그널을 알아두세요. 예를 들어, 프로세스를 일시 중지 할 때는 `kill -STOP [pid]`를 사용합니다. 전체 목록은 `man 7 signal`에서 볼 수 있습니다.

- 백그라운드 프로세스를 영원히 돌아가게 만들고 싶다면, `nohup`이나 `disown`을 사용하세요.

- 어떤 프로세스가 리스닝(역주: 특정 포트로 들어오는 패킷 리스닝)을 하고 있는지 알려면 `netstat -lntp`나 `ss -plat`을 사용해서 알 수 있습니다(TCP 일 경우입니다. UDP의 경우 `-u`옵션을 추가하세요).

- `lsof`를 이용해서 열려있는 소켓과 파일을 볼 수 있습니다.

- `uptime`이나 `w`를 이용해서 시스템이 얼마나 오래 실행 중인지 알 수 있습니다.

- 자주 사용되는 커맨드에 대해서 `alias`를 이용해서 숏컷을 만드세요. 예를들어, `alias ll='ls -latr'`은 새 단축 명령 `ll`을 만듭니다.

- 자주 사용하는 단축, 설정, 함수는 `~/.bashrc`에 저장하고, [그것을 참조하는 로그인 셸을 고쳐보세요](http://superuser.com/a/183980/7106). 이렇게 하면 설정을 모든 셸 세션에서 사용할 수 있습니다.

- 환경 변수 설정이나 로그인할 때 실행해야 할 명령은 `~/.bash_profile`에 넣으세요. 그래픽 환경의 로그인의 셸과 `cron` 잡의 셸을 분리하기 위해 설정을 분리할 필요가 있습니다.

- Git으로 여러 컴퓨터에서 같은 설정 파일을 사용하세요(예 `.bashrc`, `.bash_profile`).

- 공백이 들어간 변수명이나 파일명은 주의할 필요가 있습니다. Bash 변수를 따옴표로 감싸세요(예: `"$FOO"`). 파일 이름의 경계에 공백 문자를 허용하려면 `-0`이나 `-print0` 옵션을 사용하세요. 예를 들면, `locate -0 pattern | xargs -0 ls -al`, `find / -print0 -type d | xargs -0 ls -al`. for 문에서 공백문자가 포함된 파일 이름을 반복하려면, `IFS=$'\n'`로 IFS를 개행 문자만으로 설정하시면 됩니다.

- Bash 스크립트에서 `set -x`를 사용하면 디버깅용 출력을 사용하게 됩니다(아니면 다른 옵션  `set -v`가 있습니다. 확장되지 않은 변수와 주석을 포함한 로우 입력을 로깅합니다). 스트릭트 모드(strict mode)가 가능할 때면 사용하세요. `set -e`를 사용하면 에러가 났을 때 중단시키게 됩니다. `set -u`을 사용하면 설정되지 않은 변수를 찾아 줍니다. `set -o pipefail`을 사용하면 에러에 대해서 강경한 기준을 적용합니다(이 주제가 조금 미묘하지만 말이죠). 더 복잡한 스크립트의 경우 EXIT나 ERR에 `trap`도 사용합니다. 이렇게 스크립트를 시작하는 습관은 유용합니다. 이렇게 하면, 일반적인 에러를 찾고 중단하고, 메시지를 출력해 줍니다.
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- Bash 스크립트에서 (괄호로 둘러싸여 작성된) 서브 셸은 커맨드를 그룹으로 묶는 편리한 방법입니다. 일반적인 예로, 임시로 다른 디렉터리로 이동하여 작업하는 것이 있습니다.
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- Bash 에는 다양한 변수 확장이 있다는 것을 알아두세요. 변수가 존재하는지 확인하려면 `${name:?error message}`를 사용하세요. 예를 들어 Bash 스크립트가 하나의 argument를 요구한다면, `input_file=${1:?usage: $0 input_file}`를 사용하세요. 변수가 비어있을 때를 대비해 기본 값을 사용하세요. `${name:-default}` 이전 예제에 선택적인 파라미터를 추가하길 원한다면 `output_file=${2:-logfile}`로 할 수 있습니다. $2가 생략되어 비어있다면, `output_file`은 `logfile`로 설정됩니다. 산술 확장은 `i=$(( (i + 1) % 5 ))` 처럼 사용합니다. 순열은 `{1...10}`처럼 사용합니다. 문자열 트리밍(trimmin)은 `${var%suffix}`이나 `${var#prefix}`처럼 사용할 수 있습니다. 예를 들어 `var=foo.pdf`라면, `echo ${var$.pdf}.txt`는 `foo.txt`를 출력합니다.

- `{`...`}`를 사용한 괄호 확장은 비슷한 텍스트의 재입력을 줄이고, 아이템의 조합을 자동화할 수 있습니다. `mv foo.{txt,pdf} some-dir` (양쪽 파일들을 옮김), `cp somefile{,.bak}` (`cp somefile somefile.bak`로 확장), `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (모든 가능한 조합으로 확장해 디렉터리 트리를 생성) 같은 예제들은 유용합니다.

- 커맨드의 실행 결과 출력물은 `<(some command)`처럼 이용해서 파일처럼 다뤄질 수 있습니다. 예를 들어 로컬의 `/etc/hosts`를 리모트의 것과 비교하려면 다음처럼 하면 됩니다.
```bash
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- 스크립트를 적을 때 모든 코드를 대괄호 안에 넣을 수 있습니다. 닫는 괄호가 없으면 스크립트는 구문 에러가 되어 실행이 방지됩니다. 이는 스크립트가 웹으로부터 다운로드할 예정이라 할 때 도중까지만 다운로드된 파일이 실행 되는 걸 예방해 줍니다.
```sh
{
      # 여기에 코드를 넣으세요
}
```

- `cat << EOF...`같은 "here documents"에 대해서 알아두세요.

- Bash에서 표준 출력(standard output)과 표준 에러(standard error) 둘 다 `some-command > logfile 2>&1`같은 명령어로 리다이렉트할 수 있습니다. 종종, 커맨드가 열린 파일 핸들을 남기지 않는 것을 확실히 하기 위해, 현재 작업 중인 터미널에서 명령어에 `</dev/null`을 덧붙이는 것은 좋은 습관입니다.

- `man ascii`를 사용해서 헥스 값과 10진 값이 같이 있는 훌륭한 ASCII 테이블을 볼 수 있습니다. 일반적인 인코딩 정보를 보려면 `man unicode`, `man utf-8` 그리고 `man latin1`을 이용할 수 있습니다.

- `screen`을 이용하거나  [`tmux`](https://tmux.github.io/)를 이용해서 화면을 다중 분할할 수 있습니다. 특히 리모트 ssh 세션을 떼어내고(detach) 다시 붙이는데(re-attach) 유용합니다. `byobu`은 스크린이나 tmux보다 더 많은 정보를 제공하며, 관리를 편합니다. 세션을 영구히 유지하는 최소한의 대안은 오직 [`dtach`](https://github.com/bogner/dtach)밖에 없습니다.

- ssh에서 `-L`이나 `-D`(가끔 `-R`)를 이용해서 포트 터널링 하는 것을 알아두시면 유용합니다. 예를 들어 리모트 서버를 경유해서 웹사이트에 접속한다거나 할 때 말이죠.

- 몇 가지 ssh 설정을 최적화하는 것은 유용할 수 있습니다. 예를 들어 `~/.ssh/config`는 특정 네트워크 환경에서 연결이 끊기는 것을 회피하기 위해 압축을 사용하는 설정들을 담고 있습니다(특히 scp 명령어를 낮은 대역폭 연결에서 사용하는 경우에 도움이 됩니다. 그리고  로컬 제어 파일에서 같은 서버로 연결하는 채널을 다중화할 수 있습니다.
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

-  ssh의 몇 가지 옵션들은 보안에 민감한 옵션이며 주의를 가지고 사용되어야 합니다. 예를 들어 서브넷, 호스트 또는 신뢰되는 네트워크에서 `StrictHostKeyChecking=no`, `ForwardAgent=yes`을 사용하는 것 등입니다.

- UDP을 사용하는 ssh의 대안으로 [`mosh`](https://mosh.mit.edu/)를 고려해 보세요. 연결이 끊기는 것을 방지하고 길에 편리함이 더해집니다.(서버 사이드 설정 필요)

- 시스템 설정에 유용하지만 `ls`로 얻을 수 없고 쉽게 엉망이 되기 쉬운 파일의 권한을 8진법 형태로 얻으려면, 다음과 같은 커맨드를 사용하세요.
```sh
      stat -c '%A %a %n' /etc/timezone
```

- 다른 커맨드의 출력과 상호작용하면서 값을 선택하려면  [`percol`](https://github.com/mooz/percol)이나 [`fzf`](https://github.com/junegunn/fzf)를 사용하세요.

- 다른 커맨드(예를 들면 `git`)의 출력으로 파일과 상호작용하려면, `fpp` ([PathPicker](https://github.com/facebook/PathPicker))를 사용하세요.

- 현재 네트워크에 있는 사용자들에게 현재 디렉터리에 있는 모든 파일(과 하위 디렉터리)를 위한 단순한 웹서버를 원한다면 다음을 사용하세요:
`python -m SimpleHTTPServer 7777` (7777포트, Python 2) 그리고 `python -m http.server 7777` (7777포트, Python 3).

- 권한을 가지고 커맨드를 실행하려면, `sudo`를 사용하세요. 기본값은 root 실행하며 `sudo -u`로 다른 유저를 지정할 수 있습니다. `-i`를 이용해 다른 사람으로 로그인 할 수 있습니다.(_당신의_ 패스워드를 물어볼 것입니다)

- 셸을 다른 유저로 전환하려면 `su username`나 `su - username`를 사용하세요. `-`를 넣으면 그 유저가 방금 로그인한 것 같은 환경을 얻을 수 있습니다. 유저 이름을 생략하면 기본값은 root가 됩니다. _당신이 전환하려하는 유저의_ 비밀번호를 물어볼 것입니다.

- 커맨드 라인의 [128K 제한](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong)을 알아 두세요. "Argument list too long" 에러는 많은 파일을 와일드카드 매칭할 때 일반적으로 일어납니다. (이런 일이 일어났을 때에는 `find`, `xargs`같은 것이 도움 됩니다.)

- 단순한 계산에는(물론 일반적으로는 Python에 접근하기 위해) `python` 인터프리터를 사용하세요. 예를 들어 이렇게 사용할 수 있습니다.
```
>>> 2+3
5
```


## Processing files and data

- 현재 디렉터리에서 파일을 이름으로 찾으려면 `find . -iname '*something*'` (또는 비슷하게)를 사용하면 됩니다. 어느 곳에 있든 파일을 이름으로 찾으려면 `locate something`을 사용하세요(하지만 인내를 가져야 합니다. `updatedb`가 최근에 생성된 파일을 인덱싱하지 않았을 수 있습니다).

- 소스나 데이터 파일들에서 일반적인 검색을 할 때는(`grep -r`보다 더 복잡할 때), [`ag`](https://github.com/ggreer/the_silver_searcher)를 사용하세요.

- HTML을 텍스트로 변환할 때는 `lynx -dump -stdin`를 사용하세요.

- 마크다운, HTML, 그리고 모든 종류의 문서 변환에는 [`pandoc`](http://pandoc.org/)을 시도해보세요.

- XML을 반드시 다뤄야한다면, `xmlstarlet`을 사용하세요. 오래되었지만 좋습니다.

- JSON에는 [`jq`](http://stedolan.github.io/jq/)를 사용하세요.

- YAML에는 [`shyaml`](https://github.com/0k/shyaml)를 사용하세요.

- Excel이나 CSV파일에는 [csvkit](https://github.com/onyxfish/csvkit)가 `in2csv`, `csvcut`, `csvjoin`, `csvgrep`외 다른 도구들을 제공합니다.

- Amazon S3를 다룰 때는 [`s3cmd`](https://github.com/s3tools/s3cmd)가 편리합니다. 그리고 [`s4cmd`](https://github.com/bloomreach/s4cmd)는 빠릅니다. Amazon의  [`aws`](https://github.com/aws/aws-cli)는 다른 AWS 관련 작업에 핵심적인 도구입니다.

- `sort`와 `uniq`에 대해서 알아두세요. uniq의 `-u`, `-d`옵션을 포함해서 말이죠. 하단의 one-liner를 보세요. 그리고 `comm`도 보세요.

- 텍스트 파일들을 다루는 `cut`, `paste` 그리고 `join`에 대해서 알아두세요. 많은 사람들이 `cut`을 사용하지만 `join`에 대해서는 잊고 있습니다.

- `wc`를 이용해서 행(`-l`), 캐릭터(`-m`), 단어(`-w`) 그리고 바이트(`-c`)를 세는 것을 알아두세요.

- `tee`를 이용해서 `ls -al | tee file.txt`처럼, 표준 입력(stdin)에서 복사해서 파일로 보내거나, 표준 출력(stdout)으로 보내는 것을 알아두세요.

- 그룹, 필드 뒤집기, 통계적인 계산 같은 좀 더 복잡한 계산은 [`datamash`](https://www.gnu.org/software/datamash/)를 고려해보세요.

- 로케일이 커맨드 라인 도구에 정렬 순서(collation)와 퍼포먼스를 포함해서 미묘하게 영향을 끼치는 것을 알아두세요. 대부분의 리눅스 설치는 `LANG`이나 다른 로케일 변수를 US English와 같은 로컬 세팅으로 설정합니다. 하지만 로케일을 바꿀 경우 정렬도 바뀔 것이라는 것에 주의하세요. 그리고 i18n 루틴들도 정렬이나 다른 커맨드들을 *몇 배* 느리게 할 수 있습니다. `export LC_ALL=C`를 사용하여, 어떤 상황에서는( 밑에 있는 집합(set) 작업이나, 유일성 작업등) i18n의 느린 루틴들을 통째로 안전하게 무시할 수 있습니다. 그리고 전통적인 바이트 기반의 정렬 순서를 사용할 수 있습니다.

- `TZ=Pacific/Fiji date`처럼 특정 명령의 환경 변수를 실행 앞에 붙여 설정할 수 있습니다.

- 간단한 데이터 조작을 할 때 `awk`와 `sed`를 이용하는 것을 알아두세요. 예를 들어 텍스트 파일의 세 번째 열의 숫자들의 모든 값을 더하는 것은 이렇게 합니다: `awk '{ x += $3 } END { print x }'`. 이 방법은 같은 일을 하는 파이썬 코드보다 3배 정도 빠르고, 1/3 정도의 길이밖에 안됩니다.

- 여러 파일 안의 문자열을 바꾸려면 다음과 같이 하세요.
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- 여러 파일의 이름을 바꾸거나 검색하거나 문자열을 바꿀 때에는 [`repren`](https://github.com/jlevy/repren)를 써보세요. (어떤 경우에는 `rename` 명령을 사용해서 여러 파일의 이름을 바꿀 수도 있습니다. 하지만, 모든 리눅스 배포판에서 같은 동작을 하지 않는 것에 주의하세요.)
```sh
      # 파일 이름, 디렉터, 컨텐츠 모두 foo에서 bar로 변경
      repren --full --preserve-case --from foo --to bar .
      # 백업 파일을 whatever.bak에서 whatever로 복원
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # 가능하다면 rename으로 위와 같은 일을 할 수 있음
      rename 's/\.bak$//' *.bak
```

- man 페이지가 이야기하듯, `rsync`는 정말 빠르고 다재다능한 파일 복사 도구입니다. 기기 간의 동기화에 사용하는 것으로 알려져 있지만, 로컬에서도 충분히 유용합니다. 보안 규정이 허용한다면, `scp` 대신 `rsync`를 사용하면 처음부터 전송하는 대신 중단된 지점부터 재전송할 수 있습니다. 또 많은 수의 파일을 삭제하는 [가장 빠른 방법](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html)이기도 합니다.
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- `shuf`를 사용해서 파일 안의 임의의 행을 선택하거나, 섞을 수 있습니다.

- `sort`의 옵션을 알아두세요. `-n`은 숫자를 정렬할 때, `-h`는 사람이 읽을 수 있게 작성한 숫자의 경우(`du -h`와 같은 형태). 키가 어떻게 작동하는지 알아두세요(`-t`와 `-k`). 특별히, 첫 번째 필드로만 정렬해야 한다면 `-k1,1`을 적어야 한다는 걸 주의하세요. `-k1`은 모든 행에 대해서 정렬하라는 뜻입니다.  안정적인 정렬(`sort -s`)도 유용합니다. 예를 들어, 먼저 2번 필드로 정렬하고, 그다음에 1번 필드로 정렬할 경우, `sort -k1,1 | sort -s -k2,2`처럼 할 수 있습니다.

- 만약 탭(tab)문자를 Bash 커맨드 라인에 사용해야 할 필요가 생길 경우(예를 들면 -t argument를 이용해 정렬 할 때), **ctrl-v** **[Tab]**키를 누르거나, `$'\t'`를 쓰세요(문자쪽이 복사나 붙여넣기를 할 수 있어 더 낫습니다.).

- 소스 코드를 패치하는 기본 도구는 `diff`와 `patch`입니다. diff와 `sdiff`(새로 diff)의 통계 요약을 보려면 `diffstat`를 보세요. `diff -r`은 모든 디렉터리에 대해 작업을 수행하는 걸 알아두세요. `diff -r tree1 tree2 | diffstat`으로 변경 내역의 요약을 볼 수 있습니다.

- 바이너리 파일을 간단하게 hex 덤프를 뜨고 싶을 때는 `hd`, `hexdump`, `xxd`를 쓰세요. 바이너리 파일을 수정할 때는 `bvi`, `biew`를 사용하세요.

- `strings` (그리고 `grep`, 등) 을 사용해서 바이너리 파일 안에서 문자열 비트를 찾을 수 있습니다.

- 바이너리 파일을 diff하려면(델타 압축), `xdelta3`를 사용하세요.

- 텍스트 파일 인코딩을 변경하려면 `iconv`를 시도해보세요. 또는 `uconv`는 더 복잡한 목적에 사용할 수 있습니다. `uconv`는 몇 가지 복잡한 유니코드를 지원합니다. 예를 들어, 소문자화하고 모든 악센트를 제거하는(확장하고, 떨어트리는 것을 이용해서) 커맨드는 다음과 같습니다.
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- 파일을 여러 조각으로 나누려면 `split`(파일을 사이즈로 나눔)이나 `csplit`(파일을 패턴으로 나눔)을 보세요.

- 날짜 시간 표현식을 제어하려면 [`dateutils`](http://www.fresse.org/dateutils/)의 `dateadd`, `datediff`, `strptime`등을 사용하세요.

- `zless`, `zmore`, `zcat` 그리고`zgrep`을 이용해서 압축된 파일에 대해 작업하세요.

- 파일 속성은 `chattr`로 설정할 수 있습니다. 이는 파일 권한에 대한 저레벨 대안입니다. 예를 들어 `sudo chattr +i /critical/directory/or/file`로 불변 플래그를 붙여 실수로 파일을 지우는 것을 방지할 수 있습니다.

- `getfacl`, `setfacl`를 사용해 파일 권한을 저장하고 복원할 수 있습니다. 예를 들어,
```sh
   getfacl -R /some/path > permissions.txt
   setfacl --restore=permissions.txt
```

## System debugging

- 웹 디버깅을 위해서는 `curl` 와 `curl -I` 가 도움이 되고, `wget`도 꽤 도움이 됩니다. 그 외에 보다 현대적인 방식으로는 [`httpie`](https://github.com/jakubroztocil/httpie)이 있습니다.

- cpu/디스크의 상태를 알기 위해서는 `top` (혹은 더 나은 명령어인 `htop`), `iostat`, `iotop`을 사용하세요. `iostat -mxz 15`를 사용해 기본 CPU와 파티션 디스크별 정보와 성능 정보를 알 수 있습니다.

- 네트워크 상태를 자세히 알려면 `netstat`, `ss`를 사용하세요.

- 시스템에 어떤 일이 일어났는지 보려면 `dstat`가 특히 유용합니다. 보다 시스템의 심층적인 면들을 보려면 [`glances`](https://github.com/nicolargo/glances)를 사용해보세요.

- 메모리의 상태를 알아보려면 `free` 와 `vmstat`를 실행하고 그 결과를 해석해보세요. 특히, "cached" 값은 Linux kernel에 의해 file cache로 잡혀있는 메모리 라는 것을 알고 있어야 하고 그래서 "free"값에 대해서 보다 효율적으로 계산할 수 있습니다.

- Java 시스템의 디버깅은 조금 다른 상황입니다. 하지만 Oracle과 그 외의 회사에서 만든 다른 JVM들에서는 `kill -3 <pid>`를 실행하면 전체 stack trace 정보와 heap의 정보(시기별로 가비지 컬렉터의 세부적인 내용 같은 매우 유용한 정보)를 요약하여 stderr나 로그로 출력해주므로 간단하게 정보를 얻어올 수 있습니다. JDK의 `jps`, `jstat`, `jstack`, `jmap` 명령은 유용합니다. [SJK tools](https://github.com/aragozin/jvm-tools)은 더 고급 정보를 다룰 수 있습니다.

- 네트워크 이슈들을 알아보기 위해서는 traceroute를 사용할 수도 있지만 더 좋은 [`mtr`](http://www.bitwizard.nl/mtr/)를 사용하세요.

- 디스크가 왜 가득 찼는지 알아보기 위해서 [`ncdu`](https://dev.yorhel.nl/ncdu)를 사용해보세요.  일반적으로 사용하는 `du -sh *`와 같은 커맨드를 사용하는 것보다는 시간을 줄일 수 있습니다.

- 어떠한 소켓이나 프로세스가 사용하는 대역폭(bandwidth)를 찾아보려면 [`iftop`](http://www.ex-parrot.com/~pdw/iftop/)나 [`nethogs`](https://github.com/raboof/nethogs)를 사용하세요.

- `ab`라는 툴(Apache에 딸려있는)은 신속하고 간단하게(quick-and-dirty) 웹서버의 성능을 체크하는데 유용합니다. 보다 복잡한 부하 테스트를 할 때는 `siege`를 사용해보세요.

- 보다 심각한 경우의 네트워크 디버깅을 위해서는 [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html), [`ngrep`](http://ngrep.sourceforge.net/)를 사용하세요.

- `strace` 와 `ltrace`에 대해서 알아보세요. 이 커맨드들은 만일 어떤 프로그램에서 failing, hanging 혹은 crashing이 일어나거나 그 외에 여러분이 무슨 이유인지 알지 못하는 상황이나 성능에 대한 대략적인 내용을 얻고자 할 때 유용할 것입니다. 특히 프로파일링을 위한 옵션(`-c`)과 현재 실행 중인 프로세스에 붙이기 위한 옵션(`-p`)을 기억하세요.

- 공유 라이브러리(shared libraries) 등을 체크하기 위해서는 `ldd`에 대해 알아보세요.

- `gdb`를 가지고 현재 실행 중인 프로세스에 연결하고 그 프로세스의 stack trace들을 얻는 방법을 알아보세요.

- `/proc`를 사용하세요. 이것은 현재 발생하고 있는 문제를 디버깅할 때 종종 놀랍도록 큰 도움이 될 것입니다. 예시:`/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (`xxx`는 프로세스 id나 pid입니다).

- 과거에 왜 무엇인가가 잘못되었는지를 디버깅할 때에는 [`sar`](http://sebastien.godard.pagesperso-orange.fr/)가 매우 유용할 것입니다. 이 커맨드는 CPU, memory, network 등의 통계 내역을 보여줍니다.

- 시스템의 보다 깊은 곳을 보거나 퍼포먼스를 분석하기 위해서는, `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](http://en.wikipedia.org/wiki/Perf_(Linux)), [`sysdig`](https://github.com/draios/sysdig)를 사용해보세요.

- 여러분이 사용하는 Linux의 배포판이 무엇인지 확인(대부분의 배포판에서 작동합니다)하려면 `uname`이나 `uname -a` 또는 `lsb_release -a`를 사용하세요.

- 언제든지 무언가가 정말로 재미있는 반응을 보인다면 `dmesg`를 사용해보세요(아마도 하드웨어나 드라이버의 문제일 것입니다).

- 파일을 삭제했는데 `du`로 확인해 예상한 디스크 공간을 확보하지 못했다면, 파일이 프로세스에 의해 사용 중인지 확인해보세요.
`lsof | grep deleted | grep "filename-of-my-big-file"`


## One-liners

커맨드들을 한데 묶어서 사용하는 예제들

- `sort`/`uniq`를 사용하여 텍스트 파일의 교차점, 조합, 차이점을 확인이 필요할 때 상당한 도움이 될 겁니다. 가령 `a`와 `b`가 유일한 값들만을 가진 텍스트 파일이라 합시다. 이것이 임의의 크기인 파일을(그게 기가바이트라고 해도) 빠르게 작업할 수 있습니다. (Sort는 메모리 제한에 걸리지 않습니다만, 만약 루트 파티션이 작은 경우, `/tmp`를 사용하기 위해 `-T`옵션을 사용하면 됩니다.) 위의 `LC_ALL`에대한 내용은 `sort`의 `-u`옵션을 확인하십시오. (아래 예제에 집중하기 위해서 생략)
```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- `grep . *`을 사용해서 디렉터리 안의 모든 파일을 비주얼하게 살펴볼 수 있습니다.(r각 줄은 파일 이름과 같이 나옵니다) 아니면 `head -100 *`를 이용할 수도 있습니다.(각 파일의 해더만 볼 수 있습니다.) 이는 `/sys`, `/proc`, `/etc` 같이 설정값들로 가득한 디렉터리에서 유용합니다.


- 텍스트 파일의 세 번째 열의 숫자들의 모든 값을 더하는 것은 이렇게 합니다. 이 방법은 같은 일을 하는 파이썬 코드보다 3배 정도 빠르고, 1/3 정도의 길이밖에 안됩니다.
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- 파일 트리에서 크기와 날짜를 보려면 이렇게 하세요. 이 명령어는 `ls -l`을 재귀적으로 수행하는 것과 같지만, `ls -lR`보다 더 읽기 쉽습니다.
```sh
      find . -type f -ls
```

- 웹서버 로그 같은 텍스트 파일이 있다고 합시다. 그리고 URL 파라미터에 나타나는 `acct_id`같은 특정 값이 몇몇 행에 나타난다고 해보죠. 각각의 `acct_id`에 대해 얼마나 많은 요청이 있었는지 알고 싶다면 다음처럼 할 수 있습니다.
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- 변경을 계속 모니터링하려면 `watch`를 이용하세요. 예를 들어 `watch -d -n 2 'ls -rtlh | tail'`로 한 디렉터리 내의 파일 변경을 확인하거나, `watch -d -n 2 ifconfig`로 와이파이 설정을 고칠 때 네트워크 설정 변경을 확인할 수 있습니다.

- 다음 함수를 실행하면 이 문서에 있는 팁 중 임의의 것을 얻을 수 있습니다(마크다운을 파싱하고 항목을 추출합니다).
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

- `cut `, `paste`, `join`: 데이터를 수정할때 사용합니다

- `fmt`: 문단의 서식을 지정합니다

- `pr`: 문서의 페이지나 컬럼 서식을 지정합니다

- `fold`: 문서의 각 라인들을 특정한 길이에 맞게 수정합니다

- `column`: 문서의 컬럼이나 테이블의 서식을 지정합니다

- `expand`, `unexpand`: 탭을 공백으로 바꾸어주거나 공백을 탭으로 바꾸어줍니다

- `nl`: 줄 번호를 추가해줍니다

- `seq`: 숫자들을 출력하는데 사용합니다

- `bc`: 간단한 계산기를 실행합니다

- `factor`: 정수들을 인수분해하는데 사용합니다

- [`gpg`](https://gnupg.org/): 파일들을 암호화하고 서명하는데 사용합니다

- `toe`: terminfo 엔트리들의 테이블(table of terminfo entries)

- `nc`: 네트워크를 디버깅하거나 데이터를 전송할 때 사용합니다

- `socat`: 소켓 릴레이나 TCP 포트로 내용을 전달할 때 사용합니다(`netcat`과 비슷합니다)

- [`slurm`](https://github.com/mattthias/slurm): 네트워크 상황을 시각화하여 보여줍니다

- `dd`: 파일들이나 디바이스들 간에 데이터를 옮길때 사용합니다

- `file`: 파일의 종류를 알아내는데 사용합니다

- `tree`: 디렉터리들과 그 하위 디렉터리를 마치 ls를 반복적으로 입력한 것처럼 트리의 형태로 보여줍니다

- `stat`: 파일의 정보를 보여줍니다

- `time`: 명령을 실행하고 시간을 잽니다

- `timeout`: 특정 시간만큼 명령을 실행하고 시간이 끝나면 프로세스를 종료합니다.

- `lockfile`: `rm -f`로만 지울 수 있는 세마포어 파일을 생성합니다

- `logrotate`: 로그를 로테이트, 압축, 메일로 보냅니다

- `watch`: 명령을 반복적으로 실행해 결과를 보여주거나 변경을 하일라이트합니다

- `tac`: 파일의 내용을 역순으로 출력합니다

- `shuf`: 파일의 각 줄들을 임의의 순서로 출력합니다

- `comm`: 정렬된 파일들을 각 라인별로 비교합니다

- `pv`: 파이프를 통해서 프로세스의 정보를 모니터링하는데 사용합니다

- `hd` and `bvi`: 바이너리 파일을 수정하거나 덤프를 얻어오는데 사용합니다

- `strings`: 바이너리 파일들에서 특정 문장을 추출하는데 사용합니다

- `tr`: 문자를 변환하거나 조작하는데 사용합니다

- `iconv` or `uconv`: 문서의 인코딩방식을 변환하는데 사용합니다

- `split `and `csplit`: 파일들을 쪼개는데 사용합니다

- `sponge`: 쓰기 전에 모든 입력을 읽습니다. 같은 파일에서 읽은 후에 쓰기에 유용합니다. 예를 들면 `grep -v something some-file | sponge some-file`처럼 사용할 수 있습니다.

- `units`: 단위를 변환하거나 계산하는데 사용합니다 예를들어 furlongs/fortnight 단위를 twips/blink로 변환합니다 (`/usr/share/units/definitions.units`를 참고하세요)

- `apg`: 렌덤 패스워드를 생성합니다

- `xz`: 고효율의 파일 압축프로그램입니다

- `ldd`: 동적 라이브러리들의 정보를 보여줍니다

- `nm`: 오브젝트 파일들에 포함된 심볼정보를 얻어옵니다

- `ab`: 웹 서버를 벤치 마킹하는데 사용합니다

- `strace`: 시스템 콜을 디버깅할때 사용합니다

- [`mtr`](http://www.bitwizard.nl/mtr/): 네트워크 디버깅시에 traceroute보다 더 낫습니다

- `cssh`: 쉘을 동시에 여러개 사용할때 사용합니다

- `rsync`: SSH를 이용해 원격 파일 시스템이나, 로컬 파일시스템의 파일과 폴더들을 동기화 할때 사용합니다

- [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): 패킷정보를 가져오며 네트워킹을 디버깅하는데 사용합니다

- [`ngrep`](http://ngrep.sourceforge.net/): 네트워크 환경에서 grep과 같은 역할을 합니다

- `host`, `dig`: DNS 정보를 보여줍니다

- `lsof`: 프로세스 파일 디스크립터와 소켓의 정보를 보여줍니다

- `dstat`: 유용한 시스템 정보를 보여줍니다

- [`glances`](https://github.com/nicolargo/glances): 보다 고차원의 여러 서브시스템들의 정보를 한번에 보여줍니다

- `iostat`: 디스크의 사용량 정보를 보여줍니다

- `mpstat`: CPU 사용량 정보를 보여줍니다.

- `vmstat`: 메모리 사용량 정보를 보여줍니다.

- `htop`: 보다 개선된 형태의 top을 보여줍니다

- `last`: 로그인 했던 정보들을 보여줍니다

- `w`: 현재 누가 로그인했는지 보여줍니다

- `id`: 현재 유저나 그룹에 대한 식별 정보를 보여줍니다

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): 시스템 상태에 대한 정보를 보여줍니다

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/), [`nethogs`](https://github.com/raboof/nethogs): 소켓 또는 프로세스를 이용하여 네트워크를 정보를 보여줍니다

- `ss`: 소켓에 관한 통계자료들을 보여줍니다

- `dmesg`: 부팅 메시지와 시스템 에러 메시지들을 보여줍니다

- `sysctl`: 실행 시에 리눅스 커널 파라미터를 보여주거나 설정합니다

- `hdparm`: SATA/ATA disk들의 정보를 수정하거나 그것들이 작동하도록 합니다

- `lsblk`: 블록 디바이스들의 목록을 보여줍니다 : 여러분의 디스크들이나 디스크파티션들을 트리의 형태로 보여줍니다

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: CPU, BIOS, RAID, graphics, devices 등의 하드웨어 정보를 보여줍니다

- `lsmod`, `modifno`: 커널 모듈의 상세정보를 목록으로 보여줍니다.

- `fortune`, `ddate`, `sl`: 에... 증기기관차를 생각하고있고 그것을 인용하고 싶다면 이것은 "유용"합니다


## macOS only

*OS X에서만* 해당되는 항목입니다.

- `brew` (Homebrew)나 `port` (MacPorts)를 패키지 매니저로 사용합니다. 위의 많은 명령어를 OS X에 설치하여 사용할 수 있습니다.

- `pbcopy`를 이용하여 데스크톱 애플리케이션에 명령어 출력물을 복사하거나 `pbpaste`를 이용해 붙여넣기를 할 수 있습니다.

- OS X 터미널에서 옵션 키를 알트 키(**alt-b**, **alt-f** 같은 위에 나온 명령)로 사용하려면 Preferences -> Profiles -> Keyboard를 열어 "Use Option as Meta key"를 선택하세요.

- 데스크톱 애플리케이션에서 파일을 열기위해, `open` 또는 `open -a /Applications/Whatever.app`을 사용하면 됩니다.

- Spotlight: `mdfind`를 이용해 파일을 찾고, `mdls`를 이용해 메타데이타 (사진 EXIF 정보와 같은) 목록을 볼 수 있습니다.

- OS X는 BSD Unix 기반이며 많은 명령어들을 (예로 `ps`, `ls`, `tail`, `awk`, `sed`) 사용할 수 있으며, 이것들은 Linux 버전들과 미묘한 차이가 있습니다. 그리고 크게는 System V-style Unix와 GNU 도구들에 많은 영향을 받았습니다. 이런 내용들을 man 페이지 상단의 "BSD General Commands Manual." 라는 문구를 통해 알 수 있습니다. 가끔은 GNU 버전이 설치되기도 합니다. (예로, GNU awk와 sed인 `gawk`와 `gsed`에서). 만약 이종 플랫폼 간 Bash 스크립트를 작성하려면, 동일한 명령어 (예로, 파이썬이나 `perl`과 같은)나 테스트시 주의해야 합니다.

- OS X 릴리스 정보를 얻으시려면, `sw_vers`를 사용하세요.

## Windows only

Windows*에서만* 해당되는 항목입니다.

- Windows 10에서는 [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about)를 사용할 수 있습니다. 이는 유닉스 커맨드 라인 도구와 함께 친숙한 Bash 환경을 제공합니다. 좋은 점은, 리눅스 프로그램을 Windows에서 사용할 수있게 합니다. 하지만 Bash에서 Windows 프로그램을 사용할 수는 없습니다.

- [Cygwin](https://cygwin.com/)를 설치해 Microsoft Windows에서 유닉스 셸을 사용할 수 있습니다. 이 문서에 기술된 대부분의 것들은 그대로 동작할 것입니다.

- Cygwin의 패키지 매니저로 유닉스 프로그램을 더 설치할 수 있습니다.

- 커맨드 라인 창으로 `mintty`를 사용하세요.

- Windows의 클립보드를 `/dev/clipboard`로 접근할 수 있습니다.

- `cygstart`을 실행해 등록된 애플리케이션을 사용해 임의의 파일을 열 수 있습니다.

- Windows 레지스트리는 `regtool`로 접근할 수 있습니다.

- `C:\\` Windows 드라이브 경로는 Cygwin에서는 `/cygdrive/c`가 되고, Cygwin의 `/` Windows에서 `C:\cygwin`가 되는것을 알아 두세요. Cygwin과 Windows 스타일의 파일 패스는 `cygpath`로 변환할 수 있습니다. 이는 Windows 프로그램을 실행하는 프로그램에서 유용하게 사용됩니다.

- You can perform and script most Windows system administration tasks from the command line by learning and using `wmic`.

- Windows에서 유닉스 룩엔필을 얻는 다른 대안은 [Cash](https://github.com/dthree/cash)입니다. 이 환경에는 매우 적은 유닉스 명령과 커맨드 라인 옵션만 사용가능하니 주의하세요.

- Windows에서 GNU 개발자 툴(GCC같은)을 얻는 다른 대안으로 [MinGW](http://www.mingw.org/)와 거기에 포함된 [MSYS](http://www.mingw.org/wiki/msys) 패키지가 있습니다. 여기에는 bash, gawk, make, grep같은 도구가 포함됩니다. MSYS는 Cygwin에 비교하면 모든 기능은 없습니다. MinGW는 유닉스 툴을 네이티브 Windows로 포팅할 때 부분적으로 유용합니다.

## More resources

- [awesome-shell](https://github.com/alebcay/awesome-shell): 셸에 대한 툴과 리소스들이 잘 정리되어 있는 리스트입니다.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): OS X 커맨드 라인에 관해 더 깊이 알수 있는 가이드 입니다.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/): 보다 나은 셸 스크립트를 작성하기 위한 정보글입니다.
- [shellcheck](https://github.com/koalaman/shellcheck): 셸 스크립트 정적 분석 도구 입니다. 특히, bash/sh/zsh에 대한 린트입니다.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): 셸 스크립트에서 파일 이름을 처리하는 법을 다루는 슬프도록 복잡한 미니츄어입니다.
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools): 같은 이름의 책에서 나온, 데이터 사이언스를 위한 더 나은 명령과 도구들 입니다.


## Disclaimer

매우 작은 작업을 제외한 코드들은 다른 사람이 읽을 수 있도록 작성됩니다. 큰 힘에는 책임이 따릅니다. Bash에서 뭔가를 *할 수 있다는* 것은 Bash로 해야 된다는 의미가 아닙니다! ;)


## License

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

이 저작물은 [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/)에 따라 이용할 수 있습니다.
