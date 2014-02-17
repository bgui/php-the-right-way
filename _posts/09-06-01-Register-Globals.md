---
isChild: true
---

## Register Globals {#register_globals_title}

**NOTA:** Începând cu PHP 5.4.0 setarea `register_globals` a fost eliminată și
nu mai poate fi folosită. Prezenta este inclusă numai ca o avertizare pentru
cei ce se află în proces de actualizare a unei aplicații vechi.

Când este activată, setarea de configurare `register_globals` face ca unele tipuri de
variabile (inclusiv `$_POST`, `$_GET` și `$_REQUEST`) să fie disponibile în
scope-ul global al aplicației. Asta poate duce foarte ușor la probleme de securitate
pentru că aplicația ta nu poate stabili ușor de unde provin datele.

De exemplu: `$_GET['foo']` ar deveni disponibilă via `$foo`, care poate suprascrie
variabile care nu au fost declarate.
Dacă folosești PHP < 5.4.0 __fii sigur__ ca `register_globals` este __off__.

* [Register_globals în manualul PHP](http://www.php.net/manual/ro/security.globals.php)