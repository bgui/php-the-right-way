---
isChild: true
---

## Register Globals {#register_globals_title}

**NOTA:** Incepand cu PHP 5.4.0 setarea `register_globals` a fost eliminata si
nu mai poate fi folosita. Prezenta este inclusa numai ca o avertizare pentru
cei ce se afla in proces de actualizare a unei aplicatii vechi.

Cand este activata, setarea de configurare `register_globals` face ca unele tipuri de
variabile (inclusiv `$_POST`, `$_GET` and `$_REQUEST`) sa fie disponibile in
scope-ul global al aplicatiei. Asta poate duce foarte usor la probleme de securitate
pentru ca aplicatia ta nu poate stabili usor de unde provin datele.

De exemplu: `$_GET['foo']` ar deveni disponibila via `$foo`, care poate suprascrie
variabile care nu au fost declarate.
Daca folosesti PHP < 5.4.0 __fii sigur__ ca `register_globals` este __off__.

* [Register_globals in manualul PHP](http://www.php.net/manual/ro/security.globals.php)