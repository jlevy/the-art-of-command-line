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