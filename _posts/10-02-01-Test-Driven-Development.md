---
isChild: true
---

## Dezvoltarea centrata pe teste {#test_driven_development_title}

De la [Wikipedia](http://en.wikipedia.org/wiki/Test-driven_development):

> Dezvoltarea centrata pe teste (TDD) este un proces de dezvoltare software care se
bazeaza pe repetitia unui foarte scurt ciclu de dezvoltare: mai intai programatorul scrie un test
care esueaza care descrie o imbunatatire sau o noua functionalitate, apoi produce codul care va
satisface acel test iar in final rescrie codul cel nou intr-o maniera compatibila cu standarde.
Kent Beck, care este creditat cu dezvoltarea sau 'redescoperirea' acestei tehnici, spunea in 2003
ca TDD incurajaza arhitecturi simple si inspira incredere

Exista cateva diferite tipuri de testare pe care o poti face asupra aplicatiei tale

### Testarea unitara

Testarea unitara este o abordare programatica pentru a asigura ca functiile, clasele si metodele
functioneaza precum ne asteptam, de la momentul constructiei lor si prin tot parcursul ciclului
de dezvoltare. Verificand valorile de intrare si iesire din diferite functii si metode, te poti
asigura ca logica interna functioneaza corect. Pentru o testare de si mai mare aploare, folosind
injectarea de dependinte si construind clase "mock" si cioturi poti verifica ca dependintele
sunt folosite corect.

Cand creezi o clasa sau o functie ar trebui sa creezi si un test unitar pentru fiecare
comportament pe care trebuie sa il aiba. Ca un minimum ar trebui sa te asiguri ca este produsa
o eroare daca ii sunt furnizate argumente incorecte si ca functioneaza cand sunt primite
argumente valide. Asta va asigura ca atunci cand mai tarziu in ciclul de dezvoltare faci schimbari
in aceasta clasa sau functie, vechea functionalitate va continua sa mearga precum ne asteptam.
Singura alternativa la asta ar fi var_dump() intr-un test.php, ceeace desigur nu e o optiune serioasa.

Celalalt uz al testelor unitare este contribuirea la open source. Daca poti scrie un test care
demonstreaza functionalitate stricata (adica esueaza), si il si repari, si arati apoi ca testul
trece cu bine, apoi patch-urile vor avea mult mai multe sanse sa fie acceptate.
Daca conduci un proiect care accepta cereri pull atunci ar trebui sugerezi asta ca o cerinta.

[PHPUnit](http://phpunit.de) este framework-ul de-facto pentru scrierea de teste unitare pentru
aplicatiile PHP, dar exista si alternative

* [atoum](https://github.com/atoum/atoum)
* [Enhance PHP](https://github.com/Enhance-PHP/Enhance-PHP)
* [PUnit](http://punit.smf.me.uk/)
* [SimpleTest](http://simpletest.org)


### Testarea integrarii

De la [Wikipedia](http://en.wikipedia.org/wiki/Integration_testing):

> Testarea integrarii (uneori numita Integrare si Testare, abreviat "I&T") este faza
in testarea softwareului in care module individuale sunt combinate si testate ca un grup.
Se intampla dupa testarea unitara si inainte de testarea validarii. Testarea integrarii
ia ca input modulele care au fost testate unitar, le grupeaza in agregate mai mari,
aplica testele definite in planul de test asupra acelor agregate, si livreaza ca
output sistemul integrat gata pentru testarea sistemului.

Multe dintre acealeasi unelte care pot fi folosite pentru testare unitara pot fi folosite si
pentru testarea integrarii pentru ca multe dintre aceleasi principii sunt folosite.

### Testare functionala

Uneori cunoscuta si drept testare a acceptarii, testarea functionala inseamna folosirea de
unelte pentru a creea automat teste care folosesc cu adevarat aplicatia in loc de a
verifica doar ca bucati de cod individuale se comporta corect sau ca pot vorbi intre ele.
Aceste unelte opereaza de obicei folosind date reale si simuleaza utilizatorii reali ai aplicatiei.

#### Unelte de testare functionala

* [Selenium](http://seleniumhq.com)
* [Mink](http://mink.behat.org)
* [Codeception](http://codeception.com) este un framework de teste pentru intreaga stiva care include si unelte de testare a acceptarii
* [Storyplayer](http://datasift.github.io/storyplayer) este un framework de teste pentru intreaga stiva care include si suport pentru crearea si distrugerea mediilor de test la cerere

