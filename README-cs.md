[ Languages:
[English](README.md), [Español](README-es.md), [Italiano](README-it.md), [日本語](README-ja.md), [한국어](README-ko.md), [Português](README-pt.md), [Русский](README-ru.md), [Slovenščina](README-sl.md), [Українська](README-uk.md), [中文](README-zh.md), [Czech](README-cs.md)
]


# Umění příkazové řádky

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Meta](#meta)
- [Základy](#zaklady)
- [Každodenní použití](#kazdodenni-pouziti)
- [Zpracování souborů a dat](#zpracovani-souboru-a-dat)
- [Ladění systému](#ladeni-systemu)
- [Jednořádkové příkazy](#jednoradkove-prikazy)
- [Neobvyklé ale užitečné](#neobvykle-ale-uzitecne)
- [Pouze pro OS X](#pouze-pro-os-x)
- [Další zdroje](#dalsi-zdroje)
- [Zřeknutí se odpovědnosti](#zreknuti-se-odpovednosti)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)
Plynulost práce na příkazové řádce je umění často opomíjené nebo považované za překonané, ale zlepšuje vaši flexibilitu a produktivitu jako inženýr jak očividně tak nenápadně. Toto je výběr poznámek a tipů pro použití příkazové řádky které shledáváme užitečnými při práci na Linuxu. Některé tipy jsou základní a některé jsou velmi specifické, komplikované či nejasné. Tato stránka není dlouhá, ale pokud dokážete použít a vybavit si všechny věci zde zmíněné, máte rozsáhlé dostatečné vědomosti.

Tato práce je výsledkem [mnoha autorů a překladatelů](AUTHORS.md).
Mnoho se 
[původně](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[objevilo](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
na webu [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
ale s ohledem na zájem, který tam panoval, se zdálo vhodné použít GitHub, kde lidé více talentovaní než původní autor mohli okamžitě navrhovat zlepšení. Pokud najdete chybu či něco, co by mohlo být vylepšeno, prosím vytvořte issue nebo pull request! (Samozřejmě nejdříve zkontrolujte meta sekci a existující pull requesty a issues.)


## Meta

Rozsah:

- Tento průvodce je pro začátečníky i pro pokročilé. Cílem je *široký záběr* (vše důležité), *specifičnost* (poskytnout konkrétní příklady nejčastějšího použití) a *stručnost* (vyhnout se věcem, které nejsou nezbytné nebo podobným tématům, které lze vyhledat jinde). Každý tip je v některých případech nenahraditelný nebo značně šetří čas oproti alternativám.
- Tento dokument je napsán pro Linux s vyjímkou sekcí označených jako "[Pouze pro OS X](#os-x-only)". Mnoho ostatních položek lze použít nebo je lze nainstalovat na jiných Unixových systémech nebo MacOS (dokonce i na Cygwin).
- Zaměření dokumentu je na inteaktivní Bash ačkoli mnoho tipů lze aplikovat na jiné shelly a obecné bashové scriptování.
. Jsou zahrnuty jak "standardní" Unixové příkazy tak příkazy vyžadující instalaci extra balíčků -- pokud jsou dost důležité aby zasloužily zmínku.

Poznámky:

- Pro udržení délky textu na jednu stranu, obsah je implicitně obsažen v odkazech. Jste dostatečně inteligentní aby jste si vyhledali více detailů z jiných zdrojů jakmile znáte příkaz či myšlenku na Googlu. Použijte `apt-get`/`yum`/`dnf`/`pacman`/`pip`/`brew` podle distribuce k instalaci nových progamů.
- Použijte [Explainshell](http://explainshell.com/) pro užitečné vysvětlení co příkazy, možnosti, roury a jiné dělají.


## Zaklady

- Naučte se základy Bashe. Vlastně, napište `man bash` a alespoň si to proleťte; je to celkem jednoduché a ne tak dlouhé. Jiné shelly mohou být dobré, ale Bash je mocný a vždy dostupný (znalost *pouze* zsh, fish a jiných ačkoli lákavá na vlastním notebooku omezuje v mnoha situacích, jako například při použití existujících serverů).

- Poznejte alespoň jeden textový editor dobře. Nejlépe Vím (`vi`) jelikož opravdu nemá pro občasné úpravy v terminálu nemá konkurenci (ani pokud většinu času používáte Emacs, velké IDE nebo moderní okenní editor).

- Naučte se číst dokumentaci pomocí `man` (pro zvědavce, `man man` vypíše čísla sekcí, například 1 jsou "obvyklé" příkazy, 5 jsou soubory/konvence a 8 je administrace). Hledejte manuálové stránky pomocí `apropos`. Vězte, že některé příkazy nejsou spustitelné programy, ale funkce zabudované v Bashi a nápovědu k nim můžete zobrazit příkazem `help` a `help-d`.

- Naučte se přesměrování výstupu a vstupu pomocí `>` a `<` a roury pomocí `|`. Pamatujte, že `>` přepíše obsah výstupního souboru a `>>` přidá na jeho konec. Nezapomeňte na stdout (stndardní výstup) a stderr (standardní chybový výstup).

- Poznejte souborovou hromadnou expanzi za pomoci `*` (případně `?` a `[`...`]`) a úvozovkách a rozdílu mezi dvojitými uvozovkami `"` a jednoduchými `'`. (Více na expanzi proměných níže.)

- Seznamte se se správou činností v Bashi: `&`, **ctrl-z**, ctrl-c**, `jobs`, `fg`, `bg`, `kill`, atd.

- Seznamte se s `ssh` a základy bezheslové autentizace pomocí `ssh-agent`, `ssh-add`, atd.

- Základní správa souborů: `ls` a `ls -l` (zejména co který sloupec v `ls -l` znamená), `less`, `head`, `tail` a `tail -f` (nebo ještě lépe `less +F`), `ln` a `ln -s` (pochopte rozdíly a výhody pevného odkazu a symoblického odkazu), `chown`, `chmod`, `du` (pro krátký souhrn využití disku: `du -hs *`). Pro správu souborového systému, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. Pochopte co je inode (`ls -i` nebo `df -i`).

- základní správa síťí: `ip` nebo `ifconfig`, `dig`.

- Dobře se naučte regulárních výrazů a rozličné příznaky pro `grep`/`egrep`. Přepínače `-i`, `-o`, `-v`, `-A`, `-B` a `-C` je také vhodné znát.

- Naučte se používat `apt-get`, `yum`, `dnf` nebo `pacman` (podle vaší distribuce) k hledání a instalaci balíků. A ujistěte se, že máte `pip` k instalace Pythonových terminálových nástrojů (některé je nejjednodušší nainstalovat pomocí `pip`).


## Kazdodenni pouziti

- V Bashi používejte **Tab** k dokončení argumentů nebo vylistování všech dostupných příkazů a **ctrl-r** k vyhledávání v historii příkazů (po stisknutí pište pro hledání a poté mačkejte opakovaně **ctrl-r** k procházení více shod, **Enter** k provedení nalezeného příkazu nebo šipku vpravo pro vložení výsledku hledání do terminálu a následnou editaci).

- V Bashi používejte **ctrl-w** pro smazní posledního slova a **ctrl-u** pro smazání všeho od současné pozice kurzoru až po začátek řádku. POužívejte **alt-b** a **alt-f** k procházení řádku po slovech, **ctrl-a** pro skok na začátek řádku, **ctrl-e** pro skok kurzoru na konec řádku, **ctrl-k** pro smazání všeho od současné pozice až ke konci řádku, **ctrl-l** pro vyčištění obrazovky. Prohlédněte si `man readline` pro všechny defaultní klávesové zkratky v Bashi. Je jich hodně. Například **alt-.** projíždí předchozí argumenty a **alt-*** rozšíří řetězec.

- Pokud milujete klávesové zkratky ve stylu vi, použijte `set -o vi` (a `set -o emacs` pro návrat ke standardnímu rozložení).

- Pro úpravu dlouhých příkazů, po nastavení vašeho editoru (například `export EDITOR=vim`), **ctrl-x** **ctrl-e** otevře stávající příkaz v editoru pro víceřádkovou úpravu. Nebo ve vi stylu, **escape-v**.

- Zobrazení nedávných příkazů se provádí pomocí `history`. Existuje spousta zkratek jako `!$` (poslední argument) a `!!` (poslední příkaz), ale tyto jsou jednoduše nahraditelné pomocí **ctrl-r** a **alt-.**.

- Pro přechod do předchozího pracovního adresáře: `cd -`.

- Pokud máte zpola napsaný příkaz, ale rozmyslíte si to, stiskněte **alt-#** pro přidání `#` na začátek řádku a vložte ho jako komentář (nebo použijte **ctrl-a**, **#**, **enter**). Takto se k němu můžete později vrátit v historii příkazů.

- Používejte  `xargs` (nebo `parallel`). Jde o mocný příkaz. Nezapomeňte, že můžete ovládat kolik položek vykonat na řádku (`-L`) stejně jako paralelismus (`-P`). Pokud si nejste jisti zda to udělá co má, zkuste nejdříve `xargs echo`. Hodí se také `-I{}`.
Příklady:
```bash
      find . -name '*.py' | xargs grep nejaka_funkce
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` je užitečné zobrazení stromu procesů.

- Používejte `pgrep` a `pkill` k hledání nebo posílání signálů procesům podle jména. (`-f` je také užitečné).

- Pamatujte si rozličné signály, které lze posílat procesům. Například, k pozastavení procesu, použijte `kill -STOP [pid]`. Celý seznam signálů v `man 7 signal`.

- Používejte `nohup` nebo `disown` pokud chcete aby proces na pozadí běžel navždy.

- Kontrolujte, které procesy naslouchají pomocí `netstat -lntp` nebo `ss -plat` (pro TCP; přidejte `-u` pro UDP).

- Podívejte se také na `lsof` pro otevřené sockety a soubory.

- Jak dlouho systém běží poznáte díky `uptime` nebo `w`.

- Pomocí `alias` si nastavte zkratky pro často používané příkazy. Například `alias ll='ls -latr'` vytvoří novou zkratku `ll`.

- V Bashových scriptech používejte `set -x` (nebo jeho variantu `set -v`, která zaznamenává nezpracovaný vstup včetně nečekaných proměnných a komentářů) pro ladící výstup. Používejte přísné módy pokud nemáte dobrý důvod proč to tak nedělat: Příkazem `set -e` nastavíte přerušení při chybě (nenulový návratový kód). Použijte `set -u` pro zjištění použití neinicializovaných proměnných. Zvažte také `set -o pipefail` pro chyby v rourách (přečtěte si na tohle téma více pokud tuto možnost využijete, jelikož jde o citlivé téma). Pro více zapojených scriptů použijte `trap` na EXIT nebo ERR. Dobrým zvykem bývá začínat scripty takto, což zachytí a ukončí běh na běžných chybách a vypíše zprávu:
```bash
      set -euo pipefail
      trap "echo 'error: Script selhal: neuspesny prikaz vyse'" ERR
```

- V Bash scriptech jsou subshelly (psané s kulatými závorkami) vhodným způsobem shlukování příkazů. Běžným příkladem budiž dočasný přesun do jiného pracovního adresáře, například: 
```bash
      # udelej neco v soucasnem pracovnim adresari
      (cd /nejaky/jiny/adresar && jiny-prikaz)
      # pokracuj v puvodnim adresari
```

- Nezapomeňte, že v Bashi je mnoho druhů expanze proměnných. KOntrola, že proměnná existuje `${jmeno:?chybova hlaska}`. například, pokud script vyžaduje jediný argument, napište `vstupni_soubor=${1:?pouziti: $0 vstupni_soubor}`. Aritmetická expanze: `i=$(( (i + 1) % 5 ))`. Sekvence: `{1..10}`. Ořezání (trimming) řetězců: `${var%suffix}` a `${var#prefix}`. Pokud například `var=foo.pdf`, pak `echo ${var%.pdf}.txt` zobrazí `foo.txt`.

- Expanze složených závorek použitím `{`...`}` může snížit potřebu přepisovat podobné texty a zautomatizovat kombinaci položek. Toto může být užitečné například v `mv foo.{txt,pdf} nejaky-adresar` (což přesune oba soubory), `cp nejakysoubor{,.bak}` (což se rozšíří do `cp nejakysoubor nejakysoubor.bak`) nebo `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (což se rozšíří do všech možných kombinací a vytvoří příslušný adresářový strom).

- S výstupem některých příkazů lze zacházet jako se souborem pomocí `<(nejaky prikaz)`. Například porovnání lokálního `/etc/hosts` se vzdáleným:
```sh
      diff /etc/hosts <(ssh nejakyhost cat /etc/hosts)
```

- Poznejte "zdejší dokumenty" v Bashi, míněno `cat <<EOF ...`.

- -Přesměrujte jak standardní výstup tak standardní chybový výstup v Bashi pomocí: `nejaky-prikaz > logsoubor 2>&1` nebo `nejaky-prikaz &>logsoubor`. Častokrát, k zajištění, že příkaz nezanechá otevřený souborový držák (handle), navázání ho na terminál ve kterém jste, je dobrá praktika také přidat `</dev/null`.

- Používejte `man ascii` pro dobrou ASCII tabulku se šestnáctkovými i dekadickými hodnotami. Pro obecné kódovací informace jsou užitečné `man unicode`, `man utf-8` a `man latin1`.

- Používejte `screen` nebo [`tmux`](https://tmux.github.io/) k rozšíření obrazovky, což je užitečné zejména na vzdálených ssh připojeních a k odpojení a znovu-připojení k sezení. `byobu` dokáže vylepšit obrazovku nebo tmux a poskytovat více informací a jednodušší správu. Více minimalistická varianta pouze pro přetrvání sezení je `dtach`.

- v ssh je důležité vědět jak tunelovat porty s pomocí `-L` nebo `-D` (a příležitostně `-R`) například k přístupu na webovou stránku ze vzdáleného serveru.

- Může být užitečné udělat trochu optimalizačních úprav vašeho ssh připojení; například v `~/.ssh/config` je nastavení pro vyhýbání se odhozeným spojením v jistých sítích, používá kompresi (což je užitečné se scp přeš síť s malou šířkou pásma připojení) a multiplexové kanály ke stejnému serveru v lokálním souboru.
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Některé další možnosti vstahující se k ssh jsou bezpečnostně citlivé a měli by být povoleny s opatrností, například pro jednotlivé podsítě nebo hosty v důvěryhodných sítích: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- Zvažte [`mosh`](https://mosh.mit.edu/) jako alternativu k ssh která používá UDP, vyhýbá se padlým spojením a přidává pohodlí na cestách (vyžaduje nastavení na serveru).

- K získání oprávnění k souboru v osmičkové formě, což je užitečné pro systémovou konfiguraci, ale nedostupné v `ls` a lehko zpackatelné, použijte něco jako 
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Pro interaktivní výběr hodnot ze vstupu jinéh příkazu použijte [`percol`](https://github.com/mooz/percol) nebo [`fzf`](https://github.com/junegunn/fzf).

- Pro interakci se soubory v závislosti na vstupu jiného příkazu (třeba `git`), použijte `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- Po zpřístupnění jednoduchého webového serveru pro všechny soubory v současném adresáři (a podadresářích), přístupného každému na vaší síti použijte:
`python -m SimpleHTTPServer 7777` (pro port 7777 a Python 2) a `python -m http.server 7777` (pro port 7777 a Python 3).

- Pro spuštění příkazu s právy použijte `sudo` (pro roota) nebo `sudo -u` (pro jiného uživatele). Používejte `su` nebo `sudo bash` pokud chcete aby shell běžel skutečně pod daným uživatelem. Použitím `su -` simulujte čerstvé přihlášení jako root nebo jiný uživatel.


## Zpracovani souboru a dat

- K nalezení souboru podle jména v pracovním adresáři: `find . -iname '*something*'` (nebo podobně). K nalezení souboru podle jména kdekoliv na disku, použijte `locate jmeno` (pamatujte, že `updatedb` nemuselo nutně zaindexovat nedávno vytvořené soubory).

- Pro obecné prohledávání zdrojů nebo datových souborů (více sofistikované než `grep -r`), použijte [`ag`](https://github.com/ggreer/the_silver_searcher).

- Převeďte HTML na text pomocí `lynx -dump -stdin`.

- Vyzkoušejte [`pandoc`](http://pandoc.org/) pro Markdown, HTML a všechny druhy převodu dokumentů.

- Pokud musíte pracovat s XML `xmlstarlet` je starý, ale dobrý.

- Pro JSON použijte [`jq`](http://stedolan.github.io/jq/).

- Pro YAML, použijte [`shyaml`](https://github.com/0k/shyaml).

- Pro Excel nebo CSV suobory, [csvkit](https://github.com/onyxfish/csvkit) poskytuje `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, atd.

- Pro Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) je pohodlnější a  [`s4cmd`](https://github.com/bloomreach/s4cmd) je rychlejší. [`aws`](https://github.com/aws/aws-cli) od Amazonu a vylepšený [`saws`](https://github.com/donnemartin/saws) jsou nezbytné pro ostatní AWS úkoly.

- Mějte přehled o `sort` a `uniq`, včetně přepínače `-u` pro `uniq` a `-d` -- shlédněte jednořádkové příklady níže. A také `comm`.

- Mějte přehled také o `cut`, `paste` a `join` pro manipulaci s textovými soubory. Mnoho lidí používá `cut`, ale zapomínají na `join`.

- Udržujte přehled také o `wc` na počítání nových řádků (`-l`), znaků (`-m`), slov (`-w`) a bytů (`-c`).

- A přehled je dobré mít také o `tee` pro kopírování ze stdin do souboru a na stdout, podobně jako za použití `ls -la | tee soubor.txt`.

- Mějte na paměti, že nastavení lokalizace ovlivňuje mnoho příkazů v shellu mnoha způsoby včetně pořadí při třídění a výkonu. Většina Linuxových instalací nastaví `LANG` nebo jinou lokalizační proměnnou na lokální nastavení jako americká angličtina. Nezapomínejte však, že vaše třídění se změní změníte-li lokalizaci. A myslete na to, že i18n rutiny mohou způsobit, že třídění nebo jiné příkazy mohou běžet **mnohokrát** pomaleji. V některých situacích (při nastavování nebo testu unikátnost jako níže) lze bezpečně ignorovat pomalé i18n rutiny úplně a použít tradiční bytový pořádek pří třídění s `export LC_ALL=C`.

- Měli byste znáz základní `awk` a `sed` pro jednoduché operace s daty. Například sčítání všech čísel ve třetím sloupci textového souboru: `awk '{ x += $3 } END { print x }'`. Tento příkaz je pravděpodobně 3x rychlejší a obsahuje 3x méně kódu než jeho ekvivalent v Pythonu.

- K nahrazení všech výskytů řetězce v jedno místě nebo ve více souborech:
```sh
      perl -pi.bak -e 's/stary-retezec/novy-retezec/g' moje-soubory-*.txt
```

- K přejmenování více souborů a/nebo vyhledávání a nahrazení uvnitř těchto souborů zkuste [`repren`](https://github.com/jlevy/repren). (V některých případech příkazech `rename` také dovoluje vícenásobné přejmenování, ale buďte opatrní neboť není stejný na všech Linuxových distribucích).
```sh
      # Plne jméno souboru, adresaru a obsahu foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Obnov zalozni soubory cokoliv.bak -> cokoli:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Stejne jako vyse za pouziti jmena pokud mozne:
      rename 's/\.bak$//' *.bak
```

- Jak říká manuálová stránka, `rsync` je skutečně rychlý a neobyčejně univerzální nástroj na kopírování souborů. Je znám pro synchronizaci mezi stroji, ale je také stejně užitečný lokálně. Jde také o jednu z [nejrychlejších cest](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) k odstranění velkého množství souborů:
```sh
      mkdir prazdny && rsync -r --delete prazdny/ nejaky-adr && rmdir nejaky-adr
```

- Použijte `shuf` k zamíchání nebo vybrání náhodných řádek ze souboru.

- Mějte přehled v `sort` možnostech. Pro čísla, použijte `-n` nebo `-h` pro práci s lidsky čitelnými čísly (například z `du -h`). Pochopte jak fungují klíče (`-t` a `-k`). Zejména mějte na paměti, že musíte psát `-k,1` pro třídění za použití pouze prvního pole; `-k1` znamená třídění podle celého řádku. Stabilní třídění (`sort -s`) může být užitečné. Například k setřídění primárně podle druhého pole a sekundárně podle druhého pole můžete použít `sort -k1,1 | sort -s -k2,2`.

- Pokud někdy potřebujete zapsat znak tabulátor do příkazové řádky v Bashi (například pro -t argument pro třídění), stiskněte press **ctrl-v** **[Tab]** nebo napište $'\t'` (druhá možnost je lepší, protože výsledek můžete zkopírovat/vložit).

- Standardní nástroje pro porovnávání zdrojového kódu jsou `diff` a `patch`. Za zmínku stojí také `diffstat` zobrazující statistiky z diffu a `sdiff` pro rozdíly bok po boku. Nezapomeňte, že `diff -r` funguje pro celé adresáře. Použijte `diff -r strom1 strom2 | diffstat` pro shrnutí změn. A `vimdiff` pro porovnání a úpravu souborů.

- Pro binární soubory použijte `hd`, `hexdump` nebo `xxd` pro jednoduché hex dumpy a `bvi` nebo `biew` pro editaci binárek.

- Pro binární soubory můžete také použít `strings` (například spolu s `grep`, atd), což je nástroj pro hledání částí textu.

- Pro binární rozdíly (delta komprese) použijte `xdelta3`.

- Pro konverzi testových kódování zkuste `iconv`. Nebo `uconv` pro pokročilejší použití; podporuje některé pokročilé Unicode věci. Například tento příkaz mění text na malé znaky a odstraňuje akcenty (jejich rozvinutím a zahozením):
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- Na rozdělení souborů do částí zkuste `split` (na rozdělení podle velikosti) a `csplit` (na rozdělení podle řetězce).

- K manipulaci s datem a časem použijte `dateadd`, `datediff`, `strptime` atd. z [`dateutils`](http://www.fresse.org/dateutils/).

- Použijte `zless`, `zmore`, `zcat`, a `zgrep` k operacím s komprimovanými soubory.

