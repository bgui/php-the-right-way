---
isChild: true
---

## Problema Complexă {#complex_problem_title}

Dacă ai citit vreodată despre injectarea dependințelor atunci ai văzut probabil termenii *"Inversiunea Controlului"* sau
*"Principiul inversiunii dependinței"*. Acestea sunt problemele complexe pe care injectarea dependințelor le rezolvă.

### Inversiunea controlului

Inversiunea controlului, după cum și numele îi sugerează, este "inversarea controlului" unui sistem prin păstrarea
controlului organizațional complet separat de obiectele noastre. În termeni de injectarea dependințelor, asta înseamnă
flexibilizarea dependințelor noastre prin controlul și instanțierea lor în altă parte a sistemului.

De ani, framework-urile PHP realizau inversiunea controlului, dar, întrebarea a devenit, care parte a controlului
o inversezi, și spre ce? De exemplu, framework-urile MVC puneau la dispoziție un super obiect sau controller de bază pe
care alte controllere trebuia să îl extindă pentru a primi acces la dependințele sale. Aceasta **este** inversiune
a controlului, însă, în loc de flexibilizare a dependințelor, această metodă le mută doar în altă parte.

Injectarea dependințelor ne permite să rezolvăm mai elegant această problemă prin injectarea numai a dependințelor de
care avem nevoie, când avem nevoie de ele, fără a fi nevoie să le explicităm deloc în scris.

### Principiul inversiunii dependințelor

Principiul inversiunii dependințelor este "D"-ul din setul S.O.L.I.D de principii de proiectare orientată pe obiecte
care spune că ar trebui să *"depinzi de abstracțiuni și nu de concrete"*. Spus simplu, asta înseamnă că dependințele
noastre ar trebui să fie interfețe/contracte sau clase abstracte mai degrabă decât implementări concrete. Putem
refactoriza exemplul de mai sus ca să urmeze acest principiu.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct(AdapterInterface $adapter)
    {
        $this->adapter = $adapter;
    }
}

interface AdapterInterface {}

class MysqlAdapter implements AdapterInterface {}
{% endhighlight %}

Exista câteva beneficii acum că clasa `Database` depinde de o interfață și nu de ceva concret.

Imaginează-ți că lucrezi în echipă iar colegul tău lucrează la adaptor. În primul exemplu, ar trebui să așteptăm după
colegul ca să termine adaptorul înainte de a îl mock-ui pentru unit teste. Acum că dependința este o interfața/contract
noi putem să mock-uim liniștiți interfață știind că colegul va construi adaptorul bazat pe contract.

Un și mai mare beneficiu al acestei metode este că codul nostru este acum mai scalabil. Dacă peste un an vom decide că
vrem să migrăm la un alt tip de bază de date, putem scrie un adaptor care implementează interfața originală și să îl
injectăm pe acela, nici un pic de refactorizare nu ar fi necesară întrucât putem fi siguri că adaptorul respectă
contractul setat de interfață.
