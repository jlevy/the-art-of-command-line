🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*

# The Art of Command Line (Traduzione Italiana)

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Meta](#meta)
- [Le Basi](#le-basi)
- [Uso quotidiano](#uso-quotidiano)
- [Processare file e dati](#processare-file-e-dati)
- [Debug sistema](#debug-sistema)
- [One-liner](#one-liner)
- [Oscuri ma utili](#oscuri-ma-utili)
- [OS X](#os-x)
- [Ulteriori risorse](#ulteriori-risorse)
- [Disclaimer](#disclaimer)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

Saper usare con una certa facilità la linea di comando è spesso visto come una sorta di "sapere arcano". Anche se può sembrare, in realtà non è decisamente così: può migliorare la tua produttività e la tua flessibilità in modi che neanche immagini. Questa che stai per leggere è una selezione di trucchi e di consigli che riguardano la linea di comando, che abbiamo trovato utili lavorando con Linux. Alcune di queste nozioni sono elementari, altre molto specifiche, se non sofisticate e, a volte, oscure.

Non c'è da preoccuparsi, comunque: la pagina che stai scorrendo non è molto lunga e non ti ruberà molto tempo. Prenderci dimestichezza, saperla usare quando necessario, te ne renderà ancora di più.

Questo lavoro è il risultato degli sforzi di [svariati autori e traduttori](AUTHORS.md).

Una buona parte di ciò che leggi è [apparsa](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands), [originariamente](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix), su [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know). Tuttavia, visto l'interesse, mi è sembrato logico usare Github per raccogliere il tutto e creare un qualcosa a cui chiunque avrebbe potuto contribuire, anche con un piccolo suggerimento. Non abbiamo la pretesa di aver creato qualcosa di perfetto: se trovi qualche errore faccelo sapere, magari aprendo una Pull Request!


## Meta

Obiettivi:

- Questa guida è adatta sia a principianti che ad utenti con più conoscenze. Ci proponiamo di seguire tre principi fondamentali: *ampiezza* (cerchiamo di includere tutto quello che serve), *specificità* (dando degli esempi concreti) e *brevità* (evitando tutto il futile e il superfluo). Ogni consiglio viene dato con l'obiettivo di salvare del tempo prezioso.
- Questa guida è stata scritta per Linux, con alcune eccezioni per che abbiamo riportato nella sezione "[OS X](#os-x-only)". In ogni caso, molti dei consigli che vedrai si applicano tranquillamente ad altri sistemi operativi Unix e a MacOS.
- Il focus principale sarà su interactive Bash, nonostante non sia esclusivamente così.
- Verranno inclusi comandi "base" Unix, ma anche altri che necessiteranno di installazioni separate.

Note:

- Per tenere tutto su una sola pagina, il contenuto è stato incluso tramite reference. Crediamo che tu sia abbastanza intelligente da cercare i dettagli su qualcosa di specifico, o su un comando, usando Google. Usa `apt-get`, `yum`, `dnf`, `pacman`, `pip` o `brew` (in base alla situazione) per installare i nuovi programmi.
- Se vuoi, usa [Explainshell](http://explainshell.com/) per avere uno spaccato più completo su cosa fanno comandi, pipe, opzioni e così via.


## Le Basi

- Impara le basi di Bash. Usa `man bash` e cerca almeno di scorrere velocemente l'intero scritto. Non è troppo lungo e neanche difficile da seguire. Altre shell possono andare bene, ma Bash è molto potente e sempre disponibile (impararne una sola tra zsh, fish e così via, per quanto ti possa tentare, ti darà problemi a lungo termine, lavorando su altre piattaforme).

- Impara ad usare bene almeno un editor di testo. Idealmente, potresti usare Vim (`vi`), con il quale non c'è praticamente competizione per questo genere di cose (sì, anche se volessi usare Emacs, oppure un altro di quei grossi IDE, o magari l'ennesimo ultimo editor ultramoderno ed hipster).

- Impara a leggere la documentazione usando `man` (per i più curiosi, `man man` elenca le varie sezioni. Ad esempio, 1 indica i comandi "regolari", 5 per file/convenzioni, 8 per l'amministrazione). Trova le pagine tramite `apropos`. Ricorda inoltre che alcuni comandi non sono degli eseguibili, ma dei "builtin" di Bash. Usa `help -d` in caso di necessità.

- Impara tutto sul reindirizzamento dell'output e dell'input, usando `>`, `<` ed il pipe `|`. Impara anche che `>` sovrascrive il file output, mentre `>>` aggiunge del contenuto alla fine. Impara tutto riguardo stdout e stderr.

- Impara anche qualcosa sul file glob, l'uso di `*` (e magari anche di `?` e `[`...`]`), oltre alla differenza tra i doppi `"` e singoli `'` apici. Guarda più in giù per quanto riguarda l'espansione delle variabili.

- Acquisisci familiarità con la gestione dei job con Bash: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, e così via.

- Impara ad usare `ssh` e le basi della passwordless authentication, tramite `ssh-agent`, `ssh-add`, e così via.

- Gestione base dei file: `ls` e `ls -l` (nello specifico, impara cosa indica ognuna delle colonne che escono fuori da `ls -l`), `less`, `head`, `tail` e `tail -f` (o, anche meglio, `less +F`), `ln` e `ln -s` (impara le differenze ed i vantaggi nell'uso di hard link o soft link), `chown`, `chmod`, `du` (per una panoramica veloce, usa: `du -hs *`). Per la gestione del filesystem, guardati `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. Impara anche cos'è un inode (`ls -i` or `df -i`).

- Gestione base delle reti: `ip` or `ifconfig`, `dig`.

- Impara ad usare per bene le espressioni regolari, e le varie flag per `grep`/`egrep`. Nello specifico, varrebbe la pena anche vedersi le opzioni `-i`, `-o`, `-v`, `-A`, `-B`, e `-C`.

- Impara ad usare `apt-get`, `yum`, `dnf` o `pacman` (in base alla distro che usi) per trovare ed installare nuovi package. E assicurati anche di aver installato `pip`, in modo tale da installare agevolmente i vari tool da linea di comando basati sul linguaggio Python. Alcuni di quelli che vedrai in seguito sono più semplici da installare se usi `pip`.


## Uso quotidiano

- In Bash, usa **Tab** per completare i vari parametri dei comandi, oppure elencarli. Usa **ctrl-r** per effettuare una ricerca nella cronologia dei comandi inseriti (premi *ctrl-r*, quindi effettua la ricerca. Per vedere più risultati premi ripetutamente *ctrl-r*). Premi quindi **Invio** per eseguire il comando trovato, oppure premi su **freccia destra** per mettere il comando sulla linea attuale, in modo tale da poterlo modificare.

- In Bash, usa **ctrl-w** per cancellare l'ultima parola, **ctrl-u** per cancellare tutto fino all'inizio della riga. Usa **alt-b** ed **alt-f** per muoverti di parola in parola. **ctrl-a** ti permette di tornare all'inizio della riga attuale senza cancellare nulla, mentre con **ctrl-e** puoi spostarti direttamente alla fine. **ctrl-k** cancella tutto quello che c'è dal punto attualmente scelto fino alla fine della riga. Inoltre, **ctrl-l** pulisce lo schermo. Per vedere una lista completa di tutte le varie scorciatoie presenti (ce ne sono molte) in bash, usa `man readline`. Ad esempio, **alt-.** serve a ciclare attraverso gli argomenti precedenti.

- In alternativa se ti piacciono le scorciatoie in stile vi, usa `set -o vi` (e `set -o emacs` per tornare indietro se dovessi cambiare idea).

- Per modificare dei comandi lunghi può essere utile impostare un editor di tua scelta (esempio: `export EDITOR=vim`). Premendo **ctrl-x** **ctrl-e** aprirai l'attuale comando in un editor multi-line per una modifica più agevole. Oppure, se stai lavorando con uno stile vi, **escape-v**.

- Per vedere i comandi più recenti, usa `history`. Ci sono anche altre abbreviazioni da usare per lo stesso scopo, come `!$` (per l'ultimo) e `!!`, nonostante questi vengano spesso rimpiazzati da **ctrl-r** e **alt-.**.

- Per tornare alla directory precedente: `cd -`

- Se stai digitando un comando, sei a metà e cambi idea, usa **alt-#** per aggiungere un `#` all'inizio della linea, rendendola di fatto un commento (oppure usa la sequenza **ctrl-a**, **#**, **invio**). Puoi quindi ritornarci dopo, tramite la cronologia.

- Usa `xargs` (o `parallel`). Si tratta di un tool molto potente, che ti permette di eseguire un certo comando tante volte quanti sono gli elementi restituiti da un altro comando. Quando non sei sicuro di quello che stai facendo, usa `xargs echo` per schiarirti le idee. Inoltre, `-I{}` è abbastanza utile. Ecco un esempio:

```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` è un ottimo tool che ti mostra l'albero dei processi.

- Usa `pgrep` e `pkill` per trovare dei processi ed inviare loro un segnale specifico (`-f` è utile a riguardo).

- Impara a conoscere i vari segnali che puoi inviare ai processi. Ad esempio, per sospendere un processo puoi usare `kill -STOP [pid]`. Per una lista completa, esegui `man 7 signal`.

- Usa `nohup` o `disown` se vuoi fare in modo che un certo processo vada avanti indefinitamente.

- Controlla quali processi sono in ascolto tramite `netstat -lntp` oppure `ss -plat` (per TCP; aggiungere invece `-u` per UDP).

- Dai uno sguardo a `lsof` per un elenco di socket e file aperti.

- Usa `uptime` o `w` per sapere da quanto tempo il sistema è stato avviato.

- Usa `alias` per creare delle scorciatoie personalizzate. Ad esempio, puoi usare `alias ll='ls -latr'`, che creerà un nuovo alias `ll` per il comando `ls -latr`.

- Negli script Bash, usa `set -x` (o la variante `set -v`, che effettua un log dell'input, includendo variabili e commenti) per un migliore debug dell'output. Comunque, cerca di usare la modalità strict a meno che tu non abbia bisogno del contrario. Una buona norma suggerisce di usare lo strict mode tranne nel caso in cui tu non possa usare `set -e` per annullare un comando in caso di errore (nonzero exit code). Considera anche l'uso di `set -o pipefail`, Puoi inoltre usare `trap` su EXIT o ERR. Un'abitudine piuttosto utile è quella di iniziare uno script così, facendo in modo che annulli la propria esecuzione in caso vengano rilevati degli errori.

```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- Negli script Bash, le subshell (scritte tra parentesi) sono un ottimo modo di raggruppare dei comandi. Un esempio piuttosto comune è il muoversi temporaneamente verso una directory differente, per poi tornare a lavorare in quella attuale.

```bash
      # faccio qualcosa nella directory attuale
      (cd /some/other/dir && other-command)
      # continuo nella directory attuale
```

- In Bash esistono svariati tipi di espansione di variabile. Come controllare se una variabile esiste: `${name:?error message}`. Ad esempio, se uno script richiede un singolo parametro, scrivi `input_file=${1:?usage: $0 input_file}`. Espansione aritmetica: `i=$(( (i + 1) % 5 ))`. Sequenze: `{1..10}`. Trim di stringhe: `${var%suffix}` and `${var#prefix}`. Ad esempio, se `var=foo.pdf`, allora `echo ${var%.pdf}.txt` restituisce `foo.txt`.

- Usare la brace expansion tramite `{`...`}` può essere molto comodo in caso di necessità di automazione di alcuni task simili. Un esempio è `mv foo.{txt,pdf} some-dir` (che con un solo comando muoverà due file, il pdf ed il txt), `cp somefile{,.bak}` (che si espande a `cp somefile somefile.bak`) o `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (che espande tutte le possibili combinazioni, creando un albero di directory).

- L'output di un comando può essere trattato come un file tramite `<(some command)`. Ad esempio, per comparare il file `/etc/hosts` locale con uno in remoto:

```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Impara qualcosa sugli "here documents" in Bash, come `cat <<EOF ...`.

- In bash, redireziona gli errori standard (input ed output) usando: `some-command >logfile 2>&1` oppure `some-command &>logfile`. Spesso, per assicurarti che un certo comando non lasci un handle aperto "legandoti al terminale attuale" potrebbe essere una buona idea aggiungere `</dev/null`.

- Usa `man ascii` per ottenere una buona tabella ASCII, con valori decimali ed esadecimali. Per altre informazioni generali sulle codifiche, usa `man unicode`, `man utf-8`, e `man latin1`.

- Usa `screen` o [`tmux`](https://tmux.github.io/) per effettuare il multiplex della schermata, cosa particolarmente utile in caso di sessioni ssh in remoto, ad esempio. `byobu` può inoltre migliorare screen e tmux, fornendo più informazioni e una gestione semplificata. Un'altra alternativa, minimalista, per la persistenza di sessione è `dtach`.

- In ssh, sapere come effettuare il port tunneling con `-L` o `-D` (ed occasionalmente `-R`) è molto utile, ad esempio per accedere a siti web da un server remoto.

- Può essere utile effettuare alcune ottimizzazioni alla configurazione ssh; ad esempio, questo file `~/.ssh/config` contiene delle impostazioni utili ad evitare connessioni interrotte in specifiche reti ed ambienti, fa uso di compressione (utile in caso di connessioni lente), e multiplexing dei canali verso lo stesso server con un control file locale:

```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Altre opzioni sempre interessanti riguardo ssh sono sensibili in termini di sicurezza e dovrebbero essere gestite con cura: alcuni esempi sono `StrictHostKeyChecking=no` e `ForwardAgent=yes`;

- Considera l'uso di [`mosh`](https://mosh.mit.edu/), un'alternativa ad ssh che usa UDP, in modo tale da evitare connessioni interrotte.

- Per ottenere i permessi relativi ad un certo file in forma ottale, utile alla configurazione ma non disponibile in `ls` usa qualcosa come

```sh
      stat -c '%A %a %n' /etc/timezone
```

- Per una selezione interattiva di valori dall'output di un altro comando, valuta l'uso di [`percol`](https://github.com/mooz/percol) o [`fzf`](https://github.com/junegunn/fzf).

- Per interagire con dei file in base all'output di un certo comando (come `git`), usa `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- Se vuoi creare al volo un webserver semplice, per i file nella directory attuale (sottocartelle incluse), disponibile a tutti sulla tua rete, usa:
`python -m SimpleHTTPServer 7777` (per la porta 7777 e Python 2) e `python -m http.server 7777` (per la porta 7777 e Python 3).

- Per eseguire un comando con i privilegi di un altro utente, usa `sudo` (per l'utente root) o `sudo -u` (per un altro utente). Usa `su` o `sudo bash` per eseguire la shell come tale utente. Usa `su -` per simulare un nuovo login con un altro utente.


## Processare file e dati

- Per trovare un file partendo dal suo nome nella directory attuale, usa `find . -iname '*qualcosa*'`. Per trovare un file in generale nel sistema, usa `locate qualcosa` (ma tieni a mente che `updatedb` potrebbe non ancora aver messo nell'indice i file creati da poco).

- Per una ricerca più generale, all'interno di codice sorgente o file di dati (o comunque qualcosa di più avanzato di `grep -r`), usa [`ag`](https://github.com/ggreer/the_silver_searcher).

- Per converire del codice HTML in un testo: `lynx -dump -stdin`

- Per Markdown, HTML ed ogni tipo di conversione di documenti, prova [`pandoc`](http://pandoc.org/).

- Se devi lavorare con l'XML ricorda: `xmlstarlet` è old but gold.

- Per il JSON, usa [`jq`](http://stedolan.github.io/jq/).

- Per YAML, usa [`shyaml`](https://github.com/0k/shyaml).

- Per Excel o file CSV, [csvkit](https://github.com/onyxfish/csvkit) fornisce `in2csv`, `csvcut`, `csvjoin`, `csvgrep` e così via.

- Per Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) è un ottimo tool e [`s4cmd`](https://github.com/bloomreach/s4cmd) è invece molto più veloce. Amazon [`aws`](https://github.com/aws/aws-cli) e la sua versione migliorata, [`saws`](https://github.com/donnemartin/saws) sono qualcosa di fondamentale per ogni tipo di task legato ad AWS.

- Impara di più riguardo `sort` ed `uniq`, incluso `-u` e `-d` di `uniq`. Guardati anche `comm`.

- Impara a conoscere meglio anche `cut`, `paste` e `join` per manipolare file di testo. Molte persone spesso usano `cut` ma si scordano dell'esistenza di `join`.

- Impara ad usare `wc` per contare i ritorni a capo (`-l`), caratteri (`-m`), parole (`-w`) e byte (`-c`).

- Impara qualcosa di più riguardo `tee` per copiare da stdin ad un file ed anche verso stdout. Esempio: `ls -al | tee file.txt`.

- Ricorda che le impostazioni riguardo la localizzazione influiscono un sacco su alcuni tool da linea di comando, in molti modi. Ad esempio sugli ordinamenti (collation) e performance. Molte installazioni Linux impostano `LANG` ed altre variabili correlate automaticamente su US English (inglese americano). Se decidi di cambiare lingua, non è detto quindi che le cose rimangano così come sono. Alcuni comandi, addirittura, potrebbero diventare immediatamente molto più lenti.

- Impara le basi di `awk` e `sed` per manipolare dati. Ad esempio, per sommare tutti i numeri nella terza colonna di un file di testo, usa `awk '{ x += $3 } END { print x }'`. Probabilmente tre volte più veloce e tre volte più corto del suo equivalente in Python.

- Per rimpiazzare tutte le occorrenze di una stringa, in uno o più file:

```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- Per rinominare dei file in massa e per effettuare cerca/sostituisci al loro interno, prova anche [`repren`](https://github.com/jlevy/repren). (In alcuni casi il comando `rename` permette operazioni multiple, ma fai attenzione al risultato visto che la funzionalità non è sempre identica sulle varie distro;

```sh
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Recover backup files whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Same as above, using rename, if available:
      rename 's/\.bak$//' *.bak
```

- Come la pagina del manuale spiega, `rsync` è un ottimo tool per copiare file, versatile e velocissimo. Si, è conosciuto per sincronizzare file da una macchina all'altra, ma è ugualmente utile se viene usato localmente. Viene anche riconosciuto come [uno dei modi più veloci](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) di cancellare un grande numero di file tutti insieme:

```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Usa `shuf` per selezionare una serie di linee da un file, in ordine casuale.

- Impara a conoscere le opzioni di `sort`. Per i numeri, usa `-n`, oppure `-h` per gestire numeri leggibili dal'uomo (`du -h`). Impara a capire come funzionano le varie chiavi (`-t` e `-k`). In particolare, fai attenzione a quando scrivi `-k1,1` per ordinare solo per il valore del primo campo, visto che `-k1` significa ordinare secondo l'intera riga. Lo stable sort (`sort -s`) può esserti utile. Immagina ad esempio di voler ordinare secondo il valore del secondo campo, e secondariamente del primo. Userai `sort -k1,1 | sort -s -k2,2`.

- Se dovessi aver bisogno di scrivere, letteralmente, un tab in Bash, premi **ctrl-v** **[Tab]** o scrivi `$'\t'`.

- I tool standard per il patching del codice sono `diff` e `patch`. Guarda anche Guarda anche `diffstat` per saperne di più su una  diff e `sdiff` per una side-by-side diff. Nota bene che `diff -r` lavora con intere directory. Usa `diff -r tree1 tree2 | diffstat` per una panoramica dei cambiamenti. Usa `vimdiff` per comparare e modificare file.

- Per file binari, usa `hd`, `hexdump` o `xxd` per semplici hex dump, e `bvi` o `biew` per editing binario.

- Inoltre, sempre per file binari, usa `strings` (insieme `grep`, e così via) per trovare sezioni di testo al loro interno;

- Per diff binarie (delta compression), usa `xdelta3`.

- Per convertire un testo da una codifica ad un'altra, prova `iconv`. Oppure `uconv` in caso di necessità più avanzate; supporta svariate opzioni avanzate inerenti Unicode. Ad esempio, questo comando rimuove tutti gli accenti e trasforma le stringhe in lettere tutte minuscole:

```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- Per dividere un file in altri file più piccoli, guarda `split` (per dividere in base alla dimensione) e `csplit` (per dividere in base ad un pattern).

- Se devi manipolare date ed orari, usa `dateadd`, `datediff`, `strptime` e così via, di [`dateutils`](http://www.fresse.org/dateutils/).

- Usa `zless`, `zmore`, `zcat` e `zgrep` per lavorare su file compressi.


## Debug sistema

- Per il web debugging, `curl` e `curl -I` sono decisamente utili. La stessa cosa vale anche per l'equivalente `wget`, o ancora per il più recente [`httpie`](https://github.com/jkbrzt/httpie).

- Per avere più informazioni sullo stato attuale del sistema, dalla cpu ai dischi, il tool classico più usato è `top` (o la sua versione migliorata `htop`), `iostat` e `iotop`. Usa `iostat -mxz 15` per avere informazioni base sulla CPU ed informazioni dettagliate, per partizione, sui dischi e sulle loro performance.

- Per avere più dettagli sulle connessioni di rete, usa `netstat` e `ss`.

- Per una panoramica veloce di cosa sta succedendo nel sistema, `dstat` è ottimo. Per avere invece molte più informazioni e scendere nel dettaglio, usa [`glances`](https://github.com/nicolargo/glances).

- Per saperne di più sullo stato della memoria, esegui ed impara a capire il significato dei comandi `free` e `vmstat`. In particolare, sii consapevole del fatto che la memoria "cached" è quella mantenuta dal kernel Linux come file cache, che a tutti gli effetti poi conta come memoria libera.

- Il system debugging con Java è tutta un'altra cosa. Uno dei trucchi più semplici sulla JVM Oracle (ed anche altre) è che all'esecuzione di `kill -3 <pid>` verrà messo in log un trace full stack (inclusi molti dettagli sulla garbage collection). Anche `jps`, `jstat`, `jstack` e `jmap` del JDK sono molto utili. Ci sono poi i vari [SJK tools](https://github.com/aragozin/jvm-tools), più avanzati.

- Usa [`mtr`](http://www.bitwizard.nl/mtr/) per rilevare problemi di rete. Molto meglio di traceroute.

- Per capire perché un disco viene visto pieno, [`ncdu`](https://dev.yorhel.nl/ncdu) ti evita perdite di tempo rispetto al più comune `du -sh *`.

- Per capire quale socket o processo sta usando troppa banda prova [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) o [`nethogs`](https://github.com/raboof/nethogs).

- `ab` (incluso in Apache) è ottimo per un test di carico veloce di un webserver. Per test di carico più avanzati, prova anche `siege`.

- Per un debug di rete più avanzato, dai uno sguardo a [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) o [`ngrep`](http://ngrep.sourceforge.net/).

- Impara qualcosa di più su `strace` e `ltrace`. Possono essere molto utili quando un programma crasha, o magari rimane in blocco e tu non capisci perché. Degne di nota le opzioni di profiling (`-c`), e la possibilità di agganciare un processo in esecuzione (`-p`).

- Impara qualcosa di più riguardo `ldd` per controllare le librerie condivise.

- Impara a connetterti ad un processo in esecuzione con `gdb` e recuperare il suo stack trace.

- Usa `/proc`. Fantastico quando devi fare un live debug in caso di problemi. Esempi: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (dove `xxx` è il nome del processo o il suo pid).

- Quando vuoi debuggare qualcosa che è andato storto in passato, [`sar`](http://sebastien.godard.pagesperso-orange.fr/) può essere molto utile. Permette di controllare uno storico delle statistiche di CPU, memoria, rete e così via.

- Usa `stap` per un'analisi più approfondita del sistema in termini di performance ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_(Linux)), e [`sysdig`](https://github.com/draios/sysdig).

- Controlla quale OS stai usando con `uname` oppure `uname -a` (informazioni generali sul kernel) o `lsb_release -a` (informazioni sulla distro Linux).

- Usa `dmesg` quando il sistema si comporta in modo davvero strano (problemi hardware o legati ai driver, insomma).


## One-liner

Qualche esempio di combinazione di più comandi comandi:

- Decisamente è utile è sapere che puoi effettuare intersesione, unione e differenza di file di testo tramite `sort`/`uniq`. Immagina di avere `a` e `b`, due file di testo. Il metodo in questione è veloce e tra l'altro supporta anche file di svariati gigabyte. Guarda anche la nota riguardo `LC_ALL` e l'opzione `-u` di `sort`.

```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- Usa `grep . *` per esaminare velocemente i contenuti di tutti i file in una certa directory (in modo che ogni linea venga abbinata al nome del file), oppure `head -100 *`. Può essere molto utile per quelle directory piene file di configurazione, come `/sys`, `/proc`, `/etc`.


- Sommare tutti i numeri sulla terza colonna di un file di testo (probabilmente 3 volte più veloce e corto della controparte in Python):

```sh
      awk '{ x += $3 } END { print x }' myfile
```

- Nel caso in cui tu voglia vedere dimensioni e date per un certo "albero" di file (un po' come `ls -l`, ma ricorsivo):

```sh
      find . -type f -ls
```

- Immagina di avere un file di testo, come un log di un server, like a web server log, ed un certo valore appare di tanto in tanto tra le righe, come ad esempio un parametro `acct_id` in un URL.. Ecco come contare le richieste effettuate che contengono tale parametro `acct_id`:

```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- Per monitorare costantemente i cambiamenti ai file, usa `watch`. Ad esempio, per controllare i cambiamneti in una certa directory usa `watch -d -n 2 'ls -rtlh | tail'` oppure, se stai monitorando un file di configurazione inerente il WiFi, `watch -d -n 2 ifconfig`.

- Esegui questa funzione per ottenere un consiglio a caso da questo documento:

```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```


## Oscuri ma utili

- `expr`: esegue operazioni aritmetiche o booleane, oltre a valutare espressioni regolari.

- `m4`: un semplice macro processor.

- `yes`: stampa una stringa per un numero indefinito di volte.

- `cal`: un calendario.

- `env`: esegue un comando (utile negli script).

- `printenv`: stampa le variabili di ambiente (utile per il debug e negli script).

- `look`: trova parole inglesi (o linee in un file) partendo da una stringa.

- `cut`, `paste` e `join`: manipolazione di dati.

- `fmt`: formatta paragrafi di testo.

- `pr`: formatta del testo in pagine/colonne.

- `fold`: sistema delle linee di testo.

- `column`: formatta del testo in colonne o tabelle dalla larghezza fissa.

- `expand` ed `unexpand`: converte spazi in tab, e viceversa.

- `nl`: aggiunge il conteggio delle righe.

- `seq`: stampa dei numeri.

- `bc`: calcolatrice.

- `factor`: scompone un numero in fattori.

- [`gpg`](https://gnupg.org/): cripta e firma i file.

- `toe`: tabella di tutti i terminali disponbili.

- `nc`: per il network debugging e trasferimento dati.

- `socat`: socket relay e tcp port forwarder (simile a `netcat`).

- [`slurm`](https://github.com/mattthias/slurm): visualizzazione del traffico di rete.

- `dd`: spostamento dati tra file e dispositivi.

- `file`: identifica il tipo di un certo file.

- `tree`: mostra le sottodirectory con una struttura ad albero. A differenza di `ls`, è ricorsivo.

- `stat`: informazioni su un file.

- `time`: esegue un comando e tiene traccia del tempo di esecuzione.

- `timeout`: avvia un comando definendo anche un certo ammontare di tempo oltre il quale non si può andare. Se tale ammontare di tempo viene raggiunto, il comando viene annullato.

- `lockfile`: crea un file che può essere rimosso solo tramite `rm -f`.

- `logrotate`: gestie i log, la loro rotazione, compressione ed invio via mail.

- `watch`: esegue un comando più volte, mostrando i risultati ed evidenziando le differenze tra tali risultati.

- `tac`: stampa un file al contrario.

- `shuf`: sceglie casualmente delle righe da un file.

- `comm`: compara dei file ordinati riga per riga.

- `pv`: monitora i progressi dei dati attraverso un pipe.

- `hd`, `hexdump`, `xxd`, `biew` e `bvi`: dump o modifica di file binari.

- `strings`: estrae del testo da file binari.

- `tr`: manipolazione e trasformazione dei caratteri.

- `iconv` o `uconv`: conversione di testi in altre codifiche.

- `split` e `csplit`: divisione di un file in altri file più piccoli.

- `sponge`: legge tutto l'input prima di riscriverlo, utile in caso di lettura e scrittura sullo stesso file. Ad esempio: `grep -v something some-file | sponge some-file`.

- `units`: conversione da e verso altre unità di misura (guarda anche `/usr/share/units/definitions.units`).

- `apg`: genera password casuali.

- `7z`: compressione di file ad alta ratio.

- `ldd`: informazioni su una libreria dinamica.

- `nm`: elenca i vari simboli presenti un object file.

- `ab`: benchmark di webserver.

- `strace`: debug delle chiamate di sistema.

- [`mtr`](http://www.bitwizard.nl/mtr/): un traceroute migliore per il debug di rete.

- `cssh`: shell visuale concorrente.

- `rsync`: sincronizza file e cartelle tramite SSH oppure in locale.

- [`wireshark`](https://wireshark.org/) e [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): packet capturing e debug di rete.

- [`ngrep`](http://ngrep.sourceforge.net/): come grep... ma per il traffico di rete.

- `host` e `dig`: DNS lookup.

- `lsof`: descrittore dei processi ed informazioni su socket.

- `dstat`: statistiche di sistema.

- [`glances`](https://github.com/nicolargo/glances): overview di sistemi multipli ad alto livello.

- `iostat`: statistiche sull'uso dei dischi.

- `mpstat`: statistiche sull'uso della CPU.

- `vmstat`: statistiche sull'uso della memoria.

- `htop`: versione migliorata di top.

- `last`: cronologia dei login.

- `w`: mostra chi è autenticato.

- `id`: user/group identity info.

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): cronologia di alcune statistiche del sistema.

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) o [`nethogs`](https://github.com/raboof/nethogs): uso della rete da parte di socket e processi.

- `ss`: statistiche sui socket.

- `dmesg`: messaggi di errore di avvio e di sistema in generale.

- `sysctl`: visualizza e configura i parametri del kernel a run time.

- `hdparm`: tool di gestione dischi SATA/ATA.

- `lsblk`: visualizzazione ad albero dei dischi e relative partizioni.

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: informazioni sull'hardware, tra cui CPU, BIOS, RAID, scheda grafica e dispositivi di ogni tipo.

- `lsmod` e `modinfo`: elenco e dettaglio dei vari moduli del kernel.

- `fortune`, `ddate`, e `sl`: mmmh, beh, dipende molto da quanto consideri le locomotive a vapore e le citazioni di Zippy "utili".


## OS X

Consiera questa sezione come un'esclusiva MacOS.

- I package vengono gestiti con `brew` (Homebrew) e/o `port` (MacPorts). Possono essere usati su MacOS per installare molti dei comandi visti in questo articolo.

- Copia l'output di un qualsiasi comando tramite `pbcopy` ed incollalo, invece, con `pbpaste`.

- Per abilitare l'Option key sul terminale Mac OS come un'alt key (per riprodurre comandi quali **alt-b**, **alt-f**, e così via), apri Preferenze -> Profili -> Tastiera e scegli "Usa Option come meta key".

- Per aprire un file con un'applicazione desktop, usa `open` oppure `open -a /Applications/LaTuaApplicazione.app`.

- Cerca i file con `mdfind` ed elenca i vari metadati (come gli EXIF per le foto) con `mdls`.

- Sii consapevole del fatto che MacOS è basato su BSD Unix, e molti dei suoi comandi (ad esempio `ps`, `ls`, `tail`, `awk`, `sed`) presentano alcune variazioni rispetto alla loro controparte Linux. Per controllare tali differenze devi vedere se la pagina del manuale ha come titolo "BSD General Commands Manual". Come logica conseguenza, quindi, ricorda di non usare tali comandi se hai intenzione di scrivere degli script cross-platform.

- Per avere più informazioni sulla tua release di MacOS, usa `sw_vers`.


## Ulteriori risorse

- [awesome-shell](https://github.com/alebcay/awesome-shell): Una curatissima lista di tool e risorse
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): Una guida approfondita sulla linea di comando in Mac OSX
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) per scrivere script migliori
- [shellcheck](https://github.com/koalaman/shellcheck): Un tool di analisi per script shell. Praticamente lint per bash/sh/zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): Un compendio sul come gestire nomi dei file e path nella shell


## Disclaimer

Con l'eccezione di pochi piccoli task, il codice è stato scritto per permettere agli altri di leggerlo agevolmente. Da grandi poteri derivano grandi responsabilità. Ricorda: il fatto che tu possa *fare* qualcosa in Bash non implica comunque che tu debba per forza! ;)


## License

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

A questo lavoro è attribuita la [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
