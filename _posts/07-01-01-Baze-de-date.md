---
title: Baze de date
---

# Baze de date {#databases_title}

De multe ori codul tău PHP va folosi o bază de date pentru a perminte informațiilor să persiste. Ai câteva opțiuni de
conectare și interacțiune cu baza ta de date. Opțiunea recomandată _pană la PHP 5.1.0_ era sa folosești driveri nativi
precum [mysql][mysql], [mysqli][mysqli], [pgsql][pgsql], etc.

Driverii nativi sunt buni dacă folosești o singură bază de date în aplicația ta, dar dacă, spre exemplu, folosești MySQL
și ceva MSSQL sau ai nevoie să te conectezi la o bază Oracle, atunci nu vei putea să folosești aceiași driveri. Vei
avea nevoie să înveți un nou API pentru fiecare bază de date iar asta poate deveni ridicol.

Ca încă o observație asupra driverilor nativi, extensia mysql pentru PHP nu mai este dezvoltată activ, iar statusul
oficial începând cu PHP 5.4.0 este "Long term deprecation". Asta înseamnă că va dispărea în viitoarele lansări, așa că
în jurul versiunii 5.6 (sau ce va veni după versiunea 5.5) extensia va fi eliminată. Dacă folosești `mysql_connect()`
și `mysql_query()` în aplicația ta atunci va trebui sa o rescrii, oricum vei fi nevoit să faci acest lucru la un moment
dat, cea mai bună opțiune este să înlocuiești ușor ușor mysql cu mysqli sau cu PDO ca să nu fii brusc forțat mai târziu.
_Dacă începi de la zero atunci în nici un caz să nu folosești extensia mysql: folosește [extensia MySQLi][mysqli] sau
PDO._

* [PHP: Alegerea unui API pentru MySQL](http://php.net/manual/ro/mysqlinfo.api.choosing.php)

## PDO

PDO este o bibliotecă de abstractizare a conexiunii cu baza de date &mdash; ce vine încorporată în PHP de la 5.1.0
&mdash; și pune la dispoziție o interfață comună de a vorbi cu diferite baze de date. PDO nu va traduce interogările
tale SQL și nici nu va emula funcționalități lipsă; este doar pentru a te putea conecta la mai multe tipuri de baze de
date prin același API.

Mai important, `PDO` te lasă să injectezi în mod sigur input extern (e.g. IDs) în interogările tale SQL fără a iți face
griji despre atacuri prin injecție. Asta este posibil folosind PDO statements și parametri "bound".

Să presupunem că un script PHP primește un ID numeric ca parametru. Acest ID ar trebui să fie folosit pentru a
citi date din baza de date. Aceasta este calea `greșită` de a face asta:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NO!
{% endhighlight %}

Acest cod este foarte greșit. Inserezi un parametru brut în interogarea SQL. Asta iți va compromite securitatea într-o
clipită. Imaginează-ți ca un hacker pasează un parametru `id` inventat apelând URL-ul astfel:
`http://domain.com/?id=1%3BDELETE+FROM+users`. Asta va seta `$_GET['id']` ca `1;DELETE FROM users` care iți va șterge
toți userii! Ce trebuie să faci este sa cureți inputul pentru ID folosind parametrii PDO "bound".

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); // <-- Curatat automat de PDO
$stmt->execute();
{% endhighlight %}

Acesta este codul corect. Folosește un parametru bound pe o instrucțiune PDO. Asta sanitizează inputul extern pentru ID
înainte ca el să fie introdus în baza de date prevenind astfel un potențial atac prin injecție.

* [Învață despre PDO][1]

Ar trebui de asemenea sa știi că conexiunile cu baza de date folosesc resurse și nu puține au fost cazurile în care
toate resursele au fost epuizate dacă conexiunile nu au fost explicit închise. Totuși, acest lucru este mai des întâlnit
în alte limbaje. Folosind PDO poți închide implicit conexiunea distrugând obiectul și asigurându-te ca toate referințele
către el au fost șterse, adică setate ca NULL. Dacă nu faci asta explicit, PHP va închide automat conexiunea la
sfârșitul scriptului - exceptând desigur cazul în care folosești conexiuni persistente.

* [Învață despre conexiuni PDO][5]

## Niveluri de abstractizare

Multe framework-uri dispun de propriul nivel de abstractizare care se bazează sau nu pe PDO. Acestea vor emula deseori
funcționalități ale unui sistem de bază de date care lipsesc în altul îmbrăcând interogările prin metode PHP,
furnizându-ți efectiv o metoda de abstractizare a bazei de date. Aceastea vor veni cu un mic preț, dar dacă construiești
o aplicație portabilă care are nevoie să lucreze cu MySQL, PostgreSQL și SQLite atunci micul preț plătit va merita de
dragul curățeniei codului.

Unele niveluri de abstractizare au fost construite folosind standarde namespace [PSR-0][psr0] sau [PSR-4][psr4] încât să
poată fi instalate în orice aplicație dorești:

* [Aura SQL][6]
* [Doctrine2 DBAL][2]
* [Propel][7]
* [ZF2 Db][4]
* [ZF1 Db][3]

[1]: http://www.php.net/manual/ro/book.pdo.php
[2]: http://www.doctrine-project.org/projects/dbal.html
[3]: http://framework.zend.com/manual/ro/zend.db.html
[4]: http://packages.zendframework.com/docs/latest/manual/ro/index.html#zend-db
[5]: http://php.net/manual/ro/pdo.connections.php
[6]: https://github.com/auraphp/Aura.Sql
[7]: http://propelorm.org/Propel/

[mysql]: http://php.net/mysql
[mysqli]: http://php.net/mysqli
[pgsql]: http://php.net/pgsql
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
