🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*


# Arta liniei de comandă

[![Pune o întrebare](https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg)](https://airtable.com/shrzMhx00YiIVAWJg)

[![Alătură-te discuției https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


- [Meta](#meta)
- [Bazele](#bazele)
- [Folosire zilnică](#folosire-zilnică)
- [Procesarea fișierelor și a datelor](#procesarea-fișierelor-și-a-datelor)
- [Depanarea sistemului](#depanarea sistemului)
- [Comenzi de o linie](#comenzi-de-o-linie)
- [Obscure dar utile](#obscure-dar-utile)
- [Doar pentru OS X](#doar-pentru-os-x)
- [Doar pentru Windows](#doar-pentru-windows)
- [Mai multe resourse](#mai-multe-resurse)
- [Anunț legal](#anunț-legal)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

A folosi linia de comandă în mod eficient este o abilitate ignorată și/sau considerată obscură, dar ajută la creșterea flexibilității și productivității ca inginer. Acest ghid reprezintă o selecție de note și sfaturi pe care le-am găsit utile lucrului în Linux. Unele sfaturi sunt elementare, altele sunt foarte specifice, sofisticate sau obscure. Pagina nu este foarte lungă, dar dacă memorați și folosiți lucrurile de aici atunci știți o cantitate semnificativă de informație.

Această muncă este rezultatul eforturilor [multor autori și translatori](AUTHORS.md).
Multe dintre aceste sfaturi
[au apărut](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[original](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
pe [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
și au fost mutat pe GitHub ulteror, unde alți oameni talentați au produs numeroase îmbunătățiri.
[**Vă rugăm întrebați**](https://airtable.com/shrzMhx00YiIVAWJg) dacă aveți nelămuriri legate de linia de comandă. [**Contribuiți**](/CONTRIBUTING.md) dacă identificați o eroare sau ceva ce ar putea fi îmbunătățit!

## Meta

Scop:

- Acest ghid este atât pentru începători cât și pentru avansați. Scopurile sunt *acoperire* (tot ce este important), *specificitate* (oferirea exemplelor concrete pentru cazurilor comune) și *brevitate* (neincluderea lucrurilor neesențiale sau a digresiunilor ce pot fi găsite ușor în alte părți). Fiecare sfat este esențial în câteva situații sau reduce semnificativ timpul necesar efectuării unei cerințe comparativ cu celelalte alternative.
- Ghidul este scris pentru Linux, cu excepția secțiunilor "[Doar pentru OS X](#doar-pentru-os-x)" și "[Doar pentru Windows](#doar-pentru-windows)". Majoritatea sfaturilor din celelate secțiuni se aplică/pot fi instalate pe alte sisteme Unix sau OS X (chiar și în Cygwin).
- Scopul este pe Bash interactiv, chiar dacă unele sfaturi sunt aplicabile și altor shell-uri sau pentru Bash-scripting în general.
- Atât comenzile Unix "standard" cât și cele care necesită instalarea de pachete speciale sunt incluse -- cât timp sfaturile sunt destul de importante cât să merite incluziunea.

Note:

- Pentru a păstra totul într-o singură pagină, conținutul este inclus implicit doar prin referințe. Suntem siguri că puteți căuta mai multe detalii după ce aveți ideea/comanda după care să căutați. Folosiți `apt-get`, `yum`, `dnf`, `pacman`, `pip` sau `brew` (după caz) pentru a instala programe noi.
- Folosiți [Explainshell](http://explainshell.com/) pentru a obține un util îndrumar în ce anumite comenzi, opțiuni, etc. fac.


## Bazele

- Învățați folosirea de bază a Bash. De fapt, tastați `man bash` și treceți măcar pe diagonală prin tot conținutul; este ușor de citit și nu este prea lung. Shell-uri alternative pot fi frumoase, dar Bash este puternic și disponibil mereu (a învăța *doar* zsh, etc., chiar dacă e tentant pe laptopul propriu, vă restricționează în anumite situații, cum ar fi în folosirea unor servere existente).

- Învățați cel puțin un editor de text. Ideal Vim (`vi`), cum nu există un competitor real pentru editarea în terminal (chiar dacă folosiți Emacs, sau un editor modern în majoritatea timpului).

- Învățați să citiți documentație cu `man` (pentru curiouși, `man man` listează secțiunile, de exemplu 1 este pentru comenzi "uzuale", 5 este pentru fișiere/convenții și 8 pentru administrare). Găsiți pagini de manual cu `apropos`. Rețineți că anumite comenzi nu sunt executable ci comenzi interne în Bash și că puteți obține ajutor despre ele cu `help` sau `help -d`. Puteți vedea dacă o comandă este internă, executabilă sau doar un alias prin folosirea `type command`.

- Învățați despre redirectarea intrării și ieșirii folosint `>` și `<` și pipe-uri cu `|`. Rețineți că `>` suprascrie fișierul și `>>` adaugă la final. Învățați despre ieșirea standard și ieșirea de eroare standard.

- Învățați despre expandarea numelor de fișiere cu `*` (și poate `?` și `[`...`]`) și despre folosirea și diferențele dintre `"` și `'`. (Vedeți mai multe în secțiunea despre expandarea variabilelor mai jos).

- Familiarizați-vă cu managementul job-urilor în Bash: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, etc.

- Învățați `ssh`, și bazele autentificării fără parolă, via `ssh-agent`, `ssh-add`, etc.

- Managementul de bază al fișierelor: `ls` și `ls -l` (în special, învățați ce reprezintă fiecare coloană din `ls -l`), `less`, `head`, `tail` și `tail -f` (sau, mai bine, `less +F`), `ln` și `ln -s` (aprofundați diferențele și avantajele între link-urile hard și cele soft), `chown`, `chmod`, `du` (scurt sumar de folosire: `du -hs *`). Pentru managementul sistemului de fișiere: `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. Învățați ce este un inode (`ls -i` sau `df -i`).

- Concepte de bază de rețea: `ip` sau `ifconfig`, `dig`.

- Învățați și folosiți un sistem de versionare, precum `git`.

- Învățați expresii regulare foarte bine, precum și diversele opțiuni pentru `grep`/`egrep`. Relevante sunt `-i`, `-o`, `-v`, `-A`, `-B`, și `-C`.

- Învațați să folosiți `apt-get`, `yum`, `dnf` sau `pacman` (în funcție de distribuție) pentru a găsi și instala pachete. Fiți siguri că aveți `pip` pentru a instala comenzile bazate pe Python (câteva din utilitarele de mai jos sunt mai ușor de instalat cu `pip`).


## Folosire zilnică

- În Bash, folosiți **Tab** pentru a completa argumente sau a lista comenzile disponibile și **ctrl-r** pentru a căuta în istoricul comenzilor (după apăsare, tastați ce căutați și apăsați repetat **ctrl-r** pentru a cicla prin lista de potriviti, apăsați **Enter** pentru a executa comanda găsită sau săgeată dreapta pentru a putea edita linia curentă).

- În Bash, folosiți **ctrl-w** pentru a șterge ultimul cuvânt și **ctrl-u** pentru a șterge până la începutul liniei. Folosiți **alt-b** și **alt-f** pentru a naviga cuvânt-cu-cuvânt, **ctrl-a**  pentru a muta cursorul la începutul liniei,  **ctrl-e** pentru a-l muta la final, **ctrl-k** pentru a șterge până la finalul liniei, **ctrl-l** pentru a curăța tot ecranul. Vizualizați `man readline` pentru a vedea toate tastele implicite din Bash. Sunt o mulțime. De exemplu, **alt-.** ciclează prin toate argumentele anterioare și **alt-*** expandează un glob pattern.


- Alternativ, dacă doriți să folosiți tastele ca în vi, folosiți `set -o vi` (și `set -o emacs` pentru a vă întoarce).

- Pentru a edita comenzi lungi, după setarea editorului (de exemplu `export EDITOR=vim`), **ctrl-x** **ctrl-e** va deschide un editor cu comanda curentă pentru editare. În stilul vi puteți folosi **escape-v**.

- Comenzile recente le găsiți folosind `history`. Dacă folosiți `!n` (unde `n` este numărul comenzii) atunci o veți executa din nou. Sunt mai multe scurtături pe care le puteți folosi, foarte utile fiind `!$` pentru ultimul argument și `!!` pentru ultima comandă (vedeți "HISTORY EXPANSION" în manual). Acestea pot fi înlocuite ușor cu **ctrl-r** și **alt-.**.

- Navigați către directorul personal cu `cd`. Accesați fișiere relative la acest director cu prefixul `~` (e.g. `~/.bashrc`). În scripturile `sh`, referiți-vă la directorul personal cu `$HOME`.

- Pentru a ajunge înapoi în directorul anterior: `cd -`.

- Dacă sunteți în mijlocul editării unei comenzi dar vreți să renunțați, folosiți **alt-#** pentru a adăuga un `#` la început și a o introduce ca un comentariu (alternativ, **ctrl-a**, **#**, **enter**). Vă puteți întoarce la comandă mai târziu, folosind istoria comenzilor.

- Folosiți `xargs` (sau `parallel`). Este foarte puternic. Puteți controla câte comenzi execută pe o linie (`-L`) și paralelismul (`-L`). Dacă nu sunteți siguri că ați dat comanda corectă, folosiți întâi `xargs echo`. De asemenea, `-I{}` este foarte ultil. Exemple:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` este o modalitate ușoară de a afișa lista de procese

- Folosiți `pgrep` și `pkill` pentru a găsi și semnala procesele după nume (`-f` poate fi util).

- Învățați ce semnale pot fi trimise proceselor. De exemplu, pentru a suspenda un proces puteți folosi `kill -STOP [pid]`. Pentru a obține lista completă, vedeți `man 7 signal`.

- Folosiți `nohup` sau `disown` dacă doriți să trimiteți un proces în fundal sau să-l mențineți rulând permanent.

- Verificați ce procese ascultă pe rețea folosind `netstat -lntp` sau `ss -plat` (pentru TCP; adăugați `-u` pentru UDP).

- Vedeți `lsof` pentru fișiere și socket-uri deschise.

- Vedeți `uptime` sau `w` pentru a afla cât timp sistemul a fost funcțional.

- Folosiți `alias` pentru a crea scurtături pentru comenzile folosie des. De exemplu, `alias ll='ls -latr'` creează un nou alias `ll`.

- Salvați alias-uri, setări shell, și funcții folosite frecvent în `~/.bashrc`, și [instruiți shell-ul de login să-l citească](http://superuser.com/a/183980/7106). Asftel, veți avea aceleași setări în toate terminalele.

- Salvați setările variabilelor de mediu și comenzile care ar trebui executate la login în `~/.bash_profile`. Configurări separate sunt necesare pentru shell-uri lansate prin logarea în mediul grafic sau din task-uri `cron`.

- Sincronizați fișierele de configurare (e.g. `.bashrc` and `.bash_profile`) între mai multe calculatoare folosind Git.

- Tratați cu atenți cazurile când variabilele și fișierele conțin spații. Folosiți ghilimele în acest caz, de exemplu `"$FOO"`. Preferați să folosiți opțiunile `-0` sau `-print0` pentru a folosi caracterul null pentru a delimita fișierele, de exemplu `locate -0 pattern | xargs -0 ls -al` sau `find / -print0 -type d | xargs -0 ls -al`. Pentru a parcurge o listă de fișiere conținând spații într-o buclă for, setați variabile IFS la terminatorul de linie, `IFS=$'\n'`.

- În scripturile Bash, folosiți `set -x` (sau varianta `set -v`, care produce informație neprocesată, inclusiv variabile neexpandate și comentarii) pentru a depana outputul. Folosiți modurile strice exceptând când aveți un motiv foarte bun împotrivă: folosiți `set -e` pentru a termina execuția în caz de eroare (cod de ieșire nenul). Folosiți `set -u` pentru a detecta variable nesetate. Considerați folosirea `set -o pipefail` pentru erorile cauzate de folosirea eronată a pipe-urilor. Pentru scripturi mai complicate, folosiți `trap` pentru EXIT sau ERR. Un obicei util este să începeți scriptul într-o modalitate care va permite detecția facilă a erorilor și terminarea execuției cu un mesaj:
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- În scripturile Bash, subshell-urile (delimitate de paranteze) sunt un mod convenabil pentru a grupa comenzi. De exemplu, va puteți muta într-un alt director:
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- În Bash, există mai multe variante de expandare a variabilelor. Verifacți dacă o variabilă există: `${name:?error message}`. De exemplu, dacă un script necesită un argument unic, folosiți `input_file=${1:?usage: $0 input_file}`. Folosți o valoare implicită pentru cazul când o variabilă este goală: `${name:-default}`. Pentru parametri opționali în exemplul anterior, folosiți `output_file=${2:-logfile}`. Dacă `$2` este omis (gol), `output_file` va fi setat la `logfile`. Expandare aritmetică: `i=$(( (i + 1) % 5 ))`. Secvențe: `{1..10}`. Tăierea unor secvențe din șiruri: `${var%suffix}` și `${var#prefix}`. De exemplu, dacă `var=foo.pdf`, atunci `echo ${var%.pdf}.txt` va scrie `foo.txt`.

- Expandarea parantezelor folosind `{`...`}` previne re-tastarea textelor similare, automatizând combinațiile de itemuri. Este util în exemple precum `mv foo.{txt,pdf} some-dir` (care mută ambele fișiere), `cp somefile{,.bak}` (care se expandează la `cp somefile somefile.bak`) sau `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (care expandează toate combinațiile posibile și creează arborele de directoare).

- Outputul unei comenzi poate fi tratat ca un fișier cu `<(some command)`. De exemplu, pentru a compara fișierul `/etc/hosts` local cu unul la distanță:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Când scrieți cod, puteți prefera să încadrați tot codul în acolade. Dacă acolada de final lipsește, scriptul nu va rula. Este un lucru util, în special pentru scripturile de pe web pentru că previne execuția scripturilor parțial descărcate:
```bash
{
      # Your code here
}
```

- Folosiți "here documents", de exemplu `cat <<EOF ...`.

- În Bash, redirectați ieșirea standard și eroarea standard cu `some-command >logfile 2>&1` sau `some-command &>logfile`. De regulă, pentru a vă asigura că o comandă nu lasă un fișier deschis, fiind legată de terminalul curent, este o practică bună să adăugați `</dev/null`.

- Folosiți `man ascii` pentru o tabelă ASCII foarte bună, cu valori în hex și decimal. Pentru informatii generale de codificare,  `man unicode`, `man utf-8`, și `man latin1` sunt utile.

- Folosiți `screen` sau [`tmux`](https://tmux.github.io/) pentru a multiplexa terminalul, în special în cazul sesiunilor ssh. `byobu` poate îmbunătăți screen sau tmux fiind mai ușor de folosit. O interfață minimală pentru persistența sesiunilor este [`dtach`](https://github.com/bogner/dtach).

- În ssh, este util să știți cum să tunelați cu `-L` sau `-D` (și ocazional `-R`), e.g. pentru a accesa site-uril de pe un server remote.

- Este foarte util să optimizați configurațiile ssh, de exemplu, setarea următoare din `~/.ssh/config` permite prevenția sesiunilor eșuate în anumite condiții de rețea, folosește compresia (utilă pentru `scp` sau conexiuni peste rețele cu lățime de bandă redusă) și multiplexează canale către același server folosind un fișier de control local:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Un număr de alte opțiuni sunt relevante pentru securitate și trebuiesc tratate cu atenție, de exemplu, setări pe rețea sau mașină: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- Considerați folosirea [`mosh`](https://mosh.mit.edu/) ca o alternativă la ssh care folosește UDP, prevenind conexiunile eșuate (neceistă setup pe partea de server).

- Pentru a obține permisiunile unui fișier în forma octală, lucru util pentru configurarea sistemului, dar nedisponibil în `ls`, folosiți ceva precum:
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Pentru selecția interactivă a valorilor dintr-o altă comandă, folosiți [`percol`](https://github.com/mooz/percol) sau [`fzf`](https://github.com/junegunn/fzf).

- Pentru interacțiunea cu fișiere rezultate din outputul unei alte comenzi (like `git`), folosiți `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- Un simplu server web pentru fișierele din directorul curent și subdirectoare, disponibil pentru toți din rețeaua dumneavoastră, folosiți
`python -m SimpleHTTPServer 7777` (pentru port 7777 și Python 2) și `python -m http.server 7777` (pentru port 7777 și Python 3).

- Puteți rula o comandă ca un alt user folosind `sudo`. Implicit se va rula ca root, folosiți `-u` pentru a specifica utilizatorul. Folosiți `-i` pentru a vă loga ca acel utilizator, folosind parola _voastră_.

- Pentru a schimba tot shellul către alt user, folosiți `su username` sau `su - username`. Versiunea cu `-` obține și mediul, ca si cum userul tocmai s-a logat. Username-ul implicit este root. Veți fi întrebat parola _utilizatorului către care faceți schimbarea_.

- Amintiți-vă că orice linie de comandă are o limită de [128K](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong). Eroarea "Argument list too long" (listă de argumente prea lungă) este comună dacă un număr mare de fișiere se potrivesc unui șablon. (În acest caz, alternative precum `find` și `xargs` ajută.)

- Un calculator în bash poate fi obținut prin access to Python: `python`:
```
>>> 2+3
5
```


## Procesarea fișierelor și a datelor

- Pentru a localiza un fișier după nume, în directorul curend, `find . -iname '*something*'` (sau similar). Pentru a găsi un fișier oriunde, `locate something` (dar țineți cont de faptul că `updatedb` s-ar putea să nu fi indexat fișierele recente).

- Pentru a căuta în interiorul fișierelor (mai avansat decât `grep -r`), folosiți [`ag`](https://github.com/ggreer/the_silver_searcher).

- Pentru a converti HTML la text: `lynx -dump -stdin`

- For Markdown, HTML, and all kinds of document conversion, try [`pandoc`](http://pandoc.org/).

- Dacă trebuie să folosiți XML, `xmlstarlet` e vechi dar util.

- Pentru JSON, folosiți [`jq`](http://stedolan.github.io/jq/).

- Pentru YAML, folosiți [`shyaml`](https://github.com/0k/shyaml).

- Pentru Excel sau CSV files, [csvkit](https://github.com/onyxfish/csvkit) oferă `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, etc.

- Pentru Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) este ușor de folosit și [`s4cmd`](https://github.com/bloomreach/s4cmd) este mai rapid. [`aws`](https://github.com/aws/aws-cli) de la Amazon și varianta îmbunătățită [`saws`](https://github.com/donnemartin/saws) sunt esențiale pentru alte task-uri legate de AWS.

- Învățați `sort` și `uniq`, inclusiv opțiunile `-u` și `-d` pentru `uniq` -- mai multe exemple în secțiunea de comenzi de o linie, mai jos. Vedeți și `comm`.

- Aflați despre `cut`, `paste`, și `join` pentru a manipula fișiere text. Mulți oameni folosesc `cut` dar uită de `join`.

- Informați-vă despre `wc` pentru a număra liniile (`-l`), caracterele (`-m`), cuvintele (`-w`) și octeții (`-c`) dintr-un fișier.

- Folosți `tee` pentru a copia de la intrarea standard (stdin) într-un fișier și la ieșirea standard (stdout) simultan, ca în `ls -al | tee file.txt`.

- Pentru operații mai complexe, inclusiv grupare, inversare de câmpuri și statistică, considerați folosirea [`datamash`](https://www.gnu.org/software/datamash/).

- Țineți minte că localizarea (`locale`) influențează foarte multe comenzi în moduri subtile, inclusiv sortare sau performanță. Majoritatea instalărilor Linux setează `LANG` și alte variabile de localizare la o setare precum US English. Sortarea se va schimba dacă schimbați localizare. De asemenea, rutinele de internaționalizare (i18n) pot face comenzile să se execute *mult, mult* mai încet. În unele situații (precum operațiile pe mulțimi de mai jos), puteți ignora rutinele încete de la i18n și folosi sortarea bazată pe octeți, folosind `export LC_ALL=C`.

- Puteți seta localizarea specifică unei comenzi prin prefixarea acesteia cu variabila de mediu corespunzătoare, ca în `TZ=Pacific/Fiji date`.

- Pentru procesare de bază a textelor, folosiți `awk` și `sed`. De exemplu, pentur a aduna suma numerelor din coloana a treia a unui fișier `awk '{ x += $3 } END { print x }'` este de 3 ori mai rapid și mai scurt decât codul echivalent în Python.

- Pentru a înlocui toate aparițiile unui șir, în cel puțin un fișier:
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- Pentru a redenumi fișiere multiple și/sau căuta în fișiere încercați [`repren`](https://github.com/jlevy/repren). (În  unele cazuri, comanda `rename` permite redenumiri multiple, dar țineți cont că funcționalitatea ei nu este aceeași în toate distribuțiile Linux)
```sh
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Recover backup files whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Same as above, using rename, if available:
      rename 's/\.bak$//' *.bak
```

- După cum zice și pagina de manual, `rsync` este un utilitar foarte rapid, eficient și versatil de a copia fișiere. Este cunoscut pentru sincronizarea între calculatoare dar poate fi folosit și local. Dacă setăruile de securitate permit, folosirea `rsync` în loc de `scp` permite continuarea unui transfer eșuat fără a-l reporni. Este și una dintre cele [mai rapide metode](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) de a șterge un număr masiv de fișiere:
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Folosiți `shuf` pentru a permuta sau selecta linii aleatoare dintr-un fișier.

- Învățați opțiunile lui `sort`. ForPentru numere folosiți `-n`, sau `-h` pentru numere în format human-readable (de exemplu numere produse de `du -h`). Învățați cum funcționează cheile de sortare (`-t` și `-k`). În special, țineți cont că trebuie să scrieți `-k1,1` pentru a sorta doar prima coloană, `-k1` înseamnă sortare după toată linia. Sortarea stabilă (`sort -s`) poate fi utilă. De exemplu, pentru a sorta după câmpul 2 și apoi după 1: `sort -k1,1 | sort -s -k2,2`.

- Dacă sunteți nevoiți să scrieți un caracter tab în terminal (de exemplu pentru argumentul `-t` al `sort`) apăsați **ctrl-v** **[Tab]** sau scrieți `$'\t'` (ultima versiune e mai bună pentru că permite și copy/paste).

- Utilitarele standard pentru patch-uirea codului sunt `diff` și `patch`. De asemenea `diffstat` poate fi folosit pentru sumarizarea unui diff și `sdiff` pentru un diff side-by-side. Țineți cont că `diff -r` operează pe directoare întregi. Folosiți `diff -r tree1 tree2 | diffstat` pentru un sumar al modificărilor. Folosiți `vimdiff` pentru a compara și edita fișiere.

- Pentru fișiere binare, folosiți `hd`, `hexdump` sau `xxd` pentru operații simple și `bvi` sau `biew` pentru editare binară

- Tot pentru fișiere binare, `strings` (plus `grep`, etc.) permite găsirea bucăților de text.

- Pentru diff-uri binare (compresie delta), folosiți `xdelta3`.

- Pentru a converti codificarea textului, folosiți `iconv` sau `uconv` pentru utilizări mai avansate. Ambele suportă același set de Unicode. De exemplu, comanda următoare transformă în minuscule și elimină accentele (prin expandare sau coborâre):
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- Pentru a împărți un text în fragmente, folosiți `split` (după dimensiune) și `csplit` (după un șablon).

- Folosiți `dateadd`, `datediff`, `strptime` etc. din [`dateutils`](http://www.fresse.org/dateutils/) pentru a manipula expresii legate de timp, dată și oră.

- Pentru a opera pe fișiere comprimate: `zless`, `zmore`, `zcat`, and `zgrep`

- Atributele fișierelor pot fi stabilite cu `chattr` și oferă o alternativă de nivel scăzut la permisiunile unui fișier. De exemplu, pentru a vă proteja împotriva ștergerii accidentale puteți folosi flag-ul immutable: `sudo chattr +i /critical/directory/or/file`

- Folosiți `getfacl` și `setfacl` pentru a salva și restaura permisiunile unui fișier. De exemplu:
```sh
   getfacl -R /some/path > permissions.txt
   setfacl --restore=permissions.txt
```

## Depanarea sistemului

- Pentru depanarea problemelor legate de internet/web, `curl` și `curl -I` sunt foarte utile, la fel și echivalentele bazate pe `wget` sau pe modernul [`httpie`](https://github.com/jkbrzt/httpie).

- Pentru a vedea starea curentă a CPU-ului sau discului, instrumentele clasice sunt `top` (mai bine `htop`), `iostat`, și `iotop`. Folosiți `iostat -mxz 15` pentru informații de bază despre CPU și detaliate depsre partițiile fiecărui disc, împreună cu sfaturi pentru îmbunătățirea performanței.

- Pentru detalii legate de conexiunile la rețea, folosiți `netstat` și `ss`.

- O vedere de ansamblu a sistemului poate fi obținută folosind `dstat`. Pentru detalii, folosiți [`glances`](https://github.com/nicolargo/glances).

- Pentru a vedea starea curentă a memoriei, folosiți și analizați rezultatele `free` și `vmstat`. În particular, țineți cont că valoarea "cached" este memorie reținută de Linux ca un spațiu cache pentru fișiere, deci este efectiv spațiu "liber".

- Depanarea sistemului Java este deosebită dar un truc simplu pe anumite JVM-uri (inclusiv Oracle) este că puteți rula `kill -3 <pid>` și veți obține un stack trace complet și informații despre memoria heap, inclusiv detalii despre garbage collector. Utilitarele `jps`, `jstat`, `jstack`, `jmap` din JDK pot fi utile. [Utilitarele SJK](https://github.com/aragozin/jvm-tools) sunt mai avansate.

- Folosiți [`mtr`](http://www.bitwizard.nl/mtr/) ca un `traceroute` mai bun pentru a identifica problemele de rețea.

- Pentru a identifica de ce un disc este plin, [`ncdu`](https://dev.yorhel.nl/ncdu) salvează timp comparativ cu folosirea comenzilor uzuale precum `du -sh *`.

- Pentru a identifica socket-ul sau procesul care consumă cea mai mare bandă din rețea folosiți [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) sau [`nethogs`](https://github.com/raboof/nethogs).

- Utilitarul `ab` (vine cu Apache) este util pentru a testa rapid performanța serverului web. Pentru testare mai complexă folosiți `siege`.

- Pentru depanarea și mai serioasă a rețelei folosiți [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html), sau [`ngrep`](http://ngrep.sourceforge.net/).

- Învățați despre `strace` și `ltrace`. Aceste utilitare sunt utile dacă un program eșuează, se blochează sau crapă și nu știți de ce, sau dacă vreți să obțineți detalii generale despre performanță. Evidențiem opțiunea de profiling (`-c`), și abilitatea de atașare la un proces care rulează (`-p`).

- Folosiți `ldd` pentru a verifica bibliotecile dinamice, etc.

- Folosiți `gdb` pentru a vă conecta la un proces care rulează și a obține un stack trace.

- Folosiți `/proc`. Este foarte util în depanarea problemelor pe viu. Exemple: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (unde `xxx` este id-ul procesului - PID-ul lui).

- Pentru a depana ceva ce a fost greșit în trecut, [`sar`](http://sebastien.godard.pagesperso-orange.fr/) poate fi foarte util. Arată statistici istorice despre CPU, memorie, rețea, etc.

- Pentru analize de detaliu pentru performanța sistemului, folosiți `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_(Linux)), și [`sysdig`](https://github.com/draios/sysdig).

- Verificați ce sistem de operare folosiți cu `uname` sau `uname -a` (detalii generale despre nucleu) sau `lsb_release -a` (Linux distro).

- Folosiți `dmesg` oricând ceva funcționează total aiurea (probabil din cauza hardware-ului sau a dispozitivelor fizice).

- Dacă ștergeți un fișier și nu se eliberează cantitatea de spațiu de pe disc la care vă așteptați (conform `du`), verificați să nu cumva aveți fișierul folosit de un proces:
`lsof | grep deleted | grep "filename-of-my-big-file"`


## One-liners

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


## Obscure dar utile

- `expr`: execută operații aritmetice sau boleene și expandează expresii regulate

- `m4`: procesor simplu de macro-uri

- `yes`: afișează un șir de un număr infinit de ori

- `cal`: calendar

- `env`: execută o comandă (util în scripturi)

- `printenv`: afișează variabilele de mediu (util pentru depanare și scripturi)

- `look`: idenfică cuvinte în engleză (sau linii de fișier) care încep cu un șir

- `cut`, `paste` and `join`: manipulează date

- `fmt`: formatează paragrafe de text

- `pr`: formatează textul în paragrafe și coloane

- `fold`: înfășoară liniile unui text

- `column`: formatează textul în coloane de lungime fixă, în tabele

- `expand` și `unexpand`: convertește între tab-uri și spații

- `nl`: adaugă numere liniilor

- `seq`: afișează numere

- `bc`: calculator

- `factor`: factorizează întregi

- [`gpg`](https://gnupg.org/): criptează și semnează fișiere

- `toe`: tabel de informații despre terminal

- `nc`: depanare rețea și transfer de date

- `socat`: socket relay și forwarder pentru porturi tcp (similar cu `netcat`)

- [`slurm`](https://github.com/mattthias/slurm): vizualizează traficul de rețea

- `dd`: mută datele între fișiere și device-uri

- `file`: identifică tipul unui fișier

- `tree`: arată un arbore de directoare și subdirectoare, ca `ls` dar recursiv

- `stat`: informații despre fișier

- `time`: execută și cronometrează o comandă

- `timeout`: execută o comandă până la expirarea unei cantițăți de timp, omorând procesul la finalul timpului alocat

- `lockfile`: creează un fișier semafor care nu poate fi șters decât cu `rm -f`

- `logrotate`: rotește, comprimă și trimite jurnalele pe mail

- `watch`: execută o comandă în mod repetat, arătând rezultatele și/sau evidențiind diferențele

- `tac`: afișează conținutul fișierelor în ordine inversă

- `shuf`: selectează linii random din fișier

- `comm`: compară fișiere sortate, linie cu linie

- `pv`: monitorizează progresul datelor într-un pipe

- `hd`, `hexdump`, `xxd`, `biew` și `bvi`: afișează sau editează fișiere binare

- `strings`: extrage șiruri din fișiere

- `tr`: translatează și manipulează caractere

- `iconv` sau `uconv`: conversie între codificările posibile ale unui text

- `split` și `csplit`: sparge fișiere în componente

- `sponge`: citește tot inputul înainte de a-l afișa, util pentru a citi și apoi a scrie în același fișier: `grep -v something some-file | sponge some-file`

- `units`: conversii între unități de măsură (vedeți și `/usr/share/units/definitions.units`)

- `apg`: generateză parole random

- `xz`: compresor de fișiere foarte eficient

- `ldd`: informații despre bibliotecile dinamice

- `nm`: simboluri din fișierele obiect

- `ab`: benchmarking pentru servere web

- `strace`: depanare apeluri de sistem

- [`mtr`](http://www.bitwizard.nl/mtr/): alternative mai bună pentru `traceroute` pentru depanarea rețelei

- `cssh`: shell vizual, concurent

- `rsync`: sincronizează fișiere peste SSH sau local

- [`wireshark`](https://wireshark.org/) și [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): capturează trafic de rețea și depanează rețeaua

- [`ngrep`](http://ngrep.sourceforge.net/): grep pentru rețea

- `host` și `dig`: interogări DNS

- `lsof`: informații despre descriptorii de fișiere și sockeți

- `dstat`: statistici utile despre sistem

- [`glances`](https://github.com/nicolargo/glances): statistici utile despre sistem, la nivel înalt

- `iostat`: statistici despre folosirea discului

- `mpstat`: statistici despre folosirea CPU

- `vmstat`: statistici despre folosirea memoriei

- `htop`: versiune îmbunătățită a `top`

- `last`: istoria login-urilor

- `w`: cine este logged-in

- `id`: informații despre useri/grupuri

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): istoria statisticilor despre sistem

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) sau [`nethogs`](https://github.com/raboof/nethogs): utilizarea rețelei de fiecare socket sau proces

- `ss`: statistici socket

- `dmesg`: erori de sistem sau de pornirea sistemului

- `sysctl`: vizualizează și configurează parametrii nucleului Linux

- `hdparm`: manipulare/performanță pentru discuri SATA/ATA

- `lsblk`: afișează dispozitivele block: discuri și partiții

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: informații hardware, incluzând CPU, BIOs, RAID, plăci grafice, dispozitive, etc.

- `lsmod` și `modinfo`: afișează module de kernel

- `fortune`, `ddate`, și `sl`: depinde dacă considerați locomotive și citate "utile" (utilitare distractive)


## OS X only

These are items relevant *only* on OS X.

- Package management with `brew` (Homebrew) and/or `port` (MacPorts). These can be used to install on OS X many of the above commands.

- Copy output of any command to a desktop app with `pbcopy` and paste input from one with `pbpaste`.

- To enable the Option key in OS X Terminal as an alt key (such as used in the commands above like **alt-b**, **alt-f**, etc.), open Preferences -> Profiles -> Keyboard and select "Use Option as Meta key".

- To open a file with a desktop app, use `open` or `open -a /Applications/Whatever.app`.

- Spotlight: Search files with `mdfind` and list metadata (such as photo EXIF info) with `mdls`.

- Be aware OS X is based on BSD Unix, and many commands (for example `ps`, `ls`, `tail`, `awk`, `sed`) have many subtle variations from Linux, which is largely influenced by System V-style Unix and GNU tools. You can often tell the difference by noting a man page has the heading "BSD General Commands Manual." In some cases GNU versions can be installed, too (such as `gawk` and `gsed` for GNU awk and sed). If writing cross-platform Bash scripts, avoid such commands (for example, consider Python or `perl`) or test carefully.

- To get OS X release information, use `sw_vers`.

## Windows only

These items are relevant *only* on Windows.

- On Windows 10, you can use [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about), which provides a familiar Bash environment with Unix command line utilities. On the plus side, this allows Linux programs to run on Windows. On the other hand this does not support the running of Windows programs from the Bash prompt.

- Access the power of the Unix shell under Microsoft Windows by installing [Cygwin](https://cygwin.com/). Most of the things described in this document will work out of the box.

- Install additional Unix programs with the Cygwin's package manager.

- Use `mintty` as your command-line window.

- Access the Windows clipboard through `/dev/clipboard`.

- Run `cygstart` to open an arbitrary file through its registered application.

- Access the Windows registry with `regtool`.

- Note that a `C:\` Windows drive path becomes `/cygdrive/c` under Cygwin, and that Cygwin's `/` appears under `C:\cygwin` on Windows. Convert between Cygwin and Windows-style file paths with `cygpath`. This is most useful in scripts that invoke Windows programs.

- You can perform and script most Windows system administration tasks from the command line by learning and using `wmic`.

- Another option to get Unix look and feel under Windows is [Cash](https://github.com/dthree/cash). Note that only very few Unix commands and command-line options are available in this environment.

- An alternative option to get GNU developer tools (such as GCC) on Windows is [MinGW](http://www.mingw.org/) and its [MSYS](http://www.mingw.org/wiki/msys) package, which provides utilities such as bash, gawk, make and grep. MSYS doesn't have all the features compared to Cygwin. MinGW is particularly useful for creating native Windows ports of Unix tools.

## More resources

- [awesome-shell](https://github.com/alebcay/awesome-shell): A curated list of shell tools and resources.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): A more in-depth guide for the OS X command line.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) for writing better shell scripts.
- [shellcheck](https://github.com/koalaman/shellcheck): A shell script static analysis tool. Essentially, lint for bash/sh/zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): The sadly complex minutiae on how to handle filenames correctly in shell scripts.
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools): More commands and tools helpful for doing data science, from the book of the same name

## Disclaimer

With the exception of very small tasks, code is written so others can read it. With power comes responsibility. The fact you *can* do something in Bash doesn't necessarily mean you should! ;)


## License

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
