---
isChild: true
---

## Problema Complexa {#complex_problem_title}

Daca ai citit vreodata despre injectarea dependintelor atunci ai vazut probabil termenii *"Inversiunea Controlului"*
sau *"Principiul inversiunii dependintei"*.
Acestea sunt problemele complexe pe care injectarea dependintelor le rezolva.

### Inversiunea controlului

Inversiunea controlului este, dupa cum se aude, inversiunea controlului unui sistem prin pastrarea controlului
organizational complet separat de obiectele noastre.
In termeni de injectarea dependintelor, asta inseamna flexibilizarea dependintelor noastre prin
controlul si instantierea lor in alta parte a sistemului.

De ani, framework-urile PHP realizau inversiunea controlului, dar, intrebarea a devenit, care parte
a controlului o inversezi, si spre ce? De exemplu, framework-urile MVC puneai la dispozitie un
super obiect sau controller de baza pe care alte controllere trebuiau sa le extinda pentru a primi
acces la dependintele sale. Aceasta **este** inversiune a controlului, insa, in loc de flexibilizare
a dependintelor, aceasta metoda le muta doar in alta parte.

Injectarea dependintelor ne permite sa rezolvam mai elegant aceasta problema prin injectarea numai
dependintelor de care avem nevoie, cand avem nevoie de ele, fara a fi nevoie sa le explicitam deloc in scris.

### Principiul inversiunii dependintelor

Principiul inversiunii dependintelor este "D"-ul din setul S.O.L.I.D de principii de proiectare orientata obiect
care spune ca ar trebui sa *"depinzi de abstractiuni si nu de concret-uri"*. Spus simplu, asta inseamna ca
dependintele noastre ar trebui sa fie interfete/contracte sau clase abstracte mai degraba decat implementari
concrete. Putem refactoriza exemplul de mai sus ca sa urmeze acest principiu.

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

Exista cateva beneficii acum ca clasa `Database` depinde de o interfata si nu de ceva concret.

Imagineaza-ti ca lucrezi in echipa iar colegul tau lucreaza la adaptor. In primul exemplu, ar trebui sa asteptam
dupa colegul ca sa termine adaptorul inainte de a il mock-ui pentru unit teste. Acum ca dependinta este o
interfata/contract noi putem sa mock-uim linistiti interfata stiind ca colegul va construi adapterul bazat pe contract.

Un si mai mare beneficiu al acestei metode este ca codul nostru este acum mai scalabil. Daca peste un an vom decide ca
vrem sa migram la un alt tip de baza de date, putem scrie un adaptor care implementeaza interfata originala si
sa il injectam pe acela, nici un pic de refactorizare nu ar fi necesara intrucat putem fi siguri ca adaptorul
respecta contractul setat de interfata.
