---
isChild: true
---

## Cache de bytecode {#bytecode_cache_title}

Cand un fisier PHP este executat, sub capota este mai intai compilat spre bytecode
(cunoscut si ca opcode) si, numai apoi, bytecode-ul este executat.
Daca fisierul PHP nu este modificat, bytecodul va fi totdeauna acelasi. Asta inseamna ca
pasul de compilare este o risipa ale resurselor procesorului.

Aici intra in scena Cache-ul de bytecod. El previne compilarea redundanta stocand
bytecod in memorie si refolosindu-l la apelari ulterioare.
Setarea cache-ului de bytecode este o chestiune de minute, si aplicatia ta va fi semnificativ
mai rapida. Nu prea exista motive de a nu il folosi.

Incepand cu PHP 5.5, exista un cache de bytecod incorporat numit [OPcache](http://php.net/manual/ro/book.opcache.php). Este disponibil si pentru versiuni mai vechi.

Alte cache-uri de bytecode populare sunt:

* [APC](http://php.net/manual/ro/book.apc.php) (PHP 5.4 si mai vechi)
* [XCache](http://xcache.lighttpd.net/)
* [Zend Optimizer+](http://www.zend.com/products/server/) (part din pachetul Zend Server)
* [WinCache](http://www.iis.net/download/wincacheforphp) (extensie pentru MS Windows Server)
