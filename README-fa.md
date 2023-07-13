🌍
*[Čeština](README-cs.md) ∙ [Deutsch](README-de.md) ∙ [Ελληνικά](README-el.md) ∙ [English](README.md) ∙ [Español](README-es.md) ∙ [فارسی](README-fa.md) ∙ [Français](README-fr.md) ∙ [Indonesia](README-id.md) ∙ [Italiano](README-it.md) ∙ [日本語](README-ja.md) ∙ [한국어](README-ko.md) ∙ [polski](README-pl.md) ∙ [Português](README-pt.md) ∙ [Română](README-ro.md) ∙ [Русский](README-ru.md) ∙ [Slovenščina](README-sl.md) ∙ [Українська](README-uk.md) ∙ [简体中文](README-zh.md) ∙ [繁體中文](README-zh-Hant.md)*

<p align="right">

# هنر خط فرمان

*توجه: من قصد دارم این نوشتار را بازنویسی کنم و به دنبال یک همنویس جدید هستم که در گسترش آن به یک راهنمای جامع تر کمکم کنه. اگرچه این راهنما بسیار محبوبه، اما می تونه  گسترده تر و کمی عمیق تر هم باشه. اگر به نوشتن علاقه داری و تقریباً متخصص این مطالب هستی و می‌خواهی کمک کنی، لطفاً برای  من در  &#x202b;josh (0x40) holloway.com  پیغام بگذار. –[jlevy](https://github.com/jlevy), [Holloway](https://www.holloway.com). سپاس گذارم!*

<ul dir="rtl">
<li><a href="#%D9%85%D8%A7%D9%88%D8%B1%D8%A7">ماورا</a></li>
<li><a href="#%D9%85%D8%A8%D8%A7%D9%86%DB%8C">مبانی</a></li>
<li><a href="#%D8%A7%D8%B3%D8%AA%D9%81%D8%A7%D8%AF%D9%87-%D8%B1%D9%88%D8%B2%D9%85%D8%B1%D9%87">استفاده روزمره</a></li>
<li><a href="#%D9%BE%D8%B1%D8%AF%D8%A7%D8%B2%D8%B4-%D9%BE%D8%B1%D9%88%D9%86%D8%AF%D9%87-%D9%87%D8%A7-%D9%88-%D8%AF%D8%A7%D8%AF%D9%87-%D9%87%D8%A7">پردازش پرونده ها و داده ها</a></li>
<li><a href="#%D8%B1%D9%81%D8%B9-%D8%A7%D8%B4%DA%A9%D8%A7%D9%84-%D8%B3%DB%8C%D8%B3%D8%AA%D9%85">رفع اشکال سیستم</a></li>
<li><a href="#%D8%AA%DA%A9-%D8%AE%D8%B7%DB%8C-%D9%87%D8%A7">تک خطی ها</a></li>
<li><a href="#%D9%85%D8%A8%D9%87%D9%85-%D8%A7%D9%85%D8%A7-%D9%85%D9%81%DB%8C%D8%AF">مبهم اما مفید</a></li>
<li><a href="#%D9%81%D9%82%D8%B7-%D9%85%DA%A9-%D8%A7%D9%88%D8%A7%D8%B3">فقط مک اواس</a></li>
<li><a href="#%D9%81%D9%82%D8%B7-%D9%88%DB%8C%D9%86%D8%AF%D9%88%D8%B2">فقط ویندوز</a></li>
<li><a href="#%D9%85%D9%86%D8%A7%D8%A8%D8%B9-%D8%A8%DB%8C%D8%B4%D8%AA%D8%B1">منابع بیشتر</a></li>
<li><a href="#%D8%B3%D9%84%D8%A8-%D9%85%D8%B3%D8%A6%D9%88%D9%84%DB%8C%D8%AA">سلب مسئولیت</a></li>
</ul>

![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

تسلط به خط فرمان مهارتی است که اغلب نادیده گرفته میشه یا به عنوان یک مهارت محرمانه تلقی می شه، اما انعطاف پذیری و بهره وری تو را به عنوان یک مهندس، هم محسوس  و هم نامحسوس بهبود می بخشه.  این مجموعه ای از یادداشت ها و نکاتی است در مورد خط فرمان که برای ما هنگام کار بر روی لینوکس مفید بوده. برخی نکات ابتدایی و برخی دیگر نسبتاً خاص، پیچیده یا گمنام هستند. این صفحه طولانی نیست، اما اگر بتوانی همه موارد آن را به خاطر بسپاری  و استفاده کنی، چیزهای زیادی می دونی.

این اثر حاصل همکاری [بسیاری از نویسندگان و مترجمان](AUTHORS.md) است. برخی از این نکاتی در [ابتدا](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands) در [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know) [ظاهر شد](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)، اما بعدها به GitHub منتقل شد، جایی که افراد با استعدادتر از نویسنده اصلی، پیشرفت‌های متعددی را اعمال کردند. اگر سوالی در رابطه با خط فرمان داری، [لطفاً مطرح کن](https://airtable.com/shrzMhx00YiIVAWJg). درصورت مشاهده خطا یا رویت چیزی که بهتر می توان انجام داد، [لطفاً با ما مشارکت کن](/CONTRIBUTING.md)!

## ماورا

گستره:

<ul dir="rtl">
<li><p>این راهنما هم برای مبتدیان و هم برای کاربران با تجربست. اهداف آن عبارتند از <em>وسعت</em> (هرچیز مهم)، <em>وضوح</em> (ارائه نمونه‌های ملموس از رایج‌ترین کاربردها)، و <em>اختصار</em> (اجتناب از نکات غیرضروری یا انحرافاتی که به راحتی می‌تونی در جای دیگری جستجو کنی). هر نکته ای در جای خود ضروری است یا در شرایطی باعث صرفه جویی در زمان نسبت به دیگر گزینه های جایگزین می شه.</p></li>
<li><p>این راهنما برای لینوکس نوشته شده است، به استثنای بخش‌های <a href="#%D9%81%D9%82%D8%B7-%D9%85%DA%A9-%D8%A7%D9%88%D8%A7%D8%B3">فقط مک اواس</a> و <a href="#%D9%81%D9%82%D8%B7-%D9%88%DB%8C%D9%86%D8%AF%D9%88%D8%B2">فقط ویندوز</a>. بسیاری از نکات را میتونی بر روی "Unices" یا مک اواس (یا حتی Cygwin) نصب و اعمال کنی.</p></li>
<li><p>تمرکز این راهنما روی برنامه بَش برکنشی (interactive bash) است، هرچند نکات بسیاری را میشه  در پوسته‌های دیگه و دستورگان‌نویسی کلی بَش اعمال کرد.</p></li>
<li><p>این راهنما شامل فرمان ها "استاندارد" یونیکس و همچنین فرمان هایی است که نیاز به نصب یک بسته نرم افزاری خاص دارند - ولی همه فرمان ها به اندازه کافی مهم بودن که در اینجا گنجانده بشن.</p></li>
</ul>

تبصره:
<ul dir="rtl">
<li><p>برای نگه داشتن این راهنما در یک صفحه، محتوا به طور ضمنی با مرجع درج میشه. مطمئنا آنقدر باهوش هستی که به محض آگاهی از یک ایده یا کلمه کلیدی جستجوی گوگل، به دنبال جزئیات بیشتر در جای دیگری بگردی. برای نصب   بسته های نرم‌افزاری جدید از <code>pip</code>، <code>pacman</code>، <code>dnf</code>، <code>yum</code>، <code>apt</code> یا <code>brew</code> (در صورت لزوم) استفاده کن.</p></li>
<li><p>از <a href="http://explainshell.com/" rel="nofollow">Explainshell</a> استفاده کن تا به تفکیک مفیدی از کارهایی که فرمان ها، گزینه‌ها، پایپ ها و غیره انجام می‌دن، برسی.</p></li>
</ul>

## مبانی

<ul dir="rtl">
<li><p>اصول اولیه بَش (Bash) را یاد بگیر. عملا <code>man bash</code> را تایپ کن و حداقل همه چیز را مرور کن. دنبال کردن آن خیلی آسونه و چندان طولانی نیست. پوسته های جایگزین می تونن خوب باشن، اما بَش قدرتمند و همیشه در دسترس است (یادگیری <em>فقط</em> fish ،zsh و غیره، در حالی که در لپ تاپ شخصی وسوسه برانگیزه، تو را در بسیاری از موقعیت ها محدود می کنه، مثلاً استفاده از کارسازها).

<li><p>حداقل یک ویراستار متن را به خوبی یاد بگیر. <code>nano</code> یکی از ساده ترین ویراستارها برای باز کردن، ویرایش، ذخیره و جستجو است. ولی، برای کاربر حرفه ای در ترمینال، هیچ جایگزینی برای Vim (<code dir="ltr">vi</code>) وجود نداره، ویراستاری با فراگیری دشوار اما قابل احترام، سریع و با امکانات کامل. خیلی ها هم از Emacs کلاسیک، به ویژه برای کارهای ویرایش بزرگتر استفاده می کنند.(البته، هر پدیدآورنده نرم افزار مدرنی که روی یک پروژه گسترده کار می‌کنه، بعیده که تنها از یک ویراستار متنی استفاده کنه و باید با IDE‌ها و ابزارهای گرافیکی مدرن آشنا باشه.)

<li>بازیابی مستندات:
  <ul dir="rtl">
   <li><p>یاد بگیر چگونه اسناد رسمی را با <code>man</code> بخونی. (برای کنجکاوها، <code>man man</code> شماره بخش ها را فهرست می کنه، به عنوان مثال: 1 فرمانهای "معمولی"، 5 پرونده ها/ قراردادها و 8 برای مدیریت است). صفحات <code>man</code> را با فرمان <code>apropos</code> پیدا کن.</p></li>
  
   <li><p>بیاد داشته باش که برخی از فرمان ها برنامه اجرایی نیستند، بلکه فرمان های درونی بَش هستند و می‌تونی با <code>help</code> و <code>help -d</code> از آنها کمک بگیری. با استفاده از <code>type command</code> می‌توانی بفهمی که آیا یک فرمان اجرایی، فرمان درونی یا یک دگرنام (alias) است.</p></li>

   <li><p>فرمان <code>curl cheat.sh/command</code> یک "تقلب برگه" مختصر با مثال های رایج نحوه استفاده از فرمان shell ارائه می ده.</p></li>
  </ul>
</li>

<li><p>با هدایت کننده برونداد با استفاده از <code dir="ltr">&gt;</code> و درونداد با استفاده از <code dir="ltr">&lt;</code> و پایپ  با استفاده از <code>|</code> آشنا باش . بیاد داشته باشد <code dir="ltr">&gt;</code> پرونده برونداد را بازنویسی می کنه  و <code dir="ltr">&gt;&gt;</code> بهش اضافه می کنه. در مورد stdout و stderr اطلاعات کسب کن.</p></li>

<li><p>علامت انبساط پرونده گلوب (glob) با <code>*</code> (و همچنین <code>?</code> و <code>[</code>...<code>]</code>) و علامت گفتاورد را یاد بگیر و تفاوت بین گفتاورد <code>"</code> و نقل قول <code>'</code> را بیاموز. (در مورد انبساط متغیرها variable expansion در زیر بیشتر بخون.)</p></li>

<li><p>با مدیریت فرآیند بَش آشنا باش: <code>&amp;</code>، <code>kill</code>، <code>bg</code>، <code>fg</code>، <code>jobs</code>، <strong>ctrl-c</strong>، <strong>ctrl-z</strong>، و غیره.</p></li>

<li><p>با <code>ssh</code> و اصول اولیه اصالت سنجی بدون رمز، از طریق <code>ssh-agent</code>، <code>ssh-add</code> و غیره آشنا باش.</p></li>

<li><p>مبانی مدیریت پرونده: <code>ls</code> و <code>ls -l</code> (حتماً یاد بگیر که هر ستون در <code dir="ltr">ls -l</code> به چه معناست) <code>less</code>، <code>tail</code>، <code>head</code> و <code>tail -f</code> (یا حتی بهتر از آن، <code dir="ltr">less +F</code>) <code>ln</code> و <code dir="ltr">ln -s</code> (تفاوت ها و مزایای پیوند های سخت در مقابل پیوندهای نرم را بیاموز)، <code>du</code>، <code>chmod</code>، <code>chown</code> (برای گزارش خلاصه استفاده از رانه: <code dir="ltr">du -hs *</code>). برای مدیریت سیستم پوشه، <code dir="ltr">df</code>، <code>lsblk</code>، <code>mkfs</code>، <code>fdisk</code>، <code>mount</code>. یاد بگیرید که inode چیست (<code dir="ltr">ls -i</code> یا <code dir="ltr">df -i</code>).</p></li>

<li><p>مبانی مدیریت شبکه: <code dir="ltr">ip</code> و <code>route</code>، <code>traceroute</code>، <code>dig</code>، <code>ifconfig</code>.</p></li>

<li><p>یک سیستم کنترل نسخه مانند <code>git</code> را یاد بگیر و از آن استفاده کن.</p></li>

<li><p>عبارات با قاعده را خوب بشناس و پرچم های مختلف <code dir="ltr">grep</code>/<code>egrep</code> را خوب یاد بگیرید.  آپشن های <code dir="ltr">-i</code>، <code dir="ltr">-o</code>، <code dir="ltr">-v</code>، <code dir="ltr">-A</code>، <code dir="ltr">-B</code> و <code dir="ltr">-C</code> ارزش دونستن دارند.</p></li>

<li><p>یاد بگیر که از <code>dnf</code>، <code>yum</code>، <code>apt-get</code> یا <code>pacman</code> (بسته به سیستم عمل) برای پیدا کردن و نصب بسته ها استفاده کنی. و مطمئن شو که <code>pip</code> را برای نصب ابزارهای خط فرمان مبتنی بر پایتون داری (نصب از طریق <code>pip</code> آسانترین روش نصب بعضی از موارد زیر است).</p></li>
</ul>

## استفاده روزمره

<ul dir="rtl">
<li><p>در بَش، برای تکمیل شناسه ها یا فهرست کردن همه فرمانهای موجود از کلید جهش <strong>Tab</strong> و برای جستجو در تاریخچه فرمانها  از <strong>ctrl-r</strong> استفاده کن (پس از فشار دادن، برای جستجو شروع به تایپ کن، برای مرور نتایج، کلید <strong>ctrl-r</strong> را مکررا فشار بده. کلید <strong>Enter</strong> را فشار بده تا فرمان یافت شده را اجرا کنی، یا کلید فلش سمت راست را بزن تا نتیجه در خط فعلی قرار بگیره  تا امکان ویرایش داشته باشی).</p></li>

<li><p>در بَش، برای حذف آخرین کلمه از <strong>ctrl-w</strong> و جهت حذف محتوا از موقعیت مکان نما تا ابتدای خط از <strong>ctrl-u</strong> استفاده کن.  از <strong>alt-b</strong> و <strong>alt-f</strong> برای حرکت  کلمه به کلمه، <strong>ctrl-a</strong> برای انتقال مکان نما به ابتدای خط، <strong>ctrl-e</strong> برای انتقال مکان نما به انتهای خط، <strong>ctrl-k</strong> برای حذف محتوا تا آخر خط و از <strong>ctrl-l</strong> برای پاک کردن صفحه استفاه کن.  برای دیدن همه کلید ترابست های پیش‌فرض (default keybindings)، که کم هم نیستند،  در بَش از <code dir="ltr">man readline</code> استفاده کن. به عنوان مثال با <strong dir="ltr">alt-.</strong> میتونی شناسه های  قبلی را مرور کنی و با <strong dir="ltr">alt-</strong> گلوب  (glob) را منبسط کنی.</p></li>

<li><p>از طرف دیگر، اگر عاشق کلید ترابست های (key-bindings) به سبک vi هستی، از <code>set -o vi</code> (و <code>set -o emacs</code>) برای فعال سازی آن در بَش استفاده کن.</p></li>

<li><p>برای ویرایش فرمانها طولانی، پس از تنظیم ویراستار خود (مثلا <code>set -o emacs</code>)، <strong>ctrl-e</strong> <strong>ctrl-x</strong> فرمان فعلی را در یک ویراستار چند خطی باز می کنه. یا به سبک vi فرمان، <strong>escape-v</strong>.</p></li>

<li><p>برای مشاهده تاریخچه فرمانها، از <code>history</code> استفاده کن. با <code dir="ltr">!n</code> (که در آن <code>n</code> شماره ردیفه)   فرمانهای قبلی را مجددا اجرا کن. همچنین کوته سازی های زیادی وجود داره که می توانی از آنها استفاده کنی که مفیدترین آنها احتمالا <code dir="ltr">!$</code> برای آخرین نشانه  و <code>!!</code> برای فرمان آخره. (رجوع شود به "HISTORY EXPANSION" در صفحه man). هرچند, <strong>ctrl-r</strong> و <strong dir="ltr">alt-.</strong> جایگزینی بهتر برای این فرمانها است.</p></li>

<li><p>با <code>cd</code> به دایرکتوری خانه خود برو. با پیشوند <code>~</code> به پرونده های  مربوط به دایرکتوری خانه دسترسی پیدا کن (مثلاً <code dir="ltr">~/.bashrc</code>). در دستورگان <code>sh</code> به دایرکتوری خانه به عنوان <code dir="ltr">$HOME</code> اشاره می‌شه.</p></li>

<li><p>برای بازگشت به دایرکتوری کاری قبلی: <code dir="ltr">cd -</code>.</p></li>

<li><p>اگر در نیمه راه تایپ فرمانی هستی اما نظرت عوض شد، کلید ترکیبی <strong dir="ltr">alt-#</strong> بزن تا یک <code>#</code> در ابتدا خط اضافه بشه و فرمان تبدیل به کامنت بشه. (یا از <strong>enter</strong>، <strong>#</strong>، <strong>ctrl-a</strong> استفاده کن). بعداً می تونی از طریق تاریخچه فرمان به آن برگردی.</p></li>

<li><p>از <code>xargs</code> (یا <code>parallel</code>) استفاده کن. خیلی قدرتمنده. توجه داشته باش که می‌تونی تعداد برنامک های  که در هر خط (<code dir="ltr">-L</code>) و با موازی‌گرایی (<code dir="ltr">-P</code>) اجرا می‌شوند را کنترل کنی. اگر مطمئن نیستی که کار درست را انجام می دهد، ابتدا از <code>xargs echo</code> استفاده کنی. همچنین، <code dir="ltr">-I{}</code> مفیده. برای مثال:</p></li>
</ul>

```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```
<ul dir="rtl">
<li><p>فرمان <code>pstree -p</code> نمایش مفید درختی از فرآیندها ارائه میده.</p></li>

<li><p>فرمانهای <code>pgrep</code> و <code>pkill</code> برای پیدا کردن یا علامت دادن به فرآیندها با استفاده نام به کار میاد.(<code dir="ltr">-f</code> کمک میکنه)</p></li>

<li><p>سیگنال های مختلفی را که می تونی برای فرآیندها ارسال کنی را بشناس. برای مثال، برای تعلیق یک فرآیند، از <code dir="ltr">kill -STOP [pid]</code> استفاده کن. برای فهرست کامل، به <code>man 7 signal</code> مراجعه کن.</p></li>

<li><p>اگر می‌خواهی فرآیند پس‌زمینه برای همیشه فعال باشه، از <code>nohup</code> یا <code>disown</code> استفاده کن.</p></li>

<li><p>با فرمان <code>netstat -lntp</code> یا <code>ss -plat</code> برسی کن چه فرایندهای TCP  در حال شنود هستند (برای UDP آپشن <code dir="ltr">-u</code>)  یا فرمان <code>lsof -iTCP -sTCP:LISTEN -P -n</code> (در مک اواس هم پشتیبانی میشه)</p></li>

<li><p>همچنین برای سوکت‌ها و پرونده های باز، <code>lsof</code> و <code>fuser</code> را ببین.</p></li>

<li><p>برای اطلاع از زمان به‌کار سیستم، به <code>uptime</code> یا <code>w</code> مراجعه کن.</p></li>

<li><p>از فرمان دگرنام <code>alias</code> برای ایجاد میانبر برای فرمانهای رایج استفاده کن. به عنوان مثال، <code dir="ltr">alias ll='ls -latr'</code> دگرنام جدید <code>ll</code> ایجاد می کنه.</p></li>

<li><p>دگرنام ها، پیکربندی پوسته و توابعی را که معمولاً استفاده می کنی را  در <code dir="ltr">~/.bashrc</code> حفظ کن و <a href="http://superuser.com/a/183980/7106" rel="nofollow"> پوسته ورودی را تنظیم کن</a> تا از آن مبدأ وارد شه. با این کار تنظیمات  در تمام جلسات پوسته در دسترس خواهد بود.</p></li>

<li><p>تنظیمات متغیرهای محیطی و همچنین فرمانهایی را که باید هنگام ورود به سیستم  اجرا شوند را در <code dir="ltr">~/.bash_profile</code>، قرار بده. پیکربندی جداگانه ای برای پوسته هایی که از طریق لاگین در محیط گرافیکی و محیط های <code>cron</code> راه اندازی میشوند مورد نیاز است.</p></li>

<li><p>پرونده های پیکربندی (مانند <code dir="ltr">.bashrc</code> و <code dir="ltr">.bash_profile</code>) را در بین رایانه های مختلف با سیستم کنترل نسخه (Git) همگام‌سازی کن.</p></li>

<li><p>مراقب متغیرها و نام پرونده های دارای فضای خالی (whitespace) باش. متغیرهای بَش را با نماد  نقل قول احاطه کن، برای مثال <code dir="ltr">"$FOO"</code>. آپشن <code dir="ltr">-0</code> و <code dir="ltr">-print0</code> برای فعال کردن کاراکترهای پوچ جهت محدود کردن نام پرونده ها ترجیح بده، مثلا
<code dir="ltr">locate -0 pattern | xargs -0 ls -al</code> یا
<code dir="ltr">find / -print0 -type d | xargs -0 ls -al</code>. برای تکرار روی نام پرونده های حاوی فضای خالی در یک چرخه،  IFS را با استفاده از <code dir="ltr">IFS=$'\n'</code> فقط روی خطوط جدید تنظیم کن.</p></li>

<li><p>در دستورگان بَش، از <code>set -x</code> (یا نوع دیگر <code>set -v</code> که درونداد خام، از جمله متغیرهای غیر منتظره (unexpected variables) و کامنت ها (comments) را ثبت می‌کند) برای رفع اشکال برونداد استفاده کن. از مُد اکید (strict mode) استفاده کن مگر اینکه دلیل خوبی برای این کار نداشته باشی: برای نافرجامی در صورت بروز خطا از <code>set -e</code> استفاده کن (کد خروج غیر صفر). از <code>set -u</code> برای شناسایی متغیرهای تنظیم نشده استفاده کن. مجموعه <code>set -o pipefail</code> را برای نافرجامی در صورت بروز خطا درون pipes را  در نظر بگی (البته در این مورد بیشتر تحقیق کن، چون این موضوع کمی ظریفه). برای دستورگان با درگیری بالا، از <code>trap</code> در EXIT یا ERR  استفاده کن. یک عادت خوب اینه که دستورگان را مانند زیر شروع کنی، که باعث می شه خطاهای رایج را شناسایی و نافرجامی کنه و پیام خطا را چاپ کنه:</p></li>
</ul>

```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```
<ul dir="rtl">
<li><p>در دستورگان بَش، پوسته های فرعی (داخل پرانتز درج می شه) راهی خوبی برای گروه بندی فرمانهای مختلفه. یک کاربرد متداول این روش رفتن موقتی به یک دایرکتوری متفاوت است، به عنوان مثال:</p></li>
</ul>

```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```
<ul dir="rtl">
<li><p>توجه داشته باش در بَش، انواع زیادی از انبساط متغیر (variable expansion) وجود داره. برای بررسی اینکه آیا متغیری وجود دارد یا نه: <code dir="ltr">${name:?error message}</code>.  برای مثال، اگر یک دستورگان بَش به یک نشانه واحد نیاز داره، فقط <code dir="ltr">input_file=${1:?usage: $0 input_file}</code> را بنویس. استفاده از پیش‌فرض در صورت خالی بودن متغیر: <code dir="ltr">${name:-default}</code>. اگر می‌خواهی یک عامل اضافی (اختیاری) به مثال قبلی اضافه کنی، می‌تونی از چیزی مانند <code dir="ltr">output_file=${2:-logfile}</code> استفاده کنی. اگر <code  dir="ltr">$2</code> حذف شه و خالی باشه، <code>output_file</code> روی <code>logfile</code> تنظیم می‌شه. انبساط حسابی (Arithmetic expansion): <code dir="ltr">i=$(( (i + 1) % 5 ))</code>. دنباله ها(Sequences): <code dir="ltr">{1..10}</code>.پیرایش رشته  (Trimming of string): <code dir="ltr">${var%suffix}</code> و <code dir="ltr">${var#prefix}</code>.  برای مثال، اگر <code dir="ltr">var=foo.pdf</code> پس <code dir="ltr">echo ${var%.pdf}.txt</code> برونداد <code>foo.txt</code>  را چاپ میکنه.</p></li>

<li><p>انبساط آکولاد با استفاده از <code>{</code>...<code>}</code> متونه تضمین کنه که متن مشابه کمتر تکرار بشه  و امکان ترکیب اشیاء را فراهم میکنه. این در مواردی مانند <code>mv foo.{txt,pdf} some-dir</code> (هر دو پرونده را منتقل میکنه)، <code dir="ltr">cp somefile{,.bak}</code> (که به <code>cp somefile somefile.bak</code> گسترش میشه داد) یا <code dir="ltr">mkdir -p test-{a,b,c}/subtest-{1,2,3}</code> (همه ترکیب های ممکن را گسترش میده و یک درخت دایرکتوری ایجاد میکنه) مفیده. انبساط آکولاد باید قبل از هر انبساط دیگه ای انجام بشه.</p></li>

<li><p>ترتیب  بسط ها عبارتند از: انبساط آکولاد، انبساط tilde، انبساط عامل و متغیر، انبساط حسابی (arithmetic) و جایگزینی فرمان (از چپ به راست)، جداسازی کلمه و انبساط  نام پرونده. (به عنوان مثال، محدوده ای مانند <code>{1..20}</code> را نمی توان با متغیرهای <code dir="ltr">{$a..$b}</code> بیان کرد. در عوض، از چرخه <code>seq</code> یا <code>for</code> استفاده کن، مثلا <code>seq $a $b</code> یا <code>for((i=a; i&lt;=b; i++)); do ... ; done</code>).</p></li>

<li><p>برونداد فرمان را با استفاده از <code dir="ltr">&lt;(some command)</code> میشه مثل پرونده در نظر گرفت (بهش میگن جانشین‌سازی فرآیند یا process substitution). مثلا  <code  dir="ltr">/etc/hosts</code> لوکال را با ریموت اینطوری مقایسه کن:</p></li>
</ul>

```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

<ul dir="rtl">
<li><p>وقت نوشتن دستورگان، خوبه که اول و آخرکدتو توی آکولاد قرار بدی. اگر آکولاد بسته وجود نداشته باشد، دستورگان به دلیل خطای نحوی اجرا نمیشه. این کار وقتی دستورگان قراره از اینترنت دانلود بشه به درد میخوره، مثلا، جلوی اجرای دستورگان ناقص دانلود شده را میگیره :</p></li>
</ul>

```bash
{
      # Your code here
}
```

<ul dir="rtl">
<li><p>بستک کُد "here document" بهت اجازه میده که <a href="https://www.tldp.org/LDP/abs/html/here-docs.html" rel="nofollow">چندین خط درونداد را تغییر مسیر بدی</a>، مثل یک پرونده:</p></li>
</ul>

```
cat <<EOF
input
on multiple lines
EOF
```

<ul dir="rtl">
<li><p>توی بَش، برونداد استاندارد و خطای استاندارد را با: <code>some-command &gt;logfile 2&gt;&amp;1</code> یا <code>some-command &amp;&gt;logfile</code> تغییر مسیر بده. برای اطمینان از اینکه یک فرمان دستگیره  پرونده باز را روی  ورودی استاندارد رها نکنه و به ترمینالی که توش هستی گره اش نزنه، اغلب تمرین خوبیه که <code dir="ltr">&lt;/dev/null</code> را اضافه کنی.</p></li>

<li><p>از <code>man ascii</code> برای یک جدول ASCII خوب، با مقادیر اعشاری و هگزادسیمال استفاده کن. برای اطلاعات کلی در مورد کُدبندی، <code>man utf-8</code>، <code>man unicode</code> و <code>man latin1</code> کمکت میکنه.</p></li>

<li><p>از <code>screen</code> یا <a href="https://tmux.github.io/" rel="nofollow"><code>tmux</code></a> برای همتافت صفحه استفاده کن، مخصوصا برای دسترسی ریموت از طریق ssh و برای قطع و وصل مجدد به جلسه ترمینال. <code>byobu</code> یا tmux میتونن صفحه نمایش را با ارائه اطلاعات بیشتر و مدیریت آسان تر بهبود ببخشن. یک جایگزین حداقلی فقط برای پایایی جلسه ترمینال، <a href="https://github.com/bogner/dtach"><code>dtach</code></a> هست.</p></li>

<li><p>خوبه که بدونی چطوری میشه در ssh تونل با آپشن  <code dir="ltr">-L</code> یا <code dir="ltr">-D</code> (و گاهی <code dir="ltr">-R</code>) درگاه زد. مثلا موقع دسترسی به وبسایت از کارساز ریموت.</p></li>

<li><p>انجام برخی بهبودها در تنظیمات SSH میتونه مفید باشه. مثلا پیکربندی <code dir="ltr">~/.ssh/config</code> زیر برای جلوگیری از قطع ارتباط در محیط‌های خاص شبکه ست، از فشرده‌سازی (که برای SCP روی اتصالات با پهنای باند کم مفیده) استفاده میکنه و کانال‌ها همتافت را با استفاده از یک پرونده لوکال به کارساز متصل میکنه:</p></li>
</ul>

```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

<ul dir="rtl">
<li><p>برخی دیگر از گزینه های مربوط به SSH دارای حساسیت امنیتی هستند و باید با احتیاط فعال بشن، مثلا فعالسازی فقط روی سابنت یا شبکه  قابل اعتماد: <code dir="ltr">StrictHostKeyChecking=no</code>، <code>ForwardAgent=yes</code>.</p></li>

<li><p>نرم افزار <a href="https://mosh.mit.edu/" rel="nofollow"><code>mosh</code></a> را به عنوان جایگزینی برای ssh در نظر داشته باش، که از UDP برای جلوگیری از قطع شدن اتصالات استفاده می میکنه، که به نوعی راحت تره (البته نیاز به راه اندازی سمت کارساز  داره).</p></li>

<li><p>برای اینکه  دسترسی های هشتگانه پرونده را ببینی، قابلیتی که که برای پیکربندی سیستم مفیده و در <code>ls</code> موجود نیست، و خیلی راحت میشه خرابش کرد، از چیزی مثل این استفاده کن:</p></li>
</ul>

```sh
      stat -c '%A %a %n' /etc/timezone
```

<ul dir="rtl">
<li><p>برای انتخاب تعاملی مقادیر از برونداد یک فرمان دیگر، از <a href="https://github.com/mooz/percol"><code>percol</code></a> یا <a href="https://github.com/junegunn/fzf"><code>fzf</code></a> استفاده کن.</p></li>

<li><p>از <code>fpp</code> (<a dir="ltr" href="https://github.com/facebook/PathPicker">PathPicker</a>) برای تعامل با پرونده ها بر اساس برونداد فرمان دیگر (مانند <code>git</code>) استفاده کن.</p></li>

<li><p>برای راه انداختن یک وب کارساز ساده که همه پرونده های دایرکتوری فعلی (و زیر مجموع هاش) را در دسترس همه در شبکه قرار بده، از <code dir="ltr">python -m SimpleHTTPServer 7777</code> (برای پورت7777 و  Python2) و <code>python -m http.server 7777</code> (برای پورت7777 و  Python3) استفاده کن.</p></li>

<li><p>از <code>sudo</code> برای اجرای یک فرمان به عنوان کاربر دیگر استفاده کن. به طور پیش فرض، روت انتخاب شده. از آپشن <code dir="ltr">-u</code> برای تعیین کاربر دیگر و از <code dir="ltr">-i</code> برای ورود به سیستم به عنوان اون کاربر استفاده کن (رمز عبور<em>خودت</em>  را وارد کن).</p></li>

<li><p>برای تغییر پوسته به کاربر دیگر، از نام کاربری <code>su</code> یا <code>su - username</code> استفاده کن. دومی با "-" وارد محیطی میشی که گویی کاربر دیگری تازه وارد شده. با حذف نام کاربری به طور پیش فرض روت انتخاب میشه. ازت  رمز عبور کاربری که به آن وارد میشد خواسته می شه.</p></li>

<li><p><a href="https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong" rel="nofollow">محدودیت 128k</a> خط فرمان را یادت باشه. خطای "Argument list too long" اغلب هنگامی اتفاق میوفته که نویسۀ جانشین ​با تعداد زیادی پرونده مطابقت داشته باشه (اگر این اتفاق افتاد، گزینه های جایگزین مثل <a href="https://wiki.debian.org/CommonErrorMessages/ArgumentListTooLong" rel="nofollow">محدودیت 128k</a> و <code>xargs</code> می تونه کمک کنه)</p></li>

<li><p>برای یک ماشین حساب اولیه (و البته دسترسی به پایتون)، از مفسّر <code>python</code> استفاده کن. مثلا،</p></li>
</ul>

```
>>> 2+3
5
```

## پردازش پرونده ها و داده ها

<ul dir="rtl">
<li><p>برای پیدا کردن پرونده با نام با درنظرگرفتن دایرکتوری فعلی، <code dir="ltr">find . -iname '*something*'</code> و برای پیدا کردن پرونده با نام در کل سیستم، از <code>locate something</code> استفاده کن (البته توجه داشته باش  که ممکنه <code>updatedb</code> هنوز نمایه پرونده های اخیر را نساخته باشه).</p></li>

<li><p>برای جستجوی کلی در پرونده‌ها یا داده ها، چندین گزینه پیشرفته‌تر یا سریع‌تر از <code>updatedb</code> وجود داره، از جمله (به ترتیب تقریبی از قدیمی‌تر به جدیدتر) the silver searcher <a href="https://github.com/beyondgrep/ack2"><code>ack</code></a>، <a href="https://github.com/ggreer/the_silver_searcher"><code dir="ltr">ag</code></a> و <a href="https://github.com/BurntSushi/ripgrep"><code>rg</code></a> (ripgrep).</p></li>
the silver searcher
<li><p>برای تبدیل HTML به متن: <code>lynx -dump -stdin</code></p></li>

<li><p>برای تبدیل HTML، Markdown، و انواع دیگه تبدیل اسناد  <a href="http://pandoc.org/" rel="nofollow"><code>pandoc</code></a>را امتحان کن. مثلا، برای تبدیل سند Markdown به سند Word: <code dir="ltr">pandoc README.md --from markdown --to docx -o temp.docx</code></p></li>

<li><p>اگر باید از پس XML بر بیای، <code>xmlstarlet</code> قدیمیه ولی خوبه.</p></li>

<li><p>برای JSON، از <a href="http://stedolan.github.io/jq/" rel="nofollow"><code>jq</code></a> استفاده کن. برای استفاده تعاملی، <a href="https://github.com/simeji/jid"><code>jid</code></a> و <a href="https://github.com/fiatjaf/jiq"><code>jiq</code></a> را هم ببین.</p></li>

<li><p>برای YAML از <a href="https://github.com/0k/shyaml"><code>shyaml</code></a> استفاده کن.</p></li>

<li><p>برای پرونده های Excel و CSV،  بسته  <a href="https://github.com/onyxfish/csvkit">csvkit</a> قابلیت های <code>csvjoin</code>، <code>csvcut</code>، <code>in2csv</code>، <code>csvgrep</code>، و غیره را ارائه میده.</p></li>

<li><p> بسته <a href="https://github.com/s3tools/s3cmd"><code>s3cmd</code></a> و <a href="https://github.com/bloomreach/s4cmd"><code>s4cmd</code></a>
کار با آمازون S3 را راحت تر میکنه، <a href="https://github.com/bloomreach/s4cmd"><code>s4cmd</code></a> سریع تره، بسته آمازون <a href="https://github.com/aws/aws-cli"><code>aws</code></a> و ورژن جدیدش <a href="https://github.com/donnemartin/saws"><code>saws</code></a> برای انجام کارهای مربوط به AWS ضروریه.</p></li>

<li><p>دستورهای <code>sort</code> و <code>uniq</code> را بشناس، همینطور آپشن های uniq شامل <code dir="ltr">-u</code> و <code dir="ltr">-d</code> -- به دستورهای یک خطی پایین مراجعه شود. <code>comm</code> را هم ببین.</p></li>

<li><p>برای دستکاری پرونده‌های متنی،  از <code dir="ltr">cut</code>، <code>paste</code> و <code>join</code> استفاده کن. خیلی ها از <code>cut</code> استفاده میکنن ولی <code>join</code> را فراموش میکنن.</p></li>

<li><p>فرمان <code>wc</code> را برای شمارش خطوط جدید (<code dir="ltr">-l</code>)، کاراکترها (<code dir="ltr">-m</code>)، کلمات (<code dir="ltr">-w</code>) و بایت‌ها (<code dir=ltr>-c</code>) یاد بگیر.</p></li>

<li><p>فرمان <code>tee</code> را برای رونوشت از stdin به پرونده و همچنین به stdout (مثل <code dir="ltr">ls -al | tee file.txt</code>) یاد بگیر.</p></li>

<li><p>برای محاسبات پیچیده تر، از جمله گروه بندی، معکوس کردن فیلدها، و محاسبات آماری، <a href="https://www.gnu.org/software/datamash/" rel="nofollow"><code>datamash</code></a> را در نظر داشته باش.</p></li>

<li><p>توجه داشته باش که تنظیمات زبان محلی ("locale") بر بسیاری از ابزارهای خط فرمان به روش های ظریفی از جمله ترتیب مرتب سازی (sort)  و عملکرد آنها تأثیر می گذاره. اکثر سیستم های لینوکس <code>LANG</code> یا سایر متغیرهای محلی را روی تنظیمات محلی پیشفرض مثل US English تنظیم می‌کنند.  اما باید توجه داشته باشی که اگر locale را تغییر بدی رفتار مرتب‌سازی تغییر میکنه و بدونی که روال های "i18n" میتونه  سرعت "مرتب سازی" و سایر فرمان ها را <em>چند برابر</em> کند میکنه. در برخی موقعیت‌ها (مانند عملیات های set  یا عملیات منحصر به فردی که در زیر میاد) می‌توانید با خیال راحت روال‌های کند «i18n» را نادیده بگیری و با تنظیم <code dir="ltr">export LC_ALL=C</code> از ترتیب مرتب‌سازی سنتی مبتنی بر بایت استفاده کنی.</p></li>

<li><p>میتونی محیط یک فرمان خاص را با فراخوان فرمان بهمراه پیشوند تنظیمات متغیر محیطی تنظیم کنی، مانند <code dir="ltr">TZ=Pacific/Fiji date</code>.</p></li>

<li><p>مبانی اولیه <code>awk</code> و <code>sed</code> را برای munging ساده داده ها یاد بگیر. نمونشو در قسمت <a href="#%D8%AA%DA%A9-%D8%AE%D8%B7%DB%8C-%D9%87%D8%A7">تک خطی ها</a> ببین.</p></li>

<li><p>برای جایگزینی تمام رخدادهای یک رشته به صورت درجا، در یک یا چند پرونده:</p></li>
</ul>

```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```
<ul dir="rtl">
<li><p>برای تغییر نام چندین پرونده و همچنین جستجو/جایگزینی درون پرونده‌ها، <a href="https://github.com/jlevy/repren"><code>repren</code></a> را امتحان کن (گاهی اوقات میتونی چندین پرونده را با <code>rename</code> تغییرنام  بدی، اما مراقب باش چون عملکردش در توزیع های لینوکس متفاوت است.)</p></li>
</ul>

```sh
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Recover backup files whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Same as above, using rename, if available:
      rename 's/\.bak$//' *.bak
```

<ul dir="rtl">
<li><p>همانطور که صفحه man میگه، <code>rsync</code> واقعا یک ابزار کپی پرونده سریع و فوق العاده و همه کارست. برای همگام سازی بین ماشین ها شناخته شده اما به همون اندازه در محیط لوکال مفید است. وقتی محدودیت‌های امنیتی اجازه می‌دهند، استفاده از <code>rsync</code> به جای <code>scp</code> امکان بازیابی انتقال داده را بدون شروع مجدد از ابتدا فراهم میکنه. همچنین یکی از <a href="https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html" rel="nofollow">سریع ترین هاست</a>. جهت  حذف تعداد زیادی پرونده:</p></li>
</ul>

```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```
<ul dir="rtl">
<li><p>برای پایش و نظارت بر پیشرفت پردازش پروندها، از
<a dir="ltr" href="http://www.ivarch.com/programs/pv.shtml" rel="nofollow"><code>pv</code></a>،
<a href="https://github.com/dmerejkowsky/pycp"><code>pycp</code></a>،
<a href="https://github.com/dspinellis/pmonitor"><code>pmonitor</code></a>،
<a href="https://github.com/Xfennec/progress"><code>progress</code></a>،  <code dir="ltr">rsync --progress</code> یا برای رونوشت در سطح بلوک، از  <code>dd status=progress</code> استفاده کن.</p></li>

<li><p>از <code>shuf</code> برای مخلوط کردن  یا انتخاب خطوط تصادفی از یک پرونده استفاده کن.</p></li>

<li><p>آپشن های <code>sort</code> را بشناس. از <code dir="ltr">-n</code> یا <code dir="ltr">-h</code> برای اعداد قابل خوندن توسط انسان (مانند <code dir="ltr">du -h</code>) استفاده کن. از نحوه عملکرد کلیدها آگاه باش (<code dir="ltr">-t</code> و <code dir="ltr">-k</code>). به ویژه، توجه داشته باشید که برای مرتب سازی در فیلد اول باید از <code dir="ltr">-k1,1</code> استفاده کنی. <code dir="ltr">-k1</code> به معنای مرتب کردن بر روی کل خط است.  مرتب سازی  پایدار (<code dir="ltr">sort -s</code>) نیز می تونه مفید باشد.   به عنوان مثال، برای مرتب سازی در درجه اول بر اساس فیلد 2 و در درجه دوم بر اساس فیلد 1، میتونی از <code dir="ltr">sort -k1,1 | sort -s -k2,2</code> استفاده کنی.</p></li>

<li><p>اگر زمانی نیاز به نوشتن کاراکتر جهش  (tab literal) در خط فرمان بَش داشتی، مثلاً برای مرتب سازی نشانه t- <strong dir="ltr">ctrl-v</strong> <strong dir="ltr">[Tab]</strong> را فشار بده یا <code dir="ltr">$'\t'</code> را بنویس. (دومی بهتره چونکه میتونی بردار و بچسبان کنی).</p></li>

<li><p>ابزارهای استاندارد وصله کد منبع <code>diff</code> و <code>patch</code> هستند. همچنین برای دریافت آمار خلاصه تفاوت، <code>diffstat</code> را ببین و <code>sdiff</code> برای نمایش همبَر تفاوت ها. توجه داشته باش که <code>diff -r</code> روی کل دایرکتوری کار می کنه. از <code>diff -r tree1 tree2 | diffstat</code> برای دریافت نمای کلی از همه تغییرات استفاده کن. از <code>vimdiff</code> برای مقایسه و ویرایش پرونده ها استفاده کن.</p></li>

<li><p>برای پرونده‌های دوحالتی از <code>hd</code>، <code dir="lrt">hexdump</code> یا <code>xxd</code> برای یک <a href="https://de.wikipedia.org/wiki/Dump#Hexdump" rel="nofollow">Hexdumps</a> ساده از <code>bvi</code> و از <code>hexedit</code> و <code>biew</code> برای پیرایش دوحالتی ها استفاده کن.</p></li>

<li><p>باز هم برای دوحالتی، <code>strings</code> (به علاوه <code>grep</code> و غیره) بهت امکان میده بیت های توی متن و پیدا کنی.</p></li>

<li><p>برای تفاوت‌های دوحالتی (<a href="https://en.wikipedia.org/wiki/Binary_delta_compression" rel="nofollow">delta compression</a>)، از <code>xdelta3</code> استفاده کن.</p></li>

<li><p>برای تبدیل بین کُدبندی های مبتنی بر متن (<a href="https://en.wikipedia.org/wiki/Character_encoding" rel="nofollow">text encoding</a>)،از <code>iconv</code> یا برای موارد پیشرفته از <code>uconv</code> استفاده کن چون چیزهای پیشرفته یونیکُد را پشتیبانی میکنه.  مثلا:</p></li>
</ul>

```sh
      # Displays hex codes or actual names of characters (useful for debugging):
      uconv -f utf-8 -t utf-8 -x '::Any-Hex;' < input.txt
      uconv -f utf-8 -t utf-8 -x '::Any-Name;' < input.txt
      # Lowercase and removes all accents (by expanding and dropping them):
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC;' < input.txt > output.txt
```
<ul dir="rtl">
<li><p>برای تقسیم پرونده ها به قطعات کوچکتر از، <code>split</code> (تقسیم بر اساس اندازه) و <code>csplit</code> (تقسیم بر اساس الگو) استفاده کن.</p></li>

<li><p>تاریخ و زمان: برای دریافت تاریخ و زمان فعلی به شکل قابل استفاده <a href="https://en.wikipedia.org/wiki/ISO_8601" rel="nofollow">ISO 8601</a>، از
<code dir="ltr">date -u +"%Y-%m-%dT%H:%M:%SZ"</code>استفاده کن  (فرمت های  دیگه  <a href="https://stackoverflow.com/questions/7216358/date-command-on-os-x-doesnt-have-iso-8601-i-option" rel="nofollow">مشکل</a> <a href="https://unix.stackexchange.com/questions/164826/date-command-iso-8601-option" rel="nofollow">دارند</a>). برای دستکاری عبارات تاریخ و زمان، از  <code dir="ltr">dateadd</code>، <code>datediff</code>، <code dir="ltr">strptime</code> و غیره استفاده کن،  منبع  <a href="http://www.fresse.org/dateutils/" rel="nofollow"><code>dateutils</code></a>.</p></li>

<li><p>از <code dir="ltr">zless</code>، <code>zcat</code>،<code>zmore</code> و <code>zgrep</code> برای کار بر روی پرونده های فشرده استفاده کن.</p></li>

<li><p>ویژگی های پرونده را میتونی با <code>chattr</code> تنظیم کنی که جایگزین سطح پایین تری برای مجوزهای پرونده (file permissions) هست. مثلا، برای جلوگیری از حذف تصادفی یک پرونده، فلگ غیرقابل تغییر تنظیم کن: <code dir="ltr">sudo chattr +i /critical/directory/or/file</code></p></li>

<li><p>از <code>getfacl</code> و <code>setfacl</code> برای ذخیره و بازیابی مجوزهای پرونده استفاده کن. مثلا:</p></li>
</ul>

```sh
   getfacl -R /some/path > permissions.txt
   setfacl --restore=permissions.txt
```
<ul dir="rtl">
<li><p>برای ایجاد سریع یک پرونده خالی، از <code dir="ltr">setfacl</code> ایجاد <a href="https://en.wikipedia.org/wiki/Sparse_file" rel="nofollow">پرونده sparse</a>، <code dir="ltr">fallocate</code> سیستم‌پرونده های xfs، btrfs، ocfs2 و ext4،  <code>xfs_mkfile</code> برای تقریباً هر پرونده سیستمی ای که در بسته  xfsprogs هست، <code>mkfile</code> برای سیستم‌های مشابه یونیکس مانند Solaris، مک اواس.</p></li>
</ul>

## رفع اشکال سیستم

<ul dir="rtl">
<li><p>برای اشکال زدایی وب، <code>curl</code> و <code>curl -I</code> مفید هستند، یا مشابهش <code>wget</code>، یا مشابه مدرنترش <a href="https://github.com/jkbrzt/httpie"><code>httpie</code></a>.</p></li>

<li><p>برای اطلاع از وضعیت فعلی cpu/دیسک، ابزارهای کلاسیک عبارتند از <code>top</code>  (یا بهتر <code>htop</code>)، <code>iostat</code> و <code>iotop</code>. از <code>iostat -mxz 15</code> برای گزارش پایه از CPU و گزارش مفصل از وضعیت پارتیشن های دیسک و بینش های عملکردی استفاده کن.</p></li>

<li><p>برای جزئیات اتصال شبکه، از <code>netstat</code> و <code>ss</code> استفاده کن.</p></li>

<li><p>برای یک نمای کلی از آنچه توی سیستم اتفاق می افته، <code>dstat</code> بسیار مفیده. برای نمای کلی با جزئیات، از <a href="https://github.com/nicolargo/glances"><code>glances</code></a> استفاده کن.</p></li>

<li><p>برای اطلاع از وضعیت حافظه، برونداد <code>free</code> و <code>vmstat</code> را ببین و خوب هضمش کن. مخصصا، توجه داشته باش که مقدار"cached"، حافظه ای است که توسط هسته لینوکس به عنوان نهانگاه پرونده استفاده می شه وعملا فضای خالی حساب می شه.</p></li>

<li><p>اشکال یابی سیستم جاوا بازی موش و گربست، اما یک ترفند ساده در Oracle و برخی JVM های دیگر این است که می توانی با  <code dir="ltr">kill -3 &lt;pid&gt;</code> برگرفت کامل stack trace و خلاصه heap (شامل جزئیات garbage collection، که می میتونه خیلی بدرد بخور باشه) را به stderr/logs بفرستی. در کیت توسعه جاوا <code dir="ltr">jps</code>، <code>jmap</code>، <code>jstack</code>، <code>jstat</code> به درد میخورن. برای ابزارهای پیشرفته تر <a href="https://github.com/aragozin/jvm-tools">SJK tools</a> را ببین.</p></li>

<li><p>از <a href="http://www.bitwizard.nl/mtr/" rel="nofollow"><code>mtr</code></a> به عنوان ردیابی بهتر از traceroute  برای شناسایی مشکلات شبکه استفاده کن.</p></li>

<li><p>برای بررسی اینکه چرا دیسک پر شده، <a href="https://dev.yorhel.nl/ncdu" rel="nofollow"><code>ncdu</code></a> در مقایسه با بقیه (مثلا <code dir="ltr">du -sh *</code>) وقت کمتری میبره.</p></li>

<li><p>برای اینکه بفهمی کدام سوکت یا فرآیند از پهنای باند استفاده می کنه، <a href="http://www.ex-parrot.com/~pdw/iftop/" rel="nofollow"><code>iftop</code></a> یا <a href="https://github.com/raboof/nethogs"><code>nethogs</code></a> را امتحان کن.</p></li>

<li><p>ابزار <code>ab</code> (توی بسته Apache) برای بررسی فوری فوتی عملکرد کارسازهای وب مفیده. برای آزمایش بار پیچیده تر، <code>siege</code> را امتحان کن.
</p></li>
<li><p>برای اشکال زدایی جدی تر شبکه ، <a href="https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html" rel="nofollow"><code>tshark</code></a>، <a href="https://wireshark.org/" rel="nofollow"><code>wireshark</code></a> یا <a href="http://ngrep.sourceforge.net/" rel="nofollow"><code>ngrep</code></a> را ببین.</p></li>

<li><p>دستورهای <code>strace</code> و <code>ltrace</code> را یاد بگیر. اگر برنامه ای خراب شده، گیرکرده  یا از کار افتاده و دلیلشو ندونی، یا اگر می خوای  یک ایده کلی از عملکرد سیستم به دست بیاری، این فرمان ها می تونه مفید باشه. به آپشن پرونده سازی (<code dir="ltr">-c</code>) و قابلیت  چسبیدن به یک فرآیند در حال اجرا (<code dir="ltr">-p</code>) توجه کن. برای جلوگیری از دست دادن تماس های مهم، از trace child   آپشن (<code dir="ltr">-f</code>)  استفاده کن.</p></li>

<li><p>با <code>ldd</code> کتابخانه های مشترک و غیره را بررسی کن - اما <a href="http://www.catonmat.net/blog/ldd-arbitrary-code-execution/" rel="nofollow">هرگز روی پرونده های ناشناس اجراش نکن</a>.</p></li>

<li><p>یادبگیر که چطوری با <code>gdb</code> به یک فرآیند در حال اجرا متصل بشی  و stack trace اونرو دریافت کنی.</p></li>

<li><p> از <code dir="ltr">/proc</code> استفاده کن. بعضی وقتها  هنگام اشکال زدایی مشکلات زنده به طرز شگفت انگیزی مفیده. مثالها: 
<code dir="ltr">/proc/cpuinfo</code>، <code dir="ltr">/proc/meminfo</code>، <code dir="ltr">/proc/cmdline</code>، <code dir="ltr">/proc/xxx/cwd</code>، <code dir="ltr">/proc/xxx/exe</code>، <code dir="ltr">/proc/xxx/fd/</code>،
<code dir="ltr">/proc/xxx/smaps/</code> (که در اینجا <code>xxx</code> عبارت است از شناسه فرآیند  یا pid).</p></li>

<li><p>هنگام اشکال یابی مشکلی که در گذشته اتفاق افتاده، <a href="http://sebastien.godard.pagesperso-orange.fr/" rel="nofollow"><code>sar</code></a> میتونه خیلی مفید باشه. آمار تاریخی مربوط به CPU، حافظه، شبکه و غیره را نشون میده.</p></li>

<li><p>برای سیستم های عمیق تر و تجزیه و تحلیل عملکرد، از <a href="https://en.wikipedia.org/wiki/Perf_%28Linux%29" rel="nofollow"><code>perf</code></a>،<code>stap</code> <a href="https://sourceware.org/systemtap/wiki" rel="nofollow">SystemTap</a> و <a href="https://github.com/draios/sysdig"><code>sysdig</code></a> کمک بگیر.</p></li>

<li><p>با فرمان <code>uname</code> یا <code dir="ltr">uname -a</code> اطلاعات عمومی یونیکس/هسته را ببین  یا با <code dir="ltr">lsb_release -a</code> (اطلاعات توزیع لینوکس) ببین از چه سیستم عاملی استفاده می کنی.</p></li>

<li><p>هر وقت چیزی عجیب غریبی پیش اومد از <code>dmesg</code> استفاده کن (ممکنه سخت افزار  یا نرم افزار باشه).</p></li>

<li><p>اگر پرونده ای را حذف کردی و <code>du</code> نشون نداد که فضای مورد انتظار دیسک  آزاد شده، ببین آیا اون پرونده توسط یک فرایند دیگه استفاده میشه: <code dir="ltr">lsof | grep deleted | grep "filename-of-my-big-file"</code></p></li>
</ul>

## تک خطی ها

چند نمونه از چسبوندن فرمان ها به هم:

<ul dir="rtl">
<li><p>گاهی اوقات خیلی مفیده که میتونی تجمیع،  تقاطع و تفاوت پرونده‌های متنی را با <code>uniq</code>/<code>sort</code> انجام بدی. فرض کن <code>a</code> و <code>b</code> پرونده های منحصر به فرد متنی هستند. این روش سریعه و روی  پرونده‌هایی با اندازه دلخواه، تا چندین گیگابایت کار می‌کنه. (مرتب‌سازی به حافظه محدود نمی‌شه، اگرچه ممکنه لازم باشه از گزینه <code dir="ltr">-T</code> استفاده کنی اگر <code dir="ltr">/tmp</code> روی یک پارتیشن روت  کوچیک قرار گرفته.) همچنین به نکته <code dir="ltr">LC_ALL</code>  و آپشن <code dir="ltr">-u</code> فرمان <code>sort</code> در بالا  مراجعه کن.  (اینجا دیگه راجعبش توضیح ندادم).</p></li>
</ul>

```sh
      sort a b | uniq > c   # c is a union b
      sort a b | uniq -d > c   # c is a intersect b
      sort a b b | uniq -u > c   # c is set difference a - b
```
<ul dir="rtl">
<li><p>دو تا پرونده JSON را به زیبایی چاپ کن، syntax آنها را بهنجار (normalize) کن، سپس نتیجه را  رنگ آمیزی و صفحه بندی کن:</p></li>
</ul>

```
      diff <(jq --sort-keys . < file1.json) <(jq --sort-keys . < file2.json) | colordiff | less -R
```

<ul dir="rtl">
<li><p>برای بررسی سریع محتویات همه پرونده‌ها در یک دایرکتوری از <code dir="ltr">grep . *</code> استفاده کن. (اینطوری هر خط با نام پرونده جفت میشه) یا <code dir="ltr">head -100 *</code> (اینطوری نام پرونده به صورت هدلاین نشون داده میشه) این می تونه برای دایرکتوری هایی که پر از پرونده های تنظیمات هستند مفید باشه مثلا: <code dir="ltr">/sys</code>، <code dir="ltr">/proc</code> و <code dir="ltr">/etc</code>.</p></li>

<li><p>جمع کردن تمام اعداد در ستون سوم یک پرونده متنی (این احتمالاً 3 برابر سریعتر و 3 برابر کمتر از معادل کد پایتونه):</p></li>
</ul>

```sh
      awk '{ x += $3 } END { print x }' myfile
```

<ul dir="rtl">
<li><p>برای دیدن اندازه‌ها/ تاریخ‌ها به صورت tree، این مانند یک <code>ls -l</code> برگشتیه (recursive)، اما خوندن اون آسان‌تره از <code>ls -lR</code>:</p></li>
</ul>

```sh
      find . -type f -ls
```
<ul dir="rtl">
<li><p>فرض کنید یک پرونده متنی، مثل  گزارش وب سرور داری  و مقدار مشخصی داری که در برخی از خطوط ظاهر می شه، مانند پارامتر <code>acct_id</code> که در URL وجود دارد. اگر بخوای تعداد درخواست ها برای هر <code>acct_id</code> را محاسبه کنی:</p></li>
</ul>

```sh
      egrep -o 'acct_id=[0-9]+' access.log | cut -d= -f2 | sort | uniq -c | sort -rn
```

<ul dir="rtl">
<li><p>برای نظارت مداوم بر تغییرات، از <code>watch</code> استفاده کن، مثلا  با <code dir="ltr">watch -d -n 2 'ls -rtlh | tail'</code> تغییرات پرونده‌های موجود در دایرکتوری را بررسی کن یا هنگام عیب یابی تنظیمات وای فای با <code dir="ltr">watch -d -n 2 ifconfig</code>، تغییرات شبکه را دائم نظرات کن.</p></li>

<li><p>این تابع را اجرا کنید تا یک نکته تصادفی از این سند دریافت کنید (Markdown را تجزیه می کنه و یک مورد را استخراج می کنه):</p></li>
</ul>

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


## گمنام ولی مفید

<ul dir="rtl">
<li><p><code dir="rtl">expr</code>: انجام عملیات حسابی یا بولی یا ارزیابی عبارات منظم</p></li>

<li><p><code dir="rtl">m4</code>: یک پردازشگر ساده ماکرو</p></li>

<li><p><code dir="rtl">yes</code>: یک رشته را مدام چاپ میکنه</p></li>

<li><p><code dir="rtl">cal</code>: یک تقویم خوب</p></li>

<li><p><code dir="rtl">env</code>: اجرای فرمان (تو دستورگان‌نویسی به درد میخوره)</p></li>

<li><p><code dir="rtl">printenv</code>: چاپ متغیرهای محیطی (در اشکال زدایی و دستورگان‌ها به درد میخوره)</p></li>

<li><p><code dir="rtl">look</code>: کلمات انگلیسی (یا خطوط در پرونده) که  رشته شروع میشن و پیدا میکنه</p></li>

<li><p><code dir="rtl">cut</code>, <code>paste</code> و <code>join</code>: دستکاری داده</p></li>

<li><p><code dir="rtl">join</code>: قالب بندی پاراگراف های متنی</p></li>

<li><p><code dir="rtl">pr</code>: قالب بندی متن به صفحات/ستون ها</p></li>

<li><p><code dir="rtl">fold</code>: پیچیدن خطوط متن</p></li>

<li><p><code dir="rtl">column</code>: قالب بندی فیلدهای متنی به ستون ها یا جداول تراز شده با عرض ثابت</p></li>

<li><p><code dir="rtl">expand</code> و <code>unexpand</code>: تبدیل بین جهش  (tab) و فاصله</p></li>

<li><p><code dir="rtl">nl</code>: اضافه کردن شماره خطوط</p></li>

<li><p><code dir="rtl">seq</code>: چاپ اعداد</p></li>

<li><p><code dir="rtl">bc</code>: ماشین حساب</p></li>

<li><p><code dir="rtl">factor</code>: فاکتور کردن اعداد صحیح</p></li>

<li><p><a dir="rtl" href="https://gnupg.org/" rel="nofollow"><code>gpg</code></a>: رمزگذاری و امضا کردن پرونده ها</p></li>

<li><p><code dir="rtl">toe</code>: توضیحات ترمینال را فهرست می کنه</p></li>

<li><p><code dir="rtl">nc</code> :اشکال زدایی شبکه و انتقال داده</p></li>

<li><p><code dir="rtl">socat</code>: رله سوکت و انتقال دهنده پورت tcp
(شبیه  <code dir="rtl">netcat</code>)</p></li>

<li><p><a  dir="rtl" href="https://github.com/mattthias/slurm"><code>slurm</code></a>: تصور ترافیک شبکه</p></li>

<li><p><code dir="rtl">dd</code>: انتقال داده ها بین پرونده ها یا دستگاه ها</p></li>

<li><p><code dir="rtl">file</code>: شناسایی نوع پرونده</p></li>

<li><p><code dir="rtl">tree</code>: نمایش دایرکتوری ها و زیر شاخه ها به عنوان یک درخت tree  تودرتو. مانند `ls` اما بازگشتی</p></li>

<li><p><code dir="rtl">stat</code>: اطلاعات پرونده</p></li>

<li><p><code dir="rtl">time</code>: اجرای فرمان با تایمر</p></li>

<li><p><code dir="rtl">timeout</code>: یک فرمان را برای مدت زمان مشخصی اجرا میکنه  و پس از اتمام مدت زمان مشخص، فرآیند را متوقف میکنه.</p></li>

<li><p><code dir="rtl">lockfile</code>: پرونده سمافور ایجاد میکنه که فقط با `rm -f` قابل حذفه</p></li>

<li><p><code dir="rtl">logrotate</code>: چرخش، فشرده‌سازی و ارسال گزارش‌ها.</p></li>

<li><p><code dir="rtl">watch</code>: یک فرمان را به طور مکرر اجرا میکنه، نتایج را نشان میده و یا تغییرات را برجسته میکنه</p></li>

<li><p><a  dir="rtl" href="https://github.com/joh/when-changed"><code>when-changed</code></a>: هر وقتی که پرونده تغییر کنه، یک فرمان مشخص را اجرا میکنه. <code>inotifywait</code> و <code>entr</code> را هم ببین.</p></li>

<li><p><code dir="rtl">tac</code>: چاپ معکوس پرونده ها</p></li>

<li><p><code dir="rtl">comm</code>: پرونده های مرتب شده را خط به خط مقایسه میکنه</p></li>

<li><p><code dir="rtl">strings</code>: استخراج متن از پرونده های دوحالتی</p></li>

<li><p><code dir="rtl">tr</code>: ترجمه یا دستکاری کاراکتر</p></li>

<li><p><code dir="rtl">iconv</code> یا <code>uconv</code>: تغییر کدگذاری (encoding) متن</p></li>

<li><p><code dir="rtl">split</code> و <code>csplit</code>: تقسیم پرونده ها</p></li>

<li><p><code dir="rtl">sponge</code>: تمام ورودی ها را اول بخون بعد بنویس، مفید برای خوندن وسپس نوشتن در همون پرونده، مثلا: <code>grep -v something some-file | sponge some-file</code></p></li>

<li><p><code dir="rtl">units</code>: تبدیل واحدها  و محاسبات. تبدیل furlongs هر دو هفته یک بار در یک چشم بهم زدن به twips  (اینجا را ببین<code>/usr/share/units/definitions.units</code>)</p></li>

<li><p><code dir="rtl">apg</code>: رمزهای عبور تصادفی تولید می کنه</p></li>

<li><p><code dir="rtl">xz</code>: فشرده سازی پرونده با نسبت بالا</p></li>

<li><p><code dir="rtl">ldd</code>: اطلاعات کتابخانه پویا</p></li>

<li><p><code dir="rtl">nm</code>: لیست سیمبول های یک پرونده شیء (object)</p></li>

<li><p><code dir="rtl">ab</code> یا <a href="https://github.com/wg/wrk"><code>wrk</code></a>: محک زدن کارسازهای وب</p></li>

<li><p><code dir="rtl">strace</code>: اشکال زدایی تماس های سیستمی</p></li>

<li><p><a  dir="rtl" href="http://www.bitwizard.nl/mtr/" rel="nofollow"><code>mtr</code></a>: ردیابی بهتر (traceroute) برای اشکال زدایی شبکه</p></li>

<li><p><code dir="rtl">cssh</code>: نمایش پوسته های همزمان</p></li>

<li><p><code dir="rtl">rsync</code>: پرونده ها و پوشه ها را از طریق SSH یا در سیستم لوکال همگام سازی میکنه</p></li>

<li><p><a  dir="rtl" href="https://wireshark.org/" rel="nofollow"><code>wireshark</code></a> و <a href="https://www.wireshark.org/docs/wsug_html_chunked/AppToolstshark.html" rel="nofollow"><code>tshark</code></a>: پکت کپچر و اشکال زدایی شبکه</p></li>

<li><p><a  dir="rtl" href="http://ngrep.sourceforge.net/" rel="nofollow"><code>ngrep</code></a>: grep برای لایه شبکه</p></li>

<li><p><code dir="rtl">host</code> و <code>dig</code>: جستجوهای DNS</p></li>

<li><p><code dir="rtl">lsof</code>: پردازش توضیحات پرونده و اطلاعات سوکت</p></li>

<li><p><code dir="rtl">dstat</code>: اطلاعات آماری مفید سیستم</p></li>

<li><p><a  dir="rtl" href="https://github.com/nicolargo/glances"><code>glances</code></a>: نمای کلی زیرسیستم های متعدد</p></li>

<li><p><code dir="rtl">iostat</code>: آمار استفاده از دیسک</p></li>

<li><p><code dir="rtl">mpstat</code>: آمار استفاده ازCPU</p></li>

<li><p><code dir="rtl">vmstat</code>: آمار استفاده از حافظه</p></li>

<li><p><code dir="rtl">htop</code>: نسخه بهبود یافته top</p></li>

<li><p><code dir="rtl">last</code>: تاریخچه ورود</p></li>

<li><p><code dir="rtl">w</code>: چه کسی وارد سیستم  شده</p></li>

<li><p><code dir="rtl">id</code>: اطلاعات هویت کاربر/گروه</p></li>

<li><p><a  dir="rtl" href="http://sebastien.godard.pagesperso-orange.fr/" rel="nofollow"><code>sar</code></a>: آمار تاریخی سیستم</p></li>

<li><p><a  dir="rtl" href="http://www.ex-parrot.com/~pdw/iftop/" rel="nofollow"><code>iftop</code></a> یا <a href="https://github.com/raboof/nethogs"><code>nethogs</code></a>: بهره برداری از شبکه توسط سوکت یا فرآیند</p></li>

<li><p><code dir="rtl">ss</code>: آمار سوکت ها</p></li>

<li><p><code dir="rtl">dmesg</code>: پیام های خطای راهاندازی و سیستم</p></li>

<li><p><code dir="rtl">sysctl</code>: مشاهده و پیکربندی پارامترهای هسته لینوکس در زمان اجرا</p></li>

<li><p><code dir="rtl">hdparm</code>: عملکرد و دستکاری دیسک SATA / ATA</p></li>

<li><p><code dir="rtl">lsblk</code>: لیست بلوک دستگاه ها: نمای درختی از دیسک ها و پارتیشن های دیسک</p></li>

<li><p dir="rtl"><code>lshw</code>, <code >lscpu</code>, <code>lspci</code>, <code>lsusb</code>, <code>dmidecode</code>: اطلاعات سخت افزاری، از جمله CPU، BIOS، RAID، گرافیک، دستگاه ها و غیره.</p></li>

<li><p dir="rtl"><code >lsmod</code> و <code>modinfo</code>: فهرست و نمایش جزئیات ماژول های هسته.

<li><p dir="rtl"><code>fortune</code>, <code>ddate</code> و <code  >sl</code>: خوب، بستگی به این دارد که آیا لوکوموتیوهای بخار و نقل قول های Zippy را "مفید" بدونی</p></li>
</ul>

## فقط مک اواس

این موارد <em>فقط</em> شامل مک اواس میشن.

<ul dir="rtl">
<li><p>مدیریت بسته  با <code dir="ltr">brew</code> Homebrew و/ یا <code dir="ltr">port</code> MacPorts. از اینها میتونی برای نصب بسیاری از فرمان های بالا در مک اواس استفاده کنی.</p></li>

<li><p>برونداد فرمان را  با <code>pbcopy</code> به کلیپ برد بفرست  و با <code>pbpaste</code>  از همونجا  به ورودی ترمینال ارسال کن.</p></li>

<li><p>برای فعال کردن کلید آپشن (Option key) در ترمینال مک اواس  به عنوان کلید alt (برای  استفاده از فرمان ها بالا مثل <strong>alt-b</strong>، <strong>alt-f</strong> و غیره)، برو به  Preferences -> Profiles -> Keyboard  و آپشن  "Use Option as Meta key" را انتخاب کن .</p></li>

<li><p>برای باز کردن یک پرونده با یک برنامه رومیزی، از <code>open</code> استفاده کن یا: <code>open -a /Applications/Whatever.app</code></p></li>

<li><p>در Spotlight: پرونده‌ها را با <code>mdfind</code> جستجو کن و فراداده ها  (metadata مانند اطلاعات EXIF عکس)  را با <code>mdls</code> لیست کن.</p></li>

<li><p>توجه داشته باش که  مک اواس  مبتنی بر BSD Unix است و بسیاری از فرمان ها (مانند <code>ps</code>, <code>ls</code>, <code>tail</code>, <code>awk</code>, <code>sed</code>) به روش‌های ظریفی با لینوکس  که به شدت تحت تأثیر یونیکس به سبک V و ابزارهای GNU هست متفاوت است. اغلب می تونی تفاوت را با این واقعیت تشخیص بدی  که  صفحه man عنوان "راهنمای فرمان ها عمومی BSD" را داره. در برخی موارد، نسخه GNU فرمان ها نیز قابل نصب است (مانند <code>gawk</code> و <code>gsed</code> برای نسخه گنو awk و sed). اگر می‌خواهی دستورگان بَش بین پلتفرمی بنویسی، باید از چنین فرمان هایی اجتناب کنی (و به عنوان مثال از Python یا <code>perl</code> استفاده کنی) یا دستورگان را با دقت آزمایش کنی.</p></li>

<li><p> برای دریافت اطلاعات انتشار مک او اس، از <code>sw_vers</code> استفاده کن.</p></li>
</ul>

## فقط ویندوز

این موارد <em>فقط</em> شامل ویندوز میشن.

### روشهای بدست آوردن ابزارهای یونیکس در ویندوز
<ul dir="rtl">
<li><p>با نصب <a href="https://cygwin.com/" rel="nofollow">Cygwin</a> به قدرت پوسته یونیکس درمایکروسافت ویندوز دسترسی پیدا کن. بسیاری از مواردی که در این سند توضیح داده شده بی دردسر کار خواهد کرد.</p></li>

<li><p>در ویندوز 10، می‌توانی از <a href="https://msdn.microsoft.com/commandline/wsl/about" rel="nofollow">Windows Subsystem برای لینوکس (WSL)</a> استفاده کنی که یک محیط  بش  سازگار با ابزارهای خط فرمان یونیکس فراهم می‌کنه.</p></li>

<li><p> اگر عمدتاً می خوای از ابزارهای توسعه دهنده گنو (مانند GCC) در ویندوز استفاده کنی، <a href="http://www.mingw.org/" rel="nofollow">MinGW</a> و بسته <a href="http://www.mingw.org/wiki/msys" rel="nofollow">MSYS</a> اون را در نظر بگیر که ابزارهایی مانند bash، gawk، make و grep را ارائه می ده. MSYS در مقایسه با Cygwin همه ویژگی ها را نداره. MinGW به ویژه برای پورت ابزارهای بومی یونیکس به ویندوز مفیده.</p></li>

<li><p>گزینه دیگه برای به دست آوردن ظاهر و احساس یونیکس در ویندوز، <a href="https://github.com/dthree/cash">Cash</a> هست. توجه داشته باش که تنها تعداد بسیار کمی از فرمان ها یونیکس و گزینه های خط فرمان در این محیط وجود داره.</p></li>
</ul>

### ابزارهای مفید خط فرمان در ویندوز
<ul dir="rtl">
<li><p>با یادگیری و استفاده از <code>wmic</code> می توانی اکثر وظایف مدیریت سیستم ویندوز را از خط فرمان انجام بدی و دستورگان‌نویسی کنی.</p></li>

<li><p>ابزارهای خط فرمان بومی شبکه ویندوز که ممکنه مفید باشه  عبارتند از <code>ipconfig</code>، <code>ping</code>، <code>tracert</code> و <code>netstat</code>.</p></li>

<li><p>می توانی <a href="http://www.thewindowsclub.com/rundll32-shortcut-commands-windows" rel="nofollow">بسیاری از وظایف مفید ویندوز</a> را با فراخوانی فرمان <code>Rundll32</code> انجام بدی.</p></li>

### ترفندها و نکات Cygwin

<li><p>برنامه های اضافی یونیکس را با مدیر بسته Cygwin نصب کن.</p></li>

<li><p>از <code>mintty</code> به عنوان پنجره خط فرمان خود استفاده کنید.</p></li>

<li><p>از طریق <code dir="ltr">/dev/clipboard</code> به کلیپ بورد ویندوز دسترسی پیدا کن.</p></li>

<li><p>فرمان <code>cygstart</code> را اجرا کن تا یک پرونده دلخواه از برنامه های ثبت شده در اون  باز بشه.</p></li>

<li><p>با <code>regtool</code> به رجیستری ویندوز دسترسی پیدا کن.</p></li>

<li><p>توجه داشته باشید که مسیر درایو <code dir="ltr">C:\</code>  در زیر Cygwin به <code dir="ltr">/cygdrive/c</code> تبدیل میشه و مسیر Cygwin <code dir=ltr>/</code> در زیر <code dir="ltr">C:\cygwin</code> در ویندوز ظاهر میشه. با <code>cygpath</code> میتونی مسیرهای پرونده Cygwin و ویندوز را تبدیل کنی. این توی دستورگان هایی که برنامه های ویندوز را اجرا می کنند خیلی مفیده.</p></li>
</ul>

## منابع بیشتر
<ul dir="rtl">
<li><a dir="rtl" href="https://github.com/alebcay/awesome-shell">awesome-shell</a>: فهرستی از ابزارها و منابع پوسته.</li>
<li><a dir="rtl" href="https://github.com/herrbischoff/awesome-osx-command-line">awesome-osx-command-line</a>: راهنمای عمیق تر برای خط فرمان مک او اس.</li>
<li><a dir="rtl" href="http://redsymbol.net/articles/unofficial-bash-strict-mode/" rel="nofollow">Strict mode</a> برای نوشتن دستورگان‌ های پوسته بهتر</li>
<li><a dir="rtl" href="https://github.com/koalaman/shellcheck">shellcheck</a>: یک ابزار تجزیه و تحلیل استاتیک دستورگان پوسته. در اصل، lint برای bash/sh/zsh.</li>
<li><a dir="rtl" href="http://www.dwheeler.com/essays/filenames-in-shell.html" rel="nofollow">Filenames and Pathnames in Shell</a>: جزئیات پیچیده دلسرد کننده در مورد نحوه استفاده صحیح از نام پرونده ها در دستورگان پوسته.</li>
<li><a dir="rtl" href="http://datascienceatthecommandline.com/#tools" rel="nofollow">Data Science at the Command Line</a>: فرمان ها و ابزارهای مفید برای «علم داده» از کتابی به همین نام.</li>
</ul>

## سلب مسئولیت

به جز چند مورد انگشت شمار معدود، کُد را مینویسن تا دیگران بتونن بخونن. قدرت زیاد مسئولیت زیاد هم میاره. اینکه *می توانی* کاری را در بَش انجام بدی، لزوماً به این معنی نیست که باید اون کارو انجام بدی! ;)

## License

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

این اثر تحت مجوز [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/) منتشر میشه.
