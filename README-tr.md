🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) . [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Türkçe](README-tr.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*



# Komuta Hattı Sanatı

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


- [Meta](#meta)
- [Temel Bilgiler](#basics)
- [Günlük kullanım](#everyday-use)
- [Dosyaları ve Verileri Işleme](#processing-files-and-data)
- [Sistem Hata Ayıklama](#system-debugging)
- [Tek Gömlekler](#one-liners)
- [Belirsiz Ama Kullanışlı](#obscure-but-useful)
- [Yalnızca OS X](#os-x-only)
- [Yalnızca Windows](#windows-only)
- [Daha Fazla Kaynak](#more-resources)
- [Feragatname](#disclaimer)


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


## Temel Bilgiler

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


## Günlük kullanım

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

- Bash`te birden fazla degisken genlestirme yolu vardir. Degiskenin varligini kontrol et: `${isim:?hata mesaji}`. Ornegin, eger bir bash skripti bir arguman gerektiriyorda, sadece bunu yaz `input_file=${1:?usage: $0 input_file}`. Eger bir degisken bos ise öndeğer kullanmak icin `${name:-öndeğer}` kullanin. Eger opsiyonel olarak bir parametre eklemek isterseniz `output_file=${2:-logfile}` i kullanin. Aritmetik acilim:  `i=$(( (i + 1) % 5 ))`. Sira veya duzen `{1..10}`. String kirpmak icin `${var%suffix}` ve  `${var#prefix}` kullanin. Ornegin if `var=foo.pdf`, then `echo ${var%.pdf}.txt`  `foo.txt` yazar.


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


- ssh te tunel port icin  `-L` ve `-D` (ve bazilari `-R`) faydalidir. Uzak dağıtıcı(server)daki web sitelerine ulasmak bir ornek olarak gosterilebilir.

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

- Basit bir web sunucusu icin `python -m SimpleHTTPServer 7777` (for port 7777 and Python 2) ve `python -m http.server 7777` (for port 7777 and Python 3). Bu sunucu bulunmus oldugunuz dizin ve butun alt dizinleri icin sunucu olusturur kendi networkunuzdakiler icin.

- Baska bir kullanici olarak komut calistirmak icin `sudo`yu kullanin. Root(kok) olarak kulanabileceginiz kullanabilceginiz on degerler; `-u` baska bir kullanici belirtmek icin. `-i` baska bir kullanici icin giris yapmak icin (sifreniz sorulacaktir).

- shell'i bir baska kullanici olarak kullanmak icin,  `su username` veya `su - username` kullanin.  "-" bir baska kullanici giris yapmis gibi kabul eder. Kullanici ismi belirtmez iseniz root olarak calisir komut. Hangi kullanici icin giris yapmaya calisiyorsaniz sifreniz sorulur.

- [128K limit](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong) hakkinda bilginiz olsun komut satirlari icin. "Argument list too long"(Arguman listesi cok uzun) hatasi genel bir hatadir genel arama karakteri arandigi zaman bir cok dosya icin(`find` ve `xargs` faydali olabilir).

- Basit bir hesap makinesi icin ve genel python alani icin,  `python` yorumlayıcısini kullanin. Ornegin,
```
>>> 2+3
5
```


## Dosyaları ve verileri işleme

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

## Sistem hata ayıklama

- Web'de hata ayıklama için, `curl` ve` curl -I` kullanışlı ya da `wget` eşdeğerleri veya daha modern [` httpie`] (https://github.com/jkbrzt/httpie).

- Mevcut cpu / disk durumunu bilmek için, klasik araçlar `üst` (veya daha iyi `htop`), `iostat` ve` iotop`. Temel CPU ve ayrıntılı bölüm başına disk istatistikleri ve performans bilgisi için `iostat -mxz 15` kullanın.

- Ağ bağlantısı detayları için `netstat` ve` ss` kullanın.

- Bir sistemde olup bitenlere hızlı bir genel bakış için, `dstat` özellikle kullanışlıdır. Ayrıntılarla en geniş genel bakış için [`glances(bakışlar)`] (https://github.com/nicolargo/glances) kullanın.


- Bellek durumunu öğrenmek için, `free` ve` vmstat` çıktılarını çalıştırın ve anlayın. Özellikle, "cached(önbelleklenmiş)" değerin, Linux çekirdeği tarafından dosya önbellek olarak tutulduğunun ve dolayısıyla "özgür" değere etkili sayıldığının farkında olun.

- Java sistem hata ayıklama, farklı bir su ısıtıcısıdır, ancak Oracle ve diğer bazı JVM'lerdeki basit bir hile, `kill -3 <pid>` komutunu ve bir tam yığın izi ve yığın özetini (nesil çöp toplama ayrıntıları dahil olmak üzere) çalıştırabilirsiniz. Son derece bilgilendirici olmak için) stderr / logs'a boşaltılacaktır. JDK'nın `jps`,` jstat`, `jstack`,` jmap` faydalıdır. [SJK araçları] (https://github.com/aragozin/jvm-tools) daha gelişmiş.

- Ağ sorunlarını tanımlamak için daha iyi bir traceroute olarak [`mtr`](http://www.bitwizard.nl/mtr/) kullanın.


- Bir diskin dolu olduğunu görmek için, [`ncdu`] (https://dev.yorhel.nl/ncdu),` du -sh * `gibi zamanki komutların üzerine zaman kazandırır.


- Hangi yuvanın veya işlemin bant genişliği kullandığını bulmak için [`iftop`] (http://www.ex-parrot.com/~pdw/iftop/) veya [` nethogs`] (https://github.com/raboof/nethogs).

- `ab` aracı (Apache ile birlikte gelir) web sunucusu performansının hızlı ve kirli kontrolü için yardımcı olur. Daha karmaşık yük testleri için `kuşatma 'deneyin.

- Daha ciddi ağ hata ayıklaması için, [`wireshark`] (https://wireshark.org/), [` tshark`] (https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) veya [` Ngrep`] (http://ngrep.sourceforge.net/).

- "strace" ve "ltrace" hakkında bilgi edinin. Bunlar, bir program başarısız, asılı veya kilitleniyorsa ve nedenini bilmiyorsanız veya performans hakkında genel bir fikir edinmek istiyorsanız yararlı olabilir. Profiling seçeneğini (`-c`) ve çalışan bir işleme (` -p`) yapabilme kabiliyetine dikkat edin.

- Paylaşılan kitaplıkları vb. Kontrol etmek için `ldd` hakkında bilgi sahibi olun.

- Çalışan bir işleme "gdb" ile nasıl bağlanacağınızı ve yığın izlerini nasıl elde edeceğinizi bilin.

- `/proc` kullanın. Canlı sorunları ayıklarken inanılmaz derecede yararlıdır. Örnekler: `/ proc / cpuinfo`,` / proc / meminfo`, `/ proc / cmdline`,` / proc / xxx / cwd`, ​​`/ proc / xxx / exe`,` / proc / xxx / fd / ` , `/ Proc / xxx / smaps` (burada` xxx` süreç id veya pid'dir).

- Geçmişte bir şeylerin neden ters gittiğini hata ayıklarken, [`sar`] (http://sebastien.godard.pagesperso-orange.fr/) çok yardımcı olabilir. CPU, bellek, ağ vb. Ile ilgili tarihi istatistikleri gösterir.

- Daha derin sistemler ve performans analizleri için `stap` ([SystemTap] (https://sourceware.org/systemtap/wiki)), [` perf`] (https://en.wikipedia.org/wiki/Perf_) (Linux)) ve [`sysdig`] (https://github.com/draios/sysdig).
- `uname` veya` uname -a` (genel Unix / çekirdek bilgisi) veya `lsb_release -a` (Linux dağıtım bilgisi) ile hangi işletim sisteminde olduğunuzu kontrol edin.

- Bir şey gerçekten komik bir sekilde vakit geçirirse (donanım veya sürücü sorunları olabilir) 'dmesg' kullanın.

- Bir dosyayı silerseniz ve beklenen disk alanını `du` tarafından bildirildiği şekilde boşa çıkarmazsa dosyanın bir süreç tarafından kullanılıp kullanılmadığını kontrol edin:
Lsof | Grep silindi | Grep "dosyaismi-of-my-big-file" `


## TekGömlekler

Komutları birbirine eklemeye ilişkin birkaç örnek:

- Bazen bazen, `sort`/`uniq` ile kesişim, birleşim ve metin dosyaları farkını ayarlayabilmeniz son derece yararlıdır.`a` ve `b`'nin benzersiz metin dosyaları olduğunu varsayalım. Bu hızlıdır ve keyfi büyüklükteki dosyalar üzerinde, birçok gigabayta kadar çalışır. (Sort, bellek ile sınırlandırılmaz, ancak `/ tmp` küçük bir kök bölümündeyse` -T` seçeneğini kullanmanız gerekebilir.) Yukarıdaki `LC_ALL` ve` sort`` -u` seçeneği hakkındaki nota da bakınız (aşağıda netlik için dışarıda bırakılmıştır).

- ```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```


- `grep . *`'i kullanin. Bir dizindeki tüm dosyaların içeriğini hızlı bir şekilde incelemek için (böylece her satır dosya ismi ile eşleştirilir) veya `head -100 *` (böylece her dosyanın bir başlığı vardır). Bu, `/ sys`,` / proc`, `/ etc` gibi yapılandırma ayarları ile dolu dizinler için yararlı olabilir.

- Metin dosyasının üçüncü sütunundaki tüm sayıların toplanması (bu muhtemelen Python'dan 3 kat daha hızlı ve 3 kat daha az koddur):
- ```sh
      awk '{ x += $3 } END { print x }' myfile
```

- Bir ağaç dosyasında boyutları / tarihleri ​​görmek için, özyinelemeli `ls -l` gibidir ancak` ls -lR`'den daha okunması daha kolaydır:
```sh
      find . -type f -ls
```

- Bir web sunucusu günlüğü gibi bir metin dosyanıza ve URL'de bulunan bir 'acct_id' parametresi gibi bazı satırlarda görünen belirli bir değere sahip olduğunuzu varsayalım. Her `acct_id` için kaç tane istekte bulunacağını öğrenmek isterseniz:
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```


- Değişiklikleri sürekli izlemek için, örneğin `watch` i kullanın; ör. `watch -d -n 2 'ls -rtlh | tail'` ile bir dizinde bulunan dosyalardaki değişiklikleri kontrol edin veya ağ ayarlarına girip `watch -d -n 2 ifconfig` ile wifi ayarlarınızı gidermek.

- Bu dokümandan rastgele bir ipucu almak için bu işlevi çalıştırın (Markdown'ı ayrıştırır ve bir öğe çıkarır):
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```


## Belirsiz ama kullanışlı

- `expr ': aritmetik veya boolean işlemleri gerçekleştirir veya normal ifadeleri değerlendirir

- `m4`: basit makro işlemci

- `yes': bir dize çok yazdır

- `cal`: güzel takvim

- `env`: bir komut çalıştır (komut dosyalarında kullanışlı)

- `printenv`: ortam değişkenlerini basar (hata ayıklamada ve komut dosyalarında kullanışlıdır)

- `look`: bir dize ile başlayan İngilizce kelimeleri (veya bir dosyadaki satırları) bulmak

- `cut`,` paste` ve `join`: veri işleme

- `fmt`: metin paragraflarını formatla

- `pr`: metni sayfalara / sütunlara formatlar

- `fold`: metnin satırlarını sarar

- `column`: metin alanlarını hizalanmış, sabit genişlikli sütunlara veya tablolara formatlar

- `expand` ve `unexpand`: sekmeler ve boşluklar arasında dönüştürme

- `nl`: satır numaralarını ekleme

- `seq`: Numaraları yaz

- `bc`: hesap makinesi

- `factor`: Faktör tamsayıları

- [`gpg`](https://gnupg.org/): Dosyaları şifrelemek ve imzalamak

- `toe`: Terminfo girişleri tablosu

- `nc`: Ağ hata ayıklama ve veri aktarımı

- `socat`: Soket rölesi ve tcp port iletici (`netcat`'e benzer)

- [`slurm`](https://github.com/mattthias/slurm): Ağ trafiği görselleştirme


- `dd`: Dosya veya cihaz arasında veri taşıma

- `file`: Dosya türünü saptamak

- `tree`: Dizinleri ve alt dizinleri yuvalanmış bir ağaç olarak görüntüleyin; `ls` gibi ama yinelemeli

- `stat`: Dosya bilgisi

- `time`: Bir komut yürütmek ve zamanlama

- `timeout`: Belirtilen süre kadar bir komutu çalıştırın ve belirtilen süre dolduğunda işlemi durdurun.
- `lockfile`: Sadece `rm -f` ile kaldırılabilen semafor dosyası yarat
- `logrotate`: Döndürme, sıkıştırma ve postaları posta ile gönderme.

- `watch`: Sonuçlar ve / veya değişiklikleri vurgulayarak, bir komut tekrar tekrar çalıştırın


- `tac`: Dosyaları tersine yazdır

- `shuf`: Bir dosyadan satırların rasgele seçilmesi

- `comm`: Sıralanmış dosyaları sırayla karşılaştır

- `pv`: Verilerin bir borudan ilerlemesini izleyin

- `strings`: Ikili dosyalardan metin çıkarmak

- `tr`: Karakter çevirisi veya manipülasyon

- `iconv` or `uconv`: Metin kodlamaları için dönüşüm

- `split` ve `csplit`: Bölme dosyaları


- `sponge`: Yazmadan önce tüm girdileri okuyun, sonra aynı dosyaya okumak için yararlıdır,ornek: `grep -v something some-file | sponge some-file`

- `units`: Birim dönüşümleri ve hesaplamaları; İki haftada bir göz kırptığında göz kırpmalarına kadar bitki tellerine dönüşür (bkz. `/ Usr / share / units / definitions.units`)

- `apg`: Rasgele şifreler üretir

- `xz`: Yüksek oranlı dosya sıkıştırma

- `ldd`: Dinamik kitaplık info

- `nm`: Nesne dosyalarından semboller

- `ab`: Karşılaştırma web sunucuları

- `strace`: Hata ayıklama sistemi çağrısı

- [`mtr`](http://www.bitwizard.nl/mtr/): Ağ hata ayıklama için daha iyi traceroute
- `cssh`: Görsel eşzamanlı kabuk

- `rsync`: SSH üzerinden veya yerel dosya sisteminde dosyaları ve klasörleri senkronize edin

- [`wireshark`](https://wireshark.org/) vw [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): Paket yakalama ve ağ hata ayıklama
- [`ngrep`](http://ngrep.sourceforge.net/): Ağ katmanı için grep

- `host` ve `dig`: DNS aramaları

- `lsof`: Süreç dosya tanımlayıcısı ve soket bilgisi
- `dstat`: Kullanışlı sistem istatistikleri

- [`glances`](https://github.com/nicolargo/glances): Yüksek seviye, çoklu alt sisteme genel bakış
- `iostat`: Disk kullanım istatistikleri

- `mpstat`: CPU kullanımı istatistikleri

- `vmstat`: Bellek kullanım istatistikleri

- `htop`: Üstün gelişmiş versiyonu

- `last`: Giriş geçmişi

- `w`: Kim oturum açmış?

- `id`: Kullanıcı / grup kimlik bilgisi

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): Tarihi sistem istatistikleri
- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) veya [`nethogs`](https://github.com/raboof/nethogs): Soket veya işlemle ağ kullanımı
- `ss`: Yuva istatistikleri

- `dmesg`: Önyükleme ve sistem hata iletileri

- `sysctl`: Çalışma zamanında Linux çekirdeği parametrelerini görüntüleme ve yapılandırma

- `hdparm`: SATA / ATA disk manipülasyonu / performansı

- `lsblk`: Blok aygıtları listele: disklerinizin ve disk bölümlerinin ağaç görünümü
- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: CPU, BIOS, RAID, grafik, aygıtlar vb. Dahil olmak üzere donanım bilgileri.

- `lsmod` vw `modinfo`: Çekirdek modüllerinin detaylarını listeleme ve gösterme.

- `fortune`, `ddate`, vw `sl`: Um, bu, buhar lokomotiflerini mi yoksa Zippy tekliflerini "faydalı" mı düşününce,

## Yalnızca OS X

Bunlar, OS X'de *yalnızca* ilgili öğelerdir.

- `brew` (Homebrew) ve / veya `port` (MacPorts) ile paket yönetimi. Bunlar, OS X'de yukarıdaki komutların birçoğunu yüklemek için kullanılabilir.

- Herhangi bir komutun çıktısını `pbcopy` ile bir masaüstü uygulamasına kopyalayın ve` pbpaste` ile girdiyi yapıştırın.

- OS X Terminalinde Option tuşunu bir alt anahtar olarak etkinleştirmek için (örneğin yukarıdaki komutlarda ** alt-b **, ** alt-f **, vb. Gibi) Tercihler -> Tercihler -> Klavye'yi açın Ve "Meta tuş olarak Seçeneği Kullan" ı seçin.

- Bir masaüstü uygulaması olan bir dosyayı açmak için `open` veya` open -a/Applications/Whatever.app` kullanın.

- Spotlight: `mdfind` ile dosyaları arayın ve` mdls` ile meta verileri (fotoğraf EXIF ​​bilgisi gibi) listeleyin.

- OS X'in BSD Unix'e dayandığını ve birçok komutun (örneğin `ps`,` ls`, `tail`,` awk`, `sed`) Linux'un, System V'ten büyük oranda etkilenen birçok ince varyasyona sahip olduğunu unutmayın. - Unix ve GNU araçlarını biçimlendirin. Aradaki farkı, "BSD Genel Komutları El Kitabı" başlığına sahip bir sayfaya dikkat ederek söyleyebilirsiniz. Bazı durumlarda GNU sürümleri de kurulabilir (GNU awk ve sed için `gawk` ve` gsed` gibi). Çapraz platform Bash komut dosyaları yazıyorsanız, bu tür komutlardan kaçının (örneğin, Python veya `perl`'ı düşünün) veya dikkatli bir şekilde test edin.
- OS X sürüm bilgisi edinmek için `sw_vers` kullanın.

## Yalnızca Windows

Bunlar, Windows'ta *yalnızca* ilgili öğelerdir.

- Windows 10'da, Unix komut satırı yardımcı programlarıyla tanıdık bir Bash ortamı sağlayan [Windows'da Ubuntu'da Bash] (https://msdn.microsoft.com/commandline/wsl/about) kullanabilirsiniz. Artı tarafta, Linux programları Windows'ta çalışmasına izin verir. Öte yandan, bu, Bash isteminden Windows programlarının çalışmasını desteklemez.
- [Cygwin] (https://cygwin.com/) yükleyerek Microsoft Windows altında Unix kabuğunun gücüne erişin. Bu belgede açıklanan şeylerin çoğu kutudan çıkmaz.

- Cygwin'in paket yöneticisi ile birlikte ek Unix programları yükleyin.
- Komut satırı pencereniz olarak `mintty` kullanın.

- Windows panosuna '/ dev / clipboard` ile erişin.
- Kayıtlı uygulaması aracılığıyla keyfi bir dosya açmak için `cygstart` çalıştırın.
- Windows kayıt defterine 'regtool' ile erişin.
- Windows yolunun `C: \` kısmı Cygwin'de `/ cygdrive / c` olur ve Cygwin'in` / `harfleri Windows'ta` C: \ cygwin` altında göründüğünü unutmayın. `Cygpath` ile Cygwin ve Windows tarzı dosya yolları arasında dönüştürme yapın. Bu, Windows programlarını çalıştıran komut dosyalarında en kullanışlıdır.

- Windows sistem yönetim görevlerinin çoğunu komut satırından öğrenebilir ve `wmic` kullanarak komut verebilirsiniz.
- Unix'in Windows altında görünmesini sağlamak için bir başka seçenek de [Cash] (https://github.com/dthree/cash). Bu ortamda yalnızca çok az sayıda Unix komutunun ve komut satırı seçeneğinin kullanılabileceğini unutmayın.
- Windows'da GNU geliştirici araçlarını (GCC gibi) almak için alternatif bir seçenek [MinGW] (http://www.mingw.org/) ve onun [MSYS] (http://www.mingw.org/wiki/msys ) Paketi, bash, gawk, make ve grep gibi araçlara sahiptir. MSYS, Cygwin'e kıyasla tüm özelliklere sahip değildir. MinGW, özellikle yerel Windows bağlantı noktaları Unix araçları oluşturmak için kullanışlıdır.
## Daha fazla kaynak

- [awesome-shell](https://github.com/alebcay/awesome-shell):Kılıflandırılmış kabuk araçları ve kaynakları listesi
-  [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): AOS X komut satırı için daha ayrıntılı rehber.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) Daha iyi kabuk komut dosyaları yazmak için
- [shellcheck](https://github.com/koalaman/shellcheck):Bir kabuk komut dosyası statik analiz aracı. Esasen, bash / sh / zsh için lint.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): Kabuk betiklerinde dosya adlarını doğru şekilde işleme konusunda ne yazık ki karmaşık ayrıntılar.
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools): Aynı adı taşıyan kitaptan veri bilimi yapmak için yardımcı olan daha fazla komut ve araçlar

## Feragatname

Çok küçük görevler haricinde kod başkalarının okuyabilmesi için yazılmıştır. Güç ile birlikte sorumluluk gelir. Bash'de *bir şey yapabildiğinin*, mutlaka yapmanız gerektiği anlamına gelmez! ;)


## Lisans

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

Bu çalışma, [Creative Commons Atıf-Benzerlik 4.0 Uluslararası Lisansı] (http://creativecommons.org/licenses/by-sa/4.0/) kapsamında lisanslanmıştır.