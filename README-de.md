🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*


# The Art of Command Line

[![Ask a Question](https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg)](https://airtable.com/shrzMhx00YiIVAWJg)

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


- [Kurzbeschreibung](#kurzbeschreibung)
- [Grundlagen](#grundlagen)
- [Täglicher Gebrauch](#täglicher-gebrauch)
- [Umgang mit Dateien und Daten](#umgang-mit-dateien-und-daten)
- [Fehlerbehebung auf Systemebene](#fehlerbehebung-auf-systemebene)
- [Einzeiler](#einzeiler)
- [Eigenartig aber hilfreich](#eigenartig-aber-hilfreich)
- [Nur MacOS X](#nur-macos-x)
- [Nur Windows](#nur-windows)
- [Weitere Quellen](#weitere-quellen)
- [Haftungsausschluss](#haftungsausschluss)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

Der flüssige Umgang mit der Befehlszeile (auch Kommandozeile, engl. "command line") ist eine oft vernachlässigte oder als undurchsichtig empfundene Fähigkeit, steigert jedoch Flexibilität und Produktivität eines Informatikers auf offensichtliche als auch subtile Weise. Was folgt, ist eine Auswahl an Notizen und Tipps im Umgang mit der Befehlszeile, welche ich beim Arbeiten mit Linux zu schätzen gelernt habe. Manche dieser Hinweise beinhalten Grundwissen, andere sind sehr spezifisch, fortgeschritten oder auch eigenartig. Die Seite ist nicht lang, aber wenn du alle Punkte verstanden hast und anwenden kannst, weißt du eine ganze Menge.

Vieles davon
[erschien](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
[ursprünglich](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
auf [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
aber angesichts des Interesses scheint es vielversprechend, Github zu nutzen, wo talentiertere Menschen als ich es bin kontinuierlich Verbesserungen vorschlagen können. Wenn du einen Fehler entdeckst oder etwas, das man besser machen könnte, erstelle ein Issue oder einen PR! (Lies aber bitte zuerst die Kurzbeschreibung und überprüfe bereits vorhandene Issues/PRs.)


## Kurzbeschreibung

Umfang:

- Diese Anleitung richtet sich an Anfänger und Fortgeschrittene. Die Ziele sind *Breite* (alles ist wichtig), *Genauigkeit* (konkrete Beispiele für die gebräuchlichsten Anwendungsfälle) und *Knappheit* (Dinge, die nicht wesentlich sind oder leicht anderswo nachgeschlagen werden können, sollen vermieden werden). Jeder Tipp ist in einer bestimmten Situation wesentlich oder deutlich zeitsparend gegenüber bestehenden Alternativen.
- Sie ist für Linux geschrieben, mit der Ausnahme der Abschnitte "[Nur MacOS X](#nur-macos-x)" und "[Nur Windows](#nur-windows)". Viele der anderen Punkte lassen sich nutzen oder sind installierbar auf anderen Unices oder MacOS (oder sogar Cygwin).
- Der Fokus liegt auf interaktiver Bash, allerdings gelten viele Tipps auch auf anderen Shells sowie für allgemeines Bash-Skripting.
- Sie beinhaltet sowohl "normale" Unix-Befehle als auch solche, die bestimmte installierte Pakete voaussetzen -- sofern sie wichtig genug sind, dass sie die Aufnahme in diese Anleitung verdienen.

Hinweise:

- Um eine Seite nicht zu sprengen, ist ihr Inhalt durchgängig anhand von Verweisen aufgelistet. du bist schlau genug, anderswo zusätzliche Informationen nachzuschlagen, sobald du die Idee bzw. den Befehl dahinter kennst. Verwende `apt-get`, `yum`, `dnf`, `pacman`, `pip` oder `brew`, um ggf. neue Programme zu installieren.
- Verwende [Explainshell](http://explainshell.com/), um einen hilfreichen Einblick zu erhalten, was es mit Befehlen, Optionen, Pipes etc. auf sich hat.


## Grundlagen

- Lerne Bash-Grundlagen. Tatsächlich, gib `man bash` ein und überfliege das Ganze zumindest; es ist leicht zu verstehen und nicht allzu lang. Alternative Shells sind nett, aber Bash ist mächtig und immer verfügbar (*nur* zsh, fish, etc. zu lernen ist auf dem eigenen Laptop vielleicht reizvoll, beschränkt jedoch deine Möglichkeiten in vielerlei Hinsicht, etwa beim Arbeiten mit bestehenden Servern).

- Lerne mindestens einen Text-basierten Editor zu benutzen. Idealerweise Vim (`vi`), da es letztlich keinen vergleichbaren Mitbewerber für gelegentliche Einsätze in einem Terminal gibt (selbst dann, wenn man eine große Entwicklungsumgebung wie Emacs oder die meiste Zeit einen modernen Hipster-Editor benutzt).

- Wisse, wie man Dokumentationen mit `man` liest (für Neugierige, `man man` listet Abschnittsnummern, bspw. stehen unter 1 "reguläre" Befehle, 5 beinhaltet Dateien/Konventionen und unter 8 solche zur Rechnerverwaltung). Finde `man`-Seiten ("man pages") mit `apropos`. Wisse, dass manche Befehle keine ausführbaren Dateien, sondern Bash-Builtins sind, und dass du Hilfe zu diesen mit `help` und `help -d` erhälst.

- Lerne etwas über die Umleitung von Ein- und Ausgaben per `>` und `<` sowie `|` für Pipes. Wisse, dass `>` die Ausgabedatei überschreibt und `>>` etwas anhängt. Lerne etwas über stdout und stderr.

- Lerne etwas über die Dateinamenerweiterung mittels `*` (und eventuell `?` und `[`...`]`) sowie Anführungszeichen, etwa den Unterschied zwischen doppelten `"` und einfachen `'`. (Mehr zur Variablenerweiterung findest du unten.)

- Mach dich vertraut mit Bash-Jobmanagement: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, etc.

- Kenne `ssh` und die Grundlagen passwortloser Authentifizierung mittels `ssh-agent`, `ssh-add`, etc.

- Grundlegende Dateiverwaltung: `ls` and `ls -l` (und spezieller, lerne die Funktion jeder einzelnen Spalte von `ls -l` kennen), `less`, `head`, `tail` und `tail -f` (oder noch besser, `less +F`), `ln` und `ln -s` (lerne die Unterschiede und Vorteile von Hard- und Softlinks), `chown`, `chmod`, `du` (für eine Kurzzusammenfassung der Festplattenbelegung: `du -hs *`). Für Dateisystemmanagement `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. Lerne, was ein Inode (engl. index node) ist (`ls -i` oder `df -i`).

- Grundlagen der Netzwerkverwaltung: `ip` oder `ifconfig`, `dig`.

- Lerne etwas über Versionskontrolle und benutze ein entsprechendes System, wie etwa `git`.

- Kenne reguläre Ausdrücke gut, und die verschiedenen Statusindikatoren zu `grep`/`egrep`. Die Optionen `-i`, `-o`, `-v`, `-A`, `-B`, und `-C` sind gut zu wissen.

- Lerne den Umgang mit `apt-get`, `yum`, `dnf` oder `pacman` (je nach Linux-Distribution), um Pakete zu finden bzw. zu installieren. Und stell sicher, dass du `pip` hast, um Python-basierte Befehlszeilen-Werkzeuge nutzen zu können (einige der untenstehenden werden am einfachsten über `pip` installiert).


## Täglicher Gebrauch

- In Bash kannst du mit **Tab** Parameter vervollständigen sowie alle verfügbaren Befehle anzeigen lassen und mit **ctrl-r** bereits benutzte Befehle durchsuchen (drück die Kombination, gib dann deinen Suchtext ein und springe anschließend durch wiederholtes Drücken von **ctrl-r** durch die Suchergebnisse, mit **Enter** kannst du den gefundenen Befehl ausführen sowie mit der rechten Pfeiltaste in die aktuelle Zeile einfügen, um ihn zu bearbeiten).

- In Bash kannst du mit **ctrl-w** das letzte Wort löschen und mit **ctrl-u** alles bis zum Anfang einer Zeile. Verwende **alt-b** und **alt-f**, um dich Wort für Wort fortzubewegen, springe mit **ctrl-a** zum Beginn einer Zeile,  mit **ctrl-e** zum Ende einer Zeile, lösche mit **ctrl-k** alles bis zum Ende einer Zeile und bereinige mit **ctrl-l** den Bildschirm. Siehe `man readline` für alle voreingestellten Tastenbelegungen in Bash. Davon gibt's viele. Zum Beispiel **alt-.** wechselt durch vorherige Parameter und **alt-*** erweitert ein Suchmuster.

- Alternativ, falls du vi-artige Tastenbelegungen magst, verwende `set -o vi` (und `set -o emacs`, um es wiederzuholen).

- Um kürzlich genutzte Befehle zu sehen, `history`. Es gibt außerdem viele Abkürzungen wie etwa `!$` (letzter Parameter) und `!!` (letzter Befehl), wenngleich diese oft einfach ersetzt werden durch **ctrl-r** und **alt-.**.

- Um lange Befehle zu bearbeiten, kannst du sie (nachdem du deinen Editor angegeben hast, etwa mit `export EDITOR=vim`) mit **ctrl-x** **ctrl-e** im Editor öffnen, um mehrere Zeilen bearbeiten zu können. Oder vi-Style, **escape-v**.

- Um kürzlich verwendete Befehle anzuzeigen, benutze `history`. Anschließend `!n` (wobei `n` die Nummer des Befehls ist), um es erneut auszuführen. Es gibt zudem zahlreiche Abkürzungen, die man verwenden kann, die nützlichste ist wahrscheinlich `!$` für den letzten Parameter und `!!` für den letzten Befehl (siehe "HISTORY EXPANSION" in der `man`-Seite). Diese werden allerdings oft einfach ersetzt durch **ctrl-r** und **alt-.**.

- In dein Benutzerverzeichnis gelangst du mit `cd`. Auf Dateien relativ zu diesem kannst du mit dem Präfix `~` zugreifen (etwa so `~/.bashrc`). In `sh`-Skripts heißt das Benutzerverzeichnis `$HOME`.

- Um ins vorangegangene Arbeitsverzeichnis zu gelangen: `cd -`

- Wenn du einen Befehl eingibst und es dir auf halbem Wege anders überlegst, drücke **alt-#**, um am Zeilenanfang ein `#` einzufügen und ihn damit als Kommentar auszuweisen (oder benutze **ctrl-a**, **#**, **enter**). du kannst später über die Befehlsgeschichte zurückgelangen.

- Verwende `xargs` (oder `parallel`). Es ist sehr mächtig. Beachte, wie du viele Dinge pro Zeile (`-L`) als auch parallel (`-P`) ausführen kannst. Wenn du dir nicht sicher bist, ob das Richtige dabei herauskommt, verwende zunächst `xargs echo`. Außerdem ist`-I{}` nützlich. Beispiele:
```bash
    find . -name '*.py' | xargs grep irgendeine_funktion
    cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` liefert eine hilfreiche Anzeige des Prozessbaums.

- Verwende `pgrep` und `pkill`, um Prozesse anhand eines Namens zu finden oder festzustellen (`-f` ist hilfreich).

- Kenne die verschiedenen Signale, welche du Prozessen senden kannst. Um einen Prozess etwa zu unterbrechen, verwende `kill -STOP [pid]`. Für die vollständige Liste, siehe `man 7 signal`

- Verwende `nohup` oder `disown`, wenn du einen Hintergrundprozess für immer laufen lassen willst.

- Überprüfe mithörende Prozesse mit `netstat -lntp` oder `ss -plat` (für TCP; füge `-u` für UDP hinzu).

- Siehe zudem `lsof` für offene Sockets und Dateien.

- Siehe `uptime` oder `w`, um die laufende Betriebszeit des Systems zu erfahren,

- Verwende `alias`, um Verknüpfungen für gebräuchliche Befehle zu erstellen. So erstellt etwa `alias ll='ls -latr'` den neuen Alias `ll`.

- Speichere diese Alternativnamen ("aliases"), Shell-Einstellungen und häufig benutzte Funktionen in `~/.bashrc` und [stelle sie anderen Login-Shells zur Verfügung](http://superuser.com/a/183980/7106). So hast du auf dein Setup auch in allen anderen Shell-Sessions Zugriff.

- Platziere Einstellungen von Umgebungsvariablen sowie Befehle, welche nach einer Anmeldung ausgeführt werden sollen, in `~/.bash_profile`. Eine separate Konfiguration ist notwendig für Shells, welche du von einer grafischen Benutzeroberfläche startest sowie für `cron`-Jobs.

- Synchronisiere deine Konfigurationsdateien (etwa `.bashrc` und `.bash_profile`) zwischen mehreren Computern mit Git.

- Verstehe, dass Vorsicht geboten ist, wenn Variablen und Dateinamen Leerzeichen enthalten. Setze deine Bashvariablen daher mit Anführungszeichen: `"$FOO"`. Bevorzuge die Optionen `-0` oder `-print0`, um ungültige Schriftzeichen zu aktivieren und so Dateinamen zu begrenzen, bspw. `locate -0 pattern | xargs -0 ls -al` oder `find / -print0 -type d | xargs -0 ls -al`. Um in einem "for loop" Dateinamen durchzugehen, die Leerzeichen enthalten, sorge mit `IFS=$'\n'` dafür, dass dein IFS immer auf einer neuen Zeile steht.

- Benutze in Bash-Skripts `set -x` (oder die Abwandlung `set -v`, welche unverarbeiteten Input akzeptiert, einschließlich Kommentare und unexpandierte Variablen) zum Output der Fehlerbehebung. Benutze "strict modes", es sei denn, gute Gründe sprechen dagegen: Benutze `set -e`, um bei Fehlern abzubrechen ("nonzero exit code"). Benutze `set -u`, um die Verwendung nicht gesetzer Variablen aufzuspüren. Erwäge auch `set -o pipefail` für Fehler in Pipes (lies jedoch mehr zu diesem Thema, wenn du es vorhast, denn es ist ein wenig heikel). Benutze bei komplizierteren Skripts auch `trap` bei EXIT oder ERR. Es ist eine nützliche Angewohnheit, ein Skript folgendermaßen zu beginnen, um Fehler zu erkennen und sie ggf. mit einer entsprechenden Fehlermeldung abzubrechen:
```bash
    set -euo pipefail
    trap "echo 'error: Script failed: see failed command above'" ERR
```

- In Bash-Skripts stellen Subshells (geschrieben in runden Klammern) einen praktischen Weg dar, Befehle zusammenzufassen. Ein gebräuchliches Beispiel ist die vorübergehende Arbeit in einem anderen Arbeitsverzeichnis:
```bash
    # erledige etwas im aktuellen Verzeichnis
    (cd /irgendein/anderes/verzeichnis && anderer-befehl)
    # fahre fort im aktuellen Verzeichnis
```

- Beachte, dass es in Bash viele Möglichkeiten gibt, Variablen zu erweitern. Überprüfen, ob eine Variable existiert: `${name:?error message}`.Wenn bspw. ein Bash-Skript nur einen einzelnen Parameter benötigt, schreibe einfach `input_file=${1:?usage: $0 input_file}`. Arithmetische Erweiterung: `i=$(( (i + 1) % 5 ))`. Sequenzen: `{1..10}`. Zeichenkette kürzen: `${var%suffix}` und `${var#prefix}`. Wenn bspw. `var=foo.pdf`, dann gibt `echo ${var%.pdf}.txt` die Ausgabe `foo.txt` aus.

- Klammererweiterung mittels `{`...`}` kann dafür sorgen, ähnlichen Text seltener wiederholen zu müssen und ermöglicht die Kombination von Objekten. Das ist etwa in Fällen nützlich wie `mv foo.{txt,pdf} zielverzeichnis` (verschiebt beide Dateien), `cp datei{,.bak}` (erweitert den Ausdruck um `cp datei datei.bak`) oder `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (erweitert alle denkbaren Kombinationen und erstellt einen Verzeichnisbaum).

- Die Ausgabe eines Befehls kann wie eine Datei behandelt werden mit `<(befehl)`. Das Vergleichen der lokalen `/etc/hosts` mit einer entfernten:
```sh
    diff /etc/hosts <(ssh andererhost cat /etc/hosts)
```

- Beim Schreiben von Skripts wirst du deinen Code womöglich in geschweifte Klammern setzen wollen. Falls die schließende Klammer fehlt, wird dein Skript aufgrund eines Syntaxfehlers nicht ausgeführt. Das ist etwa dann sinnvoll, wenn es im Internet verfügbar ist, da ein unvollständig heruntergeladenes Skript so an der Ausführung gehindert wird:
```bash
{
    # Hier koennte dein Code stehen!
}
```

- Kenne "here documents" in Bash, wie etwa in `cat <<EOF ...`.

- In Bash, leite sowohl den standard output als auch den standard error um mit: `irgendein-befehl >logfile 2>&1`. Oftmals ist es gute Praxis, einen Befehl an das verwendete Terminal zu binden, um keinen offenen Dateizugriff im standard input zu erzeugen, also `</dev/null` hinzuzufügen.

- Verwende `man ascii` für eine gute ASCII-Tabelle, Mit Dezimal- und Hexadezimalwerten. Für allgemeine Informationen zu Kodierung sind `man unicode`, `man utf-8` und `man latin1` hilfreich.

- Verwende `screen` oder [`tmux`](https://tmux.github.io/), um einen Bildschirm zu multiplexen, besonders hilfreich ist dies für Fernzugriffe per `ssh` und zur Trennung und Neuverbindung mit einer Session. Eine minimalistische Alternative allein zur Aufrechterhaltung einer Session ist `dtach`.

- Bei SSH ist es hilfreich zu wissen, wie man einen Porttunnel mit `-L` oder `-D` (gelegentlich auch `-R`) einrichtet, etwa beim Zugriff auf Webseiten von einem Remote-Server.

- Es kann nützlich sein, ein paar Verbesserungen an den SSH-Einstellungen vorzunehmen; so enthält bspw. diese `~/.ssh/config` Einstellungen, um das Abreißen der Verbindung in bestimmten Netzwerkumgebungen zu vermeiden, verwendet Kompression (was hilfreich ist bei SCP über Verbindungen mit niedriger Bandbreite) und Multiplex-Kanäle zu demselben Server mithilfe einer lokalen Kontrolldatei:
```
    TCPKeepAlive=yes
    ServerAliveInterval=15
    ServerAliveCountMax=6
    Compression=yes
    ControlMaster auto
    ControlPath /tmp/%r@%h:%p
    ControlPersist yes
```

- Einige andere Optionen im Zusammenhang mit SSH sind sicherheitsrelevant und sollten nur mit Bedacht aktiviert werden, etwa Zugriff per Subnet oder Host sowie in vertrauenswürdigen Netzwerken: `StrictHostKeyChecking=no`, `ForwardAgent=yes`.

- Erwäge [`mosh`](https://mosh.mit.edu/) als Alternative zu `ssh`, die UDP benutzt, um so abgebrochene Verbindungen zu vermeiden, was ja in gewisser Hinsicht auch komfortabel ist (benötigt Server-seitiges Setup).

- Um Zugriff auf eine Datei in Oktalform zu erhalten, was zur Systemkonfiguration zwar nützlich, jedoch über `ls` nicht verfügbar und leicht zu vermasseln ist, verwende etwas wie
```sh
    stat -c '%A %a %n' /etc/timezone
```

- Verwende zur interaktiven Auswahl von Werten aus dem Output eines anderen Befehls [`percol`](https://github.com/mooz/percol) oder [`fzf`](https://github.com/junegunn/fzf).

- Verwende `fpp` ([PathPicker](https://github.com/facebook/PathPicker)) zur Interaktion mit Dateien als Output eines anderen Befehls (wie etwa `git`).

- Verwende für einen einfachen Webserver für alle Dateien im aktuellen Verzeichnis (sowie Unterverzeichnisse), der für alle in deinem Netzwerk abrufbar ist: `python -m SimpleHTTPServer 7777` (für Port 7777 und Python 2) sowie `python -m http.server 7777` (für Port 7777 und Python 3).

- Benutze `sudo`, um einen Befehl als ein anderer Benutzer auszuführen. Standardmäßig ist dies die Ausführung als root; benutze `-u` zur Angabe eines anderen benutzers sowie `-i`, um dich als dieser anzumelden (du wirst nach _deinem_ Passwort gefragt).

- Benutze `su benutzername` oder `su - benutzername`, um mit der Shell zu einem anderen Benutzer zu wechseln. Füge `-` hinzu, um eine Umgebung zu erhalten, als hättest du dich gerade mit diesem Benutzer angemeldet. Das Weglassen des Benutzernamens führt zur Anmeldung als root. du wirst gefragt nach dem Passwort _des Benutzers, als der du dich anmelden willst_.

- Kenne das [128K-Limit](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong) der Befehlszeile. Der "Argument list too long"-Fehler erscheint häufig, wenn auf sehr viele Dateien über [Wildcards](https://de.wikipedia.org/wiki/Wildcard_(Informatik)) zugegriffen wird (wenn das passiert, können Alternativen wie `find` und `xargs` helfen).

- Benutze den `python`-Interpreter als einfachen Taschenrechner (und natürlich für den Zugriff auf Python im Allgemeinen). Beispiel:
```
    >>> 2+3
    5
```


## Umgang mit Dateien und Daten

- Um eine Datei im aktuellen Verzeichnis anhand des Namens zu finden, `find . -iname '*irgendwas*'`. Um eine Datei unabhängig vom Verzeichnis anhand des Namens zu finden, verwende `locate irgendwas` (bedenke jedoch, dass `updatedb` kürzlich erstellte Datein möglicherweise noch nicht indexiert hat).

- Für das allgemeine durchsuchen von (Quell-)Dateien (fortgeschrttener als `grep -r`), verwende [`ag`](https://github.com/ggreer/the_silver_searcher).

- Um HTML in Text zu konvertieren: `lynx -dump -stdin`

- Für Markdown, HTML und alle möglichen Arten von Dokumentkonvertierung, versuch's mit [`pandoc`](http://pandoc.org/).

- Wenn du mit XML arbeiten musst, `xmlstarlet` ist alt, aber gut.

- Für JSON, verwende [`jq`](http://stedolan.github.io/jq/).

- Für YAML gibt's [`shyaml`](https://github.com/0k/shyaml).

- Für Excel- bzw. CSV-Dateien hält [csvkit](https://github.com/onyxfish/csvkit) `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, etc bereit.

- Für Amazon S3 ist [`s3cmd`](https://github.com/s3tools/s3cmd) praktisch und [`s4cmd`](https://github.com/bloomreach/s4cmd) schneller. Amazons [`aws`](https://github.com/aws/aws-cli) sowie das verbesserte [`saws`](https://github.com/donnemartin/saws) sind essentiell für andere AWS-bezogene Aufgaben.

- Kenne `sort` und `uniq`, letzteres einschließlich der Optionen `-u` und `-d` -- siehe die Einzeiler unten. Siehe auch `comm`.

- Kenne `cut`, `paste` und `join` zur Arbeit mit Textdateien. Viele Leute nutzen `cut`, vergessen aber `join`.

- Kenne `wc`, um neue Zeilen (`-l`), Zeichen (`-m`), Wörter (`-w`) und Bytes (`-c`) zu zählen.

- Kenne `tee`, um von stdin in eine Datei und sogar nach stdout zu kopieren, wie etwa mit `ls -al | tee datei.txt`.

- Bei komplexeren Berechnungen, einschließlich Gruppieren, Tauschen von Feldern und statistische Berechnungen, könnte [`datamash`](https://www.gnu.org/software/datamash/) passend sein.

- Sei dir bewusst, dass die regionale Spracheinstellung ("locale") viele Befehlszeilen-Werkzeuge auf subtile Art und Weise beeinflusst, inklusive der Sortierreihenfolge und ihrer Performance. Die meisten Linux Installation setzen `LANG` oder andere lokale Variablen auf eine lokale Einstellung wie z.B. "US English". Aber sei dir bewusst, dass sich das Sortierverhalten ändern wird, falls du die "locale" änderst. Und wisse, dass "i18n"-Routinen `sort` und andere Befehle *stark* verlangsamen können. In manchen Situationen (wie den Mengen oder Identitätsfunktionen unterhalb) kann man ruhigen Gewissens langsame "i18n"-Routinen ignorieren und traditionelle byte-basierte Sortierreihenfolge nutzen, indem man `export LC_ALL=C` setzt.

- Du kannst einem bestimmten Befehl eine Umgebung zuteilen, indem seinem Aufruf die Einstellung der Umgebungsvariable vorangestellt wird, wie hier: `TZ=Pacific/Fiji date`.

- Kenne Grundlagen von`awk` und `sed` für einfache Datenverarbeitung. Um z.B. alle Zahlen in der dritten Spalte einer Textdatei aufzusummieren: `awk '{ x += $3 } END { print x }'`. Das ist wahrscheinlich 3X schneller und 3X kürzer als das Python Äquivalent.

- Um mehrere Dateien umzubenennen sowie innerhalb von Dateien zu suchen/ersetzen, probier [`repren`](https://github.com/jlevy/repren) aus (gelegentlich kann man auch mit `rename` mehrere Dateien umbenennen, aber sei vorsichtig, da dessen Funktionsweise je nach Linux-Distribution abweicht).
```sh
    # Vollständige Umbenennung von Dateinamen, Ordnern und Inhalten - foo -> bar:
    repren --full --preserve-case --from foo --to bar .
    # Backupdateien wiederherstellen - whatever.bak -> whatever:
    repren --renames --from '(.*)\.bak' --to '\1' *.bak
    # Wie oben, aber mit rename, sofern verfügbar:
    rename 's/\.bak$//' *.bak
```

- Wie die `man`-Seite richtig sagt, ist `rsync` ein schnelles und vielseitiges Werkzeug zum Kopieren von Dateien. Es ist bekannt für das Synchronisieren zwischen Rechnern, ist lokal aber ebenso nützlich. Wenn es die Sicherheitsbestimmungen zulassen, erlaubt `rsync` im Gegensatz zu `scp` die Wiederaufnahme einer Übertragung, ohne nochmal von vorn beginnen zu müssen. Es ist zudem einer der [schnellsten Wege](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html), um große Mengen an Dateien zu löschen:
```sh
mkdir leeres-verzeichnis && rsync -r --delete leeres-verzeichnis/ verzeichnis && rmdir verzeichnis
```

- Benutze `shuf` zum Mischen oder um zufällige Zeilen aus einer Datei auszuwählen.

- Kenne die Optionen von `sort`. Benutze `-n` für Zahlen, oder `-h` um mit menschenlesbaren Zahlen umzugehen (wie z.B. von `du -h`). Sei dir bewusst, wie Schlüssel funktionieren (`-t` und `-k`). Sei dir insbesondere bewusst, dass du `-k1,1` verwenden musst, um bezüglich des ersten Felds zu sortieren;`-k1` bedeutet, sortiere anhand der ganzen Zeile. Stabiles Suchen (`sort -s`) kann ebenfalls nützlich sein. Um bspw. primär nach Feld 2 und sekundär nach Feld 1 zu sortieren, kannst du `sort -k1,1 | sort -s -k2,2` benutzen.

- Falls du jemals ein Tabulator Literal in eine Befehlszeile in Bash schreiben musst (etwa den Parameter `-t` für `sort`), drücke **ctrl-v** **[Tab]** oder schreibe `$'\t'` (letzteres ist besser, da man es Kopieren/Einfügen kann).

- Die Standardwerkzeuge für das Patchen von Quellcode sind `diff` und `patch`. Siehe auch `diffstat`, um zusammenfassende Statistiken eines diffs zu erhalten. Beachte, dass `diff -r` für komplette Verzeichnisse funktioniert. Nutze `diff -r tree1 tree2 | diffstat`, um eine Übersicht aller Änderungen zu bekommen. Benutze `vimdiff`, um Dateien zu vergleichen und zu bearbeiten.

- Benutze für Binärdateien `hd`, `hexdump` or `xxd` zur Erstellung einfacher [Hexdumps](https://de.wikipedia.org/wiki/Dump#Hexdump) und `bvi` oder `biew` zur binären Bearbeitung.

- Ebenfalls für Binärdateien kann `strings` (und `grep`, etc.) benutzt werden, um Textpassagen zu finden.

- Um Diffs für Binärdateien zu erstellen (Delta Kompression), nutze `xdelta3`.

- Um zwischen Textkodierungen zu konvertieren, solltest du `iconv` probieren, oder aber `uconv` für fortgeschrittene Anwendungsfälle; es unterstüzt einige fortgeschrittene Unicode-Dinge. Dieser Befehl bspw. wandelt alle Buchstaben in Kleinbuchstaben um und entfernt alle Akzente (indem sie erweitert und verworfen werden):
```sh
    uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- Um Dateien aufzuteilen, siehe `split` (Teilung anhand einer bestimmten Größe) und `csplit` (Teilung anhand eines bestimmten Musters).

- Benutze  `zless`, `zmore`, `zcat`, und `zgrep` um mit komprimierten Dateien zu arbeiten.

- Dateieigenschaften können mit `chattr` gesetzt werden und stellen eine niederschwelligere Alternative zu Dateiberechtungen dar. So kann man etwa, um das versehentliche Löschen einer Datei zu verhindern, eine entsprechende Flag ("immutable flag") setzen: `sudo chattr +i /wichtiges/verzeichnis/oder/datei`

- Benutze `getfacl` und `setfacl`, um Dateiberechtigungen zu speichern und wiederherzustellen. Beispiel:
```sh
   getfacl -R /irgendein/pfad > berechtigungen.txt
   setfacl --restore=berechtigungen.txt
```


## Fehlerbehebung auf Systemebene

- Zur Fehlersuche bei Webanwendungen sind `curl` und `curl -I` hilfreich, ebenso wie ihre `wget` Äquivalente oder das modernere [`httpie`](https://github.com/jakubroztocil/httpie).

- Um den aktuellen CPU-/Festplattenstatus zu erfahren, sind die Klassiker `top` (oder das bessere `htop`), `iostat` und `iotop`. Benutze `iostat -mxz 15` for basic CPU and detailed per-partition disk stats and performance insight.

- Benutze für Informationen zu Netzwerkverbindungen `netstat` und `ss`.

- Für eine schnelle Übersicht, was sich auf einem System abspielt, ist `dstat` sehr nützlich. Für einen guten Gesamtüberblick bietet sich zudem [`glances`](https://github.com/nicolargo/glances) an.

- Um den Zustand des Speichers zu erfahren, führst du am besten `free` und `vmstat` aus und verstehst deren Ausgabe. Sei dir insbesondere bewusst, dass der "cached"-Wert jener Wert ist, der vom Linux-Kernel als Dateicache genutzt wird, da dieser effektiv als zum "free"-Wert addiert werden kann.

- Fehlerbehebung ("debugging") auf Java-Systemen ist ein anderes Paar Schuhe, aber ein simpler Trick für die Oracle JVM (der teilweise auch für andere JVMs funktioniert) ist `kill -3 <pid>`, sodass ein vollständiger Strack trace und Heap Informationen (inklusive Garbage Collection Details, die sehr informativ sein können) nach stderr/logs ausgegeben werden. Die JDK-Befehle `jps`, `jstat`, `jstack`, `jmap` sind ebenfalls nützlich. [SJK-Werkzeuge](https://github.com/aragozin/jvm-tools) sind noch weiter fortgeschritten.

- Benutze [`mtr`](http://www.bitwizard.nl/mtr/) als ein besseres traceroute, um Netzwerkprobleme zu identifizieren.

- Willst du wissen, warum eine Festplatte voll ist, dann spart [`ncdu`](https://dev.yorhel.nl/ncdu) Zeit gegenüber den üblichen Befehlen wie `du -sh *`.

- Um herauszufunden, welcher Socket oder Prozess Bandbreite verbraucht, kannst du [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) oder [`nethogs`](https://github.com/raboof/nethogs) verwenden.

- Das `ab`-Werkzeug (ein Teil vom Apache) ist hilfreich, um schnell und pragmatisch die Performance eines Webservers zu messen. Für komplexere Messungen kannst du `siege` ausprobieren.

- Für eine tiefergehende Netzwerk Problemsuche, [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html), oder [`ngrep`](http://ngrep.sourceforge.net/).

- Kenne `strace` und `ltrace`. Diese können hilfreich sein, falls ein Programm fehlschlägt, hängt oder abstürzt und du weißt nicht warum, oder um einen generellen Eindruck von der Performance zu bekommen. Beachte die Profiling-Option (`-c`) und die Fähigkeit, sich mit laufenden Prozessen zu verbinden (`-p`).

- Kenne `ldd`, um "shared libraries" zu überprüfen.

- Sei in der Lage, dich mittels `gdb` mit einem laufenden Prozess zu verbinden und dessen "stack traces" zu holen.

- Benutze `/proc`. Es ist manchmal unglaublich hilfreich, um Probleme in Echtzeit zu debuggen. Beispiele: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (wobei `xxx` die Prozess-ID / pid ist).

- Bei der Frage, warum in der Vergangenheit etwas schief gelaufen ist, kann [`sar`](http://sebastien.godard.pagesperso-orange.fr/) sehr hilfreich sein. Es zeigt historische Statistiken über CPU, Speicher, Netzwerk, etc.

- Für eine genauere System und Performanceanalyse, solltest du dir `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](http://en.wikipedia.org/wiki/Perf_(Linux)), und [`sysdig`](https://github.com/draios/sysdig) ansehen.

- Finde heraus, welches Betriebssystem du nutzt mittels `uname` oder `uname -a` (allgemeine Unix-/Kernelinformationen) oder `lsb_release -a` (Informationen zur verwendeten Linux-Distribution)

- Benutze `dmesg` wenn sich etwas merkdwürdig verhält (es könnte ein Hardware oder Treiber Problem sein)

- Wenn du eine Datei löschst, jedoch laut `du` nicht der erwartete Festplattenspeicher frei wird, dann überprüfe, ob die Datei von einem Prozess verwendet wird: `lsof | grep deleted | grep "dateiname"`


## Einzeiler

Ein paar Beispiele, wie man Befehle zusammen benutzen kann:

- Manchmal ist es unglaublich hilfreich, dass man die Schnittmenge, Vereinigung und den Unterschied zwischen Textdateien via `sort`/`uniq` bilden kann. Angenommen, a und b sind Textdateien, die bereits "unique" sind. Diese Herangehensweise ist schnell und funktioniert mit Dateien beliebiger Größe, bis zu mehreren Gigabytes (`sort` ist nicht durch Speicher beschränkt, obwohl man eventuell die `-T`-Option nutzen muss, falls `/tmp` auf einer kleinen Root-Partition liegt). Siehe auch die Bemerkung über `LC_ALL` weiter oben und die `-u`-Option von `sort` (wurde oben aus Gründen der Übersichtlichkeit ausgelassen).
```sh
    cat a b | sort | uniq > c   # c ist a vereint mit b
    cat a b | sort | uniq -d > c   # c ist a geschnitten b
    cat a b b | sort | uniq -u > c   # c ist die Menge mit unterschiedlichen Elementen  a - b
```

- Eine schnelle Überprüfung der Inhalte aller Dateien in einem Verzeichnis erreichst du mit `grep . *` (damit enthält jede Zeile den Dateinamen) oder `head -100 *` (damit erhält jede Datei eine Überschrift). Dies kann nützlich sein für Verzeichnisse, die Konfigurationsdateien enthalten wie jene in `/sys`, `/proc` und `/etc`.

- Alle Zahlen in der dritten Spalte einer Textdatei aufsummieren (dieser Ansatz ist wahrscheinlich dreimal schneller und enthält dreimal weniger Code als dessen Entsprechung in Python):
```sh
    awk '{ x += $3 } END { print x }' meinedatei
```

- Falls man die Größen/Datumsangaben von einem Dateibaum wissen möchte, funktioniert das Folgende wie ein rekursives `ls -l`, aber ist leichter zu lesen als `ls -lR`:
```sh
    find . -type f -ls
```

- Um Größen/Datumsangaben in einem Verzeichnisbaum zu sehen, wirkt dies wie ein umgedrehtes `ls -l`, ist aber einfacher zu lesen als `ls -lR`:
```sh
    find . -type f -ls
```

- Angenommen innerhalb einer Textdatei, so wie ein server web log, tauch ein gewisser Wert in manchen Zeilen auf, wie z.B. ein `acct_id` Parameter in der URL. Falls eine Aufzählung gewünscht ist, wie viele Anfragen es jeweils für eine `acct_id` gibt:
```sh
    cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- Um durchgehend Änderungen zu überwachen, solltest du "watch" benutzen; z.B. Dateiänderungen in einem Verzeichnis können mittels `watch -d -n 2 'ls -rtlh | tail'` überwacht werden, während du Deine Wifi Einstellungen mittels `watch -d -n 2 ifconfig` auf Fehler überprüfen kannst.

- Führe diese Funktion aus, um einen zufälligen Tip aus diesem Dokument zu erhalten(parst das Markdown Dokument und extrahiert ein Element)
```sh
    function taocl() {
      curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README-de.md |
        pandoc -f markdown -t html |
        xmlstarlet fo --html --dropdtd |
        xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
        xmlstarlet unesc | fmt -80
    }
```


## Eigenartig aber hilfreich

- `expr`: Führe arithmetische oder bool'sche Operationen aus oder werte reguläre Ausdrücke aus

- `m4`: Simpler Macro-Auswerter

- `yes`: Gib eine Zeichenkette sehr oft aus

- `cal`: Netter Kalender

- `env`: Führe einen Befehl aus (nützlich für Skripte)

- `printenv`: Gebe Umgebungsvariablen aus (nützlich zum Debuggen und für Skripte)

- `look`: Finde englische Worte (oder Zeilen in einer Datei), die mit einer bestimmten Zeichenkette anfangen

- `cut`, `paste` und `join`: Datenmanipulation

- `fmt`: Formatiere Textabsätze

- `pr`: Formatiere Text als Seiten/Spalten

- `fold`: Breche Textzeilen um

- `column`: Formatiere Textfelder als bündige Spalten oder Tabellen mit fester Größe

- `expand` und `unexpand`: Konvertiere zwischen Tabs und Spaces

- `nl`: Füge Zeilennummern hinzu

- `seq`: Gib Zahlen aus

- `bc`: Taschenrechner

- `factor`: Faktorisiere Ganzzahlen

- [`gpg`](https://gnupg.org/): Verschlüsseln und Signieren von Dateien

- `toe`: Tabelle von `terminfo`-Einträgen

- `nc`: Netzwerk-Debugging und Datentransfer

- `socat`: Socket- und TCP-Port-Weiterleitung (ähnlich wie `netcat`)

- [`slurm`](https://github.com/mattthias/slurm): Visulaisierung des Netzwerkverkehrs ("traffic")

- `dd`: Daten zwischen Dateien und Geräten bewegen

- `file`: Identifiziere den Typ einer Datei

- `tree`: Zeige Verzeichnisse und Unterverzeichnisse als verschachtelten Baum; wie `ls` aber rekursiv

- `stat`: Datei Infomationen

- `time`: Führe einen Befehl aus und messe die Zeit

- `timeout`: Führe einen Befehl für eine bestimmte Zeit aus und beende ihn anschließend wieder

- `lockfile`: Erstelle eine Semaphordatei, die nur gelöscht werden kann mit `rm -f`

- `logrotate`: Rotiert, komprimiert und mailt System-Log-Dateien

- `watch`: Führe einen Befehl wiederholt aus, wobei die Ergebnisse angezeigt und/oder Änderungen hervorgehoben werden

- `tac`: Gebe Dateien in umgekehrter Reihenfolge aus

- `shuf`: Zufällige Auswahl von Zeilen von einer Datei

- `comm`: Vergleiche sortierte Dateien Zeile für Zeile

- `pv`: Überwache den Fortschritt von Daten durch eine Pipe

- `hd`, `hexdump`, `xxd`, `biew` und `bvi`: Ausgabe und Editieren von Binärdateien

- `strings`: Text aus Binärdateien extrahieren

- `tr`: Buchstabenübersetzung und -manipulation

- `iconv` oder `uconv`: Konvertierung von Zeichensätzen

- `split` und `csplit`: Dateien aufteilen

- `sponge`: Liest die gesamte Eingabe, bevor sie wieder ausgegeben wird. Nützlich, um aus derselben Datei zu lesen und in diese zu schreiben, bspw. `grep -v irgendwas irgendeine-datei | sponge irgendeine-datei`

- `units`: Einheiten Konvertierungen und Berechnungen; konvertiert Furlong(Achtelmeile)/Fortnights(2 Wochen) zu twips/blink (siehe `/usr/share/units/definitions.units`)

- `apg`: Generiert zufällige Passwörter

- `xz`: Hochgradige Dateikompression

- `ldd`: Informationen zu dynamisch gelinkten Bibliotheken

- `nm`: Symbole aus Objektdateien anzeigen

- `ab`: Webserver benchmarken

- `strace`: Debugging von Syscalls

- [`mtr`](http://www.bitwizard.nl/mtr/): Ein besseres "traceroute" zum Netzwerk-Debugging

- `cssh`: Visuelle, nebenläufige Shell

- `rsync`: Synchronisiere Dateien und Ordner über SSH oder im lokalen Dateisystem

- [`wireshark`](https://wireshark.org/) and [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): Pakete aufzeichnen und Netzwerk-Debugging

- [`ngrep`](http://ngrep.sourceforge.net/): grep für die Netzwerkschicht

- `host` und `dig`: DNS-Auflösung

- `lsof`: Prozess Datei Deskriptor und Socket Informationen

- `dstat`: Nützliche Systemstatistiken

- [`glances`](https://github.com/nicolargo/glances): Grobe Übersicht über zahlreiche Subsysteme

- `iostat`: Fesplatten-Nutzungsstatistiken

- `mpstat`: CPU-Nutzungstatistiken

- `vmstat`: Speicher-Nutzungsstatistiken

- `htop`: Verbesserte Version von `top`

- `last`: Loginverlauf

- `who`: Wer gerade angemeldet ist

- `id`: Identitätsinformationen zu Benutzern/Gruppen

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): Historische Systemstatistiken

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) or [`nethogs`](https://github.com/raboof/nethogs): Netzwerknutzung durch Sockets oder Prozesse

- `ss`: Socket-Statistiken

- `dmesg`: Bootvorgang und System-Fehlermeldungen

- `sysctl`: Anzeige und Konfiguration von Linux Kernel Parametern zur Laufzeit

- `hdparm`: SATA/ATA-Festplattenmanipulation/-performanceinformationen

- `lsblk`: Auflisten von block devices: eine Baumansicht deiner Festplatten und Partitionen

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: Hardware-Informationen, inklusive CPU, BIOS, RAID, Grafikkarten, Geräte, etc.

- `lsmod` und `modinfo`: Auflisten und Details anzeigen von Kernelmodulen

- `fortune`, `ddate`, und `sl`: Ähm ja, kommt darauf an, ob man Dampflokomotiven und flotte Zitate "nützlich" findet


## Nur MacOS X

Diese Hinweise sind *nur* für MacOS relevant.

- Paketverwaltung mit `brew` (Homebrew) und/oder `port` (MacPorts). Mit diesen Werkzeugen kann man viele der obrigen Programme für MacOs installieren.

- Kopiere die Ausgabe eines beliebigen Befehls an eine Desktop App mit `pbcopy` und füge die Eingabe von einer solchen ein mit `pbpaste`.

- Um die Option Taste als alt-Taste in einer Mac OS Konsole zu nutzen (so wie in den obrigen Befehle wie **alt-b**, **alt-f**, etc.), öffne Einstellungen -> Profile -> Tastatur und aktiviere "Benutze Option Taste als Meta Taste"

- Um eine Datei mit einer Desktopanwendung zu öffnen, kann man `open` oder `open -a /Applications/Whatever.app` benutzen.

- Spotlight: Dateisuche mit `mdfind` und Ausgabe von Metadaten (wie z.B. photo EXIF info) mit `mdls`.

- Man sollte sich bewusst sein, dass MacOS auf BSD Unix basiert und sich viele Befehle (wie z.B. `ps`, `ls`, `tail`, `awk`, `sed`) bezüglich subtiler Kleinigkeiten von Linux, das stark von System V-style Unix und GNU tools beeinflusst ist, unterscheiden. Oft kann man den Unterschied daran erkennen, dass eine `man`-Seite die Überschrift  "BSD General Commands Manual" trägt. In manchen Fällen kann auch die GNU-Version installiert werden (wie z.B. bei `gawk` und `gsed` für GNU awk und sed). Falls manplattformübergreifende Bash-Skripte schreiben möchte, sollte man solche Befehle vermeiden (und z.B. Python oder `perl` in Betracht ziehen) oder sorgfätig testen.

- Benutze `sw_vers` für OS X Systeminformationen.


## Nur Windows

Diese Hinweise sind *nur* für Windows relevant.

### Möglichkeiten, Unix-Tools unter Windows zu erhalten

- Zugriff auf die Macht der Unix-Shell erhälst du unter Microsoft Windows durch die Installation von  [Cygwin](https://cygwin.com/). Die meisten hier beschriebenen Dinge funktionieren damit ohne weiteren Aufwand.

- Mit Windows 10 kannst du [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about) benutzen, das eine vertraute Bash-Umgebung mit Unix-Befehlszeilen-Werkzeugen. Dies erlaubt einerseits die Nutzung von Linux-Programmen auf Windows, unterstützt andererseits jedoch nicht die Ausführung von Windows-Programmen von der Bash-Konsole.

- Eine weitere Option, GNU-Entwicklerwerkzeuge (etwa GCC) auf Windows zu nutzen, besteht darin, [MinGW](http://www.mingw.org/) und dessen Paket [MSYS](http://www.mingw.org/wiki/msys), das Hilfsprogramme wie bash, gawk, make and grep beinhaltet, zu installieren. MSYS bringt allerdings nicht so viele Features mit wie etwa Cygwin. MinGW ist besonders nützlich für die Erstellung nativer Windows-Ports von Unix-Werkzeugen.

- Eine andere Möglichkeit, ein wenig Unix auf dein Windows-System zu bringen, bietet [Cash](https://github.com/dthree/cash). Beachte allerdings, dass nur sehr wenige Unix-Befehle und Befehlszeilen-Optionen in dieser Umgebung zur Verfügung stehen.

### Nützliche Windows Befehlszeilen-Werkzeugen

- Du kannst die meisten Aufgaben der Windows-Systemverwaltung von der Befehlszeile ausführen und skripten, indem du den Umgang mit `wmic` lernst.

- Native Windows Befehlszeilen Netzwerk Werkzeugen, die du nützlich finden kannst, gehören `ping`,` ipconfig`, `traceroute` und `netstat`.

- Du kannst [viele nützliche Windows-Aufgaben] (http://www.thewindowsclub.com/rundll32-shortcut-commands-windows) durch Aufrufen des Befehls `Rundll32` ausführen.

### Cygwin Tipps und Tricks

- Installiere zusätzliche Unix-Programme mit Cygwins Paketmanager.

- Benutze `mintty` als dein Befehlszeilenfenster.

- Greife mit `/dev/clipboard` auf die Zwischenablage von Windows zu.

- Öffne beliebige Dateien über `cygstart` mit deren Standardprogramm.

- Greife mit `regtool` auf die Windows-Registry zu.

- Beachte, dass der Windows-Pfad `C:\` unter Cygwin zu `/cygdrive/c` wird und dass Cygwins `/` unter Windows als `C:\cygwin` verfügbar ist. Für die Umwandlung zwischen Cygwin- und Windows-Pfaden steht `cygpath` zur Verfügung. Dies ist inbesondere für Skripte nützlich, welche Windows-Programme ausführen.


## Weitere Quellen

- [awesome-shell](https://github.com/alebcay/awesome-shell): Eine hilfreiche Liste von Shell-Werkzeugen und Quellen.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): Eine ausführliche Anleitung für die Befehlszeile unter OS X.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/), um bessere Shell-Skripte zu schreiben.
- [shellcheck](https://github.com/koalaman/shellcheck): Ein statisches Analysetool für Shell-Skripte. Im Grunde lint für bash/sh/zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): Entmutigend komplexe Einzelheiten darüber, wie Dateinamen in Shell-Skripts richtig eingesetzt werden.
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools): Mehr Befehle und Werkzeuge, die für ["data science"](https://de.wikipedia.org/wiki/Data_Science) hilfreich sind, aus dem gleichnamigen Buch.


## Haftungsausschluss

Mit der Ausnahme einiger sehr kleiner Aufgaben ist der Code so geschrieben, dass andere ihn lesen können. Mit Macht kommt Verantwortung. Die Tatsache etwas in Bash tun zu *können*, heißt nicht zwangsläufig, dass du es tun solltest!


## Lizenz

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

Dieses Werk ist lizensiert gemäß der [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
