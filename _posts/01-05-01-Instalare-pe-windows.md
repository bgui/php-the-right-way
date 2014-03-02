---
isChild: true
---

## Instalare pe Windows {#windows_setup_title}

PHP e disponibil sub diferite forme pe Windows. Îl poți descărca sub formă de [binare][php-downloads] și până recent
puteai folosi un instalator '.msi', dar acesta nu mai e disponibil după PHP 5.3.0.

Pentru a învăța și pentru dezvoltare locală poți folosi webserver-ul încorporat în versiunea PHP 5.4+ deoarece nu ai
nevoie să îl configurezi. Dacă ți-ar plăcea un "totul-inclus" care include un webserver serios și de asemenea MySQL
atunci unelte precum [Web Platform Installer][wpi], [Zend Server CE][zsce], [XAMPP][xampp] şi [WAMP][wamp] te vor ajuta
să obții rapid un mediu de dezvoltare pe Windows. Acestea fiind spuse, aceste unelte vor fi puțin diferite faţă de
mediul de producție, și trebuie sa ții cont de posibile diferențe mai ales dacă lansezi codul pe o platforma GNU\Linux.


Dacă ai nevoie să rulezi sistemul de producție pe Windows atunci IIS7 iți va da cea mai mare stabilitate și cea mai bună
performanță. Poți folosi [phpmanager][phpmanager] (un plugin GUI pentru IIS7) pentru a configura și administra PHP mai
simplu. IIS7 vine cu FastCGI deja încorporat, ai nevoie doar să configurezi PHP ca handler. Pentru suport și resurse
adiționale există o [arie dedicata pe iis.net][php-iis] pentru PHP.

[php-downloads]: http://windows.php.net
[phpmanager]: http://phpmanager.codeplex.com/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[zsce]: http://www.zend.com/ro/products/server-ce/
[xampp]: http://www.apachefriends.org/ro/xampp.html
[wamp]: http://www.wampserver.com/
[php-iis]: http://php.iis.net/
