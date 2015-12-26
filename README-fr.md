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
