---
isChild: true
---

## Composer și Packagist {#composer_and_packagist_title}

Composer este un **genial** manager de dependințe pentru PHP. Listezi dependințele proiectului tău în fișierul `composer.json` și, cu câteva
comenzi simple Composer va descărca automat dependințele și va seta autoloading-il pentru tine.

Există deja multe biblioteci PHP care sunt compatibile cu Composer, gata să fie folosite în proiectul tău. Aceste "pachete" sunt
listate pe [Packagist][1], repository-ul oficial de biblioteci PHP compatibile Composer.

### Cum să instalezi Composer

Poți instala Composer local (în directorul curent; deși asta nu mai este recomandat) sau global (e.g. /usr/local/bin).
Să presupunem că vrei să instalezi Composer local. Din directorul rădăcina al proiectului tău:

    curl -s https://getcomposer.org/installer | php

Asta va descărca `composer.phar` (o arhivă PHP binară). Poți executa asta cu `php` pentru a administra dependințele proiectului.
<strong>Nota:</strong> dacă inserezi codul descărcat direct în interpreter, citește mai întâi codul online ca să iți confirmi ca e sigur.

### Cum să instalezi Composer (manual)

Instalarea manuală este o tehnică mai avansată; însă există varii motive pentru care un dezvoltator ar prefera
această metodă versus folosirea interactivă. Instalarea interactivă verifică instalarea ta de PHP ca să
se asigure că:

- o versiune suficientă de PHP e folosită
- fisiere `.phar` pot fi executate corect
- anumite directoare au permisiuni suficiente
- anumite extensii problematice nu sunt încărcate
- anumite setări din `php.ini` sunt setate

Deoarece o instalare manuală nu face nici unul din aceste verificări, trebuie să decizi dacă
merită pentru tine. Mai jos se arată cum obții Composer manual:

    curl -s https://getcomposer.org/composer.phar -o $HOME/local/bin/composer
    chmod +x $HOME/local/bin/composer

Calea `$HOME/local/bin` (sau alta aleasa de tine) trebuie să fie în `$PATH`. Asta va avea ca rezultat
disponibilitatea comenzii `composer`.

Când dai peste documentație care cere să rulezi Composer ca `php composer.phar install`, poți substitui cu:

    composer install

Această secțiune va presupune că ai instalat composer global.

### Cum să definești și să instalezi dependințe

Composer ține seama de dependințele proiectului tău într-un fișier numit `composer.json`. Îl poți administra manual dacă vrei,
sau poți folosi însuși Composer. Comanda `composer require` adaugă o dependință a proiectului iar dacă nu ai un fișier
`composer.json` unul va fi creat. Aici e un exemplu care adaugă [Twig][2] ca dependință a proiectului.

	composer require twig/twig:~1.8

Alternativ, comanda `composer init` te va ghida prin construcția unui fișier `composer.json` întreg pentru proiectul tău.
Oricum, când ai creat `composer.json` ii poți spune Composer-ului să descarce și să instaleze dependințele în
directorul `vendors/`. Asta se aplică și proiectelor pe care le-ai descărcat care deja au un fișier `composer.json`:

    composer install

Acum, adaugă această linie în fișierul PHP principal al proiectului tău; îi va spune lui PHP să folosească autoloader-ul
din Composer.

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Acum iți poți folosi dependințele în proiect, iar ele for fi încărcate automat când e nevoie de ele.

### Actualizarea dependințelor

Composer creeata un fișier numit `composer.lock` care stochează versiunea exactă a fiecărui pachet pe care îl
descarcă când ai executat prima data `php composer.phar install`. Dacă împărtășești proiectul tău cu alți
dezvoltatori și `composer.lock` este parte a distribuției tale, când ei execută `php composer.phar install`
ei vor obține aceleași versiuni ca și tine. Pentru a iți actualiza dependințele, rulează
`php composer.phar update`.

Asta este cel mai util când iți definești necesitățile ca versiuni flexibile. De exemplu o versiune necesară
de ~1.8 înseamnă "orice mai nou decât 1.8.0, dar mai jos decât 2.0.x-dev". Poți folosi `*` ca în `1.8.*`.
Acum comanda `php composer.phar update` va actualiza toate dependințele către cea mai nouă versiune definită de tine.

### Înștiințări de actualizare

Pentru a primi înștiințări de noi versiuni te poți înscrie în [VersionEye][3], un serviciu web care monitorizează
conturile tale GitHub și BitBucket după fișiere `composer.json` și care trimite email-uri cu noile pachete lansate.

### Verificarea dependințelor tale împotriva problemelor de securitate

[Security Advisories Checker][4] este un serviciu web și o unealtă de linie de comandă, ambele vor examina `composer.lock`
și iți vor spune dacă ai nevoie să actualizezi vreuna din dependințe.

* [Află despre Composer][5]

[1]: http://packagist.org/
[2]: http://twig.sensiolabs.org
[3]: https://www.versioneye.com/
[4]: https://security.sensiolabs.org/
[5]: http://getcomposer.org/doc/00-intro.md
