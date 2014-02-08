---
isChild: true
---

## Paradigme {#programming_paradigms_title}

PHP este un limbaj flexibil, dinamic, care suporta o varietate de tehnici de programare. A evoluat dramatic peste ani,
notabile fiind adaugarea solidului model orientat obiect in PHP 5.0 (2004), functiile anonime si namespace-uri in PHP 5.3
(2009), traits in PHP 5.4 (2012).

### Programare orientata obiect

PHP are un foarte complet set de functionalitati orientate obiect incluzand suport pentru clase, clase abstracte, interfete,
mostenire, constructori, clonare, exceptii, si multe altele.

* [Citeste despre PHP orientat-obiect][oop]
* [Citeste despre traits][traits]

### Programare functionala

PHP suporta functii de "prima clasa", asta insemnand ca o functie poate fi asignata unei variabile. Atat functii
definite de utilizator cat si cele definite de limbaj pot fi referentiate de o variabile si invocate dinamic. Functiile
pot fi furnizate ca argument catre alte functii (functionalitate denumita functii de "Inalt Nivel") sau pot returna alte functii.

Recursivitatea, o functionalitate care permite unei functii sa se auto-apeleze este suportata de limbaj, dar majoritatea
codului PHP se concentreaza pe iteratie.

Noile functii anonime (cu suport pentru closures) sunt prezente incepand cu PHP 5.3 (2009).

PHP 5.4 a adaugat abilitatea de a lega closure-uri de scope-ul obiectului si suport imbunatatit pentru callables
asa incat ele pot fi folosite interschimbabil cu functii anonime in aproape orice caz.

* Continua sa citesti pe [Programare functionala in PHP](/pages/Functional-Programming.html)
* [Citeste despre functii anonime][anonymous-functions]
* [Citeste despre clasa Closure][closure-class]
* [Mai multe detalii in RFC-ul despre closure-uri][closures-rfc]
* [Citeste despre Callables][callables]
* [Citeste despre invocarea dinamic cu `call_user_func_array`][call-user-func-array]

### Meta programare

PHP suporta diverse forme de meta-programare prin mecanisme ca Reflection API si Metode Magice. Sunt multe metode
magice disponibile precum `__get()`, `__set()`, `__clone()`, `__toString()`, `__invoke()`, etc. care permit
dezvoltatorii sa intervina in comportamentul clasei. Programatorii de Ruby spun deseori ca in PHP lipseste `method_missing`,
dar aceasta e disponibila sub forma `__call()` and `__callStatic()`.

* [Citeste despre metode magice][magic-methods]
* [Citeste despre Reflectie][reflection]

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
