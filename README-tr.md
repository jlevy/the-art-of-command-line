[ Diller:
[İngilizce](README.md), [İspanyolca](README-es.md), [İtalyanca](README-it.md), [Japonca](README-ja.md), [Korece](README-ko.md), [Portekizce](README-pt.md), [Rusça](README-ru.md), [Slovakça](README-sl.md), [Ukraynaca](README-uk.md), [Çince](README-zh.md)
]


# Komut İstemi Sanatı

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Meta](#meta)
- [Temeller](#temeller)
- [Gunluk Kullanim](#everyday-use)
- [Processing files and data](#processing-files-and-data)
- [System debugging](#system-debugging)
- [One-liners](#one-liners)
- [Obscure but useful](#obscure-but-useful)
- [MacOS X only](#macos-x-only)
- [More resources](#more-resources)
- [Disclaimer](#disclaimer)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

Fluency on the command line is a skill often neglected or considered arcane, but it improves your flexibility and productivity as an engineer in both obvious and subtle ways. This is a selection of notes and tips on using the command-line that we've found useful when working on Linux. Some tips are elementary, and some are fairly specific, sophisticated, or obscure. This page is not long, but if you can use and recall all the items here, you know a lot.

This work is the result of [many authors and translators](AUTHORS.md).
Much of this
[originally](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[appeared](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
on [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
but given the interest there, it seemed worth using GitHub, where people more talented than the original author could readily suggest improvements. If you see an error or something that could be better, please submit an issue or PR! (Of course please review the meta section and existing PRs/issues first.)


## Meta

Kapsam:

- Bu kılavuz hem başlangıç hem de profesyoneller içindir. Hedefler *geniş* (önemli herşey), *belirlilik* (yaygın kullanılan somut örnekler), and *özlülük* (konu dışı ve gerekli olmayan bilgilerden uzak durmak). Her ipuçu bazi durumlarda gerekli veya önemli ölçüde zaman kazandırır alternatif kaynaklarla karşılaştırdıgimizda.
- Bu kaynak Linux için yazilmistir, "[MacOS X only](#macos-x-only)" bölümü istisna. Diğer öğelerin çoğu Unice(Unix-gibi)'lerde veya MacOS (hatta Cygwin ) üzerinde aynıdır veya yüklenebilir.
- Etkileşimli Bash asıl hedef ancak çogu bilgi diger shell`lerde ve genel Bash scripting(komut dizisi oluşturma)`de aynıdır.
- "Standart" Unix komutlarını ve ozel paket program yüklemek gereken komutları içerir. --Yani onemli olan her sey dahil olmayi hak etmistir.

Notlar:

- Bir sayfayi gecmemek icin icerik dolayli olarak referans olarak verilmistir. Fikri ve komutu bildiginiz zaman daha detaylarini bakacak kadar zaten zekisiniz. (Uygun oldukca) Yeni program yuklemek icin su komutlari kullanin `apt-get`/`yum`/`dnf`/`pacman`/`pip`/`brew`.
- Komutlarin, seceneklerin veya veri yollarinin vs. ne yaptigi hakinda kullanisli bir analiz elde etmek icin [Explainshell](http://explainshell.com/)`i ziyaret edin.


## Temeller

- Temel Bashi ögren. Aslinda, `man bash` yaz ve en azindan hepsini hizla gozden gecir; cok uzun olmadigi gibi takip etmesi de kolay. Alternatif shelller guzel olabilir, ancak Bash güçlü ve kullanisli (*sadece* zsh, fish, etc.`i ogrenmek, kendi laptopunda deneyerek, bircok durumda kisitlayarak, mesela mevcut sunuculari kullanarak).

- En az 1 metin temelli metin düzenleyiciyi iyice ogrenin. Ideal olarak Vim (`vi`), aslinda terminal metin duzenleyicileri arasinda fazla bir rekabet yok (Emacs kullansaniz dahi, meshur bir IDE, veya yenilik iceren bir metin duzenleyici).

- Dökümantasyonlari `man` ile okumayi bilin (meraklı ve arastirmacilar icin, `man man` bolum numaralarini listeler, mesela 1 siradan komutlar, 5  dosyalar/uzlasilmis kullanislar, and 8 de admin icindir). Man sayfalarini `apropos` komutu ile bulun. Bazi komutlarin calistirilamaz oldugunu da bilin, ancak Bash oluşumiçler, ve `help` ve `help -d` yi kullanarak bu komutlar hakkinda da yardim alabileceginizi de.

- Cikis ve giris yönlendirmesi icin `>` ve `<` kullanmayi bilin ve veri yollarini da bilin  `|` \` kullanarak. `>` dosyanin uzerine yazar ve `>>` dosyaya ekler. stdout ve stderr de ogrenin.

- Genelleme yapmak icin `*` de kullanmayi bilin (ve bir ihtimalle `?` ve `[`...`]`) and  cift `"` ve tek `'` tirnak isareti arasindaki farki da bilin. (Degisken genellemesi hakkinda asagidan daha fazla bilgi alabilirsiniz.)

- Bash is veya gorev yonetimine da asina olun: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, vs.

- `ssh` i bilin, and ve sifresiz dogrulamanin temellerini de, `ssh-agent` veya `ssh-add`, etc. yoluyla.

- Temel dosya yonetimi : `ls` ve `ls -l` (ozellikle,  `ls -l` komutunda her sütunun anlamlarini bilin), `less`, `head`, `tail` ve `tail -f` (veya daha da iyisi, `less +F`), `ln` ve `ln -s` (hard link ve soft link arasindaki farki ve avantajlarini bilin), `chown`, `chmod`, `du` (hizli bir disk kullanimi ozeti icin: `du -hs *`). Dosya sistemi yonetimi icin, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`.inode  ne bilin (`ls -i` veya `df -i`).

- Basit baglanti yonetimi icin: `ip` veya `ifconfig`, `dig`.

- Kuralli veya duzenli ifadeleri iyi bilin, ve farkli isaretler `grep`/`egrep` icin. The `-i`, `-o`, `-v`, `-A`, `-B`, and `-C` options are worth knowing.

- `apt-get` i kullanmasini bilin, `yum`, `dnf` veya `pacman` (distrolara bagli farkliliklar olabilir) ki hazir packagelari bulup yukleyebilesiniz. Python-temelli komutlari kullanmak icin `pip`i kullanin  (bircogu `pip` ile kolaylikla yuklenebilir).


## Everyday use

- Bash`te otomatik tamamlama ve mevcut komutlari listelemek icin **Tab** kullanin.  Komut gecmisinde arama yapmak icin **ctrl-r**`i kullanin. **ctrl-r**`i kullanarak arama sonuclarini dolasabilirsiniz. **Enter**`a basarak o komutu calistirabilirsiniz.


- Bash`te, **ctrl-w**`i  kullanarak en sonki kelimeyi silebilirsiniz, ve **ctrl-u** satir basina kadar siler.
Kelime kelime hareket etmek icin **alt-b** ve **alt-f**`i kullanin. Gostergeyi satir basina goturmek icin **ctrl-a**`i  ve  **ctrl-e** satir sonuna goturmek icin kullanin.  **ctrl-k** satir sonuna kadar oldurmek icin kullanilir. **ctrl-l** de ekrani temizlemek icin kullanilir. `man readline`  ile kisayollar hakkinda daha fazla bilgi alabilirsiniz. Cok fazla var, mesela  **alt-.** onceki argumanlari gezer ve  **alt-*** glob`lari genisletir. 

- Eger vi-style kisayollari seviyor iseniz, `set -o vi` komutunu calistirabilirsiniz (ve `set -o emacs` eski haline getirmek icin).

- Uzun komutlari editlemek icin, editorunuzu set ettikten sonra (ornegin `export EDITOR=vim`), **ctrl-x** ve **ctrl-e** komulari mevcut komutu editorda acar. Veya vi style`da, **escape-v**.

- En son calisan komutlari gormek icin, `history`(tarih). Bazi kisayollar ise  `!$` (en son arguman) ve `!!` son komut, bunlar sayesinde **ctrl-r** ve **alt-.** de cok faydalidir.

- Bir onceki alt dizine gitmek icin: `cd -`

- Eger komutunuzun ortalarinda biyerde iseniz ve eger fikrinizi degistirirseniz,  **alt-#**`i  `#` komutunuzun basina eklemek icin kullanin, boylelikle komut yorum olur ve calismaz (veya  **ctrl-a**, **#**, **enter** kullanin).  Daha sonra isterseniz history komutu ile geri donebilirsiniz.


- `xargs`i kullanin (veya `parallel`). Cok guclu bir komuttur. Satir basi kac komut calisabilir kontrol edebilirsiniz (`-L`) ayni zamanda paralellik (`-P`). Eger komutun nasil calisacagindan emin degil iseniz,  `xargs echo`i kullanin.`-I{}` da cok kullanislidir. Ornekler:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

-  Proses agaci `pstree -p` komutu yardimi ile gorulebilir.

- `pgrep` ve `pkill` prosesleri isimlerine gore bulmak icin kullanislidir ve (`-f` secenegi de kullanislidir).

- Proseslere gonderebileceginiz farkli sinyalleri bilin. Mesela, bir prosesi duraklatmak icin,  `kill -STOP [pid]` i kullanin. Tam liste icin, bakiniz `man 7 signal`

- Eger bir arka plan prosesini her zaman duraksiz calistirmak istiyor iseniz `nohup` veya `disown` i kullanin

- Hangi proseslerin dinledigini ogrenmek icin `netstat -lntp` veya `ss -plat`i kullanin (TCP icin; UDP icin `-u` ekleyin ).

- Acik dosyalar ve soketler icin `lsof` a bakiniz

- Sisteminizin ne kadar suredir calistigini ogrenmek icin `uptime` veya `w`  a bakiniz.

- Komut kisayollari olusturmak icin `alias` kullanin. Ornegin `alias ll='ls -latr'` `ll` kisayolu olusturur. 


- Bash skriptlerde hata ayiklama(debugging) icin `set -x` i kullanin (veya bir degisik `set -v` i kullanin, bu komut degismemis girdileri, degiskenleri ve yorumlari da sunar).
Kati modlari kullanmaniz tavsiye edilir kesinlikle. Hatalarda iptal etmek icin `set -e` kullanin(sifir olmayan cikis veya bitirme kodu). Sabitlenmemis degisken kullanimlarini algilamak icin `set -u` kullanin. Hatlandirma hatalarinda `set -o` yu kullanin. Daha fazla detay icin EXIT veya ERR`lerde `trap` kullanin.



```bash
      set -euo pipefail
      trap "echo 'hata: Skript başarısız: başarısız komutlari yukarida gorebilirsiniz'" ERR
```

- Bash skriptlerde komut gruplandirmak icin alt Linux kabuklari (parantez icinkediler) elverislidir. Yaygin bir ornek olarak farkli bir dizine gitmek gosterilebilir.
```bash
      # simdiki dizinde komut calistir
      (cd /baska/bir/dizin && diger-komut)
      # baslangic dizininde komut calistirmaya devam et
```

-Bash`te birden fazla degisken genlestirme yolu vardir. Degiskenin varligini kontrol et: `${isim:?hata mesaji}`. Ornegin, eger bir bash skripti bir arguman gerektiriyorda, sadece bunu yaz `input_file=${1:?usage: $0 input_file}`. Eger bir degisken bos ise öndeğer kullanmak icin `${name:-öndeğer}` kullanin. Eger opsiyonel olarak bir parametre eklemek isterseniz `output_file=${2:-logfile}` i kullanin. Aritmetik acilim:  `i=$(( (i + 1) % 5 ))`. Sira veya duzen `{1..10}`. String kirpmak icin `${var%suffix}` ve  `${var#prefix}` kullanin. Ornegin if `var=foo.pdf`, then `echo ${var%.pdf}.txt`  `foo.txt` yazar.


- Kaşlı ayraç  `{`...`}`  ayni seyleri yazmayi azaltir ve bazi ogelerin kombinasyonunu kolaylastirir. Ornegin  `mv foo.{txt,pdf} some-dir` (iki dosyayi da tasir), `cp somefile{,.bak}` (genislemis hali `cp somefile somefile.bak`) veya `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (bu komut genisler ve seceneklerdeki kombinasyonlar ile dizinleri olusturur).

-Bir komutun ciktisi bir dosya gibi gorulebilir `<(some command)` yolu ile, yerli `/etc/hosts` dosyasini uzak dosya ile karsilastirmak icin:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Skript yazarken süslü ayraçlari kulanmak isteyebilirsiniz. Eger acilim ayraci eksik ise skriptiniz calismaz. Internetten skript indirirken de kolaylik saglar.
```bash
{
      # komut kodlari buraya
}
```

- "here documents" leri de bilin, `cat <<EOF ...` te oldugu gibi.

- Bash`te yonlendirme standart cikis ve hatalar  `some-command >logfile 2>&1` veya `some-command &>logfile` ile yapilabilir. Cogu zaman acik dosya birakmamak icin `</dev/null` kullanmak da faydali olabilir.

- Iyi bir hex ve ondalikli degerlerle ASCII tablosu icin `man ascii`yi kullanin. Genel dil kod şeması icin `man unicode`, `man utf-8`, and `man latin1` faydalidir.

- Ekrani coklamak icin `screen` veya [`tmux`](https://tmux.github.io/)i kullanin. Ozellikle uzak oturumlarda oturum acmak, baglamak ve koparmak icin faydalidir. `byobu`u kullanabilirsiniz gelişmiş ekran kolay yonetim icin. Daga minimal alternatif icin oturum dayanıklı icin [`dtach`](https://github.com/bogner/dtach).


-ssh te tunel port icin  `-L` ve `-D` (ve bazilari `-R`) faydalidir. Uzak dağıtıcı(server)daki web sitelerine ulasmak bir ornek olarak gosterilebilir.

- ssh konfigurasyonunu eniyileme icin bir kac degisiklik yapmak onerilir; Ornegin,  `~/.ssh/config` ta bazi ag cevrelinde baglanti kopuklugunu onlemek icin ayarlar bulunur. Sıkıştırma(kompres) (bant baglantilarinda scp kullanmada faydalidir), ve  kanallarinda multiplex(coklama) yapar ayni vericiye:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- ssh`teki diger secenekler guvenlik icindir ve etkinlestirme yapilirken dikkat edilmelidir. Her alt ag, host ve guvenilir aglar icin: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- ssh e alternatif olarak  [`mosh`](https://mosh.mit.edu/) u gozden geciriniz, mosh UDP kullanir. Baglanti kopuklugunu onlemek ve rahatlik icin kullanilabilir.

- Bir dosyanin izinlerini gormek icin oktal formda(ls bu optioni gostermez) bunu kullanin:
```sh
      stat -c '%A %a %n' /etc/timezone
```
- Diger komutlarin sonuclarindan etkileşimli olarak deger almak icin; [`percol`](https://github.com/mooz/percol) veya [`fzf`](https://github.com/junegunn/fzf) i kullanin.

- Komut verilerinden sonra(mesela `git`) dosyalar ile etkilesim icin `fpp`  ([PathPicker](https://github.com/facebook/PathPicker)) kullanin.

-Basit bir web sunucusu icin `python -m SimpleHTTPServer 7777` (for port 7777 and Python 2) ve `python -m http.server 7777` (for port 7777 and Python 3). Bu sunucu bulunmus oldugunuz dizin ve butun alt dizinleri icin sunucu olusturur kendi networkunuzdakiler icin.

- Baska bir kullanici olarak komut calistirmak icin `sudo`yu kullanin. Root(kok) olarak kulanabileceginiz kullanabilceginiz on degerler; `-u` baska bir kullanici belirtmek icin. `-i` baska bir kullanici icin giris yapmak icin (sifreniz sorulacaktir).

- shell'i bir baska kullanici olarak kullanmak icin,  `su username` veya `su - username` kullanin.  "-" bir baska kullanici giris yapmis gibi kabul eder. Kullanici ismi belirtmez iseniz root olarak calisir komut. Hangi kullanici icin giris yapmaya calisiyorsaniz sifreniz sorulur.

- [128K limit](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong) hakkinda bilginiz olsun komut satirlari icin. "Argument list too long"(Arguman listesi cok uzun) hatasi genel bir hatadir genel arama karakteri arandigi zaman bir cok dosya icin(`find` ve `xargs` faydali olabilir).

- Basit bir hesap makinesi icin ve genel python alani icin,  `python` yorumlayıcısini kullanin. Ornegin,
```
>>> 2+3
5
```


## Dosya ve Bilgi İşleme

- Bulunmus oldugunuz dizinde dosyalari isme gore aramak icin `find . -iname '*something*'` i kullanin. Herhangi bir yerde dosya bulmak icin `locate bir-dosya` kullanin(`updatedb` nin guncel olmadigini da goz onunde bulundurmaniz gerekebilir.)

- Kaynak veya veri dosyaları üzerinden genel arama yapmak için (`grep -r`'den daha gelismis) use [`ag`](https://github.com/ggreer/the_silver_searcher) kullanin.

- HTML'i metne dönüştürmek için: `lynx -dump -stdin`

- Markdown, HTML ve her türlü belge dönüşümü için [`pandoc`](http://pandoc.org/) deneyin.

- XML ile uğraşmanız gerekiyorsa, `xmlstarlet` eski ama iyidir.

- JSON icin [`jq`](http://stedolan.github.io/jq/)'i kullanin.

- YAML icin [`shyaml`](https://github.com/0k/shyaml)'i kullanin.

- Excel veya CSV dosyaları için [csvkit](https://github.com/onyxfish/csvkit) `in2csv`,` csvcut`, `csvjoin`,` csvgrep` vb. sağlar.

- Amazon S3 için, [`s3cmd`](https://github.com/s3tools/s3cmd) kullanışlıdır ve [`s4cmd`](https://github.com/bloomreach/s4cmd) daha hızlıdır. Amazon'un [aws] (https://github.com/aws/aws-cli) ve iyileştirilmiş [`saws`](https://github.com/donnemartin/saws) diğer AWS ile ilgili görevler için gereklidir .

- Uniq'ın `-u` ve` -d` seçenekleri de dahil olmak üzere `sort` ve` uniq` hakkında bilgi edinin - aşağıdaki tek gövdeleri görün. Ayrıca bkz. `Comm`.

- Metin dosyalarını değiştirmek için `cut`'kes', `paste`'yapıştır' ve `join`katıl' hakkında bilgi sahibi olun. Çoğu kimse `cut` kullanır fakat` join 'kelimesini unutur.

- Yeni satırları (`-l`), karakterleri (` -m`), kelimeleri (`-w`) ve baytları (` -c`) saymak için `wc` hakkında bilgi sahibi olun.

- `tee` ile ilgili bilgiyi stdin'den bir dosyaya kopyalamayi bilin , `ls -al | Tee file.txt`'da oldugu gibi.

- Gruplama, ters alanlar ve istatistiksel hesaplamalar da dahil olmak üzere daha karmaşık hesaplamalar için [`datamash`](https://www.gnu.org/software/datamash/)'i göz önünde bulundurun.

- Yerel ayarın, sıralama düzeni (harmanlama) ve performans da dahil olmak üzere çok sayıda komut satırı araçlarını ince şekillerde etkilediğini bilin. Çoğu Linux kurulumu, `LANG` veya diğer yerel ayar değişkenlerini, ABD İngilizcesi gibi yerel bir ayara ayarlar. Ancak, yerel ayarı değiştirirseniz, sıralama değişir. i18n rutinleri, sıralama veya diğer komutların *birçok kez* daha yavaş çalışmasını sağlayabilir. Bazı durumlarda(aşağıda belirlenen işlemler veya teklik işlemleri gibi) yavaş i18n yordamlarını tamamen yok sayabilir ve `export LC_ALL = C` kullanarak geleneksel bayt tabanlı sıralama düzenini kullanabilirsiniz.

- Belirli bir komut ortamını, `TZ = Pasifik / Fiji tarihi 'gibi ortam değişken ayarlarıyla önek ekleyerek ayarlayabilirsiniz.

- Basit veri mungajı için temel `awk` ve `sed` leri bilir. Örneğin, bir metin dosyasının üçüncü sütunundaki tüm sayıların toplanması: `awk'{x + = $ 3} END {print x}'` . Muhtemelen eşdeğer Python'dan 3 kat daha hızlı ve 3 kat daha kısa.

- Yerinde, bir veya daha fazla dosyada bulunan tüm dizgelerin yerini değiştirmek için:
```sh
      perl -pi.bak -e 's/eski-string/yeni-string/g' my-files-*.txt
```

- Birden fazla dosyayı yeniden adlandırmak ve / veya dosyaları aramak ve değiştirmek için,  [`repren`](https://github.com/jlevy/repren)'i deneyin. (Bazı durumlarda `rename` komutu aynı zamanda birden fazla yeniden adlandırma yapmasına izin verir, ancak tüm Linux dağıtımlarında işlevselliği aynı olmadığından dikkatli olun.)

```sh
      # Full rename of filenames, directories, and contents foo -> bar:
      # Dosya adlarının, dizinlerin ve içindekilerin tam adını değiştirme foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Recover backup files whatever.bak -> whatever:
      # Yedek dosyaları kurtarmak whatever.bak -> ne olursa olsun:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Same as above, using rename, if available:
      # Varsa, yeniden adlandırma işlevini kullanarak yukarıdakiyle aynı:
      rename 's/\.bak$//' *.bak
```

- Manual sayfasida belirtildiği gibi, `rsync` gerçekten hızlı ve özel olarak çok yönlü bir dosya kopyalama aracıdır. Makineler arasında senkronizasyon yapılması bilinir ancak yerel olarak da eşit derecede yararlıdır. Güvenlik kısıtlamaları izin verdiği zaman, `scp` yerine` rsync` kullanılması, sıfırdan başlamaksızın bir aktarımın kurtarılmasına izin verir. Ayrıca, çok sayıda dosyayı silmek için kullanılan [en hızlı yöntemler](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) arasındadır:
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

-Bir dosyadan rastgele çizgiler karıştırmak veya seçmek için `shuf` kullanın.

- `sort`un seçeneklerini bilir. Rakamlar için, insan tarafından okunabilen sayıları (ör. 'du -h') işlemek için `-n` veya `-h` kullanın. Tuşların nasıl çalıştığını bilin (`-t` ve` -k`). Özellikle, yalnızca ilk alana göre sıralamak için `-k1,1 'yazmanız gerektiğine dikkat edin; `-k1`, tüm satıra göre sıralama anlamına gelir. Kararlı sıralama (`sort -s`) faydalı olabilir. Örneğin, önce alan 2'ye, daha sonra da alan 1'e göre sıralamak için `sort -k1,1 | sort -s -k2,2`.

- Şimdiye kadar Bash'te bir komut satırı içine bir sekme literali yazmanız gerekiyorsa (örneğin, -t argümanı sıralama için) ** ctrl-v ** ** [Tab] ** tuşlarına basın ya da `$ '\ t'` yazarsanız (Kopyalama / yapıştırma gibi ikinci seçenek daha iyidir).

- Kaynak koda eklemenin standart araçları `diff` ve` patch` dir. Ayrıca diff için özet istatistikler için `diffstat` ve yan yana diff için` sdiff` bakınız. `Diff -r 'dizininin tamamı için işe yarar. `Diff -r tree1 tree2'yi kullanın. Değişikliklerin özeti için diffstat`. Dosyaları karşılaştırmak ve düzenlemek için `vimdiff 'kullanın.

- İkili dosyalar için basit hex dökümleri için `hd`,` hexdump` veya `xxd` kullanın ve ikili düzenleme için` bvi`, `hexedit` veya `biew` kullanın.

- İkili dosyalar için de, `strings '(artı `grep`, vb.) metin bitlerini bulmanızı sağlar.

- İkili farklar için (delta sıkıştırma), `xdelta3` kullanın.

- Metin kodlamalarını dönüştürmek için, `iconv`'yi deneyin. Veya daha gelişmiş kullanım için `uconv`; Bazı gelişmiş Unicode şeyleri destekler. Örneğin, bu komut, tüm vurguları azaltır ve kaldırır (bunları genişletip bırakarak):

```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- Dosyaları parçalara ayırmak için, `split` (boyuta göre bölmek için) ve` csplit` (bir desenle bölmek için) bölümüne bakın.

- Tarih ve saat ifadelerini işlemek için, [`dateutils`](http://www.fresse.org/dateutils/) içindeki `dateadd`, `datediff`,` strptime` vb. Işlevlerini kullanın.

- Sıkıştırılmış dosyalar üzerinde çalışmak için `zless`,` zmore`, `zcat` ve` zgrep` kullanın.

- File attributes are settable via `chattr` and offer a lower-level alternative to file permissions. For example, to protect against accidental file deletion the immutable flag:  `sudo chattr +i /critical/directory/or/file`

- Dosya öznitelikleri `chattr` vasıtasıyla ayarlanabilir ve dosya izinlerine alt düzey bir alternatif sunabilir. Örneğin, yanlışlıkla dosya silinmeye karşı korumak için değişmez bayrak: `sudo chattr +i /kritik/dizin/veya/dosya '

- Dosya izinlerini kaydetmek ve geri yüklemek için `getfacl` ve` setfacl` kullanın. Örneğin:
```sh
   getfacl -R /some/path > permissions.txt
   setfacl --restore=permissions.txt
```

## System debugging

- For web debugging, `curl` and `curl -I` are handy, or their `wget` equivalents, or the more modern [`httpie`](https://github.com/jkbrzt/httpie).

- To know current cpu/disk status, the classic tools are `top` (or the better `htop`), `iostat`, and `iotop`. Use `iostat -mxz 15` for basic CPU and detailed per-partition disk stats and performance insight.

- For network connection details, use `netstat` and `ss`.

- For a quick overview of what's happening on a system, `dstat` is especially useful. For broadest overview with details, use [`glances`](https://github.com/nicolargo/glances).

- To know memory status, run and understand the output of `free` and `vmstat`. In particular, be aware the "cached" value is memory held by the Linux kernel as file cache, so effectively counts toward the "free" value.

- Java system debugging is a different kettle of fish, but a simple trick on Oracle's and some other JVMs is that you can run `kill -3 <pid>` and a full stack trace and heap summary (including generational garbage collection details, which can be highly informative) will be dumped to stderr/logs. The JDK's `jps`, `jstat`, `jstack`, `jmap` are useful. [SJK tools](https://github.com/aragozin/jvm-tools) are more advanced.

- Use [`mtr`](http://www.bitwizard.nl/mtr/) as a better traceroute, to identify network issues.

- For looking at why a disk is full, [`ncdu`](https://dev.yorhel.nl/ncdu) saves time over the usual commands like `du -sh *`.

- To find which socket or process is using bandwidth, try [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) or [`nethogs`](https://github.com/raboof/nethogs).

- The `ab` tool (comes with Apache) is helpful for quick-and-dirty checking of web server performance. For more complex load testing, try `siege`.

- For more serious network debugging, [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html), or [`ngrep`](http://ngrep.sourceforge.net/).

- Know about `strace` and `ltrace`. These can be helpful if a program is failing, hanging, or crashing, and you don't know why, or if you want to get a general idea of performance. Note the profiling option (`-c`), and the ability to attach to a running process (`-p`).

- Know about `ldd` to check shared libraries etc.

- Know how to connect to a running process with `gdb` and get its stack traces.

- Use `/proc`. It's amazingly helpful sometimes when debugging live problems. Examples: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (where `xxx` is the process id or pid).

- When debugging why something went wrong in the past, [`sar`](http://sebastien.godard.pagesperso-orange.fr/) can be very helpful. It shows historic statistics on CPU, memory, network, etc.

- For deeper systems and performance analyses, look at `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_(Linux)), and [`sysdig`](https://github.com/draios/sysdig).

- Check what OS you're on with `uname` or `uname -a` (general Unix/kernel info) or `lsb_release -a` (Linux distro info).

- Use `dmesg` whenever something's acting really funny (it could be hardware or driver issues).

- If you delete a file and it doesn't free up expected disk space as reported by `du`, check whether the file is in use by a process:
`lsof | grep deleted | grep "filename-of-my-big-file"`


## One-liners

A few examples of piecing together commands:

- It is remarkably helpful sometimes that you can do set intersection, union, and difference of text files via `sort`/`uniq`. Suppose `a` and `b` are text files that are already uniqued. This is fast, and works on files of arbitrary size, up to many gigabytes. (Sort is not limited by memory, though you may need to use the `-T` option if `/tmp` is on a small root partition.) See also the note about `LC_ALL` above and `sort`'s `-u` option (left out for clarity below).
```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- Use `grep . *` to quickly examine the contents of all files in a directory (so each line is paired with the filename), or `head -100 *` (so each file has a heading). This can be useful for directories filled with config settings like those in `/sys`, `/proc`, `/etc`.


- Summing all numbers in the third column of a text file (this is probably 3X faster and 3X less code than equivalent Python):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- To see sizes/dates on a tree of files, this is like a recursive `ls -l` but is easier to read than `ls -lR`:
```sh
      find . -type f -ls
```

- Say you have a text file, like a web server log, and a certain value that appears on some lines, such as an `acct_id` parameter that is present in the URL. If you want a tally of how many requests for each `acct_id`:
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- To continuously monitor changes, use `watch`, e.g. check changes to files in a directory with `watch -d -n 2 'ls -rtlh | tail'` or to network settings while troubleshooting your wifi settings with `watch -d -n 2 ifconfig`.

- Run this function to get a random tip from this document (parses Markdown and extracts an item):
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```


## Obscure but useful

- `expr`: perform arithmetic or boolean operations or evaluate regular expressions

- `m4`: simple macro processor

- `yes`: print a string a lot

- `cal`: nice calendar

- `env`: run a command (useful in scripts)

- `printenv`: print out environment variables (useful in debugging and scripts)

- `look`: find English words (or lines in a file) beginning with a string

- `cut`, `paste` and `join`: data manipulation

- `fmt`: format text paragraphs

- `pr`: format text into pages/columns

- `fold`: wrap lines of text

- `column`: format text fields into aligned, fixed-width columns or tables

- `expand` and `unexpand`: convert between tabs and spaces

- `nl`: add line numbers

- `seq`: print numbers

- `bc`: calculator

- `factor`: factor integers

- [`gpg`](https://gnupg.org/): encrypt and sign files

- `toe`: table of terminfo entries

- `nc`: network debugging and data transfer

- `socat`: socket relay and tcp port forwarder (similar to `netcat`)

- [`slurm`](https://github.com/mattthias/slurm): network traffic visualization

- `dd`: moving data between files or devices

- `file`: identify type of a file

- `tree`: display directories and subdirectories as a nesting tree; like `ls` but recursive

- `stat`: file info

- `time`: execute and time a command

- `timeout`: execute a command for specified amount of time and stop the process when the specified amount of time completes.

- `lockfile`: create semaphore file that can only be removed by `rm -f`

- `logrotate`: rotate, compress and mail logs.

- `watch`: run a command repeatedly, showing results and/or highlighting changes

- `tac`: print files in reverse

- `shuf`: random selection of lines from a file

- `comm`: compare sorted files line by line

- `pv`: monitor the progress of data through a pipe

- `strings`: extract text from binary files

- `tr`: character translation or manipulation

- `iconv` or `uconv`: conversion for text encodings

- `split` and `csplit`: splitting files

- `sponge`: read all input before writing it, useful for reading from then writing to the same file, e.g., `grep -v something some-file | sponge some-file`

- `units`: unit conversions and calculations; converts furlongs per fortnight to twips per blink (see also `/usr/share/units/definitions.units`)

- `apg`: generates random passwords

- `xz`: high-ratio file compression

- `ldd`: dynamic library info

- `nm`: symbols from object files

- `ab`: benchmarking web servers

- `strace`: system call debugging

- [`mtr`](http://www.bitwizard.nl/mtr/): better traceroute for network debugging

- `cssh`: visual concurrent shell

- `rsync`: sync files and folders over SSH or in local file system

- [`wireshark`](https://wireshark.org/) and [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): packet capture and network debugging

- [`ngrep`](http://ngrep.sourceforge.net/): grep for the network layer

- `host` and `dig`: DNS lookups

- `lsof`: process file descriptor and socket info

- `dstat`: useful system stats

- [`glances`](https://github.com/nicolargo/glances): high level, multi-subsystem overview

- `iostat`: Disk usage stats

- `mpstat`: CPU usage stats

- `vmstat`: Memory usage stats

- `htop`: improved version of top

- `last`: login history

- `w`: who's logged on

- `id`: user/group identity info

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): historic system stats

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) or [`nethogs`](https://github.com/raboof/nethogs): network utilization by socket or process

- `ss`: socket statistics

- `dmesg`: boot and system error messages

- `sysctl`: view and configure Linux kernel parameters at run time

- `hdparm`: SATA/ATA disk manipulation/performance

- `lsblk`: list block devices: a tree view of your disks and disk partitions

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: hardware information, including CPU, BIOS, RAID, graphics, devices, etc.

- `lsmod` and `modinfo`: List and show details of kernel modules.

- `fortune`, `ddate`, and `sl`: um, well, it depends on whether you consider steam locomotives and Zippy quotations "useful"


## OS X only

These are items relevant *only* on OS X.

- Package management with `brew` (Homebrew) and/or `port` (MacPorts). These can be used to install on OS X many of the above commands.

- Copy output of any command to a desktop app with `pbcopy` and paste input from one with `pbpaste`.

- To enable the Option key in OS X Terminal as an alt key (such as used in the commands above like **alt-b**, **alt-f**, etc.), open Preferences -> Profiles -> Keyboard and select "Use Option as Meta key".

- To open a file with a desktop app, use `open` or `open -a /Applications/Whatever.app`.

- Spotlight: Search files with `mdfind` and list metadata (such as photo EXIF info) with `mdls`.

- Be aware OS X is based on BSD Unix, and many commands (for example `ps`, `ls`, `tail`, `awk`, `sed`) have many subtle variations from Linux, which is largely influenced by System V-style Unix and GNU tools. You can often tell the difference by noting a man page has the heading "BSD General Commands Manual." In some cases GNU versions can be installed, too (such as `gawk` and `gsed` for GNU awk and sed). If writing cross-platform Bash scripts, avoid such commands (for example, consider Python or `perl`) or test carefully.

- To get OS X release information, use `sw_vers`.

## Windows only

These items are relevant *only* on Windows.

- On Windows 10, you can use [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about), which provides a familiar Bash environment with Unix command line utilities. On the plus side, this allows Linux programs to run on Windows. On the other hand this does not support the running of Windows programs from the Bash prompt.

- Access the power of the Unix shell under Microsoft Windows by installing [Cygwin](https://cygwin.com/). Most of the things described in this document will work out of the box.

- Install additional Unix programs with the Cygwin's package manager.

- Use `mintty` as your command-line window.

- Access the Windows clipboard through `/dev/clipboard`.

- Run `cygstart` to open an arbitrary file through its registered application.

- Access the Windows registry with `regtool`.

- Note that a `C:\` Windows drive path becomes `/cygdrive/c` under Cygwin, and that Cygwin's `/` appears under `C:\cygwin` on Windows. Convert between Cygwin and Windows-style file paths with `cygpath`. This is most useful in scripts that invoke Windows programs.

- You can perform and script most Windows system administration tasks from the command line by learning and using `wmic`.

- Another option to get Unix look and feel under Windows is [Cash](https://github.com/dthree/cash). Note that only very few Unix commands and command-line options are available in this environment.

- An alternative option to get GNU developer tools (such as GCC) on Windows is [MinGW](http://www.mingw.org/) and its [MSYS](http://www.mingw.org/wiki/msys) package, which provides utilities such as bash, gawk, make and grep. MSYS doesn't have all the features compared to Cygwin. MinGW is particularly useful for creating native Windows ports of Unix tools.

## More resources

- [awesome-shell](https://github.com/alebcay/awesome-shell): A curated list of shell tools and resources.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): A more in-depth guide for the OS X command line.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) for writing better shell scripts.
- [shellcheck](https://github.com/koalaman/shellcheck): A shell script static analysis tool. Essentially, lint for bash/sh/zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): The sadly complex minutiae on how to handle filenames correctly in shell scripts.
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools): More commands and tools helpful for doing data science, from the book of the same name

## Disclaimer

With the exception of very small tasks, code is written so others can read it. With power comes responsibility. The fact you *can* do something in Bash doesn't necessarily mean you should! ;)


## License

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
