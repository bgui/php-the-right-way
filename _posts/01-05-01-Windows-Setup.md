---
isChild: true
---

## Instalare pe Windows {#windows_setup_title}

PHP e disponibil sub diferite forme pe Windows. Il poti descarca sub forma de [binare][php-downloads] si pana recent puteai folosi
un instalator '.msi', dar acesta nu mai e disponibil dupa PHP 5.3.0.

Pentru a invata si pentru dezvoltare locala poti folosi webserver-ul incorporat cu PHP 5.4+ asa incat nu ai nevoie
sa il configurezi. Daca ti-ar placea un "totul-inclus" care include un webserver serios si de asemenea MySQL atunci
unelte precum [Web Platform Installer][wpi], [Zend Server CE][zsce], [XAMPP][xampp] si [WAMP][wamp] te vor
ajuta sa obtii rapid un mediu de dezvoltare pe Windows. Acestea fiind spuse, aceste unele vor fi putin diferite
fata de mediul de productie, si trebuie sa tii cont de posibile diferente mai ales daca lansezi codul pe Linux.


Daca ai nevoie sa rulezi sistemul de productie pe Windows atunci IIS7 iti va da cea mai mare stabilitate si cea mai buna performanta.
Poti folosi [phpmanager][phpmanager] (un plugin GUI pentru IIS7) pentru a configura si administra PHP mai simplu.
IIS7 vine cu FastCGI deja incorporat, ai doar nevoie sa configurezi PHP ca handler. Pentru suport si resurse aditionale exista
o [arie dedicata pe iis.net][php-iis] pentru PHP.

[php-downloads]: http://windows.php.net
[phpmanager]: http://phpmanager.codeplex.com/
[wpi]: http://www.microsoft.com/web/downloads/platform.aspx
[zsce]: http://www.zend.com/ro/products/server-ce/
[xampp]: http://www.apachefriends.org/ro/xampp.html
[wamp]: http://www.wampserver.com/
[php-iis]: http://php.iis.net/
