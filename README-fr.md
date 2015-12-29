[ Langues:
[English](README.md), [Español](README-es.md), [Français](README-fr.md), [Italiano](README-it.md), [日本語](README-ja.md), [한국어](README-ko.md), [Português](README-pt.md), [Русский](README-ru.md), [Slovenščina](README-sl.md), [Українська](README-uk.md), [中文](README-zh.md)
]

# L'art de la ligne de commande

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Meta](#meta)
- [Notions de base](#notions-de-base)
- [Utilisation quotidienne](#utilisation-quotidienne)
- [Traitement des fichiers et des données](#traitement-des-fichiers-et-des-données)
- [Débogage du système](#débogage-du-système)
- [Unilignes](#unilignes)
- [Obscures mais utiles](#obscures-mais-utiles)
- [Uniquement OS X](#uniquement-os-x)
- [Ressources supplémentaires](#ressources-supplémentaires)
- [Avertissement](#avertissement)

![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

La maîtrise de la ligne de commande est une compétence souvent négligée ou considérée ésotérique, pourtant elle améliore de façon évidente et subtile votre habilité et votre productivité en tant qu'ingénieur.
Ceci est une sélection de notes et d'astuces sur l'utilisation de la ligne de commande que nous avons trouvées utiles en travaillant avec Linux.
Certaines sont élémentaires, d'autres sont assez spécifiques, complexes ou obscures.
Cette page n'est pas bien longue, mais si vous pouvez retenir et vous servir de tout ce qui se trouve dans ce document, alors vous saurez beaucoup de choses.

Ce document est le fruit du travail de [nombreux auteurs et de traducteurs](AUTHORS.md).
Une bonne partie a été [publiée](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands) [à l'origine](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix) sur [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know), mais compte tenu de l'intérêt qu'il a suscité, il nous a paru bon de le mettre sur GitHub, où des personnes plus compétentes que l'auteur originel pourraient facilement proposer des améliorations.
Si vous voyez une erreur ou quelque chose à améliorer, veuillez remplir un ticket ou soumettre un *pull request* ! (Bien sûr, veuillez d'abord consulter la section [Méta](#meta) ainsi que les *pull requests* et tickets actifs.)


## Méta

Contexte :

- Ce guide est destiné aux utilisateurs débutants et chevronnés.
Les objectifs sont l'*envergure* (tout est important), la *spécificité* (donner des exemples concrets des cas les plus courants) et la *concision* (éviter tout ce qui n'est pas essentiel et les digressions disponibles facilement ailleurs).
Chaque astuce est indispensable dans certaines situations ou fait gagner un temps considérable par rapport aux solutions alternatives.
- Il est écrit pour Linux, à l'exception de la section « [Uniquement OS X](#uniquement-os-X) ».
Beaucoup des autres items s'appliquent ou peuvent être installés sur d'autres Unices ou Mac OS (ou même Cygwin).
- L'accent est mis sur l'utilisation intéractive de Bash, bien que de nombreuses astuces s'appliquent aux autres shells et à l'écriture de scripts Bash.
- Il inclut les commandes « standard » d'Unix aussi bien que celles qui nécessitent l'installation des paquets spéciaux &mdash; tant qu'ils sont suffisamment importants pour mériter d'être mentionnés.

Remarques :

- Afin que tout tienne sur une seule page, le contenu est implicitement inclus par référence.
Vous êtes suffisamment intelligents pour chercher les renseignements ailleurs une fois que vous avez l'idée ou la commande à googler.
Utilisez `apt-get`, `yum`, `dnf`, `pacman`, `pip` ou `brew` (selon votre distribution ou OS) pour installer de nouveaux programmes.
- Utilisez [Explainshell](http://explainshell.com) pour obtenir de l'aide à propos des commandes, options, tubes, etc.


## Traitement des fichiers et des données

- Pour localiser un fichier par son nom dans le répertoire courant, `find . -iname '*something*'` (ou autres).
Pour trouver un fichier n'importe où par son nom, utilisez `locate something` (mais n'oubliez pas que `updatedb` peut ne pas avoir indexé les fichiers récemment créés).

- Pour une recherche à travers les fichiers sources ou fichiers de données (plus poussée que `grep -r`), utilisez [`ag`](https://github.com/ggreer/the_silver_searcher).

- Pour convertir du HTML en texte brut : `lynx -dump -stdin`.

- Pour le Markdown, HTML et les conversions dans toutes sortes de formats, essayez [`pandoc`](http://pandoc.org).

- Si vous devez manipuler du XML, le vieux `xmlstarlet` marche bien.

- Pour le JSON, utilisez [`jq`](http://stedolan.github.io/jq/).

- Pour le YAML, utilisez [`shyaml`](https://github.com/0k/shyaml).

- Pour les fichiers Excel ou CSV, [csvkit](https://github.com/onyxfish/csvkit) fournit `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, etc.

- Pour Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) est pratique et [`s4cmd`](https://github.com/bloomreach/s4cmd) est plus rapide.
L'outil d'Amazon [`aws`](https://github.com/aws/aws-cli) et la version améliorée [`saws`](https://github.com/donnemartin/saws) sont indispensables pour les autres tâches liées à AWS.

- Connaissez `sort` et `uniq`, y compris les options `-u` et `-d` de `uniq` (voir les unilignes plus bas). Voir aussi `comm`.

- Connaissez `cut`, `paste` et `join` pour manipuler les fichiers textes.
Beaucoup de personnes utilisent `cut` mais oublient `join`.

- Connaissez `wc` pour compter les lignes (`-l`), les caractères (`-m`), les mots (`-w`) et les octets (`-c`).

- Connaissez `tee` pour copier depuis stdin vers un fichier ou vers stdout, comme dans `ls -al | tee file.txt`.

- Sachez que la locale affecte de nombreux outils en ligne de commande de manière subtile, comme l'ordre pour les tris (collation) et les performances.
La plupart des installateurs Linux définissent la variable `LANG` ou d'autres variables locales d'environnement pour configurer une locale telle que US English.
Mais ayez à l'esprit que le tri sera modifié si vous changez la locale.
Et sachez que les routines i18n peuvent rendre les opérations de tri et d'autres commandes *beaucoup* plus lentes.
Dans certains cas (tels que les opérations concernant les ensembles et l'unicité abordées ci-dessous) vous pouvez, sans risque, complètement ignorer les lentes routines i18n et utiliser l'ordre classique basé sur les octets à l'aide de `export LC_ALL=C`.

- Connaissez `awk` et `sed` pour de l'analyse de données élémentaire.
Par exemple, pour effectuer la somme de tous les nombres de la troisième colonne d'un fichier texte&nbsp;: `awk '{ x += $3 } END { print x}'`.
C'est probablement trois fois plus rapide et trois fois plus petit que son équivalent en Python.

- Pour remplacer toutes les occurences d'une chaîne de caractères dans un ou plusieurs fichiers&nbsp;:
```sh
    perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- Pour renommer de multiple fichiers ou effectuer des recherches et remplacements dans des fichiers, essayez [`repren`](https://github.com/jlevy/repren) (dans certains cas la commande `rename` permet aussi de renommer de multiples fichiers, mais soyez prudent car ses fonctionnalités ne sont pas les mêmes sur toutes les distributions Linux).
```sh
    # Renomme les répertoires, les fichiers et leurs contenus à l'aide
    # de la substitution foo -> bar :
    repren --full --preserve-case --from foo --to bar .
    # Restaure des fichiers de sauvegarde à l'aide de la
    # substitution whatever.bak -> whatever :
    repren --renames --from '(.*)\.bak' --to '\1' *.bak
    # Même chose que ci-dessus avec rename s'il est disponible :
    rename 's/\.bak$//' *.bak
```

- Selon sa page de manuel, `rsync` est un outil de duplication de fichiers vraiment rapide et incroyablement polyvalent.
Il est connu pour faire de la synchronisation entre machines, mais est également utile pour un usage local.
Il est aussi parmi les outils [les plus rapides](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) pour effacer un grand nombre de fichiers&nbsp;:
```sh
    mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Utilisez `shuf` pour mélanger ou sélectionner aléatoirement des lignes d'un fichier.

- Connaissez les options de `sort`.
Pour les nombres, utilisez `-n`, ou `-h` pour traiter des nombres dans un format lisible par un humain (p.&nbsp;ex. issus de `du -h`).
Sachez comment les clés fonctionnent (`-t` et `-k`).
En particulier, faites attention à bien écrire `-k1,1` pour trier selon le premier champ uniquement&nbsp;: `-k1` signifie que l'on trie selon la ligne entière.
Le tri stable (`sort -s`) peut s'avérer utile.
Par exemple, pour trier d'abord selon le champ 2, puis selon le champ 1, vous pouvez utiliser `sort -k1,1 | sort -s -k2,2`.

- Si jamais vous avez besoin d'écrire un caractère de tabulation dans une ligne de commande en Bash (p.&nbsp;ex pour le paramètre de l'option de tri `-t`), entrez **ctrl-v** **[Tab]** ou écrivez `$'\t'` (préférable car vous pouvez la copier-coller).

- Les outils habituels pour *patcher* un code source sont `diff` et `patch`.
Voir aussi `diffstat` pour un relevé statistique d'un diff et `sdiff` pour un affichage côte à côte d'un diff.
Remarquez que `diff -r` marche avec des répertoires entiers.
Utilisez `diff -r tree1 tree2 | diffstat` pour obtenir un résumé des changements.
Utilisez `vimdiff` pour comparer et éditer des fichiers.

- Pour les fichiers binaires, utilisez `hd`, `hexdump` ou `xxd` pour un affichage simple en hexadécimal et `bvi`, `biew` pour éditer des fichiers binaires.

- Également pour les fichiers binaires, `strings` (ainsi que `grep`, etc) vous permet d'y trouver des bouts de texte.

- Pour effectuer des différences entre des fichiers binaires (compression différentielle), utilisez `xdelta3`.

- Pour changer l'encodage d'un texte, essayer `iconv`, ou `uconv` pour un usage plus sophistiqué : il permet quelques trucs avancés avec l'Unicode.
Par exemple, cette commande met en minuscules et retire tous les accents (en les développant et les écartant)&nbsp;:
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- Pour découper des fichiers en morceaux, voyez `split` pour un découpage en morceaux de taille donnée et `csplit` pour un découpage en morceaux délimités par un motif.

- Pour manipuler des dates et des heures, utilisez `dateadd`, `datediff`, `strptime`, etc. fournis par [`dateutils`](http://www.fresse.org/dateutils/).

- Utilisez `zless`, `zmore`, `zcat` et `zgrep` pour opérer sur des fichiers compressés.


## Débogage du système

- Pour du débogage web, `curl` et `curl -I` sont pratiques, de même que leurs
équivalents avec `wget`  ou le plus moderne [`httpie`](https://github.com/jkbrzt/httpie).

- Pour connaître l'état courant du CPU ou du disque, les outils conventionnels sont `top` (ou `htop` meilleur), `iostat` et `iotop`.
Utilisez `iostat -mxz 15` pour des statistiques de base concernant le CPU, des statistiques détaillées pour les disques et un aperçu des performances.

- Pour des informations sur les connexions réseaux, utilisez `netstat` et `ss`.

- Pour un rapide aperçu de ce qui se passe dans le système, `dstat` est particulièrement utile. 
Pour un aperçu plus étendu et détaillé, utilisez [`glances`](https://github.com/nicolargo/glances).

- Pour connaître l'état de la mémoire, exécutez `free` et `vmstat` et comprenez leurs sorties.
En particulier, ayez à l'esprit que la valeur du « cache » est la mémoire utilisée par le noyau Linux comme cache de fichiers, donc compte comme de la mémoire « libre ».

- Le système de debogage de Java est une autre paire de manche, cependant un truc simple sur la JVM d'Oracle et quelques autres JVMs consiste à exécuter `kill -3 <pid>` pour obtenir une trace complète des appels et une empreinte de la mémoire (y compris des détails sur le ramasse-miettes qui peuvent être hautement instructifs) dans stderr ou des fichiers journaux.
Les commandes `jps`, `jstat`, `jstack` et `jmap` de la JDK sont utiles. L'[outil SJK](https://github.com/aragozin/jvm-tools) est plus avancé.

- Utilisez `mtr` comme un `traceroute` amélioré pour identifier les problèmes de réseau.

- Pour déterminer les raisons pour lesquelles un disque est plein, `ncdu` permet de gagner du temps par rapport aux commandes habituelles telles que `du -sh *`.

- Pour trouver quel socket ou processus utilise la bande passante essayez `iftop` ou `nethogs`.

- L'outil `ab` (fourni avec Apache) est utile pour une vérification rapide et grossière des performances d'un serveur web.
Pour des tests de charge plus complexes servez-vous de `siege`.

- Pour du debogage réseau plus sérieux : `wireshark`, `tshark` ou `ngrep`.

- Connaîssez `strace` et `ltrace`.
Ces commandes peuvent être utiles si un programme fonctionne mal ou plante et que vous n'en connaissez pas la raison, ou si vous voulez vous faire une idée des performances.
Remarquez l'option de profilage (`-c`) et la possibilité de les rattacher à un processus en cours d'exécution (`-p`).

- Connaîssez `ldd` pour afficher les bibliothèques partagées, etc.

- Sachez comment vous connecter à un processus en cours avec `gdb` et récupérer la trace d'appels.

- Utilisez `/proc`. C'est parfois incroyablement utile pour résoudre des problèmes en live.
Exemples&nbsp;: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd`, `/proc/xxx/smaps` (où `xxx` est l'identifiant du processus ou pid).

- Pour comprendre pourquoi quelque chose a mal tourné antérieurement, `sar` peut-être très utile.
Elle fournit un historique concernant l'usage du CPU, de la mémoire, du réseau, etc.

- Pour une analyse plus approfondie du système et des performances, regardez `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_(Linux) et [`sysdig`](https://github.com/draios/sysdig).

- Vérifiez quel OS vous utilisez avec `uname` ou `uname -a` (information général sur l'Unix et le noyau) ou `lsb_release -a` (informations sur la distribution Linux).

- Utilisez `dmesg` à chaque fois que quelque chose de bizarre se produit (pour des problèmes liés au matériel ou aux drivers).


## Unilignes

Quelques exemples d'assemblages de commandes&nbsp;:

- Il est quelques fois extrèmement utile de pouvoir faire une intersection, union ou différence de fichiers texte à l'aide de `sort` et `uniq`.
Supposez que `a` et `b` soient des fichiers texte ne contenant pas de lignes répétées.
C'est rapide et fonctionne sur des fichiers de taille quelconque jusqu'à plusieurs gigaoctets (le tri n'est pas limité par la capacité mémoire bien que vous puissiez avoir besoin d'utiliser l'option `-T` si `/tmp` est sur une petite partition racine).
Voyez aussi la remarque à propos de `LC_ALL` ci-dessus et l'option `-u` de `sort` (omise ci-dessous pour plus de clarté).
```sh
    cat a b | sort | uniq > c       # c est l'union de a et b
    cat a b | sort | uniq -d > c    # c est l'intersection de a et b
    cat a b b | sort | uniq -u > c  # c est la difference  a - b
```

- Utilisez `grep . *` pour rapidement inspecter les contenus des fichiers d'un repértoire (chaque ligne est précédé du nom du fichier) ou `head -100 *` (chaque fichier a un titre).
Cela peut être utile pour des répertoires remplis de fichiers de configuration comme ceux de `/sys`, `/proc`, `/etc`.

- Pour ajouter les nombres de la troisième colonne d'un fichier texte (c'est probablement trois fois plus rapide et trois fois plus petit que son équivalent en Python)&nbsp;:
```sh
    awk '{ x += $3 } END { print x }' myfile
```

- Pour visualiser les tailles et les dates des fichiers d'une arborescence, une sorte de `ls -l` récursive, mais plus facile à lire que `ls -lR`&nbsp;:
```sh
    find . -type f -ls
```

- Supposons que vous ayez un fichier texte comme un fichier journal de serveur web et q'une certaine valeur, comme un paramètre `acct_id` présent dans l'URL, figure à certaines lignes. 
Si vous voulez un décompte du nombre de requêtes pour chaque valeur de `acct_id`&nbsp;:
```sh
    cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- Pour surveiller en permanence tout changement, utilisez `watch`, par exemple vérifiez les modifications dans les fichiers d'un répertoire avec `watch -d -n 2 'ls -rtlh | tail'` ou surveillez les paramètres de votre réseau tout en dépannant la configuration de votre wifi avec `watch -d -n 2 ifconfig`.

- Exécutez cette fonction pour afficher aléatoirement une astuce de ce texte (analyse le le code en Markdown et en extrait un élément d'une liste)&nbsp;:
```sh
     function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```


## Obscures mais utiles

- `expr` : effectue des operations arithmétiques et booléenne, et évalue des expressions régulières.

- `m4` : simple macro processeur.

- `yes` : affiche une chaîne de caractères indéfiniment.

- `cal` : un calendrier sympathique.

- `env` : exécute une commande (utile dans les scripts).

- `printenv` : imprime les variables d'environnement (utile pour le débogage et dans les scripts).

- `look` : trouve les mots anglais (ou les lignes d'un fichier) commençant par une chaîne donnée.

- `cut`, `paste` and `join` : manipulation des données.

- `fmt` : formate du texte.

- `pr` : formate un texte en page ou en colonne.

- `fold` : coupe des lignes de texte.

- `column` : formate un texte en colonnes alignées, de largeurs fixes ou en tables.

- `expand` et `unexpand` : convertit les tabulations en espaces et vice-versa.

- `nl` : numérote les lignes d'un fichier.

- `seq` : affiche une suite de nombres.

- `bc` : une calculatrice.

- `factor` : factorise des nombres entiers.

- [`gpg`](https://gnupg.org/) : chiffre et signe les fichiers.

- `toe` : table des entrées terminfo.

- `nc` : debogage réseau et transfert de données.

- `socat` : relai et réacheminement de port TCP (semblable à `netcat`).

- [`slurm`](https://github.com/mattthias/slurm) : visualisation du trafic réseau.

- `dd` : déplacer les données entre les fichiers ou les périphériques.

- `file` : détermine le type d'un fichier

- `tree` : affiche les répertoires et sous-répertoires sous la forme d'un arbre (comme `ls` mais récursivement).

- `stat` : affiche des informations sur un fichier.

- `time`: exécute et chronomètre une commande.

- `timeout`: exécute une commande avec une limite de temps et stoppe le processus après la durée indiquée.

- `lockfile` : crée un fichier sémaphore qui ne peut être supprimé que par `rm -f`

- `logrotate` : permet la rotation, la compression et l'envoi des fichiers journaux par courrier électronique.

- `watch` : exécute une commande périodiquement, affiche le résultat et surligne les différences entre les résultats.

- `tac` : affiche des fichiers à l'envers.

- `shuf` : affiche une permutation aléatoire des lignes d'un fichier.

- `comm` : compare ligne à ligne deux fichiers triés.

- `pv` : surveille la progression des données à travers un tube.

- `hd`, `hexdump`, `xxd`, `biew` et `bvi` : dump et édition de fichiers binaires.

- `strings` : extraire du texte de fichiers binaires.

- `tr` : conversion et manipulation de caractères.

- `iconv` ou `uconv` : conversion entre différents encodages de caractères.

- `split` et `csplit` : découpage de fichiers.

- `sponge` : lit l'entrée standart avant de l'écrire. Utile pour lire depuis un fichier puis écrire dans le même fichier, p.ex., `grep -v something some-file | sponge some-file`

- `units` : conversions d'unités et calculs. Convertit des furlongs par fortnight en twips par blink (voir aussi `/usr/share/units/deifinitions.units`).

- `apg` : génère des mots de passe aléatoires.

- `7z` : compresse des fichiers avec taux de compression élevé.

- `ldd` : affiche des informations sur les bibliothèques partagées.

- `nm` : affiche les symboles contenus dans un fichier objet.

- `ab` : mesure les performances de serveurs web

- `strace`: trace les appels système.

- `mtr`: un traceroute amélioré pour débugguer un réseau.

- `cssh` : visual concurrent shell

- `rsync` : synchronise des fichiers et des dossiers via SSH ou localement.

- `wireshark` et `tshark`: capture de paquets et dépannage réseau.

- `ngrep` : grep pour les couches réseau.

- `host` et `dig`: interroge les serveurs DNS.

- `lsof` : process file descriptor and socket info.

- `dstat` : statistiques sur les ressources système.

- [`glances`](https://github.com/nicolargo/glances): high level, multi-subsystem overview

- `iostat` : statistiques sur l'usage des disques.

- `mpstat` : statistiques sur l'usage des CPUs.

- `vmstat` : statistiques sur l'usage de la mémoire.

- `htop` : version améliorée de top.

- `last` : historique des connexions.

- `w` : montre qui est connecté.

- `id` : affiche les informations sur un utilisateur et ses groupes.

- `sar` : statistiques sur l'activité du système

- `iftop` ou `nethogs` : utilisation du réseau par un socket ou un processus.

- `ss` : statistiques relatives aux sockets.

- `dmesg` : messages lors du démarrage et erreurs système.

- `sysctl` : visualise et configure les paramètres du noyau Linux à chaud.

- `hdparm` : manipulation et performances d'un disque SATA ou ATA.

- `lsb_release` : informations sur la distribution Linux.

- `lsblk` : affiche les périphériques blocs (une arborescence de vos disques et partitions).

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode` : informations sur le matériel, comprenant le CPU, le BIOS, le RAID, la carte graphique, les périphériques, etc.

- `lsmod` et `modinfo` : liste des modules du noyau et informations les concernant.

- `fortune`, `ddate` et `sl` : euh, bon, seulement si vous considérez les locomotives à vapeur et les citations de Jean-Claude Van Damme « utiles ».


## Uniquement OS X

Ce qui suit ne s'applique *qu'*à Mac OS.

- Gestion des paquets avec `brew` (Homebrew) ou `port` (MacPorts).
Ceux-ci peuvent être utilisés pour installer sur Mac OS la plupart des commandes mentionnées ci-dessous.

- Copier la sortie de n'importe quelle commande dans une application de bureau avec `pbcopy` et coller l'entrée d'une commande avec `pbpaste`.

- Pour permettre à la touche Option de fonctionner comme la touche Alt dans le terminal de Mac OS (comme dans les commandes **alt-b**, **alt-f**, etc), allez dans Préférences -> Profils -> Clavier et sélectionner « Choisir la touche Option comme touche virtuelle ».

- Pour ouvrir un fichier avec une application de bureau, utilisez `open` ou `open -a /Applications/Whatever.app`.

- Spotlight&nbsp;: recherche de fichiers avec `mdfind` et affichage des métadonnées (telles que les informations EXIF d'une photo) avec `mdls`.

- Ayez à l'esprit que Mac OS dérive du système Unix BSD et que beaucoup de commandes (par exemples `ps`, `ls`, `tail`, `awk`, `sed`) présentent de légères différences avec leurs versions pour Linux, qui lui est largement influencé par System V et les outils GNU.
Vous pouvez souvent faire la distinction grâce à l'en-tête « BSD General Commands Manual » dans les pages de manuel.
Dans certains cas, les versions GNU peuvent également être installées (telles que `gawk` et `gsed` pour GNU awk et GNU sed).
Pour écrire des scripts Bash multi-plateformes évitez d'utiliser de telles commandes (par exemple, envisagez d'utiliser Python ou Perl) ou alors testez-les soigneusement.

- Pour obtenir des informations sur la version de Mac OS, servez-vous de `sw_vers`.


## Autres ressources

- [awesome-shell](https://github.com/alebcay/awesome-shell)&nbsp;: une liste organisée d'outils et ressources pour le shell.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): un guide plus approfondi sur la ligne de commande pour Mac OS.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/)&nbsp;: pour écrire de meilleurs scripts shell.
- [shellcheck](https://github.com/koalaman/shellcheck)&nbsp;: un outil d'analyse statique des scripts shell. L'équivalent de lint pour bash, sh et zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html)&nbsp;: les points de détail, malheureusement compliqués, sur la manière de manipuler correctement les noms de fichiers dans les scripts shell.


## Avertissement

Sauf pour de petites tâches, le code est écrit de sorte que d'autres personnes puissent le lire.
Il n'y a pas de pouvoir sans responsabilité : le fait que vous *puissiez* faire quelque chose en Bash ne signifie nécessairement que vous devriez le faire ! ;)


## Licence

[![Licence Creative Commons](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

Ce document est mis à disposition selon les termes de la [Licence Creative Commons Attribution - Partage dans les mêmes conditions 4.0 International](http://creativecommons.org/licenses/by-sa/4.0/).
