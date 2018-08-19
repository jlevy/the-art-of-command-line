🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*

# L'art de la ligne de commande

[![Ask a Question](https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg)](https://airtable.com/shrzMhx00YiIVAWJg)

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%19Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Méta](#méta)
- [Notions de base](#notions-de-base)
- [Utilisation quotidienne](#utilisation-quotidienne)
- [Traitement des fichiers et des données](#traitement-des-fichiers-et-des-données)
- [Débogage du système](#débogage-du-système)
- [Unilignes](#unilignes)
- [Obscures mais utiles](#obscures-mais-utiles)
- [Uniquement macOS](#uniquement-macos)
- [Uniquement Windows](#uniquement-windows)
- [Autres ressources](#autres-ressources)
- [Avertissement](#avertissement)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

La maîtrise de la ligne de commande est une compétence souvent négligée ou considérée ésotérique, pourtant elle améliore de façon évidente et subtile votre habilité et votre productivité en tant qu'ingénieur.
Ceci est une sélection de notes et d'astuces sur l'utilisation de la ligne de commande que nous avons trouvées utiles en travaillant avec Linux.
Certaines sont élémentaires, d'autres sont assez spécifiques, complexes ou obscures.
Cette page n'est pas bien longue, mais si vous pouvez retenir et vous servir de tout ce qui s'y trouve, alors vous saurez beaucoup de choses.

Ce document est le fruit du travail de [nombreux auteurs et traducteurs](AUTHORS.md).
Une partie de celui-ci a été [initialement](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands) [publiée](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix) sur [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know), mais il se trouve maintenant sur GitHub, où des personnes plus compétentes que l'auteur originel ont apporté de nombreuses améliorations.
[**N'hésitez pas à poser des questions**](https://airtable.com/shrzMhx00YiIVAWJg) sur la ligne de commande.
[**Merci de contribuer**](/CONTRIBUTING.md) si vous voyez une erreur ou quelque chose qui pourrait être amélioré !


## Méta

Contexte :

- Ce guide est destiné aux débutants et aux utilisateurs chevronnés.
Les objectifs sont l'*envergure* (tout est important), la *spécificité* (donner des exemples concrets des cas les plus courants) et la *concision* (éviter tout ce qui n'est pas essentiel et les digressions disponibles facilement ailleurs).
Chaque astuce est indispensable dans certaines situations ou fait gagner beaucoup de temps par rapport aux solutions alternatives.
- Il est écrit pour Linux, à l'exception des sections « [Uniquement macOS](#uniquement-macos) » et « [Uniquement Windows](#uniquement-windows) ».
Beaucoup d'items s'appliquent ou peuvent être installés sur d'autres Unices ou macOS (ou même Cygwin).
- L'accent est mis sur l'utilisation intéractive de Bash, bien que de nombreuses astuces s'appliquent aux autres shells et à l'écriture de scripts en Bash.
- Il inclut les commandes « standard » d'Unix aussi bien que celles qui nécessitent l'installation de paquets spéciaux &mdash; tant qu'ils sont suffisamment importants pour mériter d'être mentionnés.

Remarques :

- Afin que le guide tienne sur une seule page, du contenu est implicitement inclus par référence.
Vous êtes suffisamment intelligents pour rechercher des renseignements ailleurs une fois que vous avez l'idée ou la commande à googler.
Utilisez `apt`, `yum`, `dnf`, `pacman`, `pip` ou `brew` (selon votre distribution ou OS) pour installer de nouveaux programmes.
- Allez sur [Explainshell](http://explainshell.com) pour obtenir de l'aide à propos des commandes, options, tubes, etc.


## Notions de base

- Apprenez les bases de Bash.
En fait, tapez `man bash` et parcourez toute la page&#8239;; elle est relativement facile à suivre et pas si longue.
Les shells alternatifs peuvent être intéressants, mais Bash est puissant et disponible partout (apprendre *seulement* zsh, fish, etc., bien que cela soit tentant sur votre ordinateur portable, vous limite dans bien des situations, comme par exemple lors de l'utilisation de vrais serveurs).

- Apprenez à bien utiliser au moins un éditeur en mode texte.
L'éditeur `nano` est l'un des plus simples pour de l'édition simple (ouvrir, modifier, sauvegarder, rechercher).
Cependant pour un usage avancé dans un terminal, rien ne remplace le vénérable Vim (`vi`), éditeur difficile à prendre en main, mais rapide et très complet.
De nombreuses personnes utilisent également le classique Emacs, surtout pour d'importantes tâches d'édition (bien sûr, tout développeur moderne de logiciels travaillant sur un vaste projet n'utilise probablement pas un simple éditeur en mode texte et devrait donc aussi se familiariser avec des outils et des EDI graphiques modernes).

- Sachez comment lire une documentation avec `man` (pour les curieux, `man man` liste les sections avec leur numéro, par exemple 1 pour les commandes «&nbsp;normales&nbsp;» , 5 pour les formats des fichiers et les conventions, et 8 pour tout ce qui concerne l'administration système).
Trouvez les pages de manuel avec `apropos`.
Sachez que certaines commandes ne sont pas des exécutables, mais des commandes internes de Bash et que vous pouvez obtenir de l'aide à leur sujet avec `help` et `help -d`.
Utilisez `type command` pour déterminer si une commande est un exécutable, une commande interne du shell ou un alias.

- Apprenez à rediriger les entrées et sorties au moyen de `>` et `<`, et à créer des tubes avec `|`.
Sachez que `>` écrase le fichier de sortie et `>>` sert à ajouter.
Renseignez-vous sur stdout et stderr.

- Apprenez au sujet de l'expansion des noms de fichiers avec `*` (et peut-être `?` et `[`...`]`), des mécanismes de citation, et de la différence entre les guillemets `"` et les apostrophes `'` (voir ci-dessous).

- Familiarisez-vous avec la gestion des processus avec Bash&nbsp;: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, etc.

- Apprenez `ssh` et les principes de l'authentification sans mot de passe à l'aide de `ssh-agent`, `ssh-add`, etc.

- Les bases de la gestion des fichiers&nbsp;: `ls` et `ls -l` (en particulier, apprenez la signification de chacune des colonnes de `ls -l`), `less`, `head`, `tail` et `tail -f` (ou mieux, `less +F`), `ln` et `ln -s` (apprenez les différences et les avantages des liens durs par rapport aux liens symboliques), `chown`, `chmod`, `du` (pour un rapide résumé de l'espace disque occupé&nbsp;: `du -hs *`).
Pour la gestion du système de fichiers&nbsp;: `df`, `mount`, `fdisk`, `mkfs`, `lsblk`.
Apprenez ce qu'est un inode (`ls -i` ou `df -i`).

- Les bases de l'administration réseau&nbsp;: `ip`, `ifconfig`, `dig`, `traceroute` et `route`.

- Apprenez à vous servir d'un logiciel de gestion de versions tel que `git`, et utilisez-le.

- Apprenez les expressions régulières et les différents drapeaux de `grep` et `egrep`.
Les options `-i`, `-o`, `-v`, `-A`, `-B` et `-C` sont bonnes à connaître.

- Apprenez à utiliser `apt-get`, `yum`, `dnf` ou `pacman` (selon la distribution) pour trouver et installer des paquets.
Assurez-vous d'avoir `pip` pour installer des outils en ligne de commande écrits en Python (quelques-uns ci-dessous sont plus faciles à installer avec `pip`).


## Utilisation quotidienne

- En Bash, utilisez **Tab** pour compléter les arguments ou lister toutes les commandes disponibles, et **ctrl-r** pour rechercher dans l'historique des commandes (tapez pour rechercher, appuyez sur **ctrl-r** plusieurs fois pour parcourir les différentes correspondances, appuyez sur **Enter** pour exécuter la commande trouvée ou sur la flèche droite pour l'éditer).

- En Bash, utilisez **ctrl-w** pour effacer le mot précédent et **ctrl-u** pour effacer tout ce qui précède le curseur.
Utilisez **alt-b** et **alt-f** pour se déplacer mot par mot, **ctrl-a** pour déplacer le curseur au début de la ligne, **ctrl-e** pour déplacer le curseur à la fin de la ligne, **ctrl-k** pour effacer depuis le curseur jusqu'à la fin de la ligne, **ctrl-l** pour effacer l'écran.
Voir `man readline` pour la liste des raccourcis clavier par défault de Bash.
Il y en a beaucoup.
Par exemple **alt-.** fait défiler les arguments précédents et **alt-*** développe un glob.

- Sinon, si vous adorez les combinaisons de touches dans le style vi, utilisez `set -o vi` (`set -o emacs` pour revenir en arrière).

- Pour éditer de longues commandes, après avoir configuré votre éditeur (par exemple `export EDITOR=vim`), **ctrl-x** **ctrl-e** (**escape-v** dans le style vi) ouvre l'éditeur pour éditer la commande courante.

- Consultez les commandes récentes avec `history`.
Faites `!n` pour rappeler la commande numéro `n`.
Il y a aussi beaucoup d'autres abréviations, les plus utiles étant probalement `!$` pour le dernier argument et `!!` pour la dernière commande (voir la section « HISTORY EXPANSION » de la page de manuel).
Cependant, celles-ci peuvent être aisément remplacées par **ctrl-r** et **alt-.**.

- Placez-vous dans votre répertoire personnel avec `cd`.
Accédez aux fichiers à partir de leurs chemins relatifs par rapport à votre répertoire personnel en préfixant ceux-ci avec `~` (p.&nbsp;ex. `~/.bashrc`).
Dans les scripts shell, désignez le répertoire personnel par `$HOME`.

- Pour revenir au répertoire de travail précédent&nbsp;: `cd -`.

- Si vous êtes au milieu de la saisie d'une commande mais que vous changez d'avis, tapez **alt-#** pour ajouter `#` au début de la ligne et l'entrer comme un commentaire (ou utilisez **ctrl-a**, **#**, **enter**).
Vous pouvez alors y revenir plus tard à l'aide de la commande history.

- Utilisez `xargs` (ou `parallel`).
C'est très puissant.
Remarquez que vous pouvez contrôler le nombre d'items à exécuter par ligne (`-L`) ainsi que la parallélisation (`-P`).
Si vous n'êtes pas sûr d'avoir fait ce qu'il faut, utilisez d'abord `xargs echo`.
L'option `-I{}` est également pratique.
Exemples&nbsp;:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` fournit un affichage utile des processus sous la forme d'un arbre.

- `pgrep` et `pkill` pour rechercher ou envoyer un signal à des processus en fonction de leur nom (`-f` est utile).

- Connaissez les différents signaux que vous pouvez envoyer aux processus.
Par exemple, pour suspendre l'exécution d'un processus, utilisez `kill -STOP [pid]`.
Pour la liste complète, consultez `man 7 signal`.

- Utilisez `nohup` ou `disown` pour qu'un processus en arrière-plan reste actif indéfiniment.

- Vérifiez quels sont les processus qui écoutent à l'aide de `netstat -lntp`, `ss -plat` (pour TCP; ajoutez `-u` pour UDP) ou `lsof -iTCP -sTCP:LISTEN -P -n` (qui fonctionne aussi sur macOS). 

- Voyez également `lsof` et `fuser` pour la liste des *sockets* et fichiers ouverts.

- Voyez `uptime` ou `w` pour savoir depuis combien de temps le système fonctionne.

- Utilisez `alias` pour créer des raccourcis vers les commandes fréquemment utilisées.
Par exemple, `alias ll='ls -latr'` crée un nouvel alias `ll`.

- Conservez les aliases, les paramètres du shell et les fonctions fréquemment utilisées dans le fichier `~/.bashrc`, et [arrangez-vous pour qu'il soit chargé par le shell de connexion](http://superuser.com/a/183980/7106).
Ainsi, votre configuration s'appliquera à toutes vos sessions shell.

- Placez dans `~/.bash_profile` la configuration de vos variables d'environnement ainsi que les commandes à exécuter lorsque vous vous connectez.
Une configuration séparée est nécessaire lorsque vous vous connectez depuis un gestionnaire de connexion graphique et pour les tâches planifiées par `cron`.

- Synchronisez vos fichiers de configuration (p.&nbsp;ex. `.bashrc` et `.bash_profile`) entre plusieurs ordinateurs avec Git.

- Comprennez qu'il convient d'être prudent lorsque des variables et des noms de fichiers contiennent des espaces.
Mettez vos variables entre guillemets, par exemple `"$FOO"`.
Préférez les options `-0` ou `-print0` qui permettent de délimiter les noms des fichiers avec le caractère nul, par exemple `locate -0 pattern | xargs -0 ls -al` ou `find / -print0 -type d | xargs -0 ls -al`.
Pour itérer sur des noms de fichiers contenant des espaces dans une boucle for, positionnez la variable IFS avec le caractère de retour à la ligne à l'aide de `IFS=$'\n'`.

- Dans les scripts Bash, utilisez `set -x` (ou la variante `set -v` qui enregistre les entrées brutes, y compris les variables non référencées et les commentaires) pour l'affichage d'informations de débogage.
Utilisez les modes stricts à moins que vous ayez une bonne raison de ne pas le faire&nbsp;: utilisez `set -e` pour interrompre le script en cas d'erreur (code de sortie non nul).
Utilisez `set -u` pour détecter l'utilisation d'une variable non initialisée.
Envisagez aussi `set -o pipefail` pour détecter les erreurs dans les tubes (cependant lisez-en plus si vous l'utilisez car ce sujet est un peu délicat).
Pour des scripts plus compliqués, servez-vous également de `trap` pour intercepter EXIT ou ERR.
Une bonne habitude est de commencer un script comme cela, ce qui lui permettra de détecter les erreurs courantes, de s'interrompre et d'afficher un message&nbsp;:
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- Dans les scripts en Bash, les sous-shells (placés entre parenthèses) sont commodes pour grouper des commandes.
Un exemple classique consiste à se déplacer temporairement dans un autre répertoire de travail&nbsp;:
```bash
      # faire quelque chose dans le répertoire courant
      (cd /some/other/dir && other-command)
      # continue dans le répertoire original
```

- Notez qu'en Bash, il existe de nombreux types d'expansions de variables. Pour vérifier l'existence d'une variable&nbsp;: `${name:?error message}`.
Par exemple, si un script en Bash exige un unique argument, il suffit d'écrire `input_file=${1:?usage: $0 input_file}`.
Pour utiliser une valeur par défaut si une variable est vide&nbsp;: `${name:-default}`.
Si vous souhaitez ajouter un paramètre supplémentaire facultatif dans l'exemple précédent, vous pouvez écrire quelque chose comme `output_file=${2:-logfile}`.
Si `$2` est omis et donc vide, `output_file` prendra la valeur `logfile`.
L'évaluation arithmétique&nbsp;: `i=$(( (i+1) % 5)`.
Les listes d'entiers&nbsp;: `{1..10}`
Suppression de préfixes et de suffixes&nbsp;: `${var%suffix}` et `${var#prefix}`.
Par exemple, si `var=foo.pdf`, alors `echo ${var%.pdf}.txt` affiche `foo.txt`.

- L'expansion des accolades avec `{`...`}` évite de retaper des textes similaires et automatise les combinaisons d'éléments de listes.
C'est utile dans des exemples comme  `mv foo.{txt,pdf} some-dir` (qui déplace les deux fichiers), `cp somefile{,.bak}` (équivalent à `cp somefile somefile.bak`) ou `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (qui engendre toutes les combinaisons possibles et crée une arborescence de répertoires).
L'expansion des accolades est effectuée avant toutes les autres expansions.

- Les expansions sont exécutées dans l'ordre suivant&nbsp;: expansion des accolades, développement du tilde, remplacement des paramètres et des variables, évaluation arithmétique, substitution de commande (de la gauche vers la droite), découpage en mots, puis développement des chemins. 
Par exemple, une liste telle que `{1..20}` ne peut s'exprimer avec des variables en utilisant `{$a..$b}`.
À la place, utilisez `seq` ou une boucle `for`&nbsp;; par exemple, `seq $a $b` ou `for((i=a; i<=b; i++)); do ...; done`.

- La sortie d'une commande peut être traitée comme un fichier à l'aide de `<(some command)` (substitution de processus).
Par exemple, pour comparer le fichier local `/etc/hosts` avec un fichier distant&nbsp;:
```sh
      diff /etc/hosts/ <(ssh somehost cat /etc/hosts)
```

- Lorsque vous écrivez des scripts, vous pourriez avoir envie de placer votre code entre accolades.
S'il manque l'accolade fermante, les scripts ne pourront s'exécuter à cause d'une erreur de syntaxe.
C'est particulièrement utile pour des scripts mis à disposition sur le web, afin de prévenir leur exécution lorsqu'ils sont partiellement téléchargés.
```bash
{
    # Votre code ici
}
```

- Un «&nbsp;document intégré&nbsp;» permet de [rediriger plusieurs lignes en entrée](https://abs.traduc.org/abs-fr/ch19.html) comme si elles provenaient d'un fichier&nbsp;:
```
cat <<EOF
entrée sur
plusieurs lignes
EOF
```

- En Bash, redirigez à la fois la sortie standard et la sortie des erreurs à l'aide de `some-command > logfile 2>&1` ou `some-command &>logfile`.
Souvent, pour s'assurer qu'une commande ne laisse pas un descripteur de fichier ouvert sur l'entrée standard, l'attachant au terminal dans lequel vous vous trouvez, une bonne pratique consiste à ajouter `</dev/null`.

- Utilisez `man ascii` pour une bonne table ASCII avec les valeurs décimales et hexadécimales.
Pour des informations générales sur l'encodage, `man unicode`, `man utf-8` et `man latin1` sont utiles.

- Utilisez `screen` ou [`tmux`](https://tmux.github.io/) pour multiplexer une fenêtre de terminal, particulièrement utile pour des sessions SSH distantes, et pour détacher et rattacher une session.
`byobu` peut améliorer screen ou tmux en fournissant plus d'informations et une gestion plus facile.
Une alternative plus légère pour la persistance des sessions seulement est [`dtach`](https://github.com/bogner/dtach/).

- Il est utile de savoir comment créer un tunnel SSH avec `-L` ou `-D` (et occasionnellement `-R`), par exemple pour accéder à des sites web à partir d'un serveur distant.

- Il peut être intéressant d'effectuer quelques optimisations à votre configuration de ssh&#8239;; par exemple, le fichier `~/.ssh/config` contient des paramètres pour éviter les pertes de connexion dans certains environnements réseaux, pour utiliser la compression (ce qui est utile avec scp sur des connexions à faible bande passante), et pour le multiplexage de canaux vers le même serveur avec un fichier de contrôle local&nbsp;:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Quelques autres options relatives à ssh sont sensibles pour la sécurité et ne devraient être activées qu'avec la plus grande prudence. Par exemple, sur des sous-réseaux, des hôtes ou des réseaux sûrs&nbsp;: `StrictHostKeyChecking=no`, `ForwardAgent=yes`.

- Envisagez [`mosh`](https://mosh.mit.edu/) comme une alternative à ssh qui utilise UDP, évitant ainsi les pertes de connexion et ajoutant du confort en situation de mobilité (exige une installation côté serveur).

- Pour obtenir les permissions d'un fichier en octal, utile pour configurer le système mais non fournit par `ls`, utilisez quelque chose comme
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Pour une sélection intéractive de valeurs issues de la sortie d'une commande, utilisez [`percol`](https://github.com/mooz/percol) ou [`fzf`](https://github.com/junegunn/fzf).

- Pour intéragir avec les fichiers provenant de la sortie d'une commande (p.&nbsp;ex. `git`), utilisez `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).


- Créez un simple serveur web pour partager les fichiers du répertoire courant (et ses sous-répertoires) avec `python -m SimpleHTTPServer 7777` (port 7777 et Python 2)  et `python -m http.server 7777` (port 7777 et Python 3).

- Pour exécuter une commande avec les privilèges d'un autre utilisateur, utilisez `sudo`.
Par défaut, cet autre utilisateur est *root*&#8239;; utilisez `-u` pour spécifier un autre utilisateur.
Utilisez `-i` pour ouvrir une session en tant que cet autre utilisateur (on vous demandera *votre* mot de passe).

- Pour basculer le shell sous un autre utilisateur, utilisez `su username` ou `su - username`.
Incluez `-` pour obtenir le même environnement que lorsque cet utilisateur se connecte.
Le nom d'utilisateur par défaut est *root*.
Le système vous demandera le mot de passe *de l'utilisateur cible*.

- Sachez que l'argument de la ligne de commande a une [taille limite de 128 Kio](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong). L'erreur « Argument list too long » est fréquente avec les jokers qui reconnaissent un grand nombre de fichiers (quand cela se produit des alternatives comme `find` et `xargs` peuvent aider).

- Pour une calculatrice basique (et bien sûr accéder à Python en général), utilisez l'interpréteur `python`.
Par exemple,
```
>>> 2+3
5
```

## Traitement des fichiers et des données

- Pour localiser un fichier par son nom dans le répertoire courant, `find . -iname '*something*'` (ou autres).
Pour trouver un fichier n'importe où par son nom, utilisez `locate something` (mais n'oubliez pas que `updatedb` peut ne pas avoir indexé les fichiers récemment créés).

- Pour effectuer une recherche parmi des fichiers sources ou des fichiers de données, il existe des alternatives plus avancées ou plus rapides que `grep -r`, parmi lesquels (en gros du plus ancien au plus récent) [`ack`](https://github.com/beyondgrep/ack2), [`ag`](https://github.com/ggreer/the_silver_searcher) (« *the silver searcher* ») et [`rg`](https://github.com/BurntSushi/ripgrep) (ripgrep).

- Pour convertir du HTML en texte brut : `lynx -dump -stdin`.

- Pour convertir du Markdown, du HTML et toutes sortes de formats texte, essayez [`pandoc`](http://pandoc.org).
Par exemple, pour convertir un document Markdown au format Word : `pandoc README.md --from markdown --to docx -o temp.docx`

- Si vous devez manipuler du XML, l'ancien `xmlstarlet` marche bien.

- Pour le JSON, utilisez [`jq`](http://stedolan.github.io/jq/).
Voir également [`jid`](https://github.com/simeji/jid) and [`jiq`](https://github.com/fiatjaf/jiq) pour une utilisation intéractive.

- Pour le YAML, utilisez [`shyaml`](https://github.com/0k/shyaml).

- Pour les fichiers Excel ou CSV, [csvkit](https://github.com/onyxfish/csvkit) fournit `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, etc.

- Pour Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) est pratique et [`s4cmd`](https://github.com/bloomreach/s4cmd) est plus rapide.
L'outil d'Amazon [`aws`](https://github.com/aws/aws-cli) et la version améliorée [`saws`](https://github.com/donnemartin/saws) sont indispensables pour les autres tâches liées à AWS.

- Connaissez `sort` et `uniq`, y compris les options `-u` et `-d` de `uniq` (voir les unilignes plus bas). Voir aussi `comm`.

- Sachez utiliser `cut`, `paste` et `join` pour manipuler les fichiers texte.
Beaucoup de personnes utilisent `cut` mais oublient `join`.

- Connaissez `wc` pour compter les lignes (`-l`), les caractères (`-m`), les mots (`-w`) et les octets (`-c`).

- Connaissez `tee` pour copier depuis stdin vers un fichier ou vers stdout, comme dans `ls -al | tee file.txt`.

- Pour des calculs plus complexes, incluant les regroupements, les inversions de champs et des calculs statistiques, considérez [`datamash`](https://www.gnu.org/software/datamash/).

- Sachez que la locale affecte de nombreux outils en ligne de commande de manière subtile, comme l'ordre pour les tris (collation) et les performances.
La plupart des installateurs Linux définissent la variable `LANG` ou d'autres variables locales d'environnement pour configurer une locale telle que US English.
Mais ayez à l'esprit que le tri sera modifié si vous changez la locale.
Et sachez que les routines i18n peuvent rendre les opérations de tri et d'autres commandes *beaucoup* plus lentes.
Dans certains cas (tels que les opérations concernant les ensembles et l'unicité abordées ci-dessous) vous pouvez, sans risque, ignorer complètement les lentes routines i18n et utiliser l'ordre de tri classique fondé sur les valeurs des octets à l'aide de `export LC_ALL=C`.

- Vous pouvez modifier l'environnement d'une commande particulière en préfixant son invocation par l'affectation de variables, comme dans `TZ=Pacific/Fiji date`.

- Apprenez `awk` et `sed` pour de l'analyse de données élémentaire.
Voir la section [Unilignes](#unilignes) pour des exemples.

Par exemple, pour effectuer la somme de tous les nombres de la troisième colonne d'un fichier texte&nbsp;: `awk '{ x += $3 } END { print x}'`.
C'est probablement trois fois plus rapide et trois fois plus petit que son équivalent en Python.

- Pour remplacer toutes les occurences d'une chaîne de caractères dans un ou plusieurs fichiers&nbsp;:
```sh
    perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- Pour renommer de multiple fichiers ou effectuer des recherches et des remplacements dans des fichiers, essayez [`repren`](https://github.com/jlevy/repren) (dans certains cas la commande `rename` permet aussi de renommer de multiples fichiers, mais soyez prudent car ses fonctionnalités ne sont pas les mêmes sur toutes les distributions Linux).
```sh
    # Renomme les répertoires, les fichiers et leurs contenus à l'aide
    # de la substitution foo -> bar :
    repren --full --preserve-case --from foo --to bar .
    # Restaure des fichiers de sauvegarde à l'aide de la
    # substitution whatever.bak -> whatever :
    # Même chose que ci-dessus avec rename s'il est disponible :
    rename 's/\.bak$//' *.bak
```

- Selon sa page de manuel, `rsync` est un outil de duplication de fichiers vraiment rapide et incroyablement polyvalent.
Il est connu pour faire de la synchronisation entre machines, mais est également utile pour un usage local.
Lorsque les mesures de sécurité l'autorisent, utiliser `rsync` au lieu de `scp` permet de reprendre un transfert interrompu sans devoir le recommencer zéro.
Il est aussi l'un des outils [les plus rapides](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) pour effacer un grand nombre de fichiers&nbsp;:
```sh
    mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Pour surveiller l'état d'avancement d'une copie de fichiers, utilisez [`pv`](http://www.ivarch.com/programs/pv.shtml), [`pycp`](https://github.com/dmerejkowsky/pycp), [`pmonitor`](https://github.com/dspinellis/pmonitor), [`progress`](https://github.com/Xfennec/progress), `rsync --progress`, ou `dd status=progress` dans le cas d'une copie par blocs.

- Utilisez `shuf` pour mélanger ou sélectionner aléatoirement des lignes d'un fichier.

- Sachez les options de `sort`.
Pour les nombres, utilisez `-n`, ou `-h` s'ils sont dans un format lisible par un humain (p.&nbsp;ex. issus de `du -h`).
Comprenez le fonctionnement des clés (`-t` et `-k`).
En particulier, faites attention à bien écrire `-k1,1` pour trier seulement selon le premier champ&nbsp;: `-k1` signifie que l'on trie selon la ligne entière.
Le tri stable (`sort -s`) peut s'avérer utile.
Par exemple, pour trier d'abord selon le champ 2, puis selon le champ 1, vous pouvez utiliser `sort -k1,1 | sort -s -k2,2`.

- Si jamais vous avez besoin d'écrire un caractère de tabulation dans une ligne de commande en Bash (p.&nbsp;ex pour le paramètre de l'option de tri `-t`), entrez **ctrl-v** **[Tab]** ou écrivez `$'\t'` (préférable car vous pouvez le copier-coller).

- Les outils habituels pour *patcher* un code source sont `diff` et `patch`.
Voir aussi `diffstat` pour un relevé statistique d'un diff et `sdiff` pour un affichage côte à côte d'un diff.
Remarquez que `diff -r` marche avec des répertoires entiers.
Utilisez `diff -r tree1 tree2 | diffstat` pour obtenir un résumé des changements.
Utilisez `vimdiff` pour comparer et éditer des fichiers.

- Pour les fichiers binaires, utilisez `hd`, `hexdump` ou `xxd` pour un affichage simple en hexadécimal et `bvi`, `biew` pour éditer des fichiers binaires.

- Également pour les fichiers binaires, `strings` (ainsi que `grep`, etc) vous permet d'y trouver des bouts de texte.

- Pour effectuer des différences entre des fichiers binaires (compression différentielle), utilisez `xdelta3`.

- Pour changer l'encodage d'un texte, essayer `iconv`, ou `uconv` pour un usage plus avancée&nbsp;: il permet quelques trucs avancés avec l'Unicode.
Par exemple&nbsp;:
```sh
      # Affiche les codes hexadécimaux et les noms des caractères (utile pour déboguer) : 
      uconv -f utf-8 -t utf-8 -x '::Any-Hex;' < input.txt
      uconv -f utf-8 -t utf-8 -x '::Any-Name;' < input.txt
      # Convertit en minuscule et supprime les accents :
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; 
      ::Any-NFC;' < input.txt > output.txt
```

- Pour découper des fichiers en morceaux, regardez `split` pour un découpage en morceaux de taille donnée et `csplit` pour un découpage en morceaux délimités par un motif.

- Date et heure&nbsp;: pour obtenir la date et l'heure courantes au format [ISO 8601](https://fr.wikipedia.org/wiki/ISO_8601), utilisez `date -u +"%Y-%m-%dT%H:%M:%SZ"` (d'autres options [sont](https://stackoverflow.cmm/questions/7216358/date-command-on-os-x-doesnt-have-iso-8601-i-option) [problématiques](https://unix.stackexchange.com/questions/164826/date-command-iso-8601-option)).
Pour manipuler des dates et des heures, utilisez `dateadd`, `datediff`, `strptime`, etc. fournis par [`dateutils`](http://www.fresse.org/dateutils/).

- Utilisez `zless`, `zmore`, `zcat` et `zgrep` pour travailler sur des fichiers compressés.

- Les attributs d'un fichier peuvent être modifiés avec `chattr` et proposent une alternative de plus bas niveau aux permissions d'accès aux fichiers.
Par exemple, l'attribut *immutable* protège un fichier contre toute suppression accidentelle: `sudo chattr +i /critical/directory/or/file`.

- Utilisez `getfacl` et `setfacl` pour sauvegarder et restorer les permissions. Par exemple:
```sh
    getfacl -R /some/path > permissions.txt
    setfacl --restore=permissions.txt
```

- Pour créer rapidement un fichier vide, utilisez `truncate` (crée un [fichier creux](https://en.wikipedia.org/wiki/Sparse_file)), `fallocate` (systèmes de fichiers ext4, XFS, Btrfs et OCFS2), `xfs_mkfile` (pour presque tous les systèmes de fichiers, disponible dans le paquet xfsprogs) ou `mkfile` (pour les systèmes de type Unix comme Solaris ou Mac OS X).

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

- Utilisez [`mtr`](http://www.bitwizard.nl/mtr/) comme un `traceroute` amélioré pour identifier les problèmes de réseau.

- Pour déterminer les raisons pour lesquelles un disque est plein, [`ncdu`](https://dev.yorhel.nl/ncdu) permet de gagner du temps par rapport aux commandes habituelles telles que `du -sh *`.

- Pour trouver quel socket ou processus utilise la bande passante, essayez [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) ou [`nethogs`](https://github.com/raboof/nethogs).

- L'outil `ab` (fourni avec Apache) est utile pour une vérification rapide et grossière des performances d'un serveur web.
Pour des tests de charge plus complexes, essayez `siege`.

- Pour du debogage réseau plus sérieux : [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) ou [`ngrep`](http://ngrep.sourceforge.net/).

- Sachez utiliser `strace` et `ltrace`.
Ces commandes peuvent être utiles si un programme fonctionne mal ou plante et que vous n'en connaissez pas la raison, ou si vous voulez vous faire une idée de ses performances.
Remarquez l'option de profilage (`-c`) et la possibilité de s'attacher à un processus en cours d'exécution (`-p`).
Utilisez l'option `-f` pour ne pas manquer les appels des processus enfants.

- Connaissez `ldd` pour afficher les bibliothèques partagées, mais [ne l'utilisez jamais sur des fichiers qui ne sont pas dignes de confiance](http://www.catonmat.net/blog/ldd-arbitrary-code-execution/).

- Sachez comment vous connecter à un processus en cours d'exécution avec `gdb` et récupérer la trace des appels.

- Utilisez `/proc`. C'est parfois incroyablement utile pour résoudre des problèmes en live.
Exemples&nbsp;: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd`, `/proc/xxx/smaps` (où `xxx` est l'identifiant du processus ou pid).

- Pour comprendre pourquoi quelque chose a mal tourné antérieurement, [`sar`](http://sebastien.godard.pagesperso-orange.fr/) peut-être très utile.
Il fournit un historique concernant l'usage du CPU, de la mémoire, du réseau, etc.

- Pour une analyse plus approfondie du système et de ses performances, regardez `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_%28Linux%29) et [`sysdig`](https://github.com/draios/sysdig).

- Vérifiez quel OS vous utilisez avec `uname` ou `uname -a` (information général sur la version d'Unix et du noyau) ou `lsb_release -a` (informations sur la distribution Linux).

- Utilisez `dmesg` à chaque fois que quelque chose de bizarre se produit (pour des problèmes liés au matériel ou aux drivers).

- Si vous effacez un fichier et que `du` indique que l'espace occupé n'a pas été libéré, alors vérifiez si le fichier n'est pas utilisé par un processus:
`lsof | grep deleted | grep "filename-of-my-big-file"`


## Unilignes

Quelques exemples d'assemblages de commandes&nbsp;:

- Il est quelques fois extrèmement utile de pouvoir faire une intersection, union ou différence ensemblistes de fichiers texte à l'aide de `sort` et `uniq`.
Supposez que `a` et `b` soient des fichiers texte ne contenant pas de lignes répétées.
C'est rapide et fonctionne sur des fichiers de taille quelconque jusqu'à plusieurs gigaoctets (le tri n'est pas limité par la capacité mémoire bien que vous puissiez avoir besoin d'utiliser l'option `-T` si `/tmp` est sur une petite partition racine).
Voyez aussi la remarque à propos de `LC_ALL` ci-dessus et l'option `-u` de `sort` (omise ci-dessous pour plus de clarté).
```sh
    sort a b | uniq > c   # c is a union b
    sort a b | uniq -d > c   # c is a intersect b
    sort a b b | uniq -u > c   # c is set difference a - b
```

- Utilisez `grep . *` pour inspecter rapidement les contenus des fichiers d'un repértoire (chaque ligne est précédé du nom du fichier) ou `head -100 *` (chaque fichier a un titre).
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
    egrep -o 'acct_id=[0-9]+' access.log | cut -d= -f2 | sort | uniq -c | sort -rn
```

- Pour surveiller en permanence tout changement, utilisez `watch`, par exemple vérifiez les modifications dans les fichiers d'un répertoire avec `watch -d -n 2 'ls -rtlh | tail'` ou surveillez les paramètres de votre réseau tout en dépannant la configuration de votre wifi avec `watch -d -n 2 ifconfig`.

- Exécutez cette fonction pour afficher aléatoirement une astuce de ce guide (analyse le code en Markdown et en extrait un élément d'une des listes)&nbsp;:
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

- `pr` : formate un texte en pages ou en colonnes.

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

- [`when-changed`](https://github.com/joh/when-changed) : exécute n'importe quelle commande donnée à chaque fois qu'un fichier est modifié. Voir également `inotifywait` et `entr`. 

- `tac` : affiche des fichiers à l'envers.

- `comm` : compare ligne à ligne deux fichiers triés.

- `strings` : extrait du texte de fichiers binaires.

- `tr` : conversion et manipulation de caractères.

- `iconv` ou `uconv` : conversion entre différents encodages de caractères.

- `split` et `csplit` : découpage de fichiers.

- `sponge` : lit entièrement un flux d'entrée avant de l'écrire. Utile pour lire depuis un fichier puis écrire dans le même fichier, par exemple&nbsp;: `grep -v something some-file | sponge some-file`

- `units` : conversions d'unités et calculs. Convertit des furlongs par fortnight en twips par blink (voir aussi `/usr/share/units/deifinitions.units`).

- `apg` : génère des mots de passe aléatoires.

- `xz` : compresse des fichiers avec taux de compression élevé.

- `ldd` : affiche des informations sur les bibliothèques partagées.

- `nm` : affiche les symboles des fichiers objets.

- `ab` ou [`wrk`](https://github.com/wg/wrk) : mesure les performances de serveurs web.

- `strace`: trace les appels système.

- [`mtr`](http://www.bitwizard.nl/mtr/): un traceroute amélioré pour débugguer un réseau.

- `cssh` : visual concurrent shell

- `rsync` : synchronise des fichiers et des dossiers via SSH ou localement.

- [`wireshark`](https://wireshark.org/) et [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): capture de paquets et dépannage réseau.

- [`ngrep`](http://ngrep.sourceforge.net/) : grep pour les couches réseaux.

- `host` et `dig`: interroge les serveurs DNS.

- `lsof` : process file descriptor and socket info.

- `dstat` : statistiques sur les ressources système.

- [`glances`](https://github.com/nicolargo/glances): aperçu de haut niveau et multi-systèmes.

- `iostat` : statistiques sur l'usage du disque.

- `mpstat` : statistiques sur l'usage du CPU.

- `vmstat` : statistiques sur l'usage de la mémoire.

- `htop` : version améliorée de top.

- `last` : historique des connexions.

- `w` : montre qui est connecté.

- `id` : affiche les informations sur un utilisateur et ses groupes.

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/) : statistiques sur l'activité du système

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) ou [`nethogs`](https://github.com/raboof/nethogs) : utilisation du réseau par un socket ou un processus.

- `ss` : statistiques relatives aux sockets.

- `dmesg` : messages lors du démarrage et erreurs système.

- `sysctl` : visualise et configure les paramètres du noyau Linux à chaud.

- `hdparm` : manipulation et performances d'un disque SATA ou ATA.

- `lsblk` : affiche les périphériques blocs (une arborescence de vos disques et de leurs partitions).

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode` : informations sur le matériel, comprenant le CPU, le BIOS, le RAID, la carte graphique, les périphériques, etc.

- `lsmod` et `modinfo` : liste les modules du noyau et donne des informations sur un module.

- `fortune`, `ddate` et `sl` : euh, bon, seulement si vous estimez que les locomotives à vapeur et les citations de Jean-Claude Van Damme sont « utiles ».


## Uniquement macOS

Ce qui suit ne s'applique *qu'*à macOS.

- Gestion des paquets avec `brew` (Homebrew) ou `port` (MacPorts).
Ceux-ci peuvent être utilisés pour installer sur macOS la plupart des commandes mentionnées ci-dessus.

- Copier la sortie de n'importe quelle commande dans une application de bureau avec `pbcopy` et coller l'entrée d'une commande avec `pbpaste`.

- Pour permettre à la touche Option de fonctionner comme la touche Alt dans le terminal de macOS (comme dans les commandes **alt-b**, **alt-f**, etc), allez dans Préférences -> Profils -> Clavier et sélectionner « Choisir la touche Option comme touche virtuelle ».

- Pour ouvrir un fichier avec une application de bureau, utilisez `open` ou `open -a /Applications/Whatever.app`.

- Spotlight&nbsp;: recherche de fichiers avec `mdfind` et affichage des métadonnées (telles que les informations EXIF d'une photo) avec `mdls`.

- Ayez à l'esprit que macOS dérive du système Unix BSD et que beaucoup de commandes (par exemple `ps`, `ls`, `tail`, `awk`, `sed`) présentent de légères différences avec leurs versions pour Linux, qui lui est largement influencé par System V et les outils GNU.
Vous pouvez souvent faire la distinction grâce à l'en-tête « BSD General Commands Manual » dans les pages de manuel.
Dans certains cas, les versions GNU peuvent également être installées (telles que `gawk` et `gsed` pour GNU awk et GNU sed).
Pour écrire des scripts Bash multi-plateformes évitez d'utiliser de telles commandes (par exemple, envisagez d'utiliser Python ou Perl) ou alors testez-les soigneusement.

- Pour obtenir des informations sur la version de macOS, utilisez `sw_vers`.


## Uniquement Windows

Ce qui suit ne concerne que Windows.

### Différentes manières d'obtenir les outils Unix sous Windows

- Installez [Cygwin](http://cygwin.com) pour bénéficier de la puissance du shell Unix sous Microsoft Windows.
La majorité de ce qui est décrit dans ce document fonctionnera *out of the box*.

- Sous Windows 10, [Windows Subsystem for Linux (WSL)](https://msdn.microsoft.com/commandline/wsl/about) fournit un environnement Bash avec les utilitaires en ligne de commandes d'Unix.

- Si vous êtes surtout intéressés par les outils de developpement GNU (comme GCC) sur Windows, jetez un œil à [MinGW](http://www.mingw.org/) et à son package [MSYS](http://www.mingw.org/wiki/msys) qui fournit des utilitaires tels que bash, gawk, make et grep.
MSYS ne dispose pas de toutes les fonctionnalités de Cygwin.
MinGW est particulièrement utile pour porter sous Windows des outils Unix.

- Une autre manière d'obtenir le *look and feel* d'Unix sous Windows est d'utiliser [Cash](https://github.com/dthree/cash).
Notez que très peu de commandes Unix et d'options de ligne de commande sont disponibles dans cet environnement.

### Outils en ligne de commande utiles pour Windows

- Vous pouvez accomplir et scripter la plupart des tâches d'administration système de Windows depuis la ligne de commande à l'aide de `wmic`.

- Parmi les outils réseaux en ligne de commande nativement disponibles sous windows que vous devriez trouver utiles, on trouve `ping`, `ipconfig`, `tracert` et `netstat`.

- Vous pouvez effectuer [de nombreuses tâches sous Windows](http://www.thewindowsclub.com/rundll32-shortcut-commands-windows) en invoquant la commande `Rundll32`.

### Trucs et astuces à propos de Cygwin

- Installez des programmes Unix supplémentaires à l'aide du gestionnaire de paquets de Cygwin.

- Utilisez `mintty` comme fenêtre de ligne de commande.

- Accédez au presse-papier de Windows par `/dev/clipboard`.

- Exécutez `cygstart` pour ouvrir un fichier quelconque avec l'application associée.

- Accédez à la base de registres de Windows avec `regtool`.

- Sachez qu'on accède au lecteur `C:\` depuis Cygwin via `/cygdrive/c` et que le chemin Cygwin `\` devient `C:\cygwin` sous Windows.
Effectuez des conversions entre les deux types de chemin avec l'utilitaire `cygpath`.
C'est particulièrement utile pour invoquer des programmes Windows dans les scripts.

## Autres ressources

- [awesome-shell](https://github.com/alebcay/awesome-shell)&nbsp;: une liste organisée d'outils et de ressources pour le shell.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line)&nbsp;: un guide plus approfondi sur la ligne de commande pour macOS.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/)&nbsp;: pour écrire de meilleurs scripts shell.
- [shellcheck](https://github.com/koalaman/shellcheck)&nbsp;: un outil d'analyse statique des scripts shell. L'équivalent de lint pour bash, sh et zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html)&nbsp;: les points de détail, malheureusement compliqués, sur la manière de manipuler correctement les noms de fichiers dans les scripts shell.
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools)&nbsp;: d'autres outils en ligne de commande, utiles en science des données et discutés dans le livre du même nom.

## Avertissement

À l'exception des très petites tâches, le code est écrit de sorte que d'autres personnes puissent le lire.
Il n'y a pas de pouvoir sans responsabilité : le fait que vous *puissiez* faire quelque chose en Bash ne signifie pas nécessairement que vous devriez le faire ! ;)


## Licence

[![Licence Creative Commons](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

Ce document est mis à disposition selon les termes de la [Licence Creative Commons Attribution - Partage dans les mêmes conditions 4.0 International](http://creativecommons.org/licenses/by-sa/4.0/).
