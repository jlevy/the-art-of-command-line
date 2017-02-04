<div dir=rtl>

<p>🌍
<em><a href="README-cs.md">Čeština</a> ∙ <a href="README-de.md">Deutsch</a> ∙ <a href="README-el.md">Ελληνικά</a> ∙ <a href="README.md">English</a> ∙ <a href="README-es.md">Español</a> ∙ <a href="README-fr.md">Français</a> ∙ <a href="README-he.md">עברית</a> ∙ <a href="README-id.md">Indonesia</a> ∙ <a href="README-it.md">Italiano</a> ∙ <a href="README-ja.md">日本語</a> ∙ <a href="README-ko.md">한국어</a> ∙ <a href="README-pt.md">Português</a> ∙ <a href="README-ro.md">Română</a> ∙ <a href="README-ru.md">Русский</a> ∙ <a href="README-sl.md">Slovenščina</a> ∙ <a href="README-uk.md">Українська</a> ∙ <a href="README-zh.md">简体中文</a> ∙ <a href="README-zh-Hant.md">繁體中文</a></em></p>
<p>#האומנות שבשורת הפקודה</p>
<p><a href="https://airtable.com/shrzMhx00YiIVAWJg"><img src="https://img.shields.io/badge/%3f-Ask%20a%20Question-ff69b4.svg" alt="שאל שאלה"></a></p>
<p><a href="https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&amp;utm_medium=badge&amp;utm_campaign=pr-badge&amp;utm_content=badge"><img src="https://badges.gitter.im/Join%20Chat.svg" alt="הצטרף לצאט https://gitter.im/jlevy/the-art-of-command-line"></a></p>
<p>-<a href="#מתא">מתא</a>
-<a href="#יסודות">יסודות</a>
-<a href="#שימוש-יומיומי">שימוש יומיומי</a>
-<a href="#עיבוד-קבצים-ונתונים">עיבוד קבצים ונתונים</a>
-<a href="#דיבאג-למערכת">דיבאג למערכת</a>
-<a href="#פקודות-שורה">פקודות שורה</a>
-<a href="#שונות-שימושיות">שונות שימושיות</a> <a href="#למערכת-os-x-בלבד">למערכת OS X בלבד</a>
-<a href="#לחלונות-בלבד">לחלונות בלבד</a>
-<a href="#חומרים-נוספים">חומרים נוספים</a>
-<a href="#כתב-ויתור">כתב ויתור</a></p>
<p><img src="cowsay.png" alt="curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50"></p>
<p>מיומנות הפעלת שורת הפקודה נשארת לרוב בקרן זווית, ומשרה מסביבה אווירת מסתורין. אם זאת שליטה בשורת הפקודה משפרת את הגמישות והפרודקטיביות של המהנדס לעיטים באופנים ברורים ביותר, ולעיטים גם בדרכים הנסתרות מהעין. לפינך רשימה של נקודות וטיפים לתפעול שורת הפקודה שאנו מצאנו כשימושיים לעבודה בלינוקס. חלקן בסיסיות, חלקן ספציפיות, חלקן מתוחכמות וחלקן מוזרות. רשימה זאת איננה ארוכה, אך אם ביכולתך לזכור ולהשתמש בכל הכתוב בה, באמתחתך ידע רב.</p>
<p>עבודה זאת היא פרי עבודתם <a href="AUTHORS.md">של כותבים ומתרגמים רבים</a>. חלקו <a href="http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands">הופיע</a>
<a href="http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix">במקור</a> ב<a href="http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know">Quora</a>, אך מאז עבר לגיטהאב, שם אנשים כשרוניים יותר מהכותב המקורי הוסיפו שינויים רבים.</p>
<p><a href="https://airtable.com/shrzMhx00YiIVAWJg"><strong>אנא הוסף שאלה</strong></a> באם יש לך שאלה שקשורה לשורת הפקודה. <a href="/CONTRIBUTING.md"><strong>אנא הצטרף למאמץ</strong></a> אם נתקלת בטעות או בכל דבר שניתן לשפר!</p>
<h2 id="-">מטא</h2>
<p>מטרה:</p>
<ul>
<li>מדריך זה מיועד הן למתחילים והן למקצוענים. המטרות הם <em>בקיאות</em> (כל מה שחשוב), <em>מיקוד</em> (הבאת דוגמאות רציניות על רוב המקרים הבסיסים), ו<em>קיצור</em> (המנעות ממה שאינו הכרחי ומחריגות שניתן לקרוא עליהם בקלות במקום אחר). כל הטיפים הכרחיים במקרים מסויימים, או שחוסכים זמן רב יחסית לאפשרויות האחרות. </li>
<li>מדריך זה נכתב ללינוקס. יוצאים מן הכלל הם הפרקים "<a href="#למערכת-OS-X-בלבד">למערכת 0S X בלבד</a>" ו"<a href="#לחלונות-בלבד">לחלונות בלבד</a>". חלקים נכבדים מהפרקים האחרים ניתנים לשימוש או להתקנה על מערכות יוניקס אחרת וכן על OS X (ואפילו ב Cygwin).</li>
<li>ההתמקדות הינה בבאש אינטראקטיבי, אם זאת טיפים רבים רלוונטים לשפות shell אחרות ולסקריפטים כללים בבאש עצמו.</li>
<li>המדריך כולל הוראות יוניקס "סטנדרטיות", וכן כאלו שמחייבים התקנת חבילות יעודיות -- כל עוד הם חשובים מספיק להצדקת איזכור.</li>
</ul>
<p>לתשומת לבכם:</p>
<ul>
<li>על מנת להגביל את המדריך לעמוד יחיד, תוכנים רבים מפעים כאיזכורים בלבד.
איזכורים אלו יספיקו לכם לקבלת רעיון כללי, וילמדו אתכם את המושגים הנדרשים על מנת למצוא מידע נוסף בגוגל. השתמשו ב<code>apt-get</code>, <code>yum</code>, <code>dnf</code>, <code>pacman</code>, <code>pip</code> או <code>brew</code> (לפי מערכת ההפעלה שלכם) על מנת להתקין תוכנות חדשות.</li>
<li>השתמשו ב <a href="http://explainshell.com/">Explainshell</a> לקבלת הסבר מפורט מה פקודות, אפשריות, צינורות ועוד עושות.</li>
</ul>
<h2 id="-">יסודות</h2>
<ul>
<li><p>למד באש בסיסי. למען האמת, כתוב <code>man bash</code> ולפחות רפרף על הכתוב; הוא קל יחסית להבנה, ואינו כה ארוך. שלים (shells) אחרים יכולים להיות נחמדים אך באש הוא כלי רב עוצמה ותמיד בנמצא (למידת zhs,fish וכו' <em>בלבד</em>, אמנם מושכת, אך יעילותם מוגבלת למחשבך האישי. במקרים רבים, כגון שימוש בשרתים קיימים, תמצא את חוסר ידיעת הבאש כהגבלה רצינית).</p>
</li>
<li><p>למד טוב לפחות מעבד תמלילים מבוסס-טקסט אחד. מומלץ ללמוד ( Vim (<code>vi</code> מכיוון שכשמגעים לעריכה ראנדומאלית של טקסט בטרמיל אין לvi כל מתחרה. (גם אם הינך משתמש בEmacs, או ב IDE גדול רוב הזמן).</p>
</li>
</ul>
<p>-</p>
<h2 id="-">שימוש יומיומי</h2>
<h2 id="-">עיבוד קבצים ונתונים</h2>
<h2 id="-">דיבאג למערכת</h2>
<h2 id="-">פקודות שורה</h2>
<h2 id="-">שונות שימושיות</h2>
<h2 id="-os-x-">למערכת OS X בלבד</h2>
<h2 id="-">לחלונות בלבד</h2>
<h2 id="-">חומרים נוספים</h2>
<h2 id="-">כתב ויתור</h2>


</div>
