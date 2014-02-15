---
isChild: true
---

## Servere virtuale sau dedicate {#virtual_or_dedicated_servers_title}

Daca esti confortabil cu administrarea sistemului, sau esti interesat in invatarea lui,
serverele virtuale sau dedicate iti dau control complet al mediului de productie al aplicatiei tale.

### nginx si PHP-FPM

PHP, prin al sau FastCGI Process Manager (FPM), se imbina armonios cu [nginx](http://nginx.org),
care este un web server suplu si de inalta performanta. Foloseste mai putina memorie ca Apache
si poate sustine mai multe interogari concomitente. Asta este in mod special important pe
servere virtuale care nu au prea multa memorie de irosit.

* [Citeste mai multa despre nginx](http://nginx.org)
* [Citeste mai multa despre PHP-FPM](http://php.net/manual/ro/install.fpm.php)
* [Citeste mai multa despre configurarea nginx si PHP-FPM](https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/)

### Apache and PHP

PHP si Apache au o lunga istorie impreuna. Apache este foarte configurabil si are multe
[module](http://httpd.apache.org/docs/2.4/mod/) disponibile care ii extind functionalitatea.
Este o alegere populara pentru serverele comune si o configuratie usoara pentru
framework-urile PHP sau aplicatiile open source gen Wordpress. Din pacate, Apache
foloseste mai multe resurse decat nginx in instalarea obisnuita si nu poate manipula
tot atat de multi vizitatori in acelasi timp.

Apache are cateva posibile configurari pentru rularea PHP. Cea mai comuna si usoar de configurat
este [prefork MPM](http://httpd.apache.org/docs/2.4/mod/prefork.html) cu mod_php5. Desi nu
este cea mai eficienta, este cea mai simplu de folosit. Asta este probabil cea mai buna
alegere daca nu vrei sa te afunzi prea mult in administrarea serverului.
Nota: daca folosesti mod_php5 trebuie sa folosesti prefork MPM.

Alternativ, daca vrei sa storci mai multa performanta si stabilitate din Apache atunci
poti profita de acelasi system FPM ca si nginx si vei rula [worker MPM](http://httpd.apache.org/docs/2.4/mod/worker.html) sau [event MPM](http://httpd.apache.org/docs/2.4/mod/event.html) cu
mod_fastcgi sau mod_fcgid. Configurarea aceasta va fi semnificativ mai eficienta si mai rapida
dar este mai complicat de setat.

* [Citeste mai multa despre Apache](http://httpd.apache.org/)
* [Citeste mai multa despre Multi-Processing Modules](http://httpd.apache.org/docs/2.4/mod/mpm_common.html)
* [Citeste mai multa despre mod_fastcgi](http://www.fastcgi.com/mod_fastcgi/docs/mod_fastcgi.html)
* [Citeste mai multa despre mod_fcgid](http://httpd.apache.org/mod_fcgid/)
