---
isChild: true
---

## Servere virtuale sau dedicate {#virtual_or_dedicated_servers_title}

Dacă ești confortabil cu administrarea sistemului, sau ești interesat în învățarea lui, serverele virtuale sau dedicate
iți dau control complet asupra mediului de producție al aplicației tale.

### nginx și PHP-FPM

PHP, prin al său FastCGI Process Manager (FPM), se îmbină armonios cu [nginx](http://nginx.org),
care este un web server suplu și de înaltă performanță. Folosește mai puțină memorie ca Apache
și poate susține mai multe interogări concomitente. Asta este în mod special important pe
servere virtuale care nu au prea multă memorie de irosit.

* [Citește mai multe despre nginx](http://nginx.org)
* [Citește mai multe despre PHP-FPM](http://php.net/manual/ro/install.fpm.php)
* [Citeste mai multe despre configurarea nginx și PHP-FPM](https://nealpoole.com/blog/2011/04/setting-up-php-fastcgi-and-nginx-dont-trust-the-tutorials-check-your-configuration/)

### Apache and PHP

PHP și Apache au o lungă istorie împreună. Apache este foarte configurabil și are multe
[module](http://httpd.apache.org/docs/2.4/mod/) disponibile care îi extind funcționalitatea. Este o alegere populară
pentru serverele comune și o configurație ușoară pentru framework-urile PHP sau aplicațiile open source gen Wordpress.
Din păcate, Apache folosește mai multe resurse decât nginx în instalarea obișnuită și nu poate manipula tot atât de
mulți vizitatori în același timp.

Apache are câteva posibile configurări pentru rularea PHP. Cea mai comună și ușoară de configurat este [prefork
MPM](http://httpd.apache.org/docs/2.4/mod/prefork.html) cu mod_php5. Deși nu este cea mai eficientă, este cea mai simplă
de folosit. Asta este probabil cea mai bună alegere dacă nu vrei sa te afunzi prea mult în administrarea serverului.
Nota: dacă folosești mod_php5 trebuie sa folosești prefork MPM.

Alternativ, dacă vrei sa storci mai multa performanță și stabilitate din Apache atunci poți profita de același system
FPM ca și nginx și vei rula [worker MPM](http://httpd.apache.org/docs/2.4/mod/worker.html) sau [eventMPM](http://httpd.apache.org/docs/2.4/mod/event.html)
cu mod_fastcgi sau mod_fcgid. Configurarea aceasta va fi semnificativ mai eficientă și mai rapidă dar este mai complicat
de setat.

* [Citeste mai multe despre Apache](http://httpd.apache.org/)
* [Citeste mai multe despre Multi-Processing Modules](http://httpd.apache.org/docs/2.4/mod/mpm_common.html)
* [Citeste mai multe despre mod_fastcgi](http://www.fastcgi.com/mod_fastcgi/docs/mod_fastcgi.html)
* [Citește mai multe despre mod_fcgid](http://httpd.apache.org/mod_fcgid/)
