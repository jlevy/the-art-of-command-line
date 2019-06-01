🌍
* [Çekçe] (README-cs.md) ∙ [Almanca] (README-de.md) ∙ [Yunanca] (README-el.md) ∙ [İngilizce] (README.md) ∙ [İspanyolca] (README-es .md) ∙ [Fransızca] (README-fr.md) ∙ [Endonezce] (README-id.md) ∙ [İtalyanca] (README-it.md) ∙ [Japonca] (README-ja.md) ∙ [Korece] (README-ko.md) ∙ [Portekizce] (README-pt.md) ∙ [Romence] (README-ro.md) ∙ [Rusça] (README-ru.md) ∙ [Slovence] (README-sl) .md) ∙ [Türkçe] (README-tr.md) ∙ [Ukraynaca] (README-uk.md) ∙ [Çince] (README-zh.md) ∙ [Klasik Çince] (README-zh-Hant.md ) *


# Komut Satırı Sanatı

* Not: Bunu daha kapsamlı bir kılavuza genişletmek için yeni (ve potansiyel olarak ücret ile) bir lider yazar arıyorum. Çok kalabalık olsa da, hem daha derin hem de daha yararlı olabilir. Yazmayı seviyorsanız ve bu materyal konusunda uzman olmak ve yardım etmeyi düşünmek istiyorsanız, lütfen bana josh (0x40) holloway.com adresinden bir not bırakın. - [Jlevy] (https://github.com/jlevy), [Holloway] (https://www.holloway.com) *

- [Meta] (# meta)
- [Temel bilgiler] (# temel bilgiler)
- [Günlük kullanım] (# günlük kullanım)
- [Dosya ve veri işleme] (# işlem dosya ve veri)
- [Sistem hata ayıklama] (# sistem-hata ayıklama)
- [Bir gömlek] (# bir gömlek)
- [Karanlık ama kullanışlı] (# karanlık ama kullanışlı)
- [yalnızca macOS] (yalnızca # macos)
- [Yalnızca Windows] (yalnızca # Windows)
- [Daha fazla kaynak] (# daha fazla kaynak)
- [Feragatname] (# sorumluluk reddi)


! [curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\ w +`' | tr -d '`' | cowsay -W50] (cowsay.png)

Komut satırındaki akıcılık, genellikle ihmal edilen veya gizemli olarak kabul edilen bir beceridir, ancak bir mühendis olarak esnekliğinizi ve üretkenliğinizi geliştirir. Linux'ta çalışırken yararlı bulduğumuz komut satırını kullanma hakkında notlar ve püf noktalardır. Bazı ipuçları temeldir ve bazıları oldukça özel, karmaşık veya belirsizdir. Bu sayfa çok uzun sürmüyor, ancak buradaki tüm öğeleri kullanabilirseniz, çok şey bilirsiniz.

Bu eser [birçok yazar ve çevirmenin] (AUTHORS.md) sonucudur.
Bunun birazı
[Başlangıçta] (http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[Ortaya] (http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
[Quora] 'da (http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
ancak o zamandan beri, orijinal yazardan daha yetenekli insanların sayısız gelişme kaydettiği GitHub'a taşındı.
Komut satırıyla ilgili bir sorunuz varsa, [** Lütfen soru gönderin **] (https://airtable.com/shrzMhx00YiIVAWJg). Eğer bir hata veya daha iyi olabilecek bir şey görürseniz![** Lütfen katkıda bulunun **] (/ CONTRIBUTING.md) 

## Meta

Kapsam:

- Bu rehber; hem yeni başlayanlar hem de deneyimli olanlar içindir. Hedefler * genişlik * (önemli olan her şey), * özgünlük * (en yaygın durumun somut örneklerini verir) ve * kısalık * (temelde olmayan şeylerden kaçınmak veya başka bir yere kolayca göz atabileceğin şeylerden kaçınmaktır). Her ipucu bazı durumlarda önemlidir veya alternatiflere göre zaman kazandırır.
- Bu rehber; "[yalnızca macOS] (yalnızca # macos)" ve "[yalnızca Windows] (# # yalnızca Windows)" bölümleri hariç olmak üzere Linux için yazılmıştır. Diğer öğelerin çoğu, diğer Unices veya macOS'lara (veya hatta Cygwin) uygulanabilir veya kurulabilir.
- Bash üzerine odaklı olsa da, birçok diğer kabukları ve genel Bash komut dosyası için de geçerlidir.
- Hem "standart" Unix komutlarını hem de özel paket kurulumları gerektiren komutları içerir - dahil edilmeyi hak edecek kadar önemli oldukları sürece.

Notlar:

- Bunu bir sayfada tutmak için içerik gizli olarak referansa dahil edilmiştir. Google’ın fikrini öğrendikten sonra başka bir yerde daha fazla ayrıntı arayacak kadar zekisin. Yeni programlar yüklemek için `apt`,` yum`, dnf`, pacman`, pip veya brew (uygun olanını) kullanın.
- Komutların, seçeneklerin vb. yaptıklarını ayrıntılı olarak öğrenmek için [Explainshell] (http://explainshell.com/) kullanabilirsin.


## Temel Bilgiler

- Temel Bash'i öğrenmelisin. Aslında, 'man bash' ile en azından gözatın; O kadar uzun değil ve takip etmek oldukça kolay. Alternatif kabuklar güzel olabilir, ancak Bash güçlüdür ve her zaman kullanılabilir durumdadır (yalnızca * öğrenme * zsh, fish, vb.), Kendi dizüstü bilgisayarınızı etkilerken, mevcut sunucuları kullanma gibi birçok durumda sizi kısıtlar).

- En az bir metin tabanlı düzenleyiciyi iyi öğrenin. `Nano` editörü, temel düzenleme (açılış, düzenleme, kaydetme, arama) için en basitlerinden biridir. Ancak, bir metin terminalindeki uzman kullanıcılar için, öğrenmesi zor fakat saygıdeğer, hızlı ve tam özellikli bir editör olan Vim (`vi`) yerine geçemez. Birçok insan, özellikle daha büyük düzenleme işleri için klasik Emac'ları kullanır. (Tabii ki, kapsamlı bir proje üzerinde çalışan herhangi bir modern yazılım geliştiricinin yalnızca saf bir metin tabanlı düzenleyici kullanması pek mümkün değildir ve aynı zamanda modern grafik IDE'ler ve araçlarla da aşina olmalıdır.)

- Belgeleri bulma:
  - “Man” ile resmi belgelerin nasıl okunacağını bilin (meraklı için, “man man” bölüm numaralarını listeler, örneğin 1 "normal" komutlar, 5 dosya / kurallar ve 8 yönetim içindir).
