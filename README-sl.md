🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*


# Umetnost ukazne vrstice

[![Vprašajte](https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg)](https://airtable.com/shrzMhx00YiIVAWJg)

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


- [Meta](#meta)
- [Osnove](#osnove)
- [Vsakodnevna uporaba](#vsakodnevna-uporaba)
- [Procesiranje datotek in podatkov](#procesiranje-datotek-in-podatkov)
- [Sistemsko razhroščevanje](#sistemsko-razhroščevanje)
- [V eni vrstici](#v-eni-vrstici)
- [Nepregledno vendar uporabno](#nepregledno-vendar-uporabno)
- [Samo za macOS](#samo-za-macos)
- [Samo za Windows](#samo-za-windows)
- [Več virov](#več-virov)
- [Pogoji uporabe](#pogoji-uporabe)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

Jedrnatost v ukazni vrstici je znanje, ki je pogostokrat zanemarjeno ali smatrano za zastarelo, vendar izboljša vašo fleksibilnost in produktivnost kot inženir na očitne in neočitne načine. To so izbrani zapiski in nasveti glede uporabe ukazne vrstice, ki smo jo našli uporabno pri delu z Linux-om. Nekateri nasveti so elementarni in nekateri so precej določeni, sofisticirani ali nepregledni. Ta stran ni dolga, vendar če lahko uporabite in se spomnite vseh elementov tu, boste vedeli veliko.

To delo je rezultat [mnogih avtorjev in prevajalcev](AUTHORS.md).
Nekaj tega
se je [prvotno](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[pojavilo](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
na [Quori](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
vendar se je premaknilo na GitHub, kjer so ljudje bolj talentirani od prvotnega avtorja naredili številne izboljšave.
[**Vprašajte**](https://airtable.com/shrzMhx00YiIVAWJg), če imate vprašanje povezano z ukazno vrstico. [**Prosimo, prispevajte**](/CONTRIBUTING.md), če vidite napako ali nekaj, kar bi lahko bilo boljše!

## Meta

Obseg:

- Ta vodič je tako za začetnike kot za poznavalce. Cilji so *širina* (vse pomembno), *specifičnost* (podaja konkretne primere najpogostejših primerov uporabe) in *kratkost* (izogiba se stvarem, ki niso bistvene ali se odmikajo, kar lahko enostavno pogledate drugje). Vsak nasvet je bistven v določeni situaciji ali bistveno prihrani čas pred alternativami.
- To je napisano za Linux z izjemo sekcij "[Samo za macOS](#samo-za-macos)" in "[Samo za Windows](#samo-za-windows)". Mnogi ostali elementi veljajo ali pa so lahko nameščeni na drugih Unix-ih ali macOS (ali celo Cygwin).
- Poudarek je na interaktivnosti Bash-a, čeprav mnogo nasvetov velja za ostale lupine in splošno skriptanje Bash-a.
- Vključuje tako "standardne" ukaze Unix-a kot tudi tiste, ki zahtevajo namestitev posebnih paketov -- dokler so dovolj pomembni, da zaslužijo vključitev.

Opombe:

- Da se obdrži to na eni strani, je vsebina implicitno vključena z referencami. Ste dovolj pametni, da poiščete več podrobnosti drugje, ko enkrat poznate idejo ali ukaz za iskanje na Google-u. Uporabite `apt-get`, `yum`, `dnf`, `pacman`, `pip` ali `brew` (kot je ustrezno), da namestite nove programe.
- Uporabite [Explainshell](http://explainshell.com/), da dobite uporabne razčlenitve, kaj ukazi, opcije, cevi itd. naredijo.


## Osnove

- Naučite se osnovni Bash. Dejansko vtipkajte `man bash` in vsaj prelistajte celotno stvar; slediti je precej enostavno in ni tako dolgo. Alternativne lupine so lahko lepe, vendar Bash je močan in vedno na voljo (učenje *samo* zsh, fish itd., medtem ko poskušate na lastno pest na vašem prenosniku, vas omeji v mnogih situacijah, kot je uporaba obstoječih strežnikov).

- Dobro se naučite vsaj enega izmed tekstovnih urejevalnikov. Urejevalnik `nano` je eden izmed najenostavnejših za osnovno urejanje (odpiranje, urejanje, shranjevanje, iskanje). Vendar za bolj vešče uporabnike v tekstovnem terminalu, ni zamenjave za Vim (`vi`), težko priučljiv vendar častljiv, hiter urejevalnik poln možnosti. Mnogi uporabljajo tudi klasični Emacs, še posebej za večja opravila urejanja. (Seveda, katerikoli moderni razvijalec, ki dela na razširljivem projektu, ne bo uporabljal samo čisto tekstovnega urejevalnika in bi moral biti seznanjen tudi z modernimi IDE in orodji z grafičnimi vmesniki.)

- Spoznajte, kako brati dokumentacijo z `man` (za radovedne, `man man` izpiše številke sekcij, npr. 1 so "splošni" ukazi, 5 so datoteke/konvencije in 8 je za administracijo). Najdite strani man z `apropos`. Vedite, da nekateri ukazi niso izvršljivi, vendar vgrajeni v Bash in pomoč zanje lahko dobite s `help` in `help -d`. Z uporabo `type command` lahko izvedete, ali je ukaz izvršljiv, vgrajen v lupino ali pa je alias.

- Naučite se o preusmeritvi izpisa in vnosa z uporabo `>` in `<` ter uporabo cevi `|`. Vedite, da `>` prepiše izpis datoteke in `>>` ga pripne. Naučite se o stdout in stderr.

- Naučite se o razširitvi datotek glob z `*` (in mogoče `?` ter `[`...`]`) in citiranje ter razliko med dvojnim `"` in enojnim `'` citatom. (Poglejte več o razširitvi spremenljivk spodaj.)

- Seznanite se z upravljanjem nalog Bash-a: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill` itd.

- Spoznajte `ssh` in osnove avtentikacije brez gesla, preko `ssh-agent`, `ssh-add` itd.

- Osnovno upravljanje datotek: `ls` in `ls -l` (še posebej se naučite, kaj vsak stolpec v `ls -l` pomeni), `less`, `head`, `tail` in `tail -f` (ali celo boljše, `less +F`), `ln` in `ln -s` (naučite se razlike in prednosti trdih in mehkih povezav), `chown`, `chmod`, `du` (za hiter povzetek uporabe diska: `du -hs *`). Za upravljanje datotečnega sistema, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. Naučite se, kaj je inode (`ls -i` or `df -i`).

- Osnovno upravljanje omrežja: `ip` ali `ifconfig`, `dig`, `traceroute`, `route`.

- Naučite se in uporabljajte sistem za nadzor različic, kot je `git`.

- Poznajte tudi splošne izraze in različne zastavice za `grep`/`egrep`. Opcije `-i`, `-o`, `-v`, `-A`, `-B` in `-C` so vredne poznavanja.

- Naučite se uporabljati `apt-get`, `yum`, `dnf` ali `pacman` (odvisno od distribucije), da najdete in namestite pakete. In zagotovite, da imate `pip`, da lahko nameščate orodja ukazne vrstice na osnovi Python-a (nekaj spodnjih je najenostavneje namestiti preko `pip`).


## Vsakodnevna uporaba

- V Bash-u uporabite **Tab** za dokončanje argumentov ali izpis vseh ukazov, ki so na voljo, in **ctrl-r**, da iščete skozi zgodovino ukazov (po pritiski, vtipkajte za iskanje, pritisnite **ctrl-r** s ponavljanjem za kroženje skozi več ujemanj, pritisnite **Enter**, da izvršite najdeni ukaz, ali pritisnite desno puščico, da date trenutni rezultat v trenutno vrstico in omogočite urejanje).

- V Bash-u uporabite **ctrl-w**, da izbrišete zadnjo besedo in **ctrl-u**, da izbrišete vse do začetka vrstice. Uporabite **alt-b** in **alt-f**, da se premikate po besedah, **ctrl-a**, da premaknete kurzor na začetek vrstice, **ctrl-e**, da premaknete kurzor na konec vrstice, **ctrl-k**, da ubijete do začetka vrstice, **ctrl-l**, da počistite zaslon. Glejte `man readline` za vse privzete vezave tipk v Bash-u. Na voljo jih je veliko. Na primer **alt-.** kroži skozi prejšnje argumente in **alt-*** razširi glob.


- Alternativno, če imate radi vi-stilske vezave tipk, uporabite `set -o vi` (in `set -o emacs` za povrnitev nazaj).

- Za urejanje dolgih ukazov, po nastavitvi vašega urejevalnika (na primer `export EDITOR=vim`), **ctrl-x** **ctrl-e** bo odprlo trenutni ukaz v urejevalniku za več vrstično urejanje. Ali v stilu vi, **escape-v**.

- Če si želite ogledati nedavne ukaze, uporabite `history`. Nadalje `!n` (kjer je `n` številka ukaza), da ga ponovno izvedete. Na voljo je tudi veliko okrajšav, najuporabnejša verjetno `!$` za zadnji argument in `!!` za zadnji ukaz (glejte "HISTORY EXPANSION" na man straneh). Vendar so le-te pogostokrat enostavno zamenjane s **ctrl-r** in **alt-.**.

- Pojdite v vaš domači direktorij s `cd`. Dostopajte do datotek relativno glede na vaš domači direktorij s predpono `~` (npr. `~/.bashrc`). V `sh` skriptah se sklicujte na domači direktorij kot `$HOME`.

- Da greste nazaj na prejšnji delovni dirketorij: `cd -`

- Če ste na pol poti skozi vpisovanje ukaza, vendar si premislite, vtipkajte **alt-#**, da dodate `#` na začetek in ga vnesete kot komentar (ali uporabite **ctrl-a**, **#**, **enter**). Nato se lahko vrnete k njemu kasneje preko zgodovine ukazov.

- Uporabite `xargs` (ali `parallel`). Je zelo močan. Bodite pozorni, da lahko kontrolirate, kolikokrat izvršite na vrstico (`-L`) kot tudi paralelnost (`-P`). Če niste prepričani, da bo naredilo pravilno stvar, uporabite najprej `xargs echo`. Tudi `-I{}` je priročen. Primeri:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` je priročen prikaz drevesa procesov.

- Uporabite `pgrep` in `pkill`, da najdete ali signalizirate procese po imenu (`-f` je v pomoč).

- Poznajte različne signale, katerim lahko pošljete procese. Na primer, da suspendirate proces, uporabite `kill -STOP [pid]`. Za celotni seznam glejte `man 7 signal`

- Uporabite `nohup` ali `disown`, če želite, da proces iz ozadja vedno poteka.

- Preverite, kateri procesi se poslušajo preko `netstat -lntp` ali `ss -plat` (za TCP; dodajte `-u` za UDP) ali `lsof -iTCP -sTCP:LISTEN -P -n` (kar deluje tudi na macOS).

- Glejte tudi `lsof` in `fuser` za odprte priključke in datoteke.

- Glejte `uptime` ali `w`, da izveste, koliko časa se sistem poganja.

- Uporabite `alias`, da ustvarite bližnjice za pogosto uporabljene ukaze. Na primer, `alias ll='ls -latr'` ustvari nov alias `ll`.

- Shranite aliase, nastavitve lupine in funkcije, ki jih pogosto uporabljate v `~/.bashrc` in [uredite prijave lupin za izvorno kodo](http://superuser.com/a/183980/7106). To bo naredilo vašo namestitev na voljo v vseh sejah vaše lupine.

- Dajte nastavitve spremenljivk okolja kot tudi ukaze, ki bi morali biti izvršeni, ko se prijavite v `~/.bash_profile`. Ločena nastavitev bo potrebna za lupine, ki jih zaženete iz prijave grafičnega okolja in s periodičnimi opravili `cron`.

- Sinhronizirajte vaše nastavitvene datoteke (npr. `.bashrc` in `.bash_profile`) med različnimi računalniki s pomočjo Git.

- Razumite, da je potrebna skrb, ko spremenljivke in imena datotek vsebujejo prazne znake. Obdajte vaše spremenljivke Bash s citati, npr. `"$FOO"`. Raje cenite opciji `-0` ali `-print0`, da omogočite razmejevanje imen datotek z ničelnimi znaki, npr. `locate -0 pattern | xargs -0 ls -al` ali `find / -print0 -type d | xargs -0 ls -al`. Za iteracijo v for zanki na imenih datotek, ki vsebujejo prazne znake, nastavite da vaš IFS za nove vrstice uporablja samo `IFS=$'\n'`.

- V skriptah Bash uporabite `set -x` (ali varianto `set -v`, ki beleži dnevnik surovega izpisa, vključno z nerazširjenimi spremenljivkami in komentarji) za razhroščevanje izpisa. Uporabite striktni način razen, če imate dober razlog, da ga ne: Uporabite `set -e`, da preskočite napake (neničelna koda izhoda). Uporabite `set -u`, da zaznate uporabo nenastavljenih spremenljivk. Premislite tudi o `set -o pipefail`, da na napakah znotraj pip, (vendar preberite o tem več, če boste to uporabili, saj je ta tema nekoliko subtilna). Za bolj vključene skripte, uporabite tudi `trap` pri EXIT ali ERR. Uporabna navada je tako začeti skripto, kar bo naredilo, da lahko zazna ali prekliče na pogostih napakah in izpiše sporočilo:
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- V skriptah Bash so podlupine (napisane z oklepaji) priročen način za grupiranje ukazov. Skupen primer je začasno premakniti na različen delovni direktorij, npr.
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- V Bash-u bodite pozorni, saj je veliko vrst razširjenih spremenljivk. Preverjanje, če spremenljivka obstaja: `${name:?error message}`. Na primer, če skripta Bash zahteva en argument, samo napišite `input_file=${1:?usage: $0 input_file}`. Uporaba privzete vrednosti, če je spremenljivka prazna: `${name:-default}`. Če želite, imeti dodatni (opcijski) parameter dodan k prejšnjemu primeru, lahko uporabite nekaj takega `output_file=${2:-logfile}`. Če je `$2` izpuščen in tako prazen, bo `output_file`  nastavljen na `logfile`. Aritmetična raširitev: `i=$(( (i + 1) % 5 ))`. Sekvence: `{1..10}`. Obrezovanje nizov: `${var%suffix}` in `${var#prefix}`. Na primer, če je `var=foo.pdf`, potem `echo ${var%.pdf}.txt` izpiše `foo.txt`.

- Lupinska razširitev zavitih oklepajev z `{`...`}` lahko pomaga zmanjšati potrebo po ponovnem vpisovanju podobnega teksta in avtomatizira kombiniranje elementov. To je v pomoč v primerih kot je `mv foo.{txt,pdf} some-dir` (ki premakne obe datoteki), `cp somefile{,.bak}` (kar razširi v `cp somefile somefile.bak`) ali `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (kar razširi vse možne kombinacije in ustvari drevo direktorijev). Razširitev zavitih oklepajev je izvedena pred katerokoli drugo razširitvijo.

- Vrstni red razširitev je: razširitev zavitega oklepaja; razširitev tilda, razširitev parametra in spremenljivke, aritmetična razširitev in zamenjava ukaza (izvedeno na način levo proti desnem); delitev besed; in razširitev imena datoteke. Na primer, obseg kot je `{1..20}` ne more biti izražen s spremenljivkami z uporabo `{$a..$b}` ob predpostavki `a=1` in `b=20` in doprinese `{1..20}`. Uporabite `seq` ali `for` zanko, npr., `seq $a $b` ali `for((i=a; i<=b; i++)); do ... ; done`.

- Izpis ukaza se lahko tretira kot datoteko preko `<(some command)` (znan kot proces zamenjave). Na primer, primerjajte lokalno `/etc/hosts` z oddaljeno:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Ko pišete skripte, boste morda želeli dati vašo kodo v zavite oklepaje. Če zapirajoči se oklepaj manjka, se vaša skripta ne bo izvršila zaradi sintaktične napake. To je smiselno, ko se vašo skripto prenese iz spleta, saj preprečuje izvrševanje delno prenešene skripte:
```bash
{
    # Vaša koda
}
```

- T.i. "here document" omogoča [preusmeritev večih vrstic vnosa](https://www.tldp.org/LDP/abs/html/here-docs.html) kot da gre za datoteko:
```
cat << EOF
These lines will
print to stdout
EOF
```

- V Bash-u je preusmeritev obeh standardov izpisa in standardnih napak preko: `some-command >logfile 2>&1` ali `some-command &>logfile`. Pogosto zagotavlja, da ukaz ne pusti ročaja odprte datoteke za standardni vnos, kar ga veže na terminal v katerem se nahajate, je tudi dobra praksa, da dodate `</dev/null`.

- Uporabite `man ascii` za dobro tabelo ASCII s heksadecimalnimi in decimalnimi vrednostmi. Za splošne informacije enkodiranja so priročni `man unicode`, `man utf-8` in `man latin1`.

- Uporabite `screen` ali [`tmux`](https://tmux.github.io/), da muliplicirate zaslon, posebej uporabno na oddaljenih sejah ssh in da odstranite in se ponovno pripnete k seji. `byobu` lahko poveča t.i. screen ali tmux s ponujanjem več informacij in enostavnejšim upravljanjem. Bolj minimalna alternativa za samo obstojnost sej je [`dtach`](https://github.com/bogner/dtach).

- V ssh je poznavanje, kako usmeriti tunel z `-L` ali `-D` (in občasno `-R`) je uporaben, npr. za dostopanje do spletnih strani iz oddaljenega strežnika.

- Lahko je uporabno, da se naredi nekaj optimizacij na vaših nastavitvah ssh; na primer, ta `~/.ssh/config` vsebuje nastavitve za izogib padle povezave v določenih okoljih omrežja, uporablja kompresijo (ki je v pomoč s scp preko nizko pasovnih povezav) in multiplicira kanale na isti strežnik z lokalno krmilno datoteko:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Nekaj ostalih opcij relevantnih za ssh je varnostno občutljivih in bi morale biti omogočene s pazljivostjo, npr. na podomrežju ali gostitelju ali v zaupljivih omrežjih: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- Premislite o [`mosh`](https://mosh.mit.edu/) kot alternativi za ssh, ki uporablja UDP, da se izognete padlim povezavam in dodate priročnost, ko ste na poti (zahteva nastavitev strežniške strani).

- Da dobite pravice na datoteki v osmiškem zapisu, ki je uporaben za nastavitve sistema vendar ni na voljo pri `ls` in enostaven za mešanje, uporabite nekaj takega kot je
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Za interaktivno izbiro vrednosti iz izpisa drugega ukaza, uporabite [`percol`](https://github.com/mooz/percol) ali [`fzf`](https://github.com/junegunn/fzf).

- Za interakcijo z datotekami osnovanimi na izpisu drugega ukaza (kot je `git`), uporabite `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- Za enostaven spletni strežnik za vse datoteke v trenutnem direktoriju (in poddirektorijih), ki so na voljo komurkoli v vašem omrežju, uporabite:
`python -m SimpleHTTPServer 7777` (za port 7777 in Python 2) in `python -m http.server 7777` (za port 7777 in Python 3).

- Za pogon ukaza pod drugim uporabnikom, uporabite `sudo`. Privzeto požene kot root; uporabite `-u`, da določite drugega uporabnika. Uporabite `-i` za prijavo tega uporabnika (vprašalo vas bo za _vaše_ geslo).

- Za preklop lupine na drugega uporabnika, uporabite `su username` ali `su - username`. Pripona `-` dobi okolje, kakor da bi se drug uporabnik ravnokar prijavil. Izpustitev uporabniškega imena pomeni privzeto root. Vprašani boste za geslo _uporabnika na katerega preklapljate_.

- Spoznajte [omejitev 128K](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong) v ukaznih vrsticah. Ta napaka "Argument list too long" je pogosta, ko se nadomestni znak ujema z velikim številom datotek. (Ko se to zgodi, lahko pomagajo alternative kot sta `find` in `xargs`.)

- Za osnovni kalkulator (in seveda splošni dostop do Python-a) uporabite interpreter `python`. Na primer,
```
>>> 2+3
5
```


## Procesiranje datotek in podatkov

- Da locirate datoteko po imenu v trenutnem direktoriju, `find . -iname '*something*'` (ali podobno). Da najdete datoteko kjerkoli po imenu, uporabite `locate something` (vendar imejte v mislih, da `updatedb` morda ni poindeksiral nazadnje ustvarjenih datotek).

- Za splošno iskanje skozi izvorne ali podatkovne datoteke, na voljo je nekaj možnosti bolj naprednih in hitrejših možnosti od `grep -r`, vključno z (po surovem vrstnem redu od starejših do novejših) [`ack`](https://github.com/beyondgrep/ack2), [`ag`](https://github.com/ggreer/the_silver_searcher) ("t.i. silver searcher") in [`rg`](https://github.com/BurntSushi/ripgrep) (ripgrep).

- Da pretvorite HTML v tekst: `lynx -dump -stdin`

- Za Markdown, HTML in vse vrste pretvorb dokumentov poskusite [`pandoc`](http://pandoc.org/).

- Če morate upravljati z XML, je `xmlstarlet` star vendar dober.

- Za JSON, use [`jq`](http://stedolan.github.io/jq/). Za interaktivnost glejte tudi [`jid`](https://github.com/simeji/jid) in [`jiq`](https://github.com/fiatjaf/jiq).

- Za YAML, uporabite [`shyaml`]((https://github.com/0k/shyaml).

- Za Excel ali CSV datoteke, [csvkit](https://github.com/onyxfish/csvkit) ponuja `in2csv`, `csvcut`, `csvjoin`, `csvgrep` itd.

- Za Amazon S3 je priročen [`s3cmd`](https://github.com/s3tools/s3cmd) in [`s4cmd`](https://github.com/bloomreach/s4cmd) je hitrejši. Amazon-ov [`aws`](https://github.com/aws/aws-cli) in izboljšan [`saws`](https://github.com/donnemartin/saws) sta bistvena za druga AWS-povezana opravila.

- Naučite se o `sort` in `uniq` vključno z uniq-ovima opcijama `-u` in `-d` -- glejte spodaj sekcijo v eni vrstici. Glejte tudi `comm`.

- Naučite se o `cut`, `paste` in `join` za manipuliranje tekstovnih datotek. Mnogi uporabljajo `cut` vendar pozabijo na `join`.

- Naučite se o `wc`, da preštejete nove vrstice (`-l`), znake (`-m`), besede (`-w`) in bajte (`-c`).

- Naučite se o `tee`, da prekopirate iz stdin v datoteko in tudi v stdout, kot pri `ls -al | tee file.txt`.

- Za kompleksnejše kalkulacije, vključno z združevanjem, obračanjem polj in statističnimi izračuni, razmislite o [`datamash`](https://www.gnu.org/software/datamash/).

- Vedite, da lokalizacija vpliva na veliko orodij ukazne vrstice na subtilne načine, vključno z vrstnim redom (kolokacijo) in uspešnostjo. Večina namestitev Linux-a bo nastavila `LANG` ali druge spremenljivke lokalizacije na lokalne nastavitve kot je US English. Vendar bodite pozorni, saj se bo vrstni red spremenil, če spremenite lokalizacijo. In vedite, da rutine i18n lahko naredijo sortiranje ali poganjanje drugih ukazov *nekajkrat* počasnejše. V nekaterih situacijah (kot je skupek operacij ali unikatnih operacij spodaj) lahko v celoti varno ignorirate počasne rutine i18n in uporabite tradicionalne vrstne rede na osnovi bajtov z uporabo `export LC_ALL=C`.

- Nastavite lahko določeno okolje ukaza s predpono njegovega sklicevanja na nastavitve spremenljivk okolja, kot pri `TZ=Pacific/Fiji date`.

- Spoznajte osnove `awk` in `sed` za enostavno manipuliranje podatkov. Za primere glejte sekcijo [v eni vrstici](#v-eni-vrstici).

- Da zamenjate vsa pojavljanja niza na mestu v eni ali večih datotekah:
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- Da preimenujete več datotek in/ali poiščete in poiščete in zamenjate znotraj datotek, poskusite [`repren`](https://github.com/jlevy/repren). (V nekaterih primerih ukaz `rename` tudi omogoča preimenovanje, vendar bodite pozorni, saj funkcionalnost ni enaka na vseh distribucijah Linux).
```sh
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Recover backup files whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Same as above, using rename, if available:
      rename 's/\.bak$//' *.bak
```

- Kot pravi stran vodiča, je `rsync` resnično hiter in izredno vsestransko orodje kopiranja datotek. Znano je po sinhronizaciji med napravami vendar je enakovredno uporaben tudi lokalno. Ko omejitve varnosti omogočajo, uporaba `rsync` namesto `scp` omogoča povrnitev prenosa brez ponovnega zagona od začetka. Je tudi eden izmed [najhitrejših načinov](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) za izbris velikega števila datotek:
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Za spremljanje napredka med kopiranjem datotek uporabite [`pv`](http://www.ivarch.com/programs/pv.shtml), [`pycp`](https://github.com/dmerejkowsky/pycp), [`pmonitor`](https://github.com/dspinellis/pmonitor), [`progress`](https://github.com/Xfennec/progress), `rsync --progress`, ali za kopiranje na nivoju blokov `dd status=progress`.

- Uporabite `shuf` za naključno mešanje ali izbiro naključnih vrstic iz datoteke.

- Poznajte opcije za `sort`. Za številke uporabite `-n` ali `-h` za upravljanje številk človeku prijaznih za branje (npr. iz `du -h`). Vedite, kako delujejo ključi (`-t` in `-k`). Še posebej pazite, da morate zapisati `-k1,1`, da razvrstite samo po prvem polju; `-k1` pomeni razvrščanje glede na celotno vrstico. Stabilno razvrščanje (`sort -s`) je lahko uporabno. Na primer, da sortirate najprej po polju 2 in nato po polju 1, lahko uporabite `sort -k1,1 | sort -s -k2,2`.

- Če kadarkoli potrebujete zapisati tabulator dobesedno v ukazni vrstici v Bash-u (npr. za sortiranje argumenta -t), pritisnite **ctrl-v** **[Tab]** ali zapišite `$'\t'` (slednji je boljši, saj ga lahko kopirate in prilepite).

- Standardna orodja za popravljanje izvorne kode so `diff` in `patch`. Glejte tudi `diffstat` za povzetek statistike diff-a in `sdiff` za diff drug ob drugem. Bodite pozorni, saj `diff -r` deluje za celotne direktorije. Uporabite `diff -r tree1 tree2 | diffstat` za povzetek sprememb. Uporabite `vimdiff` za primerjanje in urejanje datotek.

- Pri binarnih datotekah uporabite `hd`, `hexdump` ali `xxd` za enostavne heksadecimalne izpise in `bvi`, `hexedit`, ali `biew` za binarno urejanje.

- `strings` (plus `grep` itd.) vam omogoča najti bite v tekstu tudi za binarne datoteke.

- Za binarne diff-e (delta kompresije) uporabite `xdelta3`.

- Da pretvorite enkodiranje teksta, poskusite `iconv`. Ali `uconv` za bolj napredno uporabo; podpira nekaj naprednih Unicode stvari. Na primer:
```sh
      # Prikaže hex kode ali dejanska imea znakov (uporabno za razhroščevanje):
      uconv -f utf-8 -t utf-8 -x '::Any-Hex;' < input.txt
      uconv -f utf-8 -t utf-8 -x '::Any-Name;' < input.txt
      # Male črke in odstrani vsa naglasna znamenja (z razširitvijo in opustitvijo):
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC;' < input.txt > output.txt
```

- Da razcepite datoteke na dele, glejte `split` (da razcepite po velikosti) in `csplit` (da razcepite po vzorcu).

- Datum in čas: Da dobite trenutni datum in čas v priročnem [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) formatu, uporabite `date -u +"%Y-%m-%dT%H:%M:%SZ"` (ostale opcije [so](https://stackoverflow.com/questions/7216358/date-command-on-os-x-doesnt-have-iso-8601-i-option) [problematične](https://unix.stackexchange.com/questions/164826/date-command-iso-8601-option)). Za manipuliranje izrazov datuma in časa, uporabite `dateadd`, `datediff`, `strptime` itd. iz [`dateutils`](http://www.fresse.org/dateutils/).

- Uporabite `zless`, `zmore`, `zcat` in `zgrep` za operiranje na kompresiranih datotekah.

- Atributi datotek so nastavljivi preko `chattr` in ponujajo nizko nivojsko alternativo pravicam datotek. Na primer za zaščito pred ponesrečenim brisanjem datoteke se uporabi nespremenljiva zastavica: `sudo chattr +i /critical/directory/or/file`

- Uporabite `getfacl` in `setfacl`, da shranite in povrnete pravice datotek. Na primer:
```sh
    getfacl -R /some/path > permissions.txt
    setfacl --restore=permissions.txt
```

- Za hitro ustvarjanje praznih datotek, uporabite `truncate` (ustvari t.i. [sparse file](https://en.wikipedia.org/wiki/Sparse_file)), `fallocate` (ext4, xfs, btrfs in ocfs2 datotečni sistemi), `xfs_mkfile` (skoraj katerikoli datotečni sistem, pride skupaj s paketom xfsprogs), `mkfile` (za Unix in podobne sisteme kot sta Solaris in Mac OS).

## Sistemsko razhroščevanje

- Za spletno razhroščevanje, sta priročna `curl` in `curl -I` ali pa njun ekvivalent `wget`, ali bolj moderen [`httpie`](https://github.com/jkbrzt/httpie).

- Da izveste trenutni status diska/procesorja/omrežja, so na voljo klasična orodja `top`, (ali bolje `htop`), `iostat` in `iotop` . Uporabite `iostat -mxz 15` za osnovno statistiko CPU in podrobno na particijo statistiko diska in vpogled v uspešnost.

- Za podrobnosti omrežne povezave uporabite `netstat` in `ss`.

- Za hiter pregled, kaj se dogaja na sistemu, je `dstat` posebno uporaben. Za širši pregled s podrobnostmi uporabite [`glances`](https://github.com/nicolargo/glances).

- Da izveste status spomina, poženite in razumite izpis `free` in `vmstat`. Še posebej bodite pozorni, da je vrednost "cached" držana v spominu s strani jedra Linux-a kot datoteka predpomnilnika, tako da efektivno šteje proti vrednosti "free".

- Sistemsko razhroščevanje Java je drugačen tip, vendar enostaven trik na JVM-jih Oracle-a in nekaterih ostalih je, da lahko poženete `kill -3 <pid>` in sledite celotnemu stack-u in povzetku kopic (vključno s podrobnostmi zbirke splošnih smeti, ki so lahko zelo informativne), ki bodo oddane v stderr/logs. JDK-jevi `jps`, `jstat`, `jstack`, `jmap` so uporabni. [SJK Tools](https://github.com/aragozin/jvm-tools) so bolj napredni.

- Uporabite [`mtr`](http://www.bitwizard.nl/mtr/) kot boljši usmerjevalnik sledenja za identifikacijo težav omrežja.

- Za iskanje, zakaj je disk poln, vam [`ncdu`](https://dev.yorhel.nl/ncdu) prihrani čas preko običajnih ukazov kot je `du -sh *`.

- Da najdete katera vtičnica ali proces uporablja pasovno širino, poskusite [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) ali [`nethogs`](https://github.com/raboof/nethogs).

- Orodje `ab` (prihaja z Apache-jem) je v pomoč za hitro in nečisto preverjanje uspešnosti spletnega strežnika. Za bolj kompleksno testiranje nalaganja poskusite `siege`.

- Za bolj resno razhroščevanje omrežja, [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) ali [`ngrep`](http://ngrep.sourceforge.net/).

- Poznajte `strace` in `ltrace`. Ta sta v pomoč, če program ni uspešen, se ustavlja ali poruši in ne veste zakaj, ali če želite dobiti splošno idejo o uspešnosti. Bodite pozorni na opcijo profiliranja (`-c`) in zmožnost dodajanja k procesu, ki se poganja (`-p`). Uporabite podrejene opcije trace (`-f`), da se izognete manjkajočim pomembnim klicem.

- Poznajte `ldd`, da preverite deljene knjižnice itd. —  vendar [nikoli ne poženite na nezaupljivih datotekah](http://www.catonmat.net/blog/ldd-arbitrary-code-execution/).

- Vedite, kako se povezati k procesu v pogonu z `gdb` in dobiti njegove sledi skladovnice.

- Uporabite `/proc`. Včasih je izjemno v pomoč, ko se razhroščuje probleme v živo. Primeri: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (kjer je `xxx` id procesa ali pid).

- Ko se razhroščuje, zakaj je šlo nekaj narobe v preteklosti, je lahko zelo uporaben [`sar`](http://sebastien.godard.pagesperso-orange.fr/). Prikazuje statistiko zgodovine na procesorju, spominu, omrežju itd.

- Za globlje analize sistema in uspešnosti, poglejte `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_%28Linux%29) in [`sysdig`](https://github.com/draios/sysdig).

- Preverite na katerem operacijskem sistemu ste z `uname` ali `uname -a` (splošne informacije Unix-a/jedra) ali `lsb_release -a` (informacije distribucuje Linux).

- Uporabite `dmesg` kadarkoli gre nekaj dejansko čudno (lahko je težava strojne opreme ali gonilnika).

- Če izbrišete datoteko in se prostor na voljo ne poveča, kot je pričakovano s poročilom `du`, preverite ali datoteko uporablja proces:
`lsof | grep deleted | grep "filename-of-my-big-file"`


## V eni vrstici

Nekaj primerov sestavljanja ukazov skupaj:

- Včasih je izredno v pomoč, da lahko nastavite presek, unijo in razliko tekstovnih datotek preko `sort`/`uniq`. Predpostavimo `a` in `b` sta tekstovni datoteki, ki sta že unikatni. To je hitro in deluje na datotekah arbitrarnih velikosti do nekaj gigabajtov. (Urejanje ni omejeno glede na spomin, čeprav morda potrebujete uporabiti opcijo `-T`, če je `/tmp` na majhni root particiji.) Glejte tudi opombo o `LC_ALL` zgoraj in `sort`-ovo opcijo `-u` (puščeno zaradi jasnosti spodaj).
```sh
      sort a b | uniq > c   # c is a union b
      sort a b | uniq -d > c   # c is a intersect b
      sort a b b | uniq -u > c   # c is set difference a - b
```

- Uporabite `grep . *`, da hitro preučite vsebine vseh datotek v direktoriju (vsaka vrstica ima par z imenom datoteke) ali `head -100 *` (da iima vsaka datoteka glavo). To je lahko uporabno za direktorije napolnjene s konfiguracijskimi nastavitvami, kot so tiste v `/sys`, `/proc`, `/etc`.


- Povzetje vseh številk v tretjem stolpcu tekstovne datoteke (to je verjetno 3X hitrejše in 3X manj kode kot Python-ov ekvivalent):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- Da vidite velikost/datume v drevesu datotek, je to kot rekurzivni `ls -l` vendar enostavnejše za branje kot `ls -lR`:
```sh
      find . -type f -ls
```

- Recimo, da imate tekstovno datoteko, kot dnevnik spletnega strežnika in določena vrednost se pojavi na nekaterih vrsticah, kot parameter `acct_id`, ki je prisoten v URL-ju. Če želite ujemanja, koliko je zahtevkov za vsak `acct_id`:
```sh
      egrep -o 'acct_id=[0-9]+' access.log | cut -d= -f2 | sort | uniq -c | sort -rn
```

- Da neprekinjeno nadzirate spremembe, uporabite `watch`, npr. preverite spremembe datotek v direktoriju z `watch -d -n 2 'ls -rtlh | tail'` ali med odpravljanjem težav vaših nastavitev wifi z `watch -d -n 2 ifconfig`.

- Poženite to funkcijo, da dobite naključni nasvet iz tega dokumenta (razčleni Markdown in izvleče element):
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          sed '/cowsay[.]png/d' |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80 | iconv -t US
      }
```


## Nepregledno vendar uporabno

- `expr`: izvede aritmetične ali logične operacije ali oceni splošne izraze

- `m4`: enostaven makro procesor

- `yes`: velikokrat izpiše niz

- `cal`: lep koledar

- `env`: požene ukaz (uporabno v skriptah)

- `printenv`: izpiše spremenljivke okolja (uporabno pri razhroščevanju in v skriptah)

- `look`: najde angleške besede (ali vrstice v datoteki) začenši z nizom

- `cut`, `paste` in `join`: manipulacija podatkov

- `fmt`: oblikuje odstavke teksta

- `pr`: oblikuje tekst v strani/stolpce

- `fold`: ovije vrstice teksta

- `column`: oblikuje tekstovna polja v poravnane stolpce s fiksno širino ali tabele

- `expand` in `unexpand`: pretvori med tabulatorji in presledki

- `nl`: doda vrstice številk

- `seq`: izpiše številke

- `bc`: kalkulator

- `factor`: celo številski faktorji

- [`gpg`](https://gnupg.org/): enkriptira in podpiše datoteke

- `toe`: tabela vnosov terminfo

- `nc`: rahroščevanje omrežja in prenos podatkov

- `socat`: rele vtičnice in odpravnik tcp porta (podobno kot `netcat`)

- [`slurm`](https://github.com/mattthias/slurm): vizualizacija prometa omrežja

- `dd`: premikanje podatkov med datotekami in napravami

- `file`: identifikacija tipa datoteke

- `tree`: prikaže direktorije in poddirektorije kot gnezdeno drevo; kot `ls` vendar rekurzivno

- `stat`: informacije datoteke

- `time`: izvrši in da ukaz v čas

- `timeout`: izvršite ukaz za določen čas in ustavite proces, ko se določen čas konča.

- `lockfile`: ustvari semaforno datoteko, ki je lahko odstranjena samo z `rm -f`

- `logrotate`: rotiranje, kompresiranje in pošiljanje dnevnikov po e-pošti.

- `watch`: večkrat požene ukaz in prikazuje rezultate in/ali poudari spremembe

- [`when-changed`](https://github.com/joh/when-changed): požene kateri koli ukaz, ki ga določite, kadarkoli opazi spremembo datoteke. Glejte tudi `inotifywait` in `entr`.

- `tac`: izpiše datoteke v obratnem redu

- `comm`: primerja sortirane datoteke vrstico za vrstico

- `strings`: izvleče tekst iz binarnih datotek

- `tr`: prevod znakov ali manipulacija

- `iconv` ali `uconv`: pretvorba enkodiranja teksta

- `split` in `csplit`: cepljenje datotek

- `sponge`: prebere vse vnose pred pisanjem, uporabno za branje iz njih in nato za pisanje v isto datoteko, npr. `grep -v something some-file | sponge some-file`

- `units`: pretvorba enot in kalkulacije; pretvori furlonge (osmino milje) na štirinajst dni v dvajsetine točke na blink (glejte tudi `/usr/share/units/definitions.units`)

- `apg`: generira naključna gesla

- `xz`: kompresija datoteke visokega razmerja

- `ldd`: informacije dinamične knjižnice

- `nm`: simboli iz datotek objekta

- `ab` ali [`wrk`](https://github.com/wg/wrk): merjenje uspešnosti spletnih strežnikov

- `strace`: razhroščevanje sistemskega klica

- [`mtr`](http://www.bitwizard.nl/mtr/): boljše sledenje usmerjanja za razhroščevanje omrežja

- `cssh`: vizualna sočasna lupina

- `rsync`: sinhronizacija datotek in map preko SSH ali v lokalnem datotečnem sistemu

- [`wireshark`](https://wireshark.org/) in [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): zajem paketov in razhroščevanje omrežja

- [`ngrep`](http://ngrep.sourceforge.net/): grep za nivo omrežja

- `host` in `dig`: pogled DNS

- `lsof`: procesira deskriptorje datoteke in informacije vtičnice

- `dstat`: uporabna statistika sistema

- [`glances`](https://github.com/nicolargo/glances): visoko nivojski, večkratni podsistemski pregled

- `iostat`: statistika uporabe diska

- `mpstat`: statistika uporabe procesorja

- `vmstat`: statistika uporabe spomina

- `htop`: izboljšana verzija top

- `last`: zgodovina prijav

- `w`: kdo je prijavljen

- `id`: informacije identifikacije uporabnika/skupine

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): statistika zgodovine sistema

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) ali [`nethogs`](https://github.com/raboof/nethogs): izkoriščenost omrežja po vtičnici ali procesu

- `ss`: statistika vtičnice

- `dmesg`: sporočila napak zagona in sistema

- `sysctl`: ogled in nastavitev parametrov jedra Linux pri pogonu

- `hdparm`: manipulacija/uspešnost SATA/ATA disk-a

- `lsblk`: izpiše blokovne naprave: drevesni pogled vaših diskov in particij diska

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: informacije strojne opreme, vključno s procesorjem, BIOS-om, RAID-om, grafiko, napravami itd.

- `lsmod` in `modinfo`: izpišeta in prikažeta podrobnosti o modulih jedra.

- `fortune`, `ddate` in `sl`: hm, torej zavisi glede na to ali smatrate parne lokomotive in dinamične kotacije "uporabne"


## Samo za macOS

To so elementi pomembni *samo* za macOS.

- Upravljanje paketov z `brew` (Homebrew) in/ali `port` (MacPorts). Te so lahko uporabljeni za namestitev mnogih zgornjih ukazov na macOS.

- Kopirajte izpis katerega koli ukaza na namizno aplikacijo s `pbcopy` in prilepite vnos iz ene s `pbpaste`.

- Da omogočite uporabo tipke Option v macOS terminalu kot tipka alt (kot je uporabljena v ukazih zgoraj kot **alt-b**, **alt-f** itd), odprite Preferences -> Profiles -> Keyboard in izberite "Use Option as Meta key".

- Da odprete datoteko z namizno aplikacijo, uporabite `open` ali `open -a /Applications/Whatever.app`.

- Spotlight: Poiščite datoteke z `mdfind` in izpišite meta podatke (kot so EXIF informacije fotografije) z `mdls`.

- Bodite pozorni, saj je macOS osnovan na BSD Unix in mnogi ukazi (na primer `ps`, `ls`, `tail`, `awk`, `sed`) imajo mnoge subtilne različice iz Linux-a, na katerega je večinoma vplival System V-style Unix in GNU tools. Pogostokrat lahko poveste razliko tako, da opazite, da ima stran man naslov "BSD General Commands Manual." V nekaterih primerih se lahko namestijo tudi GNU različice (kot so `gawk` in `gsed` za GNU awk in sed). Če pišete skripte Bash za vse platforme, se izogibajte takim ukazom (na primer, z upoštevanjem Python ali `perl`) ali pazljivo testirajte.

- Da dobite informacije o izdaji macOS, uporabite `sw_vers`.

## Samo za Windows

Sledeče velja *samo* za Windows.

### Načini pridobitve Unix orodij na Windows

- Dostopajte do moči lupine Unix na Microsoft Windows z namestitvijo [Cygwin](https://cygwin.com/). Večina stvari opisanih v tem dokumentu bo delala "Out of the Box".

- Na Windows 10 lahko uporabite [Windows Subsystem for Linux (WSL)](https://msdn.microsoft.com/commandline/wsl/about), ki ponuja znano okolje Bash z orodji ukazne vrstice Unix.

- Če želite v glavnem uporabljati GNU razvojna orodja (kot je GCC) na Windows, premislite o [MinGW](http://www.mingw.org/) in njegovem paketu [MSYS](http://www.mingw.org/wiki/msys), ki ponuja orodja, kot so bash, gawk, make in grep. MSYS nima vseh funkcij v primerjavi s Cygwin. MinGW je posebej uporaben za ustvarjanje izvornih Windows prenosov orodij Unix.

- Druga opcija, da dobite izgled in občutek Unix-a na Windows-u, je [Cash](https://github.com/dthree/cash). Upoštevajte, da so v tem okolju na voljo le nekateri ukazi Unix in opcije ukazne vrstice.

### Uporabna Windows orodja ukazne vrstice

- Izvajate in kodirate lahko večino sistemskih opravil Windows iz ukazne vrstice, če se naučite uporabljati `wmic`.

- Izvorna mrežna orodja ukazne vrstice Windows, ki jih morda najdete uporabne, vključujejo `ping`, `ipconfig`, `tracert` in `netstat`.

- Izvajate lahko [mnoga upporabna opravila Windows](http://www.thewindowsclub.com/rundll32-shortcut-commands-windows) s klicem ukaza `Rundll32`.

### Cygwin nasveti in triki

- Namestite dodatne programe Unix z upraviteljem paketov Cygwin.

- Uporabite `mintty` za vaše okno ukazne vrstice.

- Do odložišča Windows dostopajte preko `/dev/clipboard`.

- Poženite `cygstart`, da odprete poljubno datoteko preko njene registrirane aplikacije.

- Do registra Windows dostopajte z `regtool`.

- Upoštevajte, da pot diska Windows `C:\` postane v Cygwin `/cygdrive/c` in Cigwin-ov `/` se na Windows pojavi pod `C:\cygwin`. Pretvorite med Cygwin in Windows stilom poti datotek s `cygpath`. To je najbolj uporabno v skriptah, ki se sklicujejo na programe Windows.

## Več virov

- [awesome-shell](https://github.com/alebcay/awesome-shell): urejan seznam orodij lupine in virov.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): Bolj poglobljen vodič za macOS ukazno vrstico.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) za pisanje boljših skript lupine.
- [shellcheck](https://github.com/koalaman/shellcheck): lupinska skripta orodja statične analize. V osnovi, lint za bash/sh/zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): Na žalost kompleksne podrobnosti, kako pravilno ravnati z imeni datotek v lupinskih skriptah.
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools): Več koristnih ukazov in orodij za uporabo v znanosti podatkov iz knjige z enakim imenom.

## Pogoji uporabe

Z izjemo zelo majhnih opravil je koda napisana tako, da jo lahko ostali berejo. Z močjo pride odgovornost. Dejstvo, da *lahko* naredite nekaj v Bash-u ne pomeni nujno, da bi morali! ;)


## Licenca

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

To delo je izdano pod [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
