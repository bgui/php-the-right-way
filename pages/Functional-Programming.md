---
layout: page
title: Programare funcțională în PHP
---

# Programare funcțională în PHP

PHP suportă funcții de "prima mână", asta însemnând că o funcție poate fi asignată unei variabile. Atât funcții
definite de utilizator cat și cele definite de limbaj pot fi referențiate de o variabilă și invocate dinamic. Funcțiile
pot fi furnizate ca argument către alte funcții sau pot returna alte funcții (funcționalitate denumită funcții de "Înalt Nivel").

Recursivitatea, o funcționalitate care permite unei funcții să se auto-apeleze este suportată de limbaj, dar majoritatea
codului PHP se concentrează pe iterație.

Noile funcții anonime (cu suport pentru closures) sunt prezente începând cu PHP 5.3 (2009).

PHP 5.4 a adăugat abilitatea de a lega closure-uri de scope-ul obiectului și suport îmbunătățit pentru callables
așa încât ele pot fi folosite interschimbabil cu funcții anonime în aproape orice caz.

Cel mai des întâlnit uz al funcțiilor de nivel înalt este când este implementat șablonul strategie.
Funcția incorporată `array_filter` cere array-ul de intrare (data) și o funcție
(o strategie sau o callback) folosită ca filtru pe fiecare element din array.


{% highlight php %}
<?php
$input = array(1, 2, 3, 4, 5, 6);

// Creează o nouă funcție anonimă și o asignează unei variabile
$filter_even = function($item) {
    return ($item % 2) == 0;
};

// funcția incorporată array_filter primește atât datele cât și funcția
$output = array_filter($input, $filter_even);

// Funcția nu are nevoie să fie asignată unei variabile. Și asta e valid:
$output = array_filter($input, function($item) {
    return ($item % 2) == 0;
});

print_r($output);
{% endhighlight %}

O closure este o funcție anonimă care poate accesa variabile importate din afara scope-ului
fără a folosi nici o variabilă globală. Teoretic, o closure este o funcție cu unele
argumente închise (fixați) de către mediu atunci când este definită. Closure-urile pot ocoli
restricțiile de scope ale variabilelor într-un mod curat.

În următorul exemplu folosim closure-uri pentru a defini o funcție ce returnează
o singură funcție filtru pentru `array_filter`, dintr-o familie de funcții filtru.

{% highlight php %}
<?php
/**
 * Creează o funcție filtru anonimă care acceptă elemente > $min
 *
 * Returnează un singur filtru dintr-o familie de filtre "mai mare ca n"
 */
function criteria_greater_than($min)
{
    return function($item) use ($min) {
        return $item > $min;
    };
}

$input = array(1, 2, 3, 4, 5, 6);

// Folosește array_filter pe un input cu o funcție filtru selectată
$output = array_filter($input, criteria_greater_than(3));

print_r($output); // items > 3
{% endhighlight %}

Fiecare funcție filtru din familie acceptă numai elemente mai mari decât o valoare minimă.
Singurul filtru returnat de `criteria_greater_than` este un closure cu argumentul `$min` închis
de valoarea din scope (pasat ca argument când `criteria_greater_than` este apelat).

"Early Binding" este folosit pentru importarea variabilei `$min` în funcția creată.
Pentru closure-uri adevărate cu "late binding" ar trebui să folosești referințe când imporți.
Imaginează-ți o bibliotecă de șabloane sau de validarea intrărilor, unde closure este
definită pentru a captura variabile în scope și de a le accesa mai târziu când funcția anonimă e evaluată.


* [Citește despre funcții anonime][anonymous-functions]
* [Mai multe detalii în RFC-ul closures][closures-rfc]
* [Citește despre invocarea dinamică de funcții cu `call_user_func_array`][call-user-func-array]

[anonymous-functions]: http://www.php.net/manual/en/functions.anonymous.php
[call-user-func-array]: http://php.net/manual/en/function.call-user-func-array.php
[closures-rfc]: https://wiki.php.net/rfc/closures
