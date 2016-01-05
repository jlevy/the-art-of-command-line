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

