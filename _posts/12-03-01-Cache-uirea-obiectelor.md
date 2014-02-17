---
isChild: true
---

## Cache-uirea obiectelor {#object_caching_title}

Exista momente când poate fi benefic să cache-uiesti obiecte individuale în codul tău, de exemplu cu date care
sunt scump de obținut sau cu apeluri către baza de date care sunt improbabil de a se fi schimbat.
Poți folosi software pentru cache-iuirea obiectelor pentru a ține aceste bucăți de date în memorie pentru
acces rapid mai târziu. Dacă salvezi acești itemi într-o datastore după ce ii recuperezi, atunci
iai direct din cache data viitoare când ai nevoie de ei, poți câștiga o îmbunătățire semnificativa a
performantei ca și o reducere a încărcării serverului bazei de date.

De asemenea, multe din soluțiile populare de cache-uire a bytecode-ului te lasă să stochezi și date personalizate,
asa că ai chiar și mai multe motive să profiți de ele. APCu, XCache, si WinCache toate pun la dispoziție API-uri
pentru a salva date din codul tău PHP în memoria lor.

Cele mai populare sisteme de cache-uire a obiectelor sunt APCu și memcached. APCu este o excelentă alegere
pentru cache-ul de obiecte, are un API simplu pentru inserarea datelor tale în memoria sa cache si este
foarte simplu de folosit. Singura limitare a APCu este că este legată de serverul pe care e instalată.
Memcached pe de altă parte este instalat ca un serviciu separat și poate fi accesat prin intermediul rețelei,
însemnând ca poți stoca obiecte într-o magazie super-rapidă, într-o locație centrală, și mai multe sisteme
diferite le pot citi din ea.

Nota: când rulam PHP ca aplicație (Fast-)CGI inauntrul webserver-ului, fiecare proces PHP va avea propriul
cache, adică datele APCu nu sunt la comun pentru toate procesele. În aceste cazuri, probabil ai vrea să
folosești memcached, întrucât nu e legat de procesele PHP.

Într-o configurație cu rețea, APCu va performa mai bine decât memcached în termeni de viteză, dar memcached va putea
să scaleze mai rapid și mai departe. Dacă nu te aștepți să ai mai multe servere pentru aplicația ta, sau nu
ai nevoie de funcționalitate extra oferite de memcached atunci APCu este probabil cea mai bună alegere
pentru stocarea obiectelor.

Exemplu de logica folosind APCu:

{% highlight php %}
<?php
// afla dacă există date salvate ca 'expensive_data' în cache
$data = apc_fetch('expensive_data');
if ($data === false) {
    // data nu e în cache; salvăm rezultatul dupa apelare scumpă pentru uz ulterior
    apc_add('expensive_data', $data = get_expensive_data());
}

print_r($data);
{% endhighlight %}

De notat ca înainte de PHP 5.5, APC pune la dispoziție atât un cache de obiecte cât și un cache de bytecode.
APCu este un proiect care aduce cache-ul de obiecte al lui APC în PHP 5.5+, întrucât PHP are de acum deja un
bytecode cache încorporat (OPCache).

Află mai multe despre sisteme populare de cache al obiectelor:

* [APCu](https://github.com/krakjoe/apcu)
* [APC Functions](http://php.net/manual/ro/ref.apc.php)
* [Memcached](http://memcached.org/)
* [Redis](http://redis.io/)
* [XCache APIs](http://xcache.lighttpd.net/wiki/XcacheApi)
* [WinCache Functions](http://www.php.net/manual/ro/ref.wincache.php)