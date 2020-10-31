🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [polski](README-pl.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*


# Arta liniei de comandă

[![Pune o întrebare](https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg)](https://airtable.com/shrzMhx00YiIVAWJg)

[![Alătură-te discuției https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


- [Meta](#meta)
- [Bazele](#bazele)
- [Folosire zilnică](#folosire-zilnică)
- [Procesarea fișierelor și a datelor](#procesarea-fișierelor-și-a-datelor)
- [Depanarea sistemului](#depanarea-sistemului)
- [Comenzi de o linie](#comenzi-de-o-linie)
- [Obscure dar utile](#obscure-dar-utile)
- [Doar pentru OS X](#doar-pentru-os-x)
- [Doar pentru Windows](#doar-pentru-windows)
- [Mai multe resurse](#mai-multe-resurse)
- [Anunț legal](#anunț-legal)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

A folosi linia de comandă în mod eficient este o abilitate ignorată și/sau considerată obscură, dar ajută la creșterea flexibilității și productivității ca inginer atât în mod evident dar și în aspecte subtile. Acest ghid reprezintă o selecție de note și sfaturi pe care le-am găsit utile lucrului în Linux. Unele sfaturi sunt elementare, altele sunt foarte specifice, sofisticate sau obscure. Pagina nu este foarte lungă, dar dacă memorați și folosiți lucrurile de aici atunci știți o cantitate semnificativă de informație.

Această muncă este rezultatul eforturilor [multor autori și translatori](AUTHORS.md).
Multe dintre aceste sfaturi
[au apărut](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[original](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
pe [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
și au fost mutate pe GitHub ulterior, unde oameni mai talentați decât autorul original au produs numeroase îmbunătățiri.
[**Vă rugăm întrebați**](https://airtable.com/shrzMhx00YiIVAWJg) dacă aveți nelămuriri legate de linia de comandă. [**Contribuiți**](/CONTRIBUTING.md) dacă identificați o eroare sau ceva ce ar putea fi îmbunătățit!

## Meta

Scop:

- Acest ghid este atât pentru începători cât și pentru avansați. Scopurile sunt *acoperire* (tot ce este important), *specificitate* (oferirea exemplelor concrete pentru cazurilor comune) și *brevitate* (neincluderea lucrurilor neesențiale sau a digresiunilor ce pot fi găsite ușor în alte părți). Fiecare sfat este esențial în câteva situații sau reduce semnificativ timpul necesar efectuării unei cerințe comparativ cu celelalte alternative.
- Ghidul este scris pentru Linux, cu excepția secțiunilor "[Doar pentru OS X](#doar-pentru-os-x)" și "[Doar pentru Windows](#doar-pentru-windows)". Majoritatea sfaturilor din celelalte secțiuni se aplică/pot fi instalate pe alte sisteme Unix sau OS X (chiar și în Cygwin).
- Se pune accent pe Bash interactiv, chiar dacă unele sfaturi sunt aplicabile și altor shell-uri sau pentru Bash-scripting în general.
- Atât comenzile Unix "standard" cât și cele care necesită instalarea de pachete speciale sunt incluse -- cât timp sfaturile sunt destul de importante cât să merite incluziunea.

Note:

- Pentru a păstra totul într-o singură pagină, conținutul este inclus implicit doar prin referințe. Suntem siguri că puteți căuta mai multe detalii după ce aveți ideea/comanda după care să căutați. Folosiți `apt-get`, `yum`, `dnf`, `pacman`, `pip` sau `brew` (după caz) pentru a instala programe noi.
- Folosiți [Explainshell](http://explainshell.com/) pentru a obține explicații utile despre ce fac anumite comenzi, opțiuni, etc.


## Bazele

- Învățați folosirea de bază a Bash. De fapt, tastați `man bash` și treceți măcar pe diagonală prin tot conținutul; este ușor de citit și nu este prea lung. Shell-uri alternative pot fi interesante, dar Bash este puternic și disponibil mereu (a învăța *doar* zsh, etc., chiar dacă e tentant pe laptopul propriu, vă restricționează în anumite situații, cum ar fi în folosirea unor servere existente).

- Învățați cel puțin un editor de text. Editorul `nano` este foarte simplu pentru editare de bază (deschide, scriere, salvare, căutare). Dar, pentru utilizare eficientă din terminal, nu există echivalent pentru Vim (`vi`), editorul mai greu de învățat dar respectat, rapid și cu multe facilități. Mulți oameni folosesc și Emacs, în special pentru eforturile majore de editare. (Desigur, este puțin probabil ca un software developer modern care lucrează la proiecte mari să folosească doar editoare pur bazate pe text; deci ar trebui să vă familiarizați și cu editoare integrate -- IDE -- și unelte moderne).

- Învățați să citiți documentație cu `man` (pentru curioși, `man man` listează secțiunile, de exemplu 1 este pentru comenzi "uzuale", 5 este pentru fișiere/convenții și 8 pentru administrare). Găsiți pagini de manual cu `apropos`. Rețineți că anumite comenzi nu sunt programe executabile ci comenzi interne în Bash și că puteți obține ajutor despre ele cu `help` sau `help -d`. Puteți vedea dacă o comandă este internă, executabilă sau doar un alias prin folosirea `type command`.

- Învățați despre redirecționarea intrării și ieșirii folosind `>` și `<` și pipe-uri cu `|`. Rețineți că `>` suprascrie fișierul și `>>` adaugă la final. Învățați despre ieșirea standard și ieșirea de eroare standard.

- Învățați despre expandarea numelor de fișiere cu `*` (și poate `?` și `[`...`]`) și despre folosirea și diferențele dintre `"` și `'`. (Vedeți mai multe în secțiunea despre expandarea variabilelor mai jos).

- Familiarizați-vă cu managementul job-urilor în Bash: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, etc.

- Învățați `ssh`, și bazele autentificării fără parolă, via `ssh-agent`, `ssh-add`, etc.

- Managementul de bază al fișierelor: `ls` și `ls -l` (în special, învățați ce reprezintă fiecare coloană din `ls -l`), `less`, `head`, `tail` și `tail -f` (sau, mai bine, `less +F`), `ln` și `ln -s` (aprofundați diferențele și avantajele între link-urile hard și cele soft), `chown`, `chmod`, `du` (scurt sumar de folosire: `du -hs *`). Pentru managementul sistemului de fișiere: `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. Învățați ce este un inode (`ls -i` sau `df -i`).

- Concepte de bază de rețea: `ip` sau `ifconfig`, `dig`.

- Învățați și folosiți un sistem de versionare, precum `git`.

- Învățați expresii regulare foarte bine, precum și diversele opțiuni pentru `grep`/`egrep`. Relevante sunt `-i`, `-o`, `-v`, `-A`, `-B`, și `-C`.

- Învățați să folosiți `apt-get`, `yum`, `dnf` sau `pacman` (în funcție de distribuție) pentru a găsi și instala pachete. Fiți siguri că aveți `pip` pentru a instala comenzile bazate pe Python (câteva din utilitarele de mai jos sunt mai ușor de instalat cu `pip`).


## Folosire zilnică

- În Bash, folosiți **Tab** pentru a completa argumente sau a lista comenzile disponibile și **ctrl-r** pentru a căuta în istoricul comenzilor (după apăsare, tastați ce căutați și apăsați repetat **ctrl-r** pentru a cicla prin lista de potriviri, apăsați **Enter** pentru a executa comanda găsită sau săgeată dreapta pentru a putea edita linia curentă).

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

- Tratați cu atenție cazurile când variabilele și fișierele conțin spații. Folosiți ghilimele în acest caz, de exemplu `"$FOO"`. Preferați să folosiți opțiunile `-0` sau `-print0` pentru a folosi caracterul null pentru a delimita fișierele, de exemplu `locate -0 pattern | xargs -0 ls -al` sau `find / -print0 -type d | xargs -0 ls -al`. Pentru a parcurge o listă de fișiere conținând spații într-o buclă for, setați variabile IFS la terminatorul de linie, `IFS=$'\n'`.

- În scripturile Bash, folosiți `set -x` (sau varianta `set -v`, care produce informație neprocesată, inclusiv variabile neexpandate și comentarii) pentru a depana outputul. Folosiți modurile strice exceptând când aveți un motiv foarte bun împotrivă: folosiți `set -e` pentru a termina execuția în caz de eroare (cod de ieșire nenul). Folosiți `set -u` pentru a detecta variabile nesetate. Considerați folosirea `set -o pipefail` pentru erorile cauzate de folosirea eronată a pipe-urilor. Pentru scripturi mai complicate, folosiți `trap` pentru EXIT sau ERR. Un obicei util este să începeți scriptul într-o modalitate care va permite detecția facilă a erorilor și terminarea execuției cu un mesaj:
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

- Expandarea parantezelor folosind `{`...`}` previne re-tastarea textelor similare, automatizând combinațiile de elemente. Este util în exemple precum `mv foo.{txt,pdf} some-dir` (care mută ambele fișiere), `cp somefile{,.bak}` (care se expandează la `cp somefile somefile.bak`) sau `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (care expandează toate combinațiile posibile și creează arborele de directoare).

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

- În Bash, redirecționați ieșirea standard și eroarea standard cu `some-command >logfile 2>&1` sau `some-command &>logfile`. De regulă, pentru a vă asigura că o comandă nu lasă un fișier deschis, fiind legată de terminalul curent, este o practică bună să adăugați `</dev/null`.

- Folosiți `man ascii` pentru o tabelă ASCII foarte bună, cu valori în hex și decimal. Pentru informatii generale de codificare,  `man unicode`, `man utf-8`, și `man latin1` sunt utile.

- Folosiți `screen` sau [`tmux`](https://tmux.github.io/) pentru a multiplexa terminalul, în special în cazul sesiunilor ssh. `byobu` poate îmbunătăți screen sau tmux fiind mai ușor de folosit. O interfață minimală pentru persistența sesiunilor este [`dtach`](https://github.com/bogner/dtach).

- În ssh, este util să știți cum să creați un tunel cu `-L` sau `-D` (și ocazional `-R`), e.g. pentru a accesa site-urile de pe un server aflat la distanță.

- Este foarte util să optimizați configurațiile ssh, de exemplu, setarea următoare din `~/.ssh/config` permite prevenirea sesiunilor eșuate în anumite condiții de rețea, folosește compresia (utilă pentru `scp` sau conexiuni peste rețele cu lățime de bandă redusă) și multiplexează canale către același server folosind un fișier de control local:
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

- Considerați folosirea [`mosh`](https://mosh.mit.edu/) ca o alternativă la ssh care folosește UDP, prevenind conexiunile eșuate (necesită setări pe partea de server).

- Pentru a obține permisiunile unui fișier în forma octală, lucru util pentru configurarea sistemului, dar nedisponibil în `ls`, folosiți ceva precum:
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Pentru selecția interactivă a valorilor dintr-o altă comandă, folosiți [`percol`](https://github.com/mooz/percol) sau [`fzf`](https://github.com/junegunn/fzf).

- Pentru interacțiunea cu fișiere rezultate din outputul unei alte comenzi (like `git`), folosiți `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- Un simplu server web pentru fișierele din directorul curent și subdirectoare, disponibil pentru toți din rețeaua dumneavoastră, folosiți
`python -m SimpleHTTPServer 7777` (pentru port 7777 și Python 2) și `python -m http.server 7777` (pentru port 7777 și Python 3).

- Puteți rula o comandă ca un alt utilizator folosind `sudo`. Implicit se va rula ca root, folosiți `-u` pentru a specifica utilizatorul. Folosiți `-i` pentru a vă loga ca acel utilizator, folosind parola _voastră_.

- Pentru a schimba tot shellul către alt utilizator, folosiți `su utilizator` sau `su - utilizator`. Versiunea cu `-` obține și mediul, ca si cum utilizatorul tocmai s-a logat. Username-ul implicit este root. Veți fi întrebat parola _utilizatorului către care faceți schimbarea_.

- Amintiți-vă că orice linie de comandă are o limită de [128K](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong). Eroarea "Argument list too long" (listă de argumente prea lungă) este comună dacă un număr mare de fișiere se potrivesc unui șablon. (În acest caz, alternative precum `find` și `xargs` ajută.)

- Un calculator simplu poate fi accesat utilizând `python`. De exemplu:
```
>>> 2+3
5
```


## Procesarea fișierelor și a datelor

- Pentru a localiza un fișier după nume, în directorul curent, `find . -iname '*something*'` (sau similar). Pentru a găsi un fișier oriunde, `locate something` (dar țineți cont de faptul că `updatedb` s-ar putea să nu fi indexat fișierele recente).

- Pentru a căuta în interiorul fișierelor (mai avansat decât `grep -r`), folosiți [`ag`](https://github.com/ggreer/the_silver_searcher).

- Pentru a converti HTML la text: `lynx -dump -stdin`

- Pentru Markdown, HTML, și alte conversii de documente, folosiți [`pandoc`](http://pandoc.org/).

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

- Pentru procesare de bază a textelor, folosiți `awk` și `sed`. De exemplu, pentru a aduna suma numerelor din coloana a treia a unui fișier `awk '{ x += $3 } END { print x }'` este de 3 ori mai rapid și mai scurt decât codul echivalent în Python.

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

- După cum zice și pagina de manual, `rsync` este un utilitar foarte rapid, eficient și versatil de a copia fișiere. Este cunoscut pentru sincronizarea între calculatoare dar poate fi folosit și local. Dacă setările de securitate permit, folosirea `rsync` în loc de `scp` permite continuarea unui transfer eșuat fără a-l reporni. Este și una dintre cele [mai rapide metode](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) de a șterge un număr masiv de fișiere:
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Folosiți `shuf` pentru a permuta sau selecta linii aleatoare dintr-un fișier.

- Învățați opțiunile lui `sort`. Pentru numere folosiți `-n`, sau `-h` pentru numere în format human-readable (de exemplu numere produse de `du -h`). Învățați cum funcționează cheile de sortare (`-t` și `-k`). În special, țineți cont că trebuie să scrieți `-k1,1` pentru a sorta doar prima coloană, `-k1` înseamnă sortare după toată linia. Sortarea stabilă (`sort -s`) poate fi utilă. De exemplu, pentru a sorta după câmpul 2 și apoi după 1: `sort -k1,1 | sort -s -k2,2`.

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


## Comenzi de o linie

Câteva exemple de a construi comenzi complicate din comenzi simple:

- Este foarte util uneori că puteți trata fișierele ca mulțimi de rânduri și puteți implementa operațiile pe mulțimi -- intersecție, reuniune și diferență -- folosind `sort`/`uniq`. Presupunând că `a` și `b` sunt fișiere text fără linii duplicate, următoarele comenzi sunt foarte rapide și procesează fișiere de dimensiuni gigantice (`sort` nu este limitat de memorie dar este preferabil să folosiți `-T` dacă `/tmp` este pe o partiție mică). De asemenea, nu uitați de nota despre `LC_ALL` (localizare) de mai sus și de opțiunea `-u` (eliminată mai jos pentru claritate):
```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- Folosiți `grep . *` pentru a examina rapid conținutul fișierelor din director (fiecare linie este împerecheată cu fișierul din care provine) sau `head -100 *` (fiecare fișier are un header). Este un sfat util pentru directoare conținând setări precum `/sys`, `/proc`, `/etc`.


- Suma tuturor numerelor din a 3-a coloană a unui fișier (probabil de 3 ori mai rapid și de 3 ori mai puțin cod decât codul Python echivalent):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- Pentru a vedea dimensiunile și data fiecărui fișier dintr-un arbore, metoda următoare este ca un `ls -l` recursiv dar cu un output mai clar decât `ls -lR`:
```sh
      find . -type f -ls
```

- Presupunând că aveți un fișier text, de exemplu un jurnal al unui server web, și o anumită valoare apare pe câteva linii, precum o valoare pentru parametrul `acct_id` prezent în URL, dacă doriți un sumar pentru fiecare valoare a lui `acct_id`:
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- Pentru a monitoriza schimbările folosiți `watch`. De exemplu, verificați schimbările dintr-un director cu `watch -d -n 2 'ls -rtlh | tail'` sau setările de rețea în timp ce depanați probleme cu conexiunea wireless: `watch -d -n 2 ifconfig`.

- Folosiți această funcție pentru a obține un sfat aleator din acest document (parsează formatul Markdown și extrage un item):
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

- `expr`: execută operații aritmetice sau logice și expandează expresii regulate

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

- `timeout`: execută o comandă până la expirarea unui timp definit, omorând procesul la finalul timpului alocat

- `lockfile`: creează un fișier semafor care nu poate fi șters decât cu `rm -f`

- `logrotate`: rotește, comprimă și trimite jurnalele pe mail

- `watch`: execută o comandă în mod repetat, arătând rezultatele și/sau evidențiind diferențele

- `tac`: afișează conținutul fișierelor în ordine inversă

- `shuf`: selectează linii in mod aleator din fișier

- `comm`: compară fișiere sortate, linie cu linie

- `pv`: monitorizează progresul datelor într-un pipe

- `hd`, `hexdump`, `xxd`, `biew` și `bvi`: afișează sau editează fișiere binare

- `strings`: extrage șiruri din fișiere

- `tr`: translatează și manipulează caractere

- `iconv` sau `uconv`: conversie între codificările posibile ale unui text

- `split` și `csplit`: sparge fișiere în componente

- `sponge`: citește tot inputul înainte de a-l afișa, util pentru a citi și apoi a scrie în același fișier: `grep -v something some-file | sponge some-file`

- `units`: conversii între unități de măsură (vedeți și `/usr/share/units/definitions.units`)

- `apg`: generateză parole aleatoare

- `xz`: compresor de fișiere foarte eficient

- `ldd`: informații despre bibliotecile dinamice

- `nm`: simboluri din fișierele obiect

- `ab`: benchmarking pentru servere web

- `strace`: depanare apeluri de sistem

- [`mtr`](http://www.bitwizard.nl/mtr/): alternativă mai bună pentru `traceroute` pentru depanarea rețelei

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

- `id`: informații despre utilizatori/grupuri

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


## Doar pentru OS X

Aceste sfaturi sunt relevante *doar* pentru OS X.

- Managementul pachetelor cu `brew` (Homebrew) și/sau `port` (MacPorts). Aceste comenzi pot fi folosite pentru a instala multe din comenzile de mai sus pe un Mac.

- Copiați outputul unei comenzi către aplicații desktop cu `pbcopy` și lipiți conținutul de la una cu `pbpaste`.

- Pentru a mapa tasta Option în OS X Terminal ca o tastă Alt (pentru comenzile de mai sus precum **alt-b**, **alt-f**, etc.), deschideți Preferences -> Profiles -> Keyboard și selectați "Use Option as Meta key" ("Folosește Option ca tastă Meta").

- Pentru a deschide un fișier cu o aplicație desktop folosiți`open` sau `open -a /Applications/Whatever.app`.

- Spotlight: Găsiți fișiere cu `mdfind` și listați meta-date (de exemplu informații EXIF din fotografii) cu `mdls`.

- Țineți minte că OS X este la bază un BSD Unix, și multe comenzi (de exemplu `ps`, `ls`, `tail`, `awk`, `sed`) au un număr de variațiuni subtile comparativ cu Linux, un fapt influențat de diferențele între System V-style Unix și utilitarele GNU. Puteți vedea diferențele observând dacă pagina de manual are antetul "BSD General Commands Manual" ("Manual de comenzi generale BSD").  În unele cazuri, versiunile GNU pot fi instalate în paralel (precum `gawk` și `gsed` pentru GNU awk și sed). În scrierea de aplicații independente de platformă, evitați aceste comenzi (de exemplu folosiți Python sau `perl`) sau testați cu atenție.

- Informații despre versiunea OS X se pot obține cu `sw_vers`.

## Doar pentru Windows

Aceste sfaturi sunt relevante *doar* pentru Windows.

- În Windows 10, puteți folosi [Bash în Ubuntu în Windows](https://msdn.microsoft.com/commandline/wsl/about), pentru a obține mediul Bash familiar cu comenzile și utilitățile Unix descrise anterior. Ca bonus, acest lucru permite ca programele Linux să ruleze pe Windows. Pe de altă parte, nu puteți rula programe Windows din prompt-ul Bash.

- Puteți accesa shell-ul Unix sub Windows prin instalarea [Cygwin](https://cygwin.com/). Multe din lucrurile descrise aici vor funcționa implicit.

- Programele Unix adiționale se vor instala cu managerul de pachete al lui Cygwin.

- Folosiți `mintty` ca fereastra de comenzi.

- Accesați clipboard-ul Windows prin intermediul `dev/clipboard`.

- Folosiți `cygstart` pentru a deschide un fișier arbitrar cu aplicația corespunzătoare

- Accesați registrele Windows cu `regtool`.

- Observați că o cale de tip `C:\` în Windows devine `/cygdrive/c` sub Cygwin, și că root-ul Cygwin, `/`, apare ca `C:\cygwin` pe Windows. Convertiți între căile Cygwin și Windows cu `cygpath`. Acest lucru este util în scripturile care apelează programe Windows.

- Puteți executa majoritatea task-urilor de administrare a sistemului Windows din linia de comandă prin învățarea și folosirea `wmic`.

- O altă opțiune de a obține un sistem similar Unix sub Windows este [Cash](https://github.com/dthree/cash). Țineți cont că doar câte utilitare Unix sunt în prezent disponibile în acest mediu.

- O altă opțiune alternativă este să obțineți instrumentele de dezvoltare GNU (precum GCC) cu [MinGW](http://www.mingw.org/) și pachetul [MSYS](http://www.mingw.org/wiki/msys). Astfel veți obtine utilitare precum `bash`, `gawk`, `make` și `grep`. MSYS nu are toate beneficiile Cygwin dar este util în particular pentru a crea versiuni de Windows pentru instrumentele Unix.

## Mai multe resurse

- [awesome-shell](https://github.com/alebcay/awesome-shell): O listă detaliată a instrumentelor și resurselor pentru shell.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): Un ghid mai detaliat pentru folosirea liniei de comandă sub OS X
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) pentru a scrie scripturi mai bune..
- [shellcheck](https://github.com/koalaman/shellcheck): Un utilitar pentru analiza statică a scripturilor. În esență, `lint` pentru bash/sh/zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): Detalii complete despre situația tristă în folosirea căilor către fișiere corect în scripturi independente de platformă
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools): Mai multe comenzi și utilitare disponibile pentru analiza datelor, după cartea cu același nume.

## Anunț legal

Cu excepția unor task-uri foarte mici, codul scris aici este pentru ca alții să-l poate citi. Cu putere vine și responsabilitate. Faptul că *puteți* face ceva în Bash nu înseamnă neapărat că și trebuie să-l faceți ;)


## Licență

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

Această muncă este licențiată sub [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
