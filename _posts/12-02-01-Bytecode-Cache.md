---
isChild: true
---

## Cache de bytecode {#bytecode_cache_title}

Când un fișier PHP este executat, sub capota este mai întâi compilat spre bytecode
(cunoscut și ca opcode) și, numai apoi, bytecode-ul este executat.
Dacă fișierul PHP nu este modificat, bytecode-ul va fi totdeauna același. Asta înseamnă că
pasul de compilare este o risipa ale resurselor procesorului.

Aici intra în scena Cache-ul de bytecode. El previne compilarea redundantă stocând
bytecode în memorie și refolosindu-l la apelări ulterioare.
Setarea cache-ului de bytecode este o chestiune de minute, și aplicația ta va fi semnificativ
mai rapidă. Nu prea există motive de a nu îl folosi.

Începând cu PHP 5.5, există un cache de bytecode incorporat numit [OPCache](http://php.net/manual/ro/book.opcache.php). Este disponibil și pentru versiuni mai vechi.

Alte cache-uri de bytecode populare sunt:

* [APC](http://php.net/manual/ro/book.apc.php) (PHP 5.4 și mai vechi)
* [XCache](http://xcache.lighttpd.net/)
* [Zend Optimizer+](http://www.zend.com/products/server/) (part din pachetul Zend Server)
* [WinCache](http://www.iis.net/download/wincacheforphp) (extensie pentru MS Windows Server)