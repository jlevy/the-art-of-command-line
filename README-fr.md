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
