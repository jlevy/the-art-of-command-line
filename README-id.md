🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*

# Seni dalam Baris Perintah

[![Ajukan pertanyaan](https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg)](https://airtable.com/shrzMhx00YiIVAWJg)

[![Bergabung dengan obrolan di https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


- [Meta](#meta)
- [Dasar-dasar](#dasar-dasar)
- [Penggunaan sehari-hari](#penggunaan-sehari-hari)
- [Mengolah berkas dan data](#mengolah-berkas-dan-data)
- [Analisa Sistem](#analisa-sistem)
- [Perintah satu baris](#perintah-satu-baris)
- [Tidak penting tapi bermanfaat](#tidak-penting-tapi-bermanfaat)
- [Khusus OS X](#khusus-os-x)
- [Khusus Windows](#khusus-windows)
- [Bacaan lebih lanjut](#bacaan-lebih-lanjut)
- [Penyangkalan](#penyangkalan)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

Mahir dalam baris perintah merupakan keahlian yang sering diabaikan atau masih dianggap misteri, tapi hal tersebut dapat meningkatkan fleksibilitas dan produktivitas sebagai seorang teknisi secara jelas. Halaman ini merupakan kumpulan catatan dan tips dalam menggunakan baris perintah sebagaimana yang kita ketahui sangat berguna ketika bekerja pada sistem Linux. Beberapa merupakan tips dasar, dan beberapa cukup spesifik, terkini, atau yang jarang digunakan. Halaman ini tidak panjang, tetapi jika anda dapat menggunakan dan mengingat semua perintah yang ada pada halaman ini, berarti anda memiliki pengetahuan yang cukup luas.

Proyek ini merupakan hasil dari banyak [penulis dan penerjemah](AUTHORS.md).
Beberapa diantaranya [pertama kali](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[muncul](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
di [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
namun kemudian dialihkan ke GitHub, dimana banyak orang-orang yang lebih berbakat dari penulis awal telah membuat banyak penyempurnaan.
[**Silakan ajukan pertanyaan**](https://airtable.com/shrzMhx00YiIVAWJg) jika anda memiliki pertanyaan seputar perintah baris. [**Silakan berkontribusi**](/CONTRIBUTING.md) jika anda melihat ada kesalahan atau memiliki suatu ide yang lebih baik!

## Meta

Batasan masalah:

- Panduan ini ditujukan bagi pemula dan yang telah berpengalaman. Tujuan utamanya cukup *luas* (segala hal adalah penting), *spesifik* (memberikan contoh kongkrit dari kasus yang umum terjadi), dan *ringkas* (hindari hal yang tidak penting atau menyimpang yang dapat ditemukan). Setiap tip adalah penting dalam beberapa kondisi atau dapat menjadi pilihan alternatif.
- Ditulis untuk Linux, dengan pengecualian dari bagian "[Khusus OS X](#os-x-only)" and "[Khusus Windows](#windows-only)". Banyak yang menggunakan atau memasangnya dalam varian UNIX atau OS X lainnya (bahkan menggunakan Cygwin).
- Berfokus pada Bash interaktif, meskipun banyak tip yang dapat digunakan pada terminal lainnya dan skrip Bash secara umum.
- Mengandung perintah UNIX "standar" sebagaimana yang telah diketahui bahwa membutuhkan instalasi paket spesial -- selama dirasa cukup penting untuk diikut sertakan.

Catatan:

- Untuk menjaga tetap memungkinkan dalam satu halaman, materi tidak disertakan dengan referensi secara langsung. Anda cukup paham untuk mengetahui lebih detil mengenai penjelasan setiap perintah, misalnya menggunakan Google. Gunakan `apt-get`, `yum`, `dnf`, `pacman`, `pip` atau `brew` (seperlunya) untuk memasang program baru.
- Gunakan [Explainshell](http://explainshell.com/) untuk bantuan mengenai perintah, opsi, saluran, dan lain sebagainya.


## Dasar-dasar

- Pelajari dasar Bash. Sebenarnya dengan mengetikkan `man bash` anda bisa mengetahui semuanya; sangat mudah untuk dilakukan dan cukup singkat. Sebagai alternatif terminal dapat menjadi menyenangkan, tapi Bash lebih baik dan selalu tersedia (hanya mempelajari *only* zsh, fish, etc., ketika menggunakan laptop pribadi anda, membatasi anda dalam banyak situasi, seperti menggunakan server yang sudah ada).

- Pelajari setidaknya satu pengolah teks dengan baik. Secara ideal Vim (`vi`), yang mana merupakan pengolah teks berbasis terminal terbaik saat ini (meskipun anda menggunakan Emacs, sebuah IDE yang besar, atau pengolah teks modern yang unik sepanjang masa).

- Ketahui cara membaca dokumentasi dengan `man` (sebagai informasi tambahan, `man man` menampilkan daftar bagian dalam bentuk nomor, misalnya 1 adalah perintah-perintah "reguler", 5 adalah berkas-berkas atau aturan-aturan, dan 8 adalah untuk administrasi). Temukan halaman `man` dengan `apropos`. Ketahui bahwa beberapa perintah tidak dapat dijalankan secara langsung, kecuali bawaan dari Bash, dan anda dapat mencari bantuan mengenai hal tersebut dengan `help` dan `help -d`. Anda dapat mencari tahu apakah suatu perintah dapat dijalankan langsung, perintah bawaan atau sebuah alias dapat diketahui dengan `type perintah`.

- Pelajari tentang pengalihan hasil keluaran dan masukan menggunakan `>` dan `<` dan saluran menggunakan `|`. Ketahui bahwa `>` menimpa hasil keluaran dari sebuah berkas sedangkan `>>` menambahkan keluaran dibagian akhir dari berkas. Pelajari tentang `stdout` dan `stderr`.

- Pelajari tentang penyebaran berkas dengan `*` (dan mungkin `?` dan `[`...`]`) dan tanda petik dan perbedaan antara petik dua `"` dan petik sati `'`. (Penjelasan lebih lanjut pada penyebaran variabel dibawah.)

- Biasakan diri dengan pengelolaan tugas pada Bash: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, dan lain sebagainya.

- Ketahui tentang `ssh`, dan dasar autentikasi tanpa kata kunci, melalui `ssh-agent`, `ssh-add`, dan lain sebagainya.

- Dasar pengelolaan berkas: `ls` dan `ls -l` (pelajari juga maksud setiap kolom pada `ls -l`), `less`, `head`, `tail` dan `tail -f` (atau yang lebih baik, `less +F`), `ln` dan `ln -s` (pelajari perbedaan dan keuntungan menggunakan hard dan soft link), `chown`, `chmod`, `du` (untuk penjelasan singkat penggunaan disk: `du -hs *`). Untuk pengelolaan berkas sistem, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. Pelajari apa itu inode (`ls -i` atau `df -i`).

- Dasar pengelolaan jaringan: `ip` atau `ifconfig`, `dig`.

- Pelejari dan gunakan sistem pengelolaan kontrol versi, seperti `git`.

- Ketahui regular expression (regex) dengan baik, dan beberapa flags untuk `grep`/`egrep`. Flag `-i`, `-o`, `-v`, `-A`, `-B`, dan `-C` bermanfaat untuk dipelajari.

- Pelajari cara menggunakan `apt-get`, `yum`, `dnf` atau `pacman` (tergantung distro yang digunakan) untuk melakukan instalasi paket. Dan pastikan anda mempunyai `pip` untuk menginstall alat baris perintah berbasis Python (dibawah ini beberapa lebih mudah diinstall menggunakan `pip`).


## Penggunaan sehari-hari

- Dalam Bash, gunakan **Tab** untuk melengkapi secara otomatis suatu perintah atau daftar perintah yang tersedia dan **ctrl-r** untuk mencari riwayat perintah (setelah ditekan, ketikan kata kunci yang ingin dicari, tekan **ctrl-r** untuk berpindah antara perintah-perintah yang sesuai, tekan **Enter** untuk menjalankan perintah, atau menekan tanda panah kanan di keyboard).

- Dalam Bash, gunakan **ctrl-w** untuk untuk menghapus kata terakhir, dan **ctrl-u** untuk menghapus semua kata mulai dari baris pertama. Gunakan **alt-b** dan **alt-f** untuk memindahkan kata, **ctrl-a** untuk memindahkan kursor kebaris paling depan, **ctrl-e** untuk memindahkan kursor kebaris paling akhir, **ctrl-k** untuk menghentikan bagian akhir dari baris, **ctrl-l** untuk membersihkan layar tampilan. Lihat `man readline` untuk menampilkan semua kombinasi tombol yang ada dalam Bash. Ada cukup bnyak kombinasi. Contohnya **alt-.** berpindah melalui perintah sebelumnya, dan **alt-*** melebarkan glob.  

- Sebagai alternatif, jika anda lebih sendang menggunakan gaya kombinasi `vi`, gunakan `set -o vi` (dan `set -o emacs` untuk mengembalikan kepengaturan awal).

- Untuk mengelola perintah yang panjang, setelah melakukan pengaturan pengolah teks (sebagai contoh `export EDITOR=vim`), menekan kombinasi **ctrl-x** **ctrl-e** akan membuka perintah saat ini pada pengolah teks untuk melakukan pengelolaah secara langsung. Atau dalam gaya `vi`, **escape-v**.

- Untuk melihat perintah terakhir yang digunakan, `history`. Tambahkan `!n` dibagian akhir (dimana `n` merupakan jumlah perintah) untuk dijalankan kembali. Terdapat beberapa penyingkatan yang dapat digunakan, diantaranya yang paling sering digunakan `!$` untuk parameter terakhir dan `!!` untuk perintah terakhir (baca "HISTORY EXPANSION" pada halaman manual `man`). Bagaimanapun, sering digantikan dengan kombinasi **ctrl-r** dan **alt-.**.

- Pindah ke direktori home dengan `cd`. Akses berkas yang berada dibawah direktori home dengan awalan `~` (misalnya `~/.bashrc`). Dalam skrip `sh` direktori home dinyatakan dalam `$HOME`.

- Untuk kembali ke direktori sebelumnya: `cd -`.

- Jika dalam menulis perintah anda berubah fikiran, tekan **alt-#** untuk menambahkan `#` pada awal perintah untuk menjadikannya sebuah komentar (atau **ctrl-a**, **#**, **enter**). Selanjutnya anda dapat mengakses perintah tersebuh dikemudian dengan menggunakan `history`.

- Gunakan `xargs` (atau `parallel`). Sangat bagus. Anda dapat mengontrol berapa banyak item yang dapat dijalankan per-baris (`-L`) atau menjalankannya secara bersamaan (`-P`). Jika anda tidak yakin hal tersebut akan berjalan dengan baik, gunakan `xargs echo` terlebih dahulu. Atau `I{}` juga sangat bermanfaat. Contohnya:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` dapat membantu menampilkan daftar proses yang sedang berjalan.

- Gunakan `pgrep` dan `pkill` untuk mencari proses sinyal berdasarkan nama (`-f` juga cukup membantu).

- Pelajari jenis sinyal yang dapat dikirimkan ke proses. Contoh, untuk menunda sebuah proses, gunakan `kill -STOP [pid]`. Untuk daftar semua sinyal, lihat `man 7 signal`.

- Gunakan `nohup` atau `disown` untuk membuat proses tetap berjalan selamanya.

- Lihat kemana sebuah proses terhubung (listening) melalui `netstat -lntp` atau `ss -plat` (untuk TCP, gunakan `-u` untuk UDP).

- Lihat juga `lsoft` untuk membuka socket dan berkas.

- Lihat `uptime` atau `w` untuk mengetahui berapa sistem sudah berjalan (aktif).

- Gunakan `alias` untuk membuat jalan pintas untuk perintah-perintah yang sering digunakan. Misalnya, `alias ll='ls -latr'` akan menghasilkan alias `ll`.

- Menyimpan alias, pengaturan shell, dan fungsi yang sering digunakan di `~/.bashrc`, dan [atur shell untuk dibaca ketika login](http://superuser.com/a/183980/7106). Hal tersebut akan membuat pengaturan dapat berjalan disemua sesi.

- Letakkan pengaturan dari variabel sebagai perintah yang akan dijalankan ketika login di `~/.bash_profile`. Pisahkan konfigurasi yang dibutuhkan untuk menjalankan grafik login dan tugas-tugas `cron`.

- Singkronkan berkas konfigurasi (seperti `.bashrc` dan `.bash_profile`) pada banyak komputer dengan Git.

- Pahami bahwa dibutuhkan perhatian lebih ketika variabel dan nama berkas mengandung spasi. Batasi variabel Bash dengan tanda petik, misalnya `"$FOO"`. Sebaiknya gunakan opsi `-0` atau `-print0` untuk membuat karakter null dalam membatasi nama berkas, misalnya `locate -0 pattern | xargs -0 ls -al` atau `find / -print0 -type d | xargs -0 ls -al`.  Untuk membuat perulangan nama berkas yang mengandung spasi dalam `for`, atur IFS sebagai baris baru dengan `IFS=$'\n'` .

- Dalam skrip Bash, gunakan `set -x` (atau lainnya `set -v`, yang mana akan menamilkan raw masukan dalam log, termasuk variabel dan komentar) untuk keperluan debugging. Gunakan mode `strict` kecuali ada alasan lebih baik untuk tidak menggunakan `set -e` untuk membatalkan perintah ketika terjadi kesalahan (kode exit tidak 0). Gunakan `set -u` untuk mendeteksi variabel yang belum ditentukan tapi sudah digunakan. Pertimbangkan `set -o pipefail` juga, untuk kesalahan didalam saluran. Untuk skrip terkait, gunakan `trap` pada EXIT atau ERR. Disarankan untuk memulai dari skrip berikut, dimana akan mendeteksi dan membatalkan perintah ketika terjadi kesalahan tertentu kemudian menampilkannya dalam pesan:
```bash
      set -euo pipefail
      trap "echo 'Kesalahan: Skrip gagal: harap periksa kembali perintah yang anda masukkan'" ERR
```

- Dalam skrip Bash, bagian dalam shell (ditulis didalam tanda kurung) merupakan cara terbaik untuk menggabungkan perintah. Sebuah contoh yang sering digunakan adalah berpindah ke direktori kerja yang lain, contohnya:
```bash
      # melakukan sesuatu dalam direktori kerja saat ini
      (cd /direktori/kerja/lainnya && suatu-perintah)
      # melanjutkan pekerjaan dalam direktori yang sebenarnya
```

- Dalam Bash, ada banyak jenis dari pengembangan variabel. Memeriksa ketersediaan variabel: `$(nama_variabel:?pesan kesalahan)`. Sebagai contoh, jika skrip membutuhkan sebuah parameter, cukup menulis `berkas_masukan=$(1:?penggunaan: $0 berkas_masukan)`. Contoh dalam aritmatika: `i=$(( (i + 1) % 5 ))`. Urutan: `{1..10}`. Pemangkasan string: `${var%akhiran}` dan `${var#awalan}`. Sebagai contoh jika `var=foo.pdf`, maka `echo ${var%.pdf}.txt` akan menghasilkan `foo.txt`.

- Kurung kurawal `{`...`}` dapat mengurangi kesalahan dama mengetik teks yang sama dan membuat kombinasi dari banyak item secara otomatis. Ini sangat membantu misalnya dalam perintah `mv foo.{txt,pdf} suatu-direktori` (memindahkan kedua berkas sekaligus), `cp suatuberkas{,.bak}` (memiliki makna sama dengan `cp suatuberkas suatuberkas.bak`) atau `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (memiliki makna membuat semua kemungkinan kombinasi untuk struktur direktori).

- Keluaran dari perintah dapat diperlakukan sebagai sebuah berkas dengan `<(suatu perintah)`. Misalnya, membandingkan `/etc/hosts` yang ada pada lokal dengan server:
```sh
      diff /etc/hosts <(ssh suatuserver cat /etc/hosts)
```

- Ketika menulis skrip disarankan untuk membatasi semua kode dalam kurung kurawal. Jika penutuh kurung kurawal tidak ditemukan, skrip tidak dapat dijalankan karena terjadi kesalahan. Hal ini biasanya terjadi ketika mengunduh skrip dari web, kemungkinan beberapa bagian dari skrip yang telah diunduh sengaja ditulis untuk menghindari eksekusi:
```bash
{
      # Kode disini
}
```

- Ketahui tentang "here documents" dalam Bash dengan `cat <<EOF...`.

- Dalam Bash, arahkan keluaran standar dan kesalahan melalui: `suatu-perintah > berkaslog 2>&1` atau `suatu-perintah &>berkaslog`. Biasanya, untuk memastikan suatu perintah tidak meninggalkan berkas tetap terbuka setelah menerima masukan, coba pada terminal anda saat ini, merupakan hal baik untuk menambahkan `</dev/null`.

- Gunakan `man ascii` untuk melihan tabel ASCII, dengan nilai hex dan decimal. Untuk informasi umum mengenai unicode, `man unicode`, `man utf-8`, dan `man latin1` juga sangat berguna.

- Gunakan `screen` atau [`tmux`](https://tmux.github.io/) untuk tampilan multi layar, terutama sangat bermanfaat dalam sesi ssh, melepas dan menyambung kembali sebuah sesi. `byobu`
- Use `screen` or [`tmux`](https://tmux.github.io/) to multiplex the screen, especially useful on remote ssh sessions and to detach and re-attach to a session. `byobu` can enhance screen or tmux providing more information and easier management. A more minimal alternative for session persistence only is [`dtach`](https://github.com/bogner/dtach).

- Dalam ssh, mengetahui bagaimana cara menggunaakn saluran (port tunnel) dengan `-L` atau `-D` (dan terkadang `-R`) juga berguna. Misalnya untuk mengakses situs web dari kendali server jarak jauh.

- Akan sangat bermanfaat untuk melakukan optimisasi pada konfigurasi ssh; misalnya, `~/.ssh/config` mengandung pengaturan untuk menghindari putusnya koneksi antar jaringan, menggunakan kompresi (bermanfaat bagi yang memiliki bandwidth rendah), dan terhubung dengan banyak saluran pada suatu server dengan kontrol lokal:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Beberapa opsi lain untuk SSH terkait sensitifitas keamanan dan sebaiknya diaktifkan dengan hati-hati, misalnya pada subnet atau host atau pada jaringan yang terpercaya: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- Pertimbangkan [`mosh`](https://mosh.mit.edu/) sebagai alternatif untuk SSH yang mana menggunakan UDP, dapat menjaga terputusnya koneksi dan lebih nyaman untuk digunakan (perlu konfigurasi disisi server).

- Untuk mendapatkan hak akses pada sebuah berkas, yang mana berguna untuk konfigurasi sistem tapi tidak tersedia pada `ls`, gunakan perintah perikut
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Untuk memilih nilai keluaran dari perintah lain secara interaktif, gunakan [`percol`](https://github.com/mooz/percol) or [`fzf`](https://github.com/junegunn/fzf).

- For interaction with files based on the output of another command (like `git`), use `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- For a simple web server for all files in the current directory (and subdirs), available to anyone on your network, use:
`python -m SimpleHTTPServer 7777` (for port 7777 and Python 2) and `python -m http.server 7777` (for port 7777 and Python 3).

- For running a command with privileges, use `sudo` (for root) or `sudo -u` (for another user). Use `su` or `sudo bash` to actually run a shell as that user. Use `su -` to simulate a fresh login as root or another user.

- Untuk berganti ke pengguna Shell lain, gunakan `su username` atau `su - username`. Sertakan `-` untuk mendapatkan lingkungan jika pengguna telah login. Hindari menggunakan username menjadi root. Anda akan dimintai password _untuk pengguna yang ingin diganti_.

- Ketahui [batasan 128k](https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong) pada sebuah perintah. Kesalahan "Argument list too long" sering terjadi ketika karakter (wildcard) mewakili berkas yang sangat banyak. (Saat ini terjadi dapat menggunakan `find` dan `xargs` sebagai bantuan.)

- Untuk sebuah perhitungan dasar (secara umum akses Python), gunakan interpreter `python`. Contohnya,
```
>>> 2+3
5
```

## Mengolah berkas dan data

- Untuk menemukan berkas berdasarkan nama dalam direktori saat ini, `find . -iname '*sesuatu*'` (atau yang mirip). Untuk mencari berkas dibanyak tempat berdasarkan nama, gunakan `locate sesuatu` (tapi ingat `updatedb` mungkin belum menyimpan berkas terbaru yang dibuat).

- Untuk pencarian umum berdasarkan isi berkas (lebih dalam dibandingkan dengan `grep -r`), gunakan [`ag`](https://github.com/ggreer/the_silver_searcher).

- Untuk mengkonversi HTML menjadi teks: `lynx -dump -stdin`

- Untuk Markdown, HTML, dan semua jenis konversi dokumen, coba [`pandoc`](http://pandoc.org/).

- Jika anda mengelola XML, `xmlstarlet` adalah pilihan yang paling tua namun terbaik.

- Untuk JSON, gunakan [`jq`](http://stedolan.github.io/jq/).

- Untuk YAML, gunakan [`shyaml`](https://github.com/0k/shyaml).

- Untuk Excel atau berkas CSV, [csvkit](https://github.com/onyxfish/csvkit) menyediakan `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, dan lain sebagainya.

- Untuk Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) lebih nyaman digunakan dan [`s4cmd`](https://github.com/bloomreach/s4cmd) lebih cepat. Amazon [`aws`](https://github.com/aws/aws-cli) dan yang telah dikembangkan [`saws`](https://github.com/donnemartin/saws) tetap penting untuk pekerjaan yang berhubungan dengan AWS lainnya.

- Ketahui tentang `sort` dan `uniq`, termasuk opsi `-u` dan `-d` -- lihat Perintah satu baris dibawah. Lihat juga `comm`.

- Ketahui tentang `cut`, `paste`, dan `join` dalam memanipulasi teks pada berkas. Banyak orang menggunakan `cut` tapi melupakan tentang `join`.

- Ketahui tentang `wc` untuk menghitung jumlah baris (`-l`), karakter (`-m`), kata (`-w`) dan byte (`-c`).

- Ketahui tentang `tee` untuk menyalin dari stdin sebuah berkas ke stdout, seperti dalam `ls -al | tee file.txt`.

- Untuk kalkulasi yang cukup kompleks, termasuk pengelompokan, konversi nilai, dan statistik, pertimbangkan untuk menggunakan [`datamash`](https://www.gnu.org/software/datamash/).

- Ketahui bahwa locale cukup berdampak pada banyak perintah, termasuk pengurutan (pemeriksaan) dan dan kinerja. Kebanyakan distribusi Linux akan menggunakan `LANG` atau variabel locale lainnya untuk melakukan pengaturan bahasa seperti ID Indonesia. Tapi waspada karena pengurutan akan berubah jika locale juga telah dirubah. Dan ketahui aktifitas i18n dapat membuat banyak perintah *seringkali* menjadi lambat. Dalam kondisi tertentu (seperti beberapa perintah operasi dibawah) anda dapat menghindari i18n dan menggunakan pengurutan tradisional, gunakan `export LC_ALL=C`.

- Anda dapat menentukan perintah tertentu dengan memberikan awalan saat pemanggilan dengan variabel pengaturan, seperti `TZ=Pacific/Fiji date`.

- Ketahui mengenai dasar `awk` dan `sed` untuk manipulasi data. Sebagai contoh, menjumlahkan semua nomor yang ada pada kolom ketiga dari sebuah berkas: `awk '{ x += $3 } END { print x }'`. Ini memungkinkan komputasi 3x lebih cepat dan 3x lebih singkat dibandingkan dengan persamaan Python.

- Untuk mengganti semua string yang cocok, dalam satu atau lebih dari satu berkas:
```sh
      perl -pi.bak -e 's/string-lama/string-baru/g' my-files-*.txt
```

- Untuk mengganti nama banyak berkas atau mencari dan/atau mengganti dalam berkas, coba [`repren`](https://github.com/jlevy/repren). (Dalam beberapa kasus perintah `rename` memungkinkan untuk mengganti banyak nama sekaligus, namun perlu berhati-hati karena fungsionalitas mungkin tidak akan sama pada distribusi Linux lainnya.)
```sh
      # Mengganti nama berkas, direktori, dan isi berkas secara penuh dari foo --> bar:
      repren --full --preserve-case --from foo --to bar .
      # Mengembalikan backup berkas whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Sama seperti diatas, menggunakan rename, jika ada yang cocok:
      rename 's/\.bak$//' *.bak
```

- Sesuai dengan yang ada pada halaman manual, `rsync`  adalah perintah untuk menyalin berkas yang cukup cepat dan memiliki banyak fitur. Mampu melakukan singkronisasi antar host yang mana sangat berguna untuk host lokal. Jika keamanan tidak diutamakan, gunakan `rsync` daripada `scp` untuk pemulihan tanpa harus mengulang dari awal. Perintah tersebut merupakan [cara tercepat](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) untuk menghapus banyak berkas sekaligus:
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Gunakan `shuf` untuk mengacak atau memilih baris secara acak dalam sebuah berkas.

- Ketahui perintah `sort`. Untuk angka, funakan opsi `-n`, atau `-h` untuk menampilkan angka yang mudah dibaca manusia (contoh `du -h`). Ketahui bagaimana cara kerja kunci (`-t` dan `-k`).  Terkadang membutuhkan `k1,1` untuk mengurutkan kolom pertama saja; `k1` berarti mengurutkan semua barus.  Pengurutan yang stabil (`sort -s`) juga cukup berguna. FContoh, untuk mengurutkan yang pertama berdasarkan kolom 2, yang kedua berdasarkan kolom 1, akan menjadi `soft -k1,1 | sort -s -k2m2`.  

- Jika perlu untuk membuat tab pada terminal dalam Bash (misalnya argumen `-t` untuk mengurutkan), tekan **ctrl-v** **[Tab]** atau dengan menulis `$'\t'` (menulis langsung lebih baik dari copy/paste).

- Alat yang umum digunakan untuk menambal sumber kode adalah `diff` dan `patch`. Lihat juga `diffstat` untuk hasil berupa statistik dari `diff` dan `sdiff`. Ingat bahwa `diff -r` berlaku pada semua direktori. Gunakan `diff -r tree1 tree2 | diffstat` untuk ringkasan perubahan. Gunakan `vimdiff` untuk membandingkan dan memperbarui berkas.

- Untuk berkas binari, gunakan `hd`, `hexdump` atau `xxd` untuk menampilkan kode hex yang sederhana dan `bvi` atau `blew` untuk memperbarui berkas biner.

- Alat lainnya untuk berkas biner, `strings` (dikombinasikan dengan `grep`, dan lainnya) memungkinkan pencarian teks berdasarkan bit-bit.

- Untuk membandingkan berkas biner (kompresi delta), gunakan `xdelta3`.

- Untuk mengkonversi sandi penulisan teks, coba `iconv`. Atau `uconv` untuk penggunaan lebih lanjut; telah mendukung hal yang berkaitan dengan Unicode. Sebagai contoh, perintah berikut membuat tulisan kecil dan menghapus semua aksen (dengan mengembangkan atau menghapusnya).
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```
- Untuk memecah berkas menjadi beberapa bagian, lihat `split` (memisahkan berdasarkan ukuran) dan `csplit` (memisahkan berdasarkan pola).

- Untuk memanipulasi tanggal dan waktu, gunakan `dateadd`, `datediff`, `strptime` etc. dari [`dateutils`](http://www.fresse.org/dateutils/).

- Gunakan `zless`, `zmore`, `zcat`, dan `zgrep` untuk digunakan pada berkas yang terkompres.

- Atribut dari sebuah berkas dapat diset melalui `chattr` dan disediakan alternatif untuk level terendah pada hak akses berkas. Sebagai contoh, untuk melindungi ketidak sengajaan pada penghapusan berkas gunakan flag kebal: `sudo chattr +i /direktori/berkas/penting`

- Gunakan `getfacl` dan `setfacl` untuk menyimpan dan mengembalikan hak akses pada suatu berkas. Contohnya:
```sh
   getfacl -R /suatu/path > hakakses.txt
   setfacl --restore=hakakses.txt
```

## Analisa sistem

- Untuk analisa web, `curl` dan `curl -I` cukup berguna, atau yang sama lainnya seperti `wget`, atau yang lebih modern [`httpie`](https://github.com/jkbrzt/httpie).

- Untuk mengetahui status CPU/penyimpanan, perintah klasik `top` (lebih baik lagi `htop`), `iostat`, dan `iotop`. Gunakan `iostat -mxz 15` untuk melihat detil CPU tiap bagian (partition) penyimpanan dan pengetahuan tentang kinerja.

- Untuk detail koneksi jaringan, gunakan `netstat` dan `ss`.

- Untuk melihat sekilas yang terjadi pada sistem, `dstat` cukup berguna. Untuk detil secara menyeluruh, gunakan [`glances`](https://github.com/nicolargo/glances).

- Untuk status memory, jalankan dan perhatikan keluaran dari `free` dan `vmstat`. Dalam kondisi tertentu, hati-hati terhadap "cached" yang dihasilkann oleh kernel Linux, jadi perhatikan sebaik mungkin keluaran dari `free`.

- Analisa sistem Java sedikit berbeda, tapi ada trik sederhana untuk JVM dari Oracle dan yang lainnya yakni dapat dijalankan perintah `kill -3 <pid>` dan penelusuran (full stack trace) dan beberapa ringkasan utama (termasuk informasi pembangkitan sampah sistem, informasi yang sangat berguna) akan dikeluarkan melalui stderr/logs. JDK seperti `jps`, `jstat`, jstack`, `jmap` cukup berguna. [Perlengkapan SJK](https://github.com/aragozin/jvm-tools) untuk penggunaan lebih lanjut.

- Gunakan [`mtr`](http://www.bitwizard.nl/mtr/) sebagai pilihan terbaik `traceroute`, untuk menelusuri masalah jaringan.

- Untuk mengungkapkan kenapa penyimpanan penuh, perintah [`ncdu`](https://dev.yorhel.nl/ncdu) lebih menghemat waktu dibangdingkan `du -sh *`.

- Untuk mencari socket atau process yang sedang menggunakan bandwidth, coba [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) atau [`nethogs`](https://github.com/raboof/nethogs).

- Perintah `ab` (paket dari Apache) sangat berguna untuk melihat kinerja dari server web. Untuk test lebih lanjut, gunakan `siege`.

- Untuk analisa jaringan yang lebih serius, [`wireshark`](https://wireshark.org/), [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html), atau [`ngrep`](http://ngrep.sourceforge.net/).

- Ketahui tentang `strace` dan `ltrace`. Perintah tersebut membantu ketika sebuah program gagal, hang, atau crash secara tiba-tiba, atau jika ingin mengetahui kinerja aplikasi secara umum. Catatan gunakan opsi profiling (`-c`), dan kemampuan untuk menertakan proses yang sedang berjalan (`-p`).

- Ketahui tentang `ldd` untuk memeriksa pustaka berbagi dan sebagainya.

- Ketahui bagaimana cara terhubung dengan proses yang sedang berjalan dengan `gdb` dan periksa alur stack-nya.

- Gunakan `/proc` untuk melakukan analisis permasalahan secara live. Contohnya: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (dimana `xxx` adalah ID proses id atau pid).

- Untuk mengetahui kesalahan yang terjadi pada proses analisa sebelumnya, gunakan [`sar`](http://sebastien.godard.pagesperso-orange.fr/). Perintah tersebut dapat menampilkan riwayat statistik pada CPU, memory, jaringan, dan lain sebagainya.

- Untuk analisa kinerja sistem lebih mendalam, periksa `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_(Linux)), dan [`sysdig`](https://github.com/draios/sysdig).

- Periksa Sistem Operasi yang digunakan dengan `uname` atau `uname -a` (Unix/kernel pada umumnya) atau `lsb_release -a` (distro linux).

- Gunakan `dmesg` ketika terjadi sesuatu yang tidak disangka (mungkin masalah perangkat kerasa atau driver).

- Jika anda menghapus sebuah berkas dan tidak dapat meningkatkan kapasitas media penyimpanan sebagaimana hasil pengecekan `du`, periksa kemungkinan berkas tersebut sedang digunakan oleh suatu proses:
`lsof | grep deleted | grep "berkas-yang-sangat-besar"`


## Perintah satu baris

Beberapa contoh untuk menggabungkan perintah sekaligus:

- Terkadang cukup membantu ketika ingin mencari kesamaan, kesatuan, dan perbedaan dari beberapa berkas melalui `sort`/`uniq`. Misalkan `a` dan `b` adalah berkas yang berbeda. Perintah ini cukup cepat, dan dapat bekerja pada berkas dengan ukuran sampai gigabyte. (Pengurutan tidak dibatasi oleh memory, tapi diperlukan opsi `-T` jika `/tmp` berada dalam partisi root yang kecil.) Lihat juga catatan tentang `LC_ALL` diatas dan opsi yang terdapat pada `sort` (penjelasan lebih jelas dibawah berikut).
```sh
      cat a b | sort | uniq > c   # c berisi kesatuan antara a dan b
      cat a b | sort | uniq -d > c   # c berisi persamaan antara a dan b
      cat a b b | sort | uniq -u > c   # c berisi perbedaan antara a dan b
```

- Gunakan `grep . *` untuk menguji isi dari semua berkas dalam sebuah direktori (hasil tiap berisnya berkaitan dengan nama berkas), atau `head -180 *` (setiap berkas memiliki informasi kepala). Hal ini sangat bermanfaat untuk direktori yang berisi berkas konfigurasi seperti `/sys`, `/proc`, `/etc`.

- Untuk menjumlahkan semua nomor pada kolom ketiga dari sebuah berkas (memungkinkan proses 3x lebih cepat dan skrip 3x lebih pendek dari Python):
```sh
      awk '{ x += $3 } END { print x }' suatuberkas
```

- Untuk melihat ukuran atau tanggal berkas dalam bentuk struktur pohon, mirip dengan rekursif `ls -l` namun lebih mudah untuk dibaca dari `ls -lR`:
```sh
      find . -type f -ls
```

- Ketika terdapat sebuah berkas teks seperti log web server, dan nilai tertentu muncul pada beberapa baris, misalnya parameter `acct_id` yang terdapat pada URL. Jika ingin mengetahui berapa banyak akses `acct_id`:
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- Untuk memantau perubahan secara terus menerus, gunakan `watch`, misalnya perubahan berkas pada sebuah direktori, gunakan `watch -d -n 2 'ls -rtlh | tail` atau pada pengaturan jaringan wifi ketika melakukan perbaikan dengan `watch -d -n 2 ifconfig`.

- Jalankan fungsi berikut untuk mendapatkan sesuatu yang acak dari dokumen ini (mengolah Markdown dan mengeluarkan sebuah item):
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```

## Tidak penting tapi bermanfaat

- `expr` : melakukan perhitungan aritmatika atau mengevaluasi regular expression (regex)

- `m4` : pemroses macro yang sederhana

- `yes` : menampilkan cukup banyak string

- `cal` : menampilkan kalender

- `env` : menjalankan sebuah perintah (berguna dalam skrip)

- `printenv` : menampilkan variabel environment (berguna dalam analisa dan skrip)

- `look` : mencari kata dalam bahasa English (atau baris dalam sebuah berkas) diawali dengan sebuah string

- `cut`, `paste` dan `join`: manipulasi data

- `fmt`: teks dengan format paragraf

- `pr`: teks dengan format halaman/kolom

- `fold`: membatasi baris dari teks

- `column`: membuat format teks jadi rata, lebar kolom tertentu atau bentuk tabel

- `expand` dan `unexpand`: konversi antara tab dan spasi

- `nl`: menambahkan baris baru

- `seq`: menampilkan angka

- `bc`: kalkulator

- `factor`: angka faktorial

- [`gpg`](https://gnupg.org/): mengenkripsi dan menandatangani berkas

- `toe`: isi dari tabel terminfo

- `nc`: analisa jaringan dan aktifitas datanya

- `socat`: jalur tunda dan penerus jalur tcp (mirip dengan `netcat`)

- [`slurm`](https://github.com/mattthias/slurm): visualisasi aktifitas jaringan

- `dd`: memindahkan data antar berkas atau perangkat

- `file`: identifikasi jenis dari berkas

- `tree`: menampilkan struktur pohon dari direktori dan subdirektori secara bersarang; mirip `ls` namun dapat rekursif

- `stat`: informasi berkas

- `time`: menjadwalkan dan menjalankan sebuah perintah

- `timeout`: menjalankan sebuah perintah dalam waktu yang telah ditentukan dan melanjutkan kembali dalam waktu yang telah ditentukan pula.

- `lockfile`: membuat berkas dengan tanda hanya dapat dihapus oleh `rm -f`

- `logrotate`: menggulirkan, mengkompres serta mengirimkan via email berkas logs

- `watch`: menjalankan program secara berulang, menampilkan hasil dan/atau memfokuskan pada perubahan

- `tac`: menmapilkan kebalikan dari berkas

- `shuf`: memilih baris secara acak dari sebuah berkas

- `comm`: membandingkan berkas yang terurut berdasarkan baris

- `pv`: memantau perkembangan data yang melalui sebuah saluran

- `hd`, `hexdump`, `xxd`, `biew` dan `bvi`: menampilkan atau memperbaiki berkas dalam biner

- `strings`: mengeluarkan teks dari berkas biner

- `tr`: konversi atau menipulasi sebuah karakter

- `iconv` atau `uconv`: konversi kode teks

- `split` dan `csplit`: membagi berkas

- `sponge`: membaca semua masukan sebelum menuliskannya, berguna untuk membaca dan menulis pada berkas yang sama, misalnya `grep -v sesuatu nama-berkas | sponge nama-berkas`

- `units`: konversi dan kalkulasi unit; mengkonversi jarak mil per dua minggu (lihat juga `/usr/share/units/definitions.units`)

- `apg`: membangkitkan kata kunci acak

- `xz`: kompresi berkas dengan rasio yang tinggi

- `ldd`: informasi dynamic library

- `nm`: simbil dari objek berkas

- `ab`: patokan untuk web server

- `strace`: analisa sistem pemanggilan

- [`mtr`](http://www.bitwizard.nl/mtr/): traceroute yang lebih baik untuk analisa jaringan

- `cssh`: visual shell dalam jumlah banyak secara bersamaan

- `rsync`: singkronisasi berkas dan direktori melalui SSH atau berkas sistem dalam satu mesin

- [`wireshark`](https://wireshark.org/) dan [`tshark`](https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html): penangkap paket dan analisa jaringan

- [`ngrep`](http://ngrep.sourceforge.net/): grep untuk jaringan

- `host` dan `dig`: pencarian DNS

- `lsof`: deskripsi berkas process dan informasi socket

- `dstat`: berguna untuk statistik sistem

- [`glances`](https://github.com/nicolargo/glances): tingkat tinggi, informasi singkat banyak subsistem

- `iostat`: statistik penggunaan penyimpanan

- `mpstat`: statistik penggunaan CPU

- `vmstat`: statistik penggunaan memory

- `htop`: versi terbaru dari top

- `last`: riwayat login

- `w`: melihat siapa yang sedang login

- `id`: informasi identitas pengguna atau grup

- [`sar`](http://sebastien.godard.pagesperso-orange.fr/): riwayat statistik sistem

- [`iftop`](http://www.ex-parrot.com/~pdw/iftop/) or [`nethogs`](https://github.com/raboof/nethogs): penggunaan jaringan berdasarkan socket atau process

- `ss`: statistik socket

- `dmesg`: pesan ketika boot dan sistem error

- `sysctl`: melihat dan mengkonfigurasi parameter kernel Linux saat sedang berjalan

- `hdparm`: manipulasi atau melihat kinerja media SATA/ATA

- `lsblk`: daftar blok perangkat: berbentuk struktur pohon yang berisi media penyimpanan beserta partisinya

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: informasi perangkat keras, termasuk CPU, BIOS, RAID, grafis, dan lain sebagainya.

- `lsmod` and `modinfo`: menampilkan daftar dan detil modul kernel

- `fortune`, `ddate`, dan `sl`: tergantung bagaimana anda menyebutnya "bermanfaat"


## Khusus OS X

Berikut ini *hanya* berlaku pada OS X.

- Manajemen paket menggunakan `brew` (homebrew) dan/atau `port` (MacPorts). Dapat digunakan untuk memasang banyak aplikasi OS X untuk menggunakan perintah-perintah diatas.

- Salin keluaran dari perintah ke aplikasi desktop menggunakan `pbcopy` dan tempel menggunakan `pbpaste`.

- Untuk mengaktifkan tombol Option pada aplikasi Terminal OS X sebagai tombol alt (seperti menggunakan perintah diatas **alt-b**, **alt-f**, dan lain sebagainya), buka Preferences -> Profiles -> Keyboard dan pilih "Use Option as Meta key".

- Untuk membuka berkas pada aplikasi desktop, gunakan `open` atau `open -a /Applications/namaaplikasi.app`.

- Spotlight: Mencari berkas dengan `mdfind` dan menampilkan metadata (seperti info EXIF foto) dengan `mdls`.

- Berhati-hati karena OS X berbasis pada BSD Unix, dan banyak perintah (seperti `ps`, `ls`, `tail`, `awk`, `sed`) beberapa memiliki varian yang berbeda dengan Linux, yang mana akan berdampak besar pada System V-style Unix dan peralatan GNU lainnya. Perbedaannya dapat diketahui dengan mencari pada halaman manual "BSD General Command Manual". Pada beberapa kasus versi GNU dapat dipasang juga (seperti `gawk` dan `gsed` untuk GNU awk dan sed). Ketika menulis skrip Bash lintas platform, hundari beberapa perintah (seperti mempertimbangkan Python atau `perl`) atau coba kembali dengan hati-hati.

- Untuk mendapatkan informasi rilis OS X, gunakan `sw_vers`.

## Hanya Windows

Berikut ini *hanya* berlaku pada Windows.

- Pada Windows 10, anda dapat menggunakan [Bash di Ubuntu pada Windows](https://msdn.microsoft.com/commandline/wsl/about), dimana menyediakan lingkungan Bash yang mirip dengan perintah baris pada lingkungan Unix. Sebagai tambahan, memungkinkan program Linux untuk berjalan pada Windows. Namun disisi lain tidak memungkinkan untuk menjalankan aplikasi windows melalui jendela Bash.

- Akses fasilitas dari Shell Unix pada Microsoft Windows dengan memasang [Cygwin](https://cygwin.com/). Banyak hal telah dijelaskan pada dokumen ini akan bekerja secara normal.

- Pasang program Unix tambahan dengan paket manajer Cygwin.

- Gunakan `mintty` sebagai aplikasi perintah baris.

- Akses clipboard pada Windows pada `/dev/clipboard`.

- Gunakan `cygstart` untuk membuka berkas melalui aplikasi yang telah terdaftar.

- Akses registry pada Windows dengan `regtool`.

- Ingat bahwa `C:\` Windows akan menjadi `/cygdrive/c` pada Cygwin, dan `/` pada Cygwin akan berada di `C:\cygwin` pada Windows. Konversi antara Cygwin dan gaya Windows file path dengan `cygpath`. Hal ini berguna dalam skrip yang menjalankan program Windows.

- Anda dapat menjalankan skrip sistem administrasi pada Windows dari perintah baris dengan mempelajari dan menggunakan `wmic`.

- Pilihan lainnya untuk membuat mendapatkan Unix pada Windows adalah [Cash](https://github.com/dthree/cash). Sebagai catatan bahwa hanya tersedia beberapa fasilitas perintah baris Unix yang tersedia dalam lingkungan ini.

- Sebagai pilihan alternatif untuk mendapatkan alat pengembangan dalam GNU (seperti GCC) pada Windows adalah [MinGW](http://www.mingw.org/) dan paketnya [MSYS](http://www.mingw.org/wiki/msys), dimana menyediakan beberapa fasilitas seperti bash, gawk, make dan grep. MSYS tidak sepenuhnya memiliki semua fasilitas jika dibandingkan dengan Cygwin. Cygwin biasanya berguna untuk membuat port Windows dari Unix.

## Bacaan lebih lanjut

- [awesome-shell](https://github.com/alebcay/awesome-shell): Daftar alat dan sumber Shell lainnya.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): Penjelasan lebih dalam perintah baris pada OS X.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) untuk  menulis skrip Shell yang lebih baik.
- [shellcheck](https://github.com/koalaman/shellcheck): Analisis Shell skrip. Pada dasarnya, lint untuk bash/sh/zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): Cara menangani nama berkas yang baik dan benar pada skrip Shell.
- [Data Science at the Command Line](http://datascienceatthecommandline.com/#tools): Perintah dan alat yang berguna untuk mengolah data sains, dari buku dengan nama yang sama.

## Penyangkalan

Dengan pengecualian dari tugas yang sangat kecil, kode ditulis sehingga orang lain dapat membacanya. Dengan kekuatan datang tanggung jawab. Bahkan Anda * dapat * melakukan sesuatu di Bash tidak berarti Anda harus! ;)
Dengan beberapa pengecualian, sebuah kode ditulis sehingga orang lain dapat membacanya. Dengan adanya kekuatan datang pula tanggung jawab. Faktanya anda *dapat* melakukan hal yang tidak seharusnya dalam Bash! ;)


## Lisensi

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

Hasil kerja ini memiliki lisensi dibatah [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
