---
isChild: true
---

## Paradigme {#programming_paradigms_title}

PHP este un limbaj flexibil, dinamic, care suportă o varietate de tehnici de programare. A evoluat dramatic peste ani,
notabile fiind adăugarea solidului model orientat obiect în PHP 5.0 (2004), funcțiile anonime și namespace-uri în PHP 5.3
(2009), traits în PHP 5.4 (2012).

### Programare orientată obiect

PHP are un complet set de funcționalități orientate obiect incluzând suport pentru clase, clase abstracte, interfețe,
moștenire, constructori, clonare, excepții, și multe altele.

* [Citește despre PHP orientat-obiect][oop]
* [Citește despre traits][traits]

### Programare funcțională

PHP suporta funcții de "prima mână", asta însemnând ca o funcție poate fi asignată unei variabile. Atât funcții
definite de utilizator cat și cele definite de limbaj pot fi referențiate de o variabilă și invocate dinamic. Funcțiile
pot fi furnizate ca argument către alte funcții (funcționalitate denumită funcții de "Înalt Nivel") sau pot returna alte funcții.

Recursivitatea, o funcționalitate care permite unei funcții să se auto-apeleze este suportată de limbaj, dar majoritatea
codului PHP se concentrează pe iterație.

Noile funcții anonime (cu suport pentru closures) sunt prezente începând cu PHP 5.3 (2009).

PHP 5.4 a adăugat abilitatea de a lega closure-uri de scope-ul obiectului și suport îmbunătățit pentru callables
așa încât ele pot fi folosite interschimbabil cu funcții anonime în aproape orice caz.

* Continuă să citești pe [Programare functionala in PHP](/pages/Functional-Programming.html)
* [Citește despre funcții anonime][anonymous-functions]
* [Citește despre clasa Closure][closure-class]
* [Mai multe detalii în RFC-ul despre closure-uri][closures-rfc]
* [Citește despre Callables][callables]
* [Citește despre invocarea dinamic cu `call_user_func_array`][call-user-func-array]

### Meta programare

PHP suportă diverse forme de meta-programare prin mecanisme ca Reflection API și Metode Magice. Sunt multe metode
magice disponibile precum `__get()`, `__set()`, `__clone()`, `__toString()`, `__invoke()`, etc. care permit
dezvoltatorilor să intervină în comportamentul clasei. Programatorii de Ruby spun deseori că în PHP lipsește `method_missing`,
dar aceasta e disponibilă sub forma `__call()` and `__callStatic()`.

* [Citește despre metode magice][magic-methods]
* [Citește despre Reflecție][reflection]

[namespaces]: http://php.net/manual/ro/language.namespaces.php
[overloading]: http://php.net/manual/ro/language.oop5.overloading.php
[oop]: http://www.php.net/manual/ro/language.oop5.php
[anonymous-functions]: http://www.php.net/manual/ro/functions.anonymous.php
[closure-class]: http://php.net/manual/ro/class.closure.php
[callables]: http://php.net/manual/ro/language.types.callable.php
[magic-methods]: http://php.net/manual/ro/language.oop5.magic.php
[reflection]: http://www.php.net/manual/ro/intro.reflection.php
[traits]: http://www.php.net/traits
[call-user-func-array]: http://php.net/manual/ro/function.call-user-func-array.php
[closures-rfc]: https://wiki.php.net/rfc/closures