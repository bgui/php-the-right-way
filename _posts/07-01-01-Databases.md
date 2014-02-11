---
title: Baze de date
---

# Baze de date {#databases_title}

De multe ori codul tau PHP va folosi o baza de date pentru a persista informatii. Ai cateva optiuni de conectare si interactiune cu baza ta de date. Optiunea recomandata _pana la PHP 5.1.0_ era sa folosesti driveri nativi precum [mysql][mysql], [mysqli][mysqli], [pgsql][pgsql], etc.

Driverii nativi sunt buni daca folosesti o singura baza de date in aplicatia ta, dar daca, spre exemplu, folosesti MySQL si putintel MSSQL sau ai nevoie sa te conectezi la o baza Oracle, atunci nu vei putea sa folosesti aceeasi driveri.
Vei avea nevoie sa inveti un noi API pentru fiecare baza iar asta poate deveni ridicol.

Ca inca o observatie asupra driverilor nativi, extensia mysql pentru PHP nu mai este dezvoltata activ,
iar statusul oficial incepand cu PHP 5.4.0 este "Long term deprecation". Asta inseamna ca va disparea
in viitoarele cateva lansari, asa ca in jurul 5.6 (sau ce vine dupa 5.5) s-ar putea sa fii disparut.
Daca folosesti `mysql_connect()` si `mysql_query()` in aplicatia ta atunci va trebui sa o rescrii la
un moment dat, asa ca cea mai buna optiune este sa inlocuiesti usor usor mysql cu mysqli sau cu PDO
ca sa nu fii brusc fortat mai tarziu. _Daca incepi de la zero atunci in nici un caz sa nu folosesti extensia
mysql: foloseste [extensia MySQLi][mysqli] sau PDO._

* [PHP: Alegerea unui API pentru MySQL](http://php.net/manual/ro/mysqlinfo.api.choosing.php)

## PDO

PDO este o biblioteca de abstractionare a conexiunii cu baza de date &mdash; ce vine incorporata in PHP de la 5.1.0 &mdash; si
pune la dispozitie o interfata comuna de a vorbi cu diferite baze de date. PDO nu va traduce interogarile tale SQL si nici nu
va emula functionalitati lipsa; este doar pentru a conecta la mai multe tipuri de baze de date prin acelasi API.

Mai important, `PDO` te lasa sa injectezi in mod sigur input extern (e.g. IDs) in interogarile tale SQL fara
a iti face griji despre atacuri prin injectie. Asta este posibil folosind PDO statements si parametri "bound".

Sa presupunem ca un script PHP primeste un ID numeric ca parametru. Acest ID ar trebui sa fie folosit pentru a
citi date din baza. Aceasta este calea `gresita` de a face asta:

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$pdo->query("SELECT name FROM users WHERE id = " . $_GET['id']); // <-- NO!
{% endhighlight %}

Acesta este cod foarte gresit. Inserezi un parametru brut in interogarea SQL. Asta iti va compromite
securitatea intr-o clipita. Imagineaza-ti ca un hacker paseaza un parametru `id` inventat
apeland URL-ul astfel:
`http://domain.com/?id=1%3BDELETE+FROM+users`. Asta va seta `$_GET['id']` ca `1;DELETE FROM users`
care iti va sterge toti userii! Ce trebuie sa faci este sa cureti inputul pentru ID folosind parametrii PDO "bound".

{% highlight php %}
<?php
$pdo = new PDO('sqlite:users.db');
$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); // <-- Curatat automat de PDO
$stmt->execute();
{% endhighlight %}

Acesta este codul corect. Foloseste un parametru bound pe o instructiune PDO. Asta sanitizeaza inputul extern
pentru ID inainte ca el sa fie introdus in baza de date prevenind astfel un potential atac prin injectie.

* [Invata despre PDO][1]

Ar trebui de asemenea sa stii ca conexiunile cu baza folosesc resurse si nu este neauzit ca toate
resursele sa fie epuizate daca conexiunile nu au fost explicit inchise. Totusi asta este mai des intalnit
in alte limbaje. Folosind PDO poti inchide implicit conexiunea distrugand obiectul si asigurandu-te ca
toate referintele catre el au fost sterse, adica setate la NULL. Daca nu faci asta explicit, PHP va inchide
automat conexiunea la sfarsitul scriptului - exceptand desigur cazul in care folosesti conexiuni persistente.

* [Invata despre conexiuni PDO][5]

## Niveluri de abstractiune

Multe framework-uri dispun de propriul nivel de abstractiune care se bazeaza sau nu pe PDO.  Acestea vor emula
deseori functionalitati ai unui sistem de baza de date care lipsesc in altul inbracand interogarile prin
metode PHP, furnizandu-ti efectiv o abstractiune a bazei de date.
Aceasta desigur va necesita un mic pret, dar daca construieste o aplicatie portabila care are nevoie sa
lucreze cu MySQL, PostgreSQL si SQLite atunci micul pret platit va merita de dragul curateniei codului.

Unele niveluri de abstractiune au fost construite folosind standarde namespace [PSR-0][psr0] or [PSR-4][psr4]
incat sa poata fi instalate in orice aplicatie doresti:

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
