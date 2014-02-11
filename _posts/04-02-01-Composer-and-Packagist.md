---
isChild: true
---

## Composer si Packagist {#composer_and_packagist_title}

Composer este un **genial** manager de dependinte pentru PHP. Listezi dependintele proiectului tau in fisierul `composer.json` si, cu cateva
comenzi simple Composer va descarca automat dependintele si va seta autoloading pentru tine.

Exista deja multe biblioteci PHP care sunt compatibile cu Composer, gata sa fie folosite in proiectul tau. Aceste "pachete" sunt
listate pe [Packagist][1], repository-ul oficial de biblioteci PHP compatibile Composer.

### Cum sa instalezi Composer

Poti instala Composer local (in directorul curent; desi asta nu mai este recomandat) sau global (e.g. /usr/local/bin).
Sa presupunem ca vrei sa instalezi Composer local. Din directorul radacina al proiectului tau:

    curl -s https://getcomposer.org/installer | php

Asta va descarca `composer.phar` (o arhiva PHP binara). Poti executa asta cu `php` pentru a administra dependintele proiectului.
<strong>Nota:</strong> daca inserezi codul descarcat direct in interpreter, citeste mai intai codul online ca sa iti confirmi ca e sigur.

### Cum sa instalezi Composer (manual)

Instalarea manuala este o tehnica mai avansata; insa exista varii motive pentru care un dezvoltator ar prefera
aceasta metoda versus folosirea interactiva. Instalarea interactiva verifica instalarea ta de PHP ca sa
se asigure ca:

- o versiune suficienta de PHP e folosita
- fisiere `.phar` pot fi executate corect
- anumite directoare au permisiuni suficiente
- anumite extensii problematice nu sunt incarcate
- anumite setari din `php.ini` sunt setate

Deoarece o instalare manuala nu face nici unul din aceste verificari, trebuie sa decizi daca
merita pentru tine. Mai jos este cum obtii Composer manual:

    curl -s https://getcomposer.org/composer.phar -o $HOME/local/bin/composer
    chmod +x $HOME/local/bin/composer

Calea `$HOME/local/bin` (sau alta aleasa de tine) trebuie sa fie in `$PATH`. Asta va avea ca rezultat
disponibilitatea comenzii `composer`.

Cand dai peste documentatie care cere sa rulezi Composer ca `php composer.phar install`, poti substitui cu:

    composer install
    
Aceasta sectiune va presupune ca ai instalat composer global.

### Cum sa definesti si sa instalezi dependinte

Composer tine seama de dependintele proiectului tau intr-un fisier numit `composer.json`. Il poti administra manual daca vrei,
sau poti folosi insusi Composer. Comanda `composer require` adauga o dependinta a proiectului iar daca nu ai un fisier
`composer.json` unul va fi creeat. Aici e un exemplu care adauga [Twig][2] ca dependinta a proiectului.

	composer require twig/twig:~1.8

Alternativ, comanda `composer init` te va ghida prin constructia unui fisier `composer.json` intreg pentru proiectul tau.
Oricum, cand ai creeat `composer.json` ii poti spune Composer-ului sa descarce si sa instaleze dependintele in
directorul `vendors/`. Asta se aplica si proiectelor pe care le-ai descarcat care deja au un fisier `composer.json`:

    composer install

Acum, adauga aceasta linie in fisierul PHP principal al proiectului tau; ii va spune lui PHP sa foloseasca autoloaderul
din Composer.

{% highlight php %}
<?php
require 'vendor/autoload.php';
{% endhighlight %}

Acum iti poti folosi dependintele in proiect, iar ele for fi incarcate automat cand e nevoie de ele.

### Actualizarea dependintelor

Composer creeaza un fisier numit `composer.lock` care stocheaza versiunea exacta a fiecarui pachet pe care il
descarca cand ai executat prima data `php composer.phar install`. Daca impartasesti proiectul tau cu alti
dezvoltatori si `composer.lock` este parte a distributiei tale, cand ei executa `php composer.phar install`
ei vor obtine aceleasi versiuni ca si tine. Pentru a iti actualiza dependintele, ruleaza
`php composer.phar update`.

Asta este cel mai util cand iti definesti necesitatile ca versiuni flexibile. De exemplu o versiune necesara
de ~1.8 inseamna "orice mai noi decat 1.8.0, dar mai jos decat 2.0.x-dev". Poti folosi `*` ca in `1.8.*`.
Acum comanda `php composer.phar update` va actualiza toate dependintele catre cea mai noua versiune definita de tine.

### Instiintari de actualizare

Pentru a primi instiintari de noi versiuni te poti inscrie in [VersionEye][3], un serviciu web care monitorizeaza
conturile tale GitHub si BitBucket dupa fisiere `composer.json` si care trimite email-uri cu noile pachete lansate.

### Verificarea dependintelor tale impotriva problemelor de securitate

[Security Advisories Checker][4] este un serviciu web si o unealta de linie de comanda, ambele vor examina `composer.lock`
si iti vor spune daca ai nevoie sa actualizezi vreuna din dependinte.

* [Afla despre Composer][5]

[1]: http://packagist.org/
[2]: http://twig.sensiolabs.org
[3]: https://www.versioneye.com/
[4]: https://security.sensiolabs.org/
[5]: http://getcomposer.org/doc/00-intro.md

