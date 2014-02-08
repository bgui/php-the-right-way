---
isChild: true
---

## Namespace-uri {#namespaces_title}

Dupa cum am mentionat mai sus, comunitatea PHP e formata din multi dezvoltatori care creeaza mult cod.
Asta inseamna ca intr-o biblioteca poate fi folosit acelas nume de clasa ca in alta biblioteca. Cand ambele
biblioteci sunt folosite in acelas namespace ele sunt in coliziune si cauzeaza probleme.

_Namespace_-urile rezolva aceasta problema. Precum e descris in manualul PHP, namespace-urile pot fi comparate
cu directoarele unui sistem de operare ce contin fisiere; doua fisiere cu acelas nume pot co-exista in
directoare separate. De asemenea, doua clase PHP cu acelas nume pot co-exista in namespace-uri PHP
diferite. Este atat de simplu.

E important sa iti bagi codul intr-un namespace asa incat sa poate fi folosit si de alti dezvoltatori fara
frica de coliziune cu alte biblioteci.

O metoda recomandata de a folosi namespace-uri este prezentata in [PSR-0][psr0], care se doreste sa furnizeze
o conventie standard de fisiere, clase si namespace-uri pentru a permite cod "plug-and-play".

In Decembrie 2013 PHP-FIG a creeat un nou standard pentru autoloading: [PSR-4][psr4], care probabil intr-o zi
va inlocui PSR-0. Momentan ambele sunt uzabile intrucat PSR-4 necesita PHP 5.3 iar multe proiecte 5.2 implementeaza
PSR-0. Daca vei folosi un standard pentru autoloading pentru o noua aplicatie sau pachet atunci aproape sigur vei
vrea sa te uiti spre PSR-4.

* [Citeste despre Namespace-uri][namespaces]
* [Citeste despre PSR-0][psr0]
* [Citeste despre PSR-4][psr4]

[namespaces]: http://php.net/manual/ro/language.namespaces.php
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md