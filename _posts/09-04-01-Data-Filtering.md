---
isChild: true
---

## Filtrarea datelor {#data_filtering_title}

Niciodată să nu ai încredere în input străin ce intră în codul tău PHP. Totdeauna sanitizează și
validează datele de intrare străine înainte de a le folosi în cod. Funcțiile `filter_var` și
`filter_input` pot sanitiza text și valida formate text (e.g. adrese de email)

Input străin poate fi orice: `$_GET` și formulare `$_POST`, unele valori din super-globalul
`$_SERVER`, și corpul interogării HTTP via `fopen('php://input', 'r')`. Tine minte,
input-ul străin nu e limitat la date de formular trimise de utilizatori. Fișiere încărcate sau
descărcate, valori de sesiune, date cookie, date de la servicii web terțe sunt de asemenea
străine.

Când datele străine pot fi stocate, combinate, și accesate mai târziu, sunt încă străine.
De fiecare dată când procesezi, afișezi, concatenezi sau incluzi datele în codul tău,
întreabă-te dacă au fost filtrate corespunzător și dacă sunt de încredere.

Datele pot fi _filtrate_ diferit în funcție de scopul sau. De exemplu, când input străin
este pasat în conținutul paginii HTML, el poate executa HTML și Javascript pe siteul tău!
Asta se numește Cross-Site Scripting (XSS) și poate fi un atac foarte periculos. O metodă
de a evita un atac XSS este să sanitizezi orice data generată de utilizatori înainte de
a o afișa pe pagina ta prin eliminarea tag-urilor HTML cu funcția `strip_tags` sau
escape-ând caractere cu sens special în entitățile lor HTML respective folosind
funcțiile `htmlentities` sau `htmlspecialchars`.

Alt exemplu este pasarea opțiunilor ce vor fi executate în linia de comandă. Aceasta poate
fi extrem de periculos (și e de obicei o idee rea), dar poți folosi funcția incorporată
`escapeshellarg` pentru a sanitiza argumentele comenzii executate.

Un ultim exemplu este acceptarea intrărilor străine pentru a determina un fișier
de încărcat din sistemul de fișiere. Asta poate fi exploatată prin schimbarea
numelui fișierului într-o cale de fișiere. Poți șterge "/", "../", [null bytes][6],
sau alte caractere din calea fișierului așa încât să nu poată încărca fișiere ascunse,
non-publice, sau fișiere sensitive.

* [Află despre filtrarea datelor][1]
* [Află despre `filter_var`][4]
* [Află despre `filter_input`][5]
* [Află despre null bytes][6]

### Sanitizare

Sanitizarea elimină(sau escape-ează) caractere ilegale sau nesigure din inputul străin.

De exemplu, ar trebui sanitizat inputul străin înainte de includerea sa în HTML sau de
inserarea sa într-o interogare SQL brută. Când folosești parametri bound cu [PDO](#databases),
el va sanitiza input-ul pentru tine.

Uneori este necesar să lași unele tag-uri HTML permise în input atunci când îl incluzi
în pagina HTML. Asta este foarte greu de făcut iar mulți evita chestia asta prin
folosirea unui mod de formatare mai restricționat precum Markdown sau BBCode, deși
biblioteci de validare precum [HTML Purifier][html-purifier] există exact pentru
acest scop.

[Vezi filtre de sanitizare][2]

### Validare

Validarea asigură că inputul străin este ceea ce te așteptai sa fie. De exemplu, ai putea dori
să validezi o adresa email, un număr de telefon, sau vârsta când procesezi o
cerere de înregistrare.

[Vezi filtre de validare][3]

[1]: http://www.php.net/manual/ro/book.filter.php
[2]: http://www.php.net/manual/ro/filter.filters.sanitize.php
[3]: http://www.php.net/manual/ro/filter.filters.validate.php
[4]: http://php.net/manual/ro/function.filter-var.php
[5]: http://www.php.net/manual/ro/function.filter-input.php
[6]: http://php.net/manual/ro/security.filesystem.nullbytes.php
[html-purifier]: http://htmlpurifier.org/