---
isChild: true
---

## Filtrarea datelor {#data_filtering_title}

Niciodata sa nu ai incredere in input strain ce intra in codul tau PHP. Totdeauna sanitizeaza si
valideaza datele de intrare straine inainte de a le folosi in cod. Functiile `filter_var` si
`filter_input` pot sanitiza text si valida formate text (e.g. adrese de email)

Input strain poate fi orice: `$_GET` si formulare `$_POST`, unele valori din superglobalul
`$_SERVER`, si corpul interogarii HTTP via `fopen('php://input', 'r')`. Tine minte,
input-ul strain nu e limitat la date de formular trimise de utilizatori. Fisiere incarcate sau
descarcate, valori de sesiune, date cookie, date de la servicii web terte sunt de asemenea
straine.

Cand datele straine pot fi stocate, combinate, si accesate mai tarziu, sunt inca straine.
De fiecare data cand procesezi, afisezi, concatenezi sau incluzi datele in codul tau,
intreaba-te daca au fost filtrate corespunzator si daca sunt de incredere.

Datele pot fi _filtrate_ diferit in functie de scopul sau. De exemplu, cand input strain
este pasat in continutul paginii HTML, el poate executa HTML si Javascript pe siteul tau!
Asta se numeste Cross-Site Scripting (XSS) si poate fi un atac foarte periculos. O metoda
de a evita un atac XSS este sa sanitizezi orice data generata de utilizatori inainte de
a o afisa pe pagina ta prin eliminarea tag-urilor HTML cu functia `strip_tags` sau
escape-and caractere cu sens special in entitatile lor HTML respective folosind
functiile `htmlentities` sau `htmlspecialchars`.

Alt exemplu este pasarea optiunilor ce vor fi executate in linia de comanda. Aceasta poate
fi extrem de periculos (si e de obicei o idee rea), dar poti folosi functia incorporata
`escapeshellarg` pentru a sanitiza argumentele comenzii executate.

Un ultim exemplu este acceptarea intrarilor straine pentru a determina un fisier
de incarcat din sistemul de fisiere. Asta poate fi exploatata prin schimbarea
numelui fisierului intr-o cale de fisiere. Poti sterge "/", "../", [null bytes][6],
sau alte caractere din calea fisierului asa incat sa nu poata incarca fisiere ascunse,
non-publice, sau fisiere sensitive.

* [Afla despre filtrarea datelor][1]
* [Afla despre `filter_var`][4]
* [Afla despre `filter_input`][5]
* [Afla despre null bytes][6]

### Sanitizare

Sanitizarea elimina(sau escape-eaza) caractere ilegale sau nesigure din inputul strain.

De exemplu, ar trebui sanitizat inputul strain inainte de includerea sa in HTML sau de
inserarea sa intr-o interogare SQL bruta. Cand folosesti parametri bound cu [PDO](#databases),
el va sanitiza input-ul pentru tine.

Uneori este necesar sa lasi unele tag-uri HTML permise in input atunci cand il incluzi
in pagina HTML. Asta este foarte greu de facut iar multi evita chestia asta prin
folosirea unui mod de formatare mai restrictionat precum Markdown sau BBCode, desi
biblioteci de validare precum [HTML Purifier][html-purifier] exista exact pentru
acest scop.

[Vezi filtre de sanitizare][2]

### Validare

Validarea asigura ca inputul strain este ceeace te asteptai sa fie. De exemplu, ai putea dori
sa validezi o adresa email, un numar de telefon, sau varsta cand procesezi o
cerere de inregistrare.

[Vezi filtre de validare][3]

[1]: http://www.php.net/manual/ro/book.filter.php
[2]: http://www.php.net/manual/ro/filter.filters.sanitize.php
[3]: http://www.php.net/manual/ro/filter.filters.validate.php
[4]: http://php.net/manual/ro/function.filter-var.php
[5]: http://www.php.net/manual/ro/function.filter-input.php
[6]: http://php.net/manual/ro/security.filesystem.nullbytes.php
[html-purifier]: http://htmlpurifier.org/
