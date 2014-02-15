---
isChild: true
---

## Cache-uirea obiectelor {#object_caching_title}

Exista momente cand poate fi benefic sa cache-uiesti obiecte individuale in codul tau, de exemplu cu date care
sunt scump de obtinut sau cu apeluri catre baza de date care nu sunt improbabil de a se fi schimbat.
Poti folosi software pentru cache-uirea obiectelor pentru a tine aceste bucati de date in memorie pentru
acces rapid mai tarziu. Daca salvezi acesti itemi intr-o datastore dupa ce ii recuperezi, atunci
iai direct din cache data viitoare cand ai nevoie de ei, poti castiga o imbunatatire semnificativa a
performantei ca si o reducere a incarcarii serverului bazei de date.

De asemenea, multe din solutiile populare de cache-uire a bytecode-ului te lasa sa stochezi si date personalizate,
asa ca ai chiar si mai multe motive sa profiti de ele. APCu, XCache, si WinCache toate pun la dispozitie API-uri
pentru a salva date din codul tau PHP in memoria lor.

Cele mai populare sisteme de cache-uire a obiectelor sunt APCu si memcached. APCu este o excelenta alegere
pentru cache-ul de obiecte, are un API simplu pentru inserarea datelor tale in memoria sa cache si este
foarte simplu de folosit. Singura limitare a APCu este ca este legata de serverul pe care e instalata.
Memcached pe de alta parte este instalat ca un serviciu separat si poate fi accesat prin intermediul retelei,
insemnand ca poti stoca obiecte intr-o magazie super-rapida, intr-o locatie centrala, si mai multe sisteme
diferite le pot citi din ea.

Nota: cand rulam PHP ca aplicatie (Fast-)CGI intauntrul webserver-ului, fiecare proces PHP va avea propriul
cache, adica datele APCu nu sunt la comun pentru toate proceselor. In aceste cazuri, probabil ai vrea sa
folosesti memcached, intrucat nu e legat de procesele PHP.

Intr-o configuratie cu retea, APCu va performa mai bine decat memcached in termeni de viteza, dar memcached va putea
sa scaleze mai rapid si mai departe. Daca nu te astepti sa ai mai multe servere pentru aplicatia ta, sau nu
ai nevoie de functionalitatile extra oferite de memcached atunci APCu este probabil cea mai buna alegere
pentru stocarea obiectelor.

Exemplu de logica folosind APCu:

{% highlight php %}
<?php
// afla daca exista date salvate ca 'expensive_data' in cache
$data = apc_fetch('expensive_data');
if ($data === false) {
    // data nu e in cache; salvam rezultatul lui apelare scumpa pentru uz ulterior
    apc_add('expensive_data', $data = get_expensive_data());
}

print_r($data);
{% endhighlight %}

De notat ca inainte de PHP 5.5, APC pune la dispozitie atat un cache de obiecte cat si un cache de bytecode.
APCu este un proiect care aduce cache-ul de obiecte al lui APC in PHP 5.5+, intrucat PHP are de acum deja un
bytecode cache incorporat (OPCache).

Afla mai multe despre sisteme populare de cache al obiectelor:

* [APCu](https://github.com/krakjoe/apcu)
* [APC Functions](http://php.net/manual/ro/ref.apc.php)
* [Memcached](http://memcached.org/)
* [Redis](http://redis.io/)
* [XCache APIs](http://xcache.lighttpd.net/wiki/XcacheApi)
* [WinCache Functions](http://www.php.net/manual/ro/ref.wincache.php)
