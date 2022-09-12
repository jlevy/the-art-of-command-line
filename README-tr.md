🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [polski](README-pl.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Türkçe](README-tr.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*

# Komut Satırı Sanatı

*Not: Bunu gözden geçirmeyi planlıyorum ve bunu daha kapsamlı bir rehber haline getirmeye yardımcı olacak yeni bir ortak yazar arıyorum. Çok popüler olsa da, daha geniş ve biraz daha derin olabilir. Yazmayı seviyorsanız ve bu malzemede uzman olmaya yakınsanız ve yardım etmeyi düşünüyorsanız, lütfen bana josh (0x40) holloway.com'a bir not bırakın. –[jlevy](https://github.com/jlevy), [Holloway](https://www.holloway.com). Teşekkürler!*

- [Meta](#meta)
- [Temel bilgiler](#temel-bilgiler)
- [Günlük kullanım](#günlük-kullanım)
- [Dosyaların ve verilerin işlenmesi](#dosyaların-ve-verilerin-işlenmesi)
- [Sistem hata ayıklama](#sistem-hata-ayıklama)
- [Tek satırlık kodlar](#tek-satırlık-kodlar)
- [Anlaması güç ama kullanışlı](#anlaması-güç-ama-kullanışlı)
- [Yalnızca macOS için](#yalnızca-macos-için)
- [Yalnızca Windows için](#yalnızca-windows-için)
- [Daha fazla kaynak](#daha-fazla-kaynak)
- [Sorumluluk reddi](#sorumluluk-reddi)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

Komut satırında akıcılık genellikle ihmal edilen veya gizemli kabul edilen bir beceridir, ancak bir mühendis olarak esnekliğinizi ve üretkenliğinizi hem açık hem de ince yollarla geliştirir. Bu, Linux üzerinde çalışırken yararlı bulduğumuz komut satırı kullanımına ilişkin notlar ve ipuçlarından oluşan bir seçkidir. Bazı ipuçları basit, bazıları ise oldukça spesifik, sofistike veya belirsizdir. Bu sayfa uzun değildir, ancak buradaki tüm öğeleri kullanabilir ve hatırlayabilirseniz, çok şey biliyorsunuz demektir.

Bu çalışma [birçok yazar ve çevirmenin](AUTHORS.md) ürünüdür. 
Bunların bir kısmı 
[ilk olarak](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[Quora'da](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
[yayınlandı](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
ancak o zamandan beri GitHub'a taşındı ve burada orijinal yazardan daha yetenekli insanlar çok sayıda iyileştirme yaptı.
Komut satırı ile ilgili bir sorunuz varsa lütfen [**bir soru gönderin**](https://airtable.com/shrzMhx00YiIVAWJg). 
Bir hata veya daha iyi olabilecek bir şey görürseniz lütfen [**katkıda bulunun**](/CONTRIBUTING.md)!

## Meta

Kapsam:

- Bu kılavuz hem yeni başlayanlar hem de deneyimli kullanıcılar içindir. Hedefler genişlik (önemli olan her şey), özgüllük (en yaygın durumla ilgili somut örnekler vermek) ve kısalıktır (gerekli olmayan şeylerden veya başka bir yerde kolayca arayabileceğiniz ayrıntılardan kaçının). Her ipucu bazı durumlarda gereklidir veya alternatiflere göre önemli ölçüde zaman kazandırır.
- Bu kitap, "[yalnızca macOS için](#yalnızca-macos-için)" ve "[yalnızca Windows için](#yalnızca-windows-için)" bölümleri dışında Linux için yazılmıştır. Diğer öğelerin çoğu diğer Unices veya macOS (hatta Cygwin) için de geçerlidir veya kurulabilir.
- Odak noktası etkileşimli Bash olmakla birlikte, birçok ipucu diğer kabuklar ve genel Bash komut dosyası yazmak için de geçerlidir.
- Hem "standart" Unix komutlarını hem de özel paket yüklemeleri gerektiren komutları içermektedir - dahil edilmeyi hak edecek kadar önemli oldukları sürece.

Not:

- Bunu tek sayfa tutmak için, içerik referans yoluyla dolaylı olarak dahil edilmiştir. Google'da aratacağınız fikri veya komutu öğrendikten sonra başka bir yerde daha fazla ayrıntı arayacak kadar akıllısınız. Yeni programlar yüklemek için `apt`, `yum`, `dnf`, `pacman`, `pip` veya `brew` (uygun olacak şekilde) kullanın.
- Komutların, seçeneklerin, küme komutların vb. ne işe yaradığının yararlı bir dökümünü almak için [Explainshell](http://explainshell.com/)'i kullanın.


## Temel bilgiler

- Temel Bash öğrenin. Aslında, `man bash` yazın ve en azından tamamını gözden geçirin; takip etmesi oldukça kolaydır ve o kadar da uzun değildir. Alternatif kabuklar güzel olabilir, ancak Bash güçlüdür ve her zaman kullanılabilir (yalnızca zsh, fish vb. öğrenmek, kendi dizüstü bilgisayarınızda cazip olsa da, mevcut sunucuları kullanmak gibi birçok durumda sizi kısıtlar).

- En az bir metin tabanlı editörü iyi öğrenin. `nano` editörü temel düzenleme (açma, düzenleme, kaydetme, arama) için en basitlerinden biridir. Bununla birlikte, bir metin terminalindeki usta kullanıcılar için, öğrenmesi zor ama saygıdeğer, hızlı ve tam özellikli bir editör olan Vim'in (`vi`) yerini hiçbir şey tutamaz. Birçok kişi, özellikle daha büyük düzenleme görevleri için klasik Emacs'ı da kullanır. (Elbette, kapsamlı bir proje üzerinde çalışan herhangi bir modern yazılım geliştiricisinin yalnızca saf metin tabanlı bir düzenleyici kullanması olası değildir ve modern grafik IDE'lere ve araçlara da aşina olması gerekir).

- Dokümantasyon bulma:
  - Resmi dokümantasyonu `man` ile nasıl okuyacağınızı bilin (meraklılar için `man man` bölüm numaralarını listeler, örneğin 1 "normal" komutlar, 5 dosyalar / teamüller ve 8 yönetim içindir). Man sayfalarını `apropos` ile  bulun.
  - Bazı komutların çalıştırılabilir (executable) değil, Bash yerleşik komutları (builtin) olduğunu ve `help` ve `help -d` ile bu komutlar hakkında yardım alabileceğinizi bilin. Bir komutun çalıştırılabilir mi, kabuk yerleşik komut mu yoksa takma ad (alias) mı olduğunu `type command` kullanarak öğrenebilirsiniz.
  - `curl cheat.sh/command` bir kabuk komutunun nasıl kullanılacağına dair yaygın örnekler içeren kısa bir "kopya kağıdı" verecektir.

- Girdi ve çıktının `>` ve `<` kullanılarak yeniden yönlendirilmesi ve `|` kullanılarak yapılan küme komutlar hakkında bilgi edinin. Büyüktür `>` işaretinin çıktı dosyasının üstüne yazdığını ve `>>` işaretinin dosyanın sonuna eklediğini bilin. stdout ve stderr hakkında bilgi edinin.

- Yıldız işareti ile `*` (ve belki `?` ve `[`...`]`) ile dosya glob genişletmesi ve çift `"` ve tek `'` tırnak işaretleri arasındaki fark hakkında bilgi edinin. (Değişken genişletme hakkında daha fazla bilgi için aşağıya bakınız).

- Bash iş yönetimine aşina olun: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, vb.

- `ssh` ve `ssh-agent`, `ssh-add` vb. aracılığıyla parolasız kimlik doğrulamanın temellerini bilin.

- Temel dosya yönetimi: `ls` ve `ls -l` (özellikle `ls -l`deki her sütunun ne anlama geldiğini öğrenin), `less`, `head`, `tail` ve `tail -f` (hatta daha iyisi, `less +F`), `ln` ve `ln -s` (hard ve soft linklerin farklarını ve avantajlarını öğrenin), `chown`, `chmod`, `du` (disk kullanımının hızlı bir özeti için: `du -hs *`). Dosya sistemi yönetimi için `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. Bir inode'un ne olduğunu öğrenin (`ls -i` veya `df -i`).

- Temel ağ yönetimi: `ip` veya `ifconfig`, `dig`, `traceroute`, `route`.

- Örneğin `git` gibi bir sürüm kontrol yönetim sistemini öğrenin ve kullanın.

- Düzenli ifadeleri ve `grep`/`egrep` için çeşitli bayrakları iyi bilin. `i`, `-o`, `-v`, `-A`, `-B` ve `-C` seçenekleri bilinmeye değerdir.

- Paketleri bulmak ve yüklemek için `apt-get`, `yum`, `dnf` veya `pacman` (dağıtıma bağlı olarak) kullanmayı öğrenin. Ve Python tabanlı komut satırı araçlarını yüklemek için `pip`e sahip olduğunuzdan emin olun (aşağıdaki birkaçını `pip` ile yüklemek en kolay yoldur).


## Günlük kullanım

- Bash'te, argümanları tamamlamak veya mevcut tüm komutları listelemek için **Tab** ve komut geçmişinde arama yapmak için **ctrl-r** tuşlarını kullanın (tuşuna bastıktan sonra, aramak için yazın, daha fazla eşleşme arasında geçiş yapmak için **ctrl-r** tuşuna tekrar tekrar basın, bulunan komutu çalıştırmak için **Enter** tuşuna basın veya sonucu düzenlemeye izin vermek üzere geçerli satıra koymak için sağ oka basın).

- Bash'te, son kelimeyi silmek için **ctrl-w** ve geçerli imleçten satırın başına kadar olan içeriği silmek için **ctrl-u** kullanın. Kelime bazında hareket etmek için **alt-b** ve **alt-f**, imleci satır başına taşımak için **ctrl-a**, imleci satır sonuna taşımak için **ctrl-e**, satır sonuna kadar öldürmek için **ctrl-k**, ekranı temizlemek için **ctrl-l** kullanın. Bash'teki tüm varsayılan tuş atamaları için `man readline` bölümüne bakın. Çok fazla var. Örneğin **alt-.** önceki argümanlar arasında geçiş yapar ve **alt-*** bir globu genişletir.


- Alternatif olarak, vi-tarzı tuş atamalarını seviyorsanız, `set -o vi` (ve geri koymak için `set -o emacs`) kullanın.

- Uzun komutları düzenlemek için, editörünüzü ayarladıktan sonra (örneğin `export EDITOR=vim`), **ctrl-x** **ctrl-e** mevcut komutu çok satırlı düzenleme için bir editörde açacaktır. Veya vi tarzında, **escape-v**.

- Son komutları görmek için `history` kullanın. Tekrar çalıştırmak için `!n` (burada `n` komut numarasıdır) ile takip edin. Ayrıca kullanabileceğiniz birçok kısaltma vardır, muhtemelen en kullanışlı olanları son argüman için `!$` ve son komut için `!!` (man sayfasındaki "HISTORY EXPANSION" bölümüne bakınız). Ancak, bunlar genellikle **ctrl-r** ve **alt-.** ile kolayca değiştirilebilir.

- `cd` ile ev dizininize gidin. Ev dizininize göre dosyalara `~` önekiyle erişin (örneğin `~/.bashrc`). Ayrica `sh` betiklerinde ev dizinine `$HOME` olarak atıfta bulunulur.

- Önceki çalışma dizinine geri dönmek için: `cd -`.

- Bir komutu yazmanın yarısına geldiğinizde fikrinizi değiştirirseniz, başına bir `#` eklemek için **alt-#** tuşuna basın ve bunu bir yorum olarak girin (veya **ctrl-a**, **#**, **enter** tuşlarını kullanın). Daha sonra komut geçmişi aracılığıyla geri dönebilirsiniz.

- `xargs` (veya `parallel`) kullanın. Bu çok güçlüdür. Satır başına kaç öğenin çalıştırılacağını (`-L`) ve paralelliği (`-P`) kontrol edebileceğinizi unutmayın. Doğru şeyi yapıp yapmayacağından emin değilseniz, önce `xargs echo` kullanın. Ayrıca, `-I{}` kullanışlıdır. Örnekler:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` işlem ağacının yararlı bir görüntüsüdür.

- Süreçleri isimlerine göre bulmak veya sinyallemek için `pgrep` ve `pkill` kullanın (`-f` yardımcı olur).

- Süreçlere gönderebileceğiniz çeşitli sinyalleri bilin. Örneğin, bir süreci askıya almak için `kill -STOP [pid]` kullanın. Tam liste için `man 7 signal` bölümüne bakın

- Bir arka plan işleminin sonsuza kadar çalışmaya devam etmesini istiyorsanız `nohup` veya `disown` kullanın.

- Hangi süreçlerin dinlediğini `netstat -lntp` veya `ss -plat` (TCP içindir; UDP için `-u` ekleyin) veya `lsof -iTCP -sTCP:LISTEN -P -n` (macOS'ta da çalışır) aracılığıyla kontrol edin.

- Açık soketler ve dosyalar için `lsof` ve `fuser` öğelerine de bakın.

- Sistemin ne kadar süredir çalıştığını öğrenmek için `uptime` veya `w`'ye bakın.

- Sık kullanılan komutlar için kısayollar oluşturmak için `alias` kullanın. Örneğin, `alias ll='ls -latr'` yeni bir `ll` takma adı oluşturur.

- Sık kullandığınız takma adları, kabuk ayarlarını ve işlevleri `~/.bashrc` dosyasına kaydedin ve [giriş kabuklarının bu dosyayı kaynak olarak kullanmasını sağlayın](http://superuser.com/a/183980/7106). Bu, kurulumunuzu tüm kabuk oturumlarınızda kullanılabilir hale getirecektir.

- Ortam değişkenlerinin ayarlarını ve oturum açtığınızda çalıştırılması gereken komutları `~/.bash_profile` dosyasına koyun. Grafik ortam girişlerinden ve `cron` işlerinden başlattığınız kabuklar için ayrı yapılandırma gerekecektir.

- Yapılandırma dosyalarınızı (örneğin `.bashrc` ve `.bash_profile`) Git ile çeşitli bilgisayarlar arasında senkronize edin.

- Değişkenler ve dosya adları boşluk içerdiğinde dikkatli olunması gerektiğini anlayın. Bash değişkenlerinizi tırnak işaretleri ile çevreleyin, örneğin `"$FOO"`. Boş karakterlerin dosya adlarını sınırlandırmasını sağlamak için `-0` veya `-print0` seçeneklerini tercih edin, örneğin `locate -0 pattern | xargs -0 ls -al` veya `find / -print0 -type d | xargs -0 ls -al`. Bir for döngüsünde boşluk içeren dosya adlarını yinelemek için, IFS'nizi yalnızca `IFS=$'\n'` kullanarak bir satırbaşı olacak şekilde ayarlayın.

- Bash betiklerinde, hata ayıklama çıktısı için `set -x` (veya genişletilmemiş değişkenler ve yorumlar dahil olmak üzere ham girdiyi kütüğe kaydeden (loglayan) `set -v` varyantını) kullanın. İyi bir nedeniniz olmadığı sürece katı modları kullanın: Hatalarda (sıfır olmayan çıkış kodu) iptal etmek için `set -e` kullanın. Ayarlanmamış değişken kullanımlarını tespit etmek için `set -u` kullanın. Borulardaki hatalarda iptal etmek için `set -o pipefail` seçeneğini de göz önünde bulundurun (bu konu biraz incelikli olduğu için daha fazla bilgi edinin). Daha karmaşık betikler için EXIT veya ERR'de `trap` kullanın. Yararlı bir alışkanlık, bunun gibi bir betik başlatmaktır; bu, yaygın hataları algılayıp iptal etmesini ve bir mesaj yazdırmasını sağlar:
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- Bash betiklerinde, alt kabuklar (parantezlerle yazılır) komutları gruplamak için uygun yollardır. Yaygın bir örnek, geçici olarak farklı bir çalışma dizinine geçmektir, örn.
```bash
      # mevcut dizinde bir sey yap
      (cd /some/other/dir && other-command)
      # orijinal dizinde devam et
```

- Bash'te birçok değişken genişletme türü olduğunu unutmayın. Bir değişkenin var olup olmadığını kontrol etme: `${name:?error message}`. Örneğin, bir Bash betiği tek bir argüman gerektiriyorsa, sadece `input_file=${1:?usage: $0 input_file}` yazmanız yeterlidir. Bir değişken boşsa varsayılan bir değer kullanmak: `${name:-default}`. Önceki örneğe ek (isteğe bağlı) bir parametre eklemek istiyorsanız, `output_file=${2:-logfile}` gibi bir şey kullanabilirsiniz. Eğer `$2` atlanır ve dolayısıyla boş bırakılırsa, `output_file` `logfile` olarak ayarlanacaktır. Aritmetik genişletme: `i=$(( (i + 1) % 5 ))`. Diziler: `{1..10}`. Dizelerin kırpılması: `${var%suffix}` ve `${var#prefix}`. Örneğin `var=foo.pdf` ise, `echo ${var%.pdf}.txt`, `foo.txt` yazdırır.

- `{`...`}` kullanarak ayraç genişletme, benzer metni yeniden yazmak zorunda kalmayı azaltabilir ve öğe kombinasyonlarını otomatikleştirebilir.  Bu, `mv foo.{txt,pdf} some-dir` (her iki dosyayı da taşır), `cp somefile{,.bak}` (`cp somefile somefile.bak` olarak genişler) veya `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (tüm olası kombinasyonları genişletir ve bir dizin ağacı oluşturur) gibi örneklerde yararlıdır. Ayraç genişletme işlemi diğer genişletme işlemlerinden önce gerçekleştirilir.

- Genişletmelerin sırası şöyledir: ayraç genişletme; tilde genişletme, parametre ve değişken genişletme, aritmetik genişletme ve komut ikamesi (soldan sağa doğru yapılır); kelime bölme; ve dosya adı genişletme. (Örneğin, `{1..20}` gibi bir aralık `{$a..$b}` kullanılarak değişkenlerle ifade edilemez. Bunun yerine `seq` veya `for` döngüsü kullanın, örneğin, `seq $a $b` veya `for((i=a; i<=b; i++)); do ... ; done`.)

- Bir komutun çıktısı `<(some command)` (process substitution olarak bilinir) aracılığıyla bir dosya gibi ele alınabilir. Örneğin, yerel `/etc/hosts` dosyasını uzaktaki bir dosya ile karşılaştırın:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Komut dosyaları yazarken tüm kodunuzu küme parantezleri içine almak isteyebilirsiniz. Kapanış parantezi eksikse, bir sözdizimi hatası nedeniyle kodunuzun yürütülmesi engellenecektir. Bu, betiğiniz web'den indirilecekse mantıklıdır, çünkü kısmen indirilmiş betiklerin yürütülmesini önler:
```bash
{
      # Sizin kodunuz
}
```

- Bir "here document" [birden fazla girdi satırının yeniden yönlendirilmesine](https://www.tldp.org/LDP/abs/html/here-docs.html) bir dosyadan geliyormuş gibi izin verir:
```
cat <<EOF
input
on multiple lines
EOF
```

- Bash'te hem standart çıktıyı hem de standart hatayı şu yolla yönlendirin: `some-command >logfile 2>&1` veya `some-command &>logfile`. Genellikle, bir komutun standart girdiye açık bir dosya tanıtıcısı bırakmadığından emin olmak için, onu bulunduğunuz terminale bağlayarak, `</dev/null` eklemek de iyi bir uygulamadır.

- Onaltılık ve ondalık değerlerle iyi bir ASCII tablosu için `man ascii` kullanın. Genel kodlama (encoding) bilgisi için `man unicode`, `man utf-8` ve `man latin1` yardımcı olur.

- Ekranı çoğullamak için `screen` veya [`tmux`](https://tmux.github.io/) kullanın, özellikle uzak ssh oturumlarında ve bir oturumu ayırmak ve yeniden bağlamak için kullanışlıdır. `byobu` daha fazla bilgi ve daha kolay yönetim sağlayarak ekranı veya tmux'ı geliştirebilir. Sadece oturum kalıcılığı için daha minimal bir alternatif [`dtach`](https://github.com/bogner/dtach).

- Ssh'de, `-L` veya `-D` (ve bazen `-R`) ile nasıl port tüneli yapılacağını bilmek, örneğin uzak (remote) sunucudan web sitelerine erişmek için yararlıdır.

- Ssh yapılandırmanızda birkaç optimizasyon yapmak yararlı olabilir; örneğin, bu `~/.ssh/config` belirli ağ ortamlarında bağlantıların düşmesini önlemek için ayarlar içerir, sıkıştırma kullanır (düşük bant genişliğine sahip bağlantılarda scp ile yararlıdır) ve yerel bir kontrol dosyası ile aynı sunucuya kanalları çoğaltır:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Ssh ile ilgili diğer birkaç seçenek güvenlik açısından hassastır ve dikkatli bir şekilde etkinleştirilmelidir. Örneğin alt ağ veya ana bilgisayar başına veya güvenilir ağlarda: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- UDP kullanan, düşen bağlantılardan kaçınan ve işlem sırasında kolaylık sağlayan bir ssh alternatifi olarak [`mosh`](https://mosh.mit.edu/)'u düşünün (sunucu tarafı kurulumu gerektirir).

- Sistem yapılandırması için yararlı olan ancak `ls`de bulunmayan ve karıştırılması kolay olan sekizli formdaki bir dosyadaki izinleri almak için aşağıdaki gibi bir şey kullanın
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Başka bir komutun çıktısından etkileşimli değer seçimi için [`percol`](https://github.com/mooz/percol) veya [`fzf`](https://github.com/junegunn/fzf) kullanın.

- Başka bir komutun çıktısına dayalı olarak dosyalarla etkileşim için (`git` gibi), `fpp` ([PathPicker](https://github.com/facebook/PathPicker)) kullanın.

- Geçerli dizindeki (ve alt dizinlerdeki) tüm dosyalar için basit bir web sunucusu için, ağınızdaki herkes tarafından kullanılabilir, kullanın:
`python -m SimpleHTTPServer 7777` (7777 portu ve Python 2 için) ve `python -m http.server 7777` (7777 portu ve Python 3 için).

- Bir komutu başka bir kullanıcı olarak çalıştırmak için `sudo` kullanın. Varsayılan olarak root olarak çalışır; başka bir kullanıcı belirtmek için `-u` kullanın. Bu kullanıcı olarak oturum açmak için `-i` kullanın (_sizin_ parolanız sorulacaktır).

- Kabuğu başka bir kullanıcıya geçirmek için `su kullanıcıadı` veya `su - kullanıcıadı` kullanın. İkincisi "-" ile sanki başka bir kullanıcı giriş yapmış gibi bir ortam oluşturur. Kullanıcı adı atlandığında varsayılan olarak root kullanılır. _Geçiş yaptığınız kullanıcının_ parolası sorulacaktır.

- Komut satırlarındaki [128K sınırı](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong) hakkında bilgi edinin. Bu "Argüman listesi çok uzun" hatası, çok sayıda dosyayı joker karakterle eşleştirirken yaygındır. (Bu olduğunda `find` ve `xargs` gibi alternatifler yardımcı olabilir).

- Temel bir hesap makinesi için (ve tabii ki genel olarak Python'a erişim için) `python` yorumlayıcısını kullanın. Örneğin,
```
>>> 2+3
5
```


## Dosyaların ve verilerin işlenmesi

- Geçerli dizinde bir dosyayı ismine göre bulmak için, `find . -iname '*something*'` (veya benzeri). Herhangi bir yerdeki bir dosyayı ismiyle bulmak için `locate something` kullanın (ancak `updatedb`nin yakın zamanda oluşturulmuş dosyaları indekslememiş olabileceğini unutmayın).

- Kaynak veya veri dosyalarında genel arama yapmak için, `grep -r`den daha gelişmiş veya daha hızlı birkaç seçenek vardır (kabaca eskiden yeniye doğru) [`ack`](https://github.com/beyondgrep/ack2), [`ag`](https://github.com/ggreer/the_silver_searcher) ("the silver searcher") ve [`rg`](https://github.com/BurntSushi/ripgrep) (ripgrep).

- HTML'yi metne dönüştürmek için: `lynx -dump -stdin`

- Markdown, HTML ve her türlü belge dönüştürme işlemi için [`pandoc`](http://pandoc.org/) adresini deneyin. Örneğin, bir Markdown belgesini Word biçimine dönüştürmek için: `pandoc README.md --from markdown --to docx -o temp.docx`

- Eğer XML ile uğraşmanız gerekiyorsa, `xmlstarlet` eski ama iyidir.

- JSON için [`jq`](http://stedolan.github.io/jq/) kullanın. Etkileşimli kullanım için ayrıca [`jid`](https://github.com/simeji/jid) ve [`jiq`](https://github.com/fiatjaf/jiq) adreslerine bakın.

- YAML için [`shyaml`](https://github.com/0k/shyaml) kullanın.

- Excel veya CSV dosyaları için, [csvkit](https://github.com/onyxfish/csvkit) `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, vb. (komutlarını) sağlar.

- Amazon S3 için [`s3cmd`](https://github.com/s3tools/s3cmd) kullanışlıdır ve [`s4cmd`](https://github.com/bloomreach/s4cmd) daha hızlıdır. Amazon'un [`aws`](https://github.com/aws/aws-cli) ve daha geliştirilmiş [`saws`](https://github.com/donnemartin/saws) AWS ile ilgili diğer görevler için gereklidir.

- uniq'in `-u` ve `-d` seçenekleri de dahil olmak üzere `sort` ve `uniq` hakkında bilgi sahibi olun - aşağıdaki tek satırlık kodlara bakın. Ayrıca `comm` seçeneğine de bakın.

- Metin dosyalarını işlemek için `cut`, `paste` ve `join` hakkında bilgi sahibi olun. Birçok kişi `cut` kullanır ama `join` komutunu unutur.

- `wc` ile Yeni satırları (`-l`), karakterleri (`-m`), kelimeleri (`-w`) ve baytları (`-c`) saymak için `wc` hakkında bilgi sahibi olun.

- stdin`den bir dosyaya ve ayrıca stdout`a kopyalamak için `tee` hakkında bilgi edinin, `ls -al | tee file.txt` gibi.

- Gruplama, alanları tersine çevirme ve istatistiksel hesaplamalar dahil olmak üzere daha karmaşık hesaplamalar için [`datamash`](https://www.gnu.org/software/datamash/)'i düşünün.

- Yerel ayarın, sıralama düzeni (collation) ve performans dahil olmak üzere birçok komut satırı aracını ince şekillerde etkilediğini bilin. Çoğu Linux kurulumu `LANG` veya diğer yerel ayar değişkenlerini ABD İngilizcesi gibi yerel bir ayara ayarlayacaktır. Ancak yerel ayarı değiştirirseniz sıralamanın değişeceğini unutmayın. Ve i18n rutinlerinin sıralama ya da diğer komutların *birçok kez* daha yavaş çalışmasına neden olabileceğini bilin. Bazı durumlarda (aşağıdaki set işlemleri veya benzersizlik işlemleri gibi) yavaş i18n rutinlerini tamamen göz ardı edebilir ve `export LC_ALL=C` kullanarak geleneksel bayt tabanlı sıralama düzenini kullanabilirsiniz.

- Belirli bir komutun ortamını, `TZ=Pacific/Fiji date` komutunda olduğu gibi, komutun çağrılmasının önüne ortam değişkeni ayarlarını ekleyerek ayarlayabilirsiniz.

- Basit veri munging için temel `awk` ve `sed` bilin. Örnekler için [Tek satırlık kodlar](#tek-satırlık-kodlar) bölümüne bakın.

- Bir veya daha fazla dosyada bir dizenin tüm oluşumlarını yerinde değiştirmek için:
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- Birden fazla dosyayı yeniden adlandırmak ve/veya dosyalar içinde arama ve değiştirme yapmak için [`repren`](https://github.com/jlevy/repren) komutunu deneyin. (Bazı durumlarda `rename` komutu da çoklu yeniden adlandırmaya izin verir, ancak işlevselliği tüm Linux dağıtımlarında aynı olmadığından dikkatli olun).
```sh
      # Dosya adlarının, dizinlerin ve içeriklerin tam yeniden adlandırılması foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # whatever.bak -> whatever yedek dosyalarını kurtarın:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # usttekiyle ayni ve uygunsa, rename kullanimi:
      rename 's/\.bak$//' *.bak
```

- Man sayfasında belirtildiği gibi, `rsync` gerçekten hızlı ve olağanüstü çok yönlü bir dosya kopyalama aracıdır. Makineler arasında senkronizasyon için bilinir ancak yerel olarak da aynı derecede kullanışlıdır. Güvenlik kısıtlamaları izin verdiğinde, `scp` yerine `rsync` kullanmak, sıfırdan başlamadan bir aktarımın kurtarılmasını sağlar. Ayrıca çok sayıda dosyayı silmek için [en hızlı yollar](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) arasındadır:
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Dosyaları işlerken ilerlemeyi izlemek için [`pv`](http://www.ivarch.com/programs/pv.shtml), [`pycp`](https://github.com/dmerejkowsky/pycp), [`pmonitor`](https://github.com/dspinellis/pmonitor), [`progress`](https://github.com/Xfennec/progress), `rsync --progress` veya blok düzeyinde kopyalama için `dd status=progress` kullanın.

- Bir dosyadan rastgele satırları karıştırmak veya seçmek için `shuf` kullanın.

- `sort`'un seçeneklerini bilin. Sayılar için `-n` veya insan tarafından okunabilir sayıları işlemek için `-h` kullanın (örneğin `du -h` ile). Anahtarların nasıl çalıştığını bilin (`-t` ve `-k`). Özellikle, sadece ilk alana göre sıralamak için `-k1,1` yazmanız gerektiğine dikkat edin; `-k1` tüm satıra göre sıralama anlamına gelir. Kararlı sıralama (`sort -s`) yararlı olabilir. Örneğin, önce 2. alana göre, sonra ikincil olarak 1. alana göre sıralamak için `sort -k1,1 | sort -s -k2,2` kullanabilirsiniz.

- Bash'te bir komut satırında bir sekme değişmezi yazmanız gerekirse (örneğin, sıralamak için -t argümanı için), **ctrl-v** **[Tab]** tuşlarına basın veya `$'\t'` yazın (ikincisi kopyalayıp yapıştırabileceğiniz için daha iyidir).

- Kaynak kodu yamalamak için standart araçlar `diff` ve `patch`tir. Bir diff'in özet istatistikleri için `diffstat` ve yan yana fark için `sdiff` araçlarına da bakınız. Not `diff -r` tüm dizinler için çalışır. Değişikliklerin bir özeti için `diff -r tree1 tree2 | diffstat` kullanın. Dosyaları karşılaştırmak ve düzenlemek için `vimdiff` kullanın.

- İkili dosyalar için, basit hex dökümleri için `hd`, `hexdump` veya `xxd` ve ikili düzenleme için `bvi`, `hexedit` veya `biew` kullanın.

- Ayrıca ikili dosyalar için `strings` (artı `grep`, vb.) metin parçalarını bulmanızı sağlar.

- İkili farklar (delta sıkıştırma) için `xdelta3` kullanın.

- Metin kodlamalarını dönüştürmek için `iconv`yi deneyin. Veya daha gelişmiş kullanım için `uconv`; bazı gelişmiş Unicode şeylerini destekler. Örneğin:
```sh
      # Karakterlerin hex kodlarını veya gerçek adlarını görüntüler (hata ayıklama için kullanışlıdır):
      uconv -f utf-8 -t utf-8 -x '::Any-Hex;' < input.txt
      uconv -f utf-8 -t utf-8 -x '::Any-Name;' < input.txt
      # Küçük harf ve tüm aksanları kaldırır (genişletip bırakarak):
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC;' < input.txt > output.txt
```

- Dosyaları parçalara ayırmak için `split` (boyuta göre bölmek için) ve `csplit` (bir desene göre bölmek için) seçeneklerine bakın.

- Tarih ve saat: Geçerli tarih ve saati yararlı [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) biçiminde almak için `date -u +"%Y-%m-%dT%H:%M:%SZ"` kullanın (diğer seçenekler [ise](https://stackoverflow.com/questions/7216358/date-command-on-os-x-doesnt-have-iso-8601-i-option) [problemli](https://unix.stackexchange.com/questions/164826/date-command-iso-8601-option)). Tarih ve saat ifadelerini işlemek için [`dateutils`](http://www.fresse.org/dateutils/) adresinden `dateadd`, `datediff`, `strptime` vb. kullanın.

- Sıkıştırılmış dosyalar üzerinde işlem yapmak için `zless`, `zmore`, `zcat` ve `zgrep` kullanın.

- Dosya nitelikleri `chattr` aracılığıyla ayarlanabilir ve dosya izinlerine daha düşük seviyeli bir alternatif sunar. Örneğin, dosyanın yanlışlıkla silinmesine karşı koruma sağlamak için değişmez bayrağı: `sudo chattr +i /critical/directory/or/file`

- Dosya izinlerini kaydetmek ve geri yüklemek için `getfacl` ve `setfacl` kullanın. Örneğin:
```sh
   getfacl -R /some/path > permissions.txt
   setfacl --restore=permissions.txt
```

- Hızlı bir şekilde boş dosyalar oluşturmak için `truncate` ([sparse file](https://en.wikipedia.org/wiki/Sparse_file) oluşturur), `fallocate` (ext4, xfs, btrfs ve ocfs2 dosya sistemleri), `xfs_mkfile` (neredeyse tüm dosya sistemleri, xfsprogs paketinde gelir), `mkfile` (Solaris, Mac OS gibi Unix benzeri sistemler için) kullanın.

## Sistem hata ayıklama

- Web hata ayıklama için `curl` ve `curl -I` ya da `wget` eşdeğerleri ya da daha modern [`httpie`](https://github.com/jkbrzt/httpie) kullanışlıdır.

- Mevcut cpu/disk durumunu öğrenmek için klasik araçlar `top` (ya da daha iyisi `htop`), `iostat` ve `iotop`tur. Temel CPU ve bölüm başına ayrıntılı disk istatistikleri ve performans bilgisi için `iostat -mxz 15` kullanın.

- Ağ bağlantısı detayları için `netstat` ve `ss` kullanın.

- Bir sistemde neler olup bittiğine hızlı bir genel bakış için `dstat` özellikle yararlıdır. Ayrıntılarla birlikte en geniş genel bakış için [`glances`](https://github.com/nicolargo/glances) kullanın.

- Bellek durumunu öğrenmek için `free` ve `vmstat` çalıştırın ve çıktılarını anlayın. Özellikle, "cached" değerinin Linux çekirdeği tarafından dosya önbelleği olarak tutulan bellek olduğunu unutmayın, bu nedenle "free" değerine doğru etkili bir şekilde sayılır.

- Java sistem hata ayıklaması farklı bir konudur, ancak Oracle'ın ve diğer bazı JVM'lerin basit bir hilesi `kill -3 <pid>` komutunu çalıştırabilmeniz ve tam bir yığın izi ve yığın özetinin (oldukça bilgilendirici olabilen nesilsel çöp toplama ayrıntıları dahil) stderr/log'lara dökülmesidir. JDK'nın `jps`, `jstat`, `jstack`, `jmap` araçları kullanışlıdır. [SJK araçları](https://github.com/aragozin/jvm-tools) daha gelişmiştir.

- Ağ sorunlarını tanımlamak için daha iyi bir traceroute olarak [`mtr`](http://www.bitwizard.nl/mtr/) kullanın.

- Bir diskin neden dolu olduğuna bakmak için [`ncdu`](https://dev.yorhel.nl/ncdu), `du -sh *` gibi normal komutlara göre zaman kazandırır.

- Hangi soketin ya da sürecin bant genişliğini kullandığını bulmak için [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) ya da [`nethogs`](https://github.com/raboof/nethogs) komutlarını deneyin.

- Apache ile birlikte gelen `ab` aracı web sunucusunun performansını hızlı ve kolay bir şekilde kontrol etmek için faydalıdır. Daha karmaşık yük testleri için `siege` aracını deneyin.

- Daha ciddi ağ hata ayıklaması için [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html) veya [`ngrep`](http://ngrep.sourceforge.net/).

- `strace` ve `ltrace` hakkında bilgi sahibi olun. Bunlar, bir program başarısız oluyor, takılıyor veya çöküyorsa ve nedenini bilmiyorsanız veya performans hakkında genel bir fikir edinmek istiyorsanız yardımcı olabilir. Profil oluşturma seçeneğine (`-c`) ve çalışan bir sürece bağlanma yeteneğine (`-p`) dikkat edin. Önemli çağrıları kaçırmamak için trace child seçeneğini (`-f`) kullanın.

- Paylaşılan kütüphaneleri vb. kontrol etmek için `ldd` hakkında bilgi sahibi olun - ancak [asla güvenilmeyen dosyalar üzerinde çalıştırmayın] (http://www.catonmat.net/blog/ldd-arbitrary-code-execution/).

- Çalışan bir sürece `gdb` ile nasıl bağlanacağınızı ve yığın izlerini nasıl alacağınızı bilin.

- `/proc` kullanın. Bazen canlı sorunlarda hata ayıklarken inanılmaz derecede yardımcı olur. Örnekler: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (burada `xxx` süreç id'si veya pid'dir).

- Geçmişte bir şeyin neden yanlış gittiğini ayıklarken, [`sar`](http://sebastien.godard.pagesperso-orange.fr/) çok yardımcı olabilir. CPU, bellek, ağ vb. ile ilgili geçmiş istatistikleri gösterir.

- Daha derin sistem ve performans analizleri için `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_%28Linux%29) ve [`sysdig`](https://github.com/draios/sysdig)'e bakın.

- Hangi işletim sisteminde olduğunuzu `uname` veya `uname -a` (genel Unix/çekirdek bilgisi) veya `lsb_release -a` (Linux dağıtım bilgisi) ile kontrol edin.

- Bir şey gerçekten garip davrandığında `dmesg` kullanın (donanım veya sürücü sorunları olabilir).

- Eğer bir dosyayı silerseniz ve `du` tarafından bildirildiği gibi beklenen disk alanı boşalmazsa, dosyanın bir işlem tarafından kullanılıp kullanılmadığını kontrol edin:
`lsof | grep deleted | grep "benim-buyuk-dosyamin-adi"`


## Tek satırlık kodlar

Komutları bir araya getirmek için birkaç örnek:

- Bazen `sort`/`uniq` aracılığıyla metin dosyalarının kesişimini, birleşimini ve farkını ayarlayabilmeniz oldukça yararlıdır. Diyelim ki `a` ve `b` zaten benzersiz olan metin dosyaları. Bu hızlıdır ve birçok gigabayta kadar rastgele boyuttaki dosyalar üzerinde çalışır. (Sıralama bellekle sınırlı değildir, ancak `/tmp` küçük bir kök bölüm üzerindeyse `-T` seçeneğini kullanmanız gerekebilir). Ayrıca yukarıdaki `LC_ALL` ile ilgili nota ve `sort`un `-u` seçeneğine (aşağıda açıklık için atlanmıştır) bakın.
```sh
      sort a b | uniq > c   # c, a birleşimidir b
      sort a b | uniq -d > c   # c, a kesişim b
      sort a b b | uniq -u > c   # c, a küme farkı b
```

- İki JSON dosyasını güzel bir şekilde yazdırın, sözdizimlerini normalleştirin, ardından sonucu renklendirin ve sayfalandırın:
```
      diff <(jq --sort-keys . < file1.json) <(jq --sort-keys . < file2.json) | colordiff | less -R
```

- Bir dizindeki tüm dosyaların içeriğini hızlıca incelemek için `grep . *` (böylece her satır dosya adıyla eşleştirilir) veya `head -100 *` (böylece her dosyanın bir başlığı vardır) kullanın. Bu, `/sys`, `/proc`, `/etc` gibi yapılandırma ayarlarıyla dolu dizinler için yararlı olabilir.


- Bir metin dosyasının üçüncü sütunundaki tüm sayıları toplamak (bu muhtemelen eşdeğer Python'dan 3 kat daha hızlı ve 3 kat daha az koddur):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- Bir dosya ağacındaki boyutları/tarihleri görmek için, bu özyinelemeli bir `ls -l` gibidir, ancak `ls -lR` komutundan daha kolay okunur:
```sh
      find . -type f -ls
```

- Bir web sunucusu günlüğü gibi bir metin dosyanız ve URL'de bulunan bir `acct_id` parametresi gibi bazı satırlarda görünen belirli bir değeriniz olduğunu varsayalım. Her bir `acct_id` için kaç istek yapıldığına dair bir çetele istiyorsanız:
```sh
      egrep -o 'acct_id=[0-9]+' access.log | cut -d= -f2 | sort | uniq -c | sort -rn
```

- Değişiklikleri sürekli olarak izlemek için `watch` kullanın, örneğin `watch -d -n 2 'ls -rtlh | tail'` ile bir dizindeki dosyalarda veya `watch -d -n 2 ifconfig` ile wifi ayarlarınızda sorun giderirken ağ ayarlarında yapılan değişiklikleri kontrol edin.

- Bu belgeden rastgele bir ipucu almak için bu işlevi çalıştırın (Markdown'u ayrıştırır ve bir öğeyi çıkarır):
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


## Anlaması güç ama kullanışlı

- `expr`: aritmetik veya mantıksal (boolean) işlemleri gerçekleştirir veya düzenli ifadeleri (regular expressions) değerlendirir

- `m4`: basit makro işlemci

- `yes`: bir dizeyi çok yazdırır

- `cal`: güzel takvim

- `env`: bir komut çalıştırır (komut dosyalarında kullanışlıdır)

- `printenv`: ortam değişkenlerini yazdırır (hata ayıklama ve komut dosyalarında kullanışlıdır)

- `look`: bir dizeyle başlayan İngilizce sözcükleri (veya bir dosyadaki satırları) bulur

- `cut`, `paste` ve `join`: veri manipülasyonu

- `fmt`: metin paragraflarını biçimlendir

- `pr`: metni sayfalar/sütunlar halinde biçimlendirir

- `fold`: metin satırlarını sarar

- column`: metin alanlarını hizalanmış, sabit genişlikte sütunlar veya tablolar halinde biçimlendirir

- `expand` ve `unexpand`: sekmeler ve boşluklar arasında dönüştürme

- `nl`: satır numaralarını ekle

- `seq`: sayıları yazdır

- `bc`: hesap makinesi

- `factor`: faktör tamsayıları

- [`gpg`](https://gnupg.org/): dosyaları şifreleyin ve imzalayın

- `toe`: terminfo girdileri tablosu

- `nc`: ağ hata ayıklama ve veri aktarımı

- `socat`: soket aktarıcı ve tcp port iletici (`netcat` benzeri)

- [`slurm`](https://github.com/mattthias/slurm): ağ trafiği görselleştirme

- `dd`: dosyalar veya cihazlar arasında veri taşıma

- `file`: bir dosyanın türünü tanımlar

- `tree`: dizinleri ve alt dizinleri iç içe geçmiş bir ağaç olarak görüntüler; `ls` gibi ama özyinelemeli

- `stat`: dosya bilgisi

- `time`: bir komutu çalıştırın ve zamanlayın

- `timeout`: bir komutu belirtilen süre boyunca çalıştırır ve belirtilen süre tamamlandığında işlemi durdurur.

- `lockfile`: sadece `rm -f` tarafından kaldırılabilen semafor dosyası oluşturur.

- `logrotate`: günlükleri döndürür, sıkıştırır ve postalar.

- `watch`: bir komutu tekrar tekrar çalıştırarak sonuçları gösterir ve/veya değişiklikleri vurgular

- [`when-changed`](https://github.com/joh/when-changed): dosya değişikliği gördüğünde belirttiğiniz herhangi bir komutu çalıştırır. Ayrıca `inotifywait` ve `entr` komutlarına da bakınız.

- `tac`: dosyaları tersten yazdırır

- `comm`: sıralanmış dosyaları satır satır karşılaştırın

- `strings`: ikili dosyalardan metin ayıklama

- `tr`: karakter çevirisi veya manipülasyonu

- `iconv` veya `uconv`: metin kodlamaları için dönüştürme

- `split` ve `csplit`: dosyaları bölme

- `sponge`: yazmadan önce tüm girdiyi okur, aynı dosyadan okuyup sonra aynı dosyaya yazmak için kullanışlıdır, örneğin, `grep -v something some-file | sponge some-file`

- `units`: birim dönüşümleri ve hesaplamaları; iki haftada bir furlong'u göz kırpma başına twips'e dönüştürür (ayrıca bkz. `/usr/share/units/definitions.units`)

- `apg`: rastgele parolalar üretir

- `xz`: yüksek oranlı dosya sıkıştırma

- `ldd`: dinamik kütüphane bilgisi

- `nm`: nesne dosyalarından semboller

- `ab` veya [`wrk`](https://github.com/wg/wrk): web sunucularını kıyaslama

- `strace`: sistem çağrısı hata ayıklama

- [`mtr`](http://www.bitwizard.nl/mtr/): ağ hata ayıklama için daha iyi traceroute

- `cssh`: görsel eşzamanlı kabuk

- `rsync`: SSH üzerinden veya yerel dosya sistemindeki dosya ve klasörleri senkronize edin

- [`wireshark`](https://wireshark.org/) ve [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): paket yakalama ve ağ hata ayıklama

- [`ngrep`](http://ngrep.sourceforge.net/): ağ katmanı için grep

- `host` ve `dig`: DNS aramaları

- `lsof`: işlem dosyası tanımlayıcısı ve soket bilgisi

- `dstat`: yararlı sistem istatistikleri

- [`glances`](https://github.com/nicolargo/glances): üst düzey, çoklu alt sisteme genel bakış

- `iostat`: Disk kullanım istatistikleri

- `mpstat`: CPU kullanım istatistikleri

- `vmstat`: Bellek kullanım istatistikleri

- `htop`: top`un geliştirilmiş versiyonu

- `last`: giriş geçmişi

- `w`: kim oturum açtı

- `id`: kullanıcı/grup kimlik bilgisi

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): geçmiş sistem istatistikleri

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) veya [`nethogs`](https://github.com/raboof/nethogs): soket veya işleme göre ağ kullanımı

- `ss`: soket istatistikleri

- `dmesg`: önyükleme ve sistem hata mesajları

- `sysctl`: Linux çekirdek parametrelerini çalışma zamanında görüntüleme ve yapılandırma

- `hdparm`: SATA/ATA disk manipülasyonu/performansı

- `lsblk`: blok aygıtlarını listele: disklerinizin ve disk bölümlerinizin ağaç görünümü

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: CPU, BIOS, RAID, grafikler, aygıtlar vb. dahil olmak üzere donanım bilgileri.

- `lsmod` ve `modinfo`: Çekirdek modüllerinin ayrıntılarını listeler ve gösterir.

- `fortune`, `ddate` ve `sl`: um, şey, buharlı lokomotifleri ve Zippy alıntılarını "yararlı" olarak görüp görmediğinize bağlı


## Yalnızca macOS için

Bunlar *sadece* macOS ile ilgili öğelerdir.

- `brew` (Homebrew) ve/veya `port` (MacPorts) ile paket yönetimi. Bunlar yukarıdaki komutların çoğunu macOS'a yüklemek için kullanılabilir.

- Herhangi bir komutun çıktısını `pbcopy` ile bir masaüstü uygulamasına kopyalayın ve `pbpaste` ile bir komuttan gelen girdiyi yapıştırın.

- macOS Terminal'de Option tuşunu alt tuş olarak etkinleştirmek için (yukarıdaki komutlarda kullanılan **alt-b**, **alt-f**, vb. gibi), Tercihler -> Profiller -> Klavye'yi açın ve "Option'ı Meta tuşu olarak kullan "ı seçin.

- Bir masaüstü uygulamasıyla bir dosya açmak için `open` veya `open -a /Applications/Whatever.app` komutunu kullanın.

- Spotlight: Dosyaları `mdfind` ile arayın ve meta verileri (fotoğraf EXIF bilgileri gibi) `mdls` ile listeleyin.

- macOS'in BSD Unix tabanlı olduğunu ve birçok komutun (örneğin `ps`, `ls`, `tail`, `awk`, `sed`) büyük ölçüde System V tarzı Unix ve GNU araçlarından etkilenen Linux'tan birçok ince varyasyona sahip olduğunu unutmayın. Farkı genellikle bir man sayfasının "BSD Genel Komutlar Kılavuzu" başlığına sahip olmasına dikkat ederek anlayabilirsiniz. Bazı durumlarda GNU sürümleri de kurulabilir (GNU awk ve sed için `gawk` ve `gsed` gibi). Platformlar arası Bash komut dosyaları yazıyorsanız, bu tür komutlardan kaçının (örneğin, Python veya `perl` düşünün) veya dikkatlice test edin.

- macOS sürüm bilgilerini almak için `sw_vers` komutunu kullanın.

## Yalnızca Windows için

Bu öğeler *sadece* Windows ile ilgilidir.

### Windows altında Unix araçlarını edinme yolları

- [Cygwin](https://cygwin.com/) yükleyerek Microsoft Windows altında Unix kabuğunun gücüne erişin. Bu belgede açıklanan şeylerin çoğu direkt çalışacaktır.

- Windows 10'da, Unix komut satırı yardımcı programları ile tanıdık bir Bash ortamı sağlayan [Windows Subsystem for Linux (WSL)](https://msdn.microsoft.com/commandline/wsl/about) kullanabilirsiniz.

- Windows'ta esas olarak GNU geliştirici araçlarını (GCC gibi) kullanmak istiyorsanız, [MinGW](http://www.mingw.org/) ve bash, gawk, make ve grep gibi yardımcı programları sağlayan [MSYS](http://www.mingw.org/wiki/msys) paketini düşünün. MSYS, Cygwin ile karşılaştırıldığında tüm özelliklere sahip değildir. MinGW özellikle Unix araçlarının yerel Windows portlarını oluşturmak için kullanışlıdır.

- Windows altında Unix görünümü ve hissi elde etmek için başka bir seçenek de [Cash](https://github.com/dthree/cash). Bu ortamda sadece çok az Unix komutu ve komut satırı seçeneğinin mevcut olduğunu unutmayın.

### Yararlı Windows komut satırı araçları

- `wmic` öğrenerek ve kullanarak Windows sistem yönetimi görevlerinin çoğunu komut satırından gerçekleştirebilir ve komut dosyası oluşturabilirsiniz.

- Yararlı bulabileceğiniz native komut satırı Windows ağ araçları arasında `ping`, `ipconfig`, `tracert` ve `netstat` bulunur.

- `Rundll32` komutunu çağırarak [birçok yararlı Windows görevini](http://www.thewindowsclub.com/rundll32-shortcut-commands-windows) gerçekleştirebilirsiniz.

### Cygwin ipuçları ve püf noktaları

- Cygwin'in paket yöneticisi ile ek Unix programları yükleyin.

- Komut satırı pencereniz olarak `mintty` kullanın.

- Windows panosuna `/dev/clipboard` aracılığıyla erişin.

- Kayıtlı uygulaması aracılığıyla rastgele bir dosya açmak için `cygstart` çalıştırın.

- Windows kayıt defterine `regtool` ile erişin.

- Bir `C:\` Windows sürücü yolunun Cygwin altında `/cygdrive/c` haline geldiğini ve Cygwin'in `/` Windows'ta `C:\cygwin` altında göründüğünü unutmayın. Cygwin ve Windows tarzı dosya yolları arasında `cygpath` ile dönüşüm yapın. Bu en çok Windows programlarını çağıran betiklerde kullanışlıdır.

## Daha fazla kaynak

- [awesome-shell](https://github.com/alebcay/awesome-shell): Kabuk araçları ve kaynaklarının derlenmiş bir listesi.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): macOS komut satırı için daha derinlemesine bir kılavuz.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) daha iyi kabuk komut dosyaları yazmak için.
- [shellcheck](https://github.com/koalaman/shellcheck): Bir kabuk betiği statik analiz aracı. Esasen, bash/sh/zsh için lint.
- [Shell'de Dosya Adları ve Yol Adları](http://www.dwheeler.com/essays/filenames-in-shell.html): Kabuk betiklerinde dosya adlarının doğru bir şekilde nasıl ele alınacağına dair üzücü derecede karmaşık ayrıntılar.
- [Komut Satırında Veri Bilimi](http://datascienceatthecommandline.com/#tools): Aynı adlı kitaptan veri bilimi yapmak için yararlı daha fazla komut ve araç

## Sorumluluk reddi

Çok küçük görevler dışında, kod başkalarının okuyabilmesi için yazılır. Güçle birlikte sorumluluk da gelir. Bash'te bir şeyi *yapabiliyor* olmanız, mutlaka yapmanız gerektiği anlamına gelmez! ;)


## Lisans

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

Bu çalışma [Creative Commons Attribution-ShareAlike 4.0 Uluslararası Lisansı](http://creativecommons.org/licenses/by-sa/4.0/) altında lisanslanmıştır.
