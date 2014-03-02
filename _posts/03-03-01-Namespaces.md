---
isChild: true
---

## Namespace-uri {#namespaces_title}

După cum am menționat mai sus, comunitatea PHP e formată din multi dezvoltatori care creează mult cod. Asta înseamnă că
într-o bibliotecă poate fi folosit același nume de clasă ca în altă bibliotecă. Când ambele biblioteci sunt folosite în
același namespace ele sunt în coliziune și cauzează probleme.

_Namespace_-urile rezolvă această problemă. Precum e descris în manualul PHP, namespace-urile pot fi comparate cu
directoarele unui sistem de operare ce conțin fișiere; doua fișiere cu același nume pot co-exista în directoare
separate. De asemenea, două clase PHP cu același nume pot co-exista în namespace-uri PHP diferite. Este atât de simplu.

E important să iți bagi codul într-un namespace așa încât să poată fi folosit și de alți dezvoltatori fără frica de
coliziune cu alte biblioteci.

O metodă recomandată de a folosi namespace-uri este prezentată în [PSR-0][psr0], care se dorește să furnizeze
o convenție standard de fișiere, clase și namespace-uri pentru a permite cod "plug-and-play".

În Decembrie 2013 PHP-FIG a creat un nou standard pentru autoloading: [PSR-4][psr4], care probabil într-o zi va înlocui
PSR-0. Momentan ambele sunt folosite întrucât PSR-4 necesită PHP 5.3 iar multe proiecte 5.2 implementează PSR-0. Dacă
vei folosi un standard pentru autoloading pentru o nouă aplicație sau pachet atunci aproape sigur vei vrea să te uiți
spre PSR-4.

* [Citește despre Namespace-uri][namespaces]
* [Citește despre PSR-0][psr0]
* [Citește despre PSR-4][psr4]

[namespaces]: http://php.net/manual/ro/language.namespaces.php
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
