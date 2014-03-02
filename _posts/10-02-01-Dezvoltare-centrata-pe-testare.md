---
isChild: true
---

## Dezvoltarea centrata pe teste {#test_driven_development_title}

De la [Wikipedia](http://en.wikipedia.org/wiki/Test-driven_development):

> Dezvoltarea centrata pe teste (TDD) este un proces de dezvoltare software care se bazează pe repetiția unui foarte
> scurt ciclu de dezvoltare: mai întâi programatorul scrie un test care eșuează care descrie o îmbunătățire sau o nouă
> funcționalitate, apoi produce codul care va satisface acel test iar în final rescrie codul cel nou într-o maniera
> compatibila cu standarde. Kent Beck, care este creditat cu dezvoltarea sau 'redescoperirea' acestei tehnici, spunea în
> 2003 ca TDD încurajează arhitecturi simple și inspira încredere

Exista câteva tipuri diferite de testare pe care le poți implementa în aplicațiile tale.

### Testarea unitara

Testarea unitara este o abordare programatica pentru a asigura ca funcțiile, clasele și metodele funcționează precum ne
așteptăm, de la momentul construcției lor și prin tot parcursul ciclului de dezvoltare. Verificând valorile de intrare
și ieșire din diferite funcții și metode, te poți asigura ca logica interna funcționează corect. Pentru o testare de și
mai mare amploare, folosind injectarea de dependințe și construind clase "mock" și cioturi poți verifica ca dependințele
sunt folosite corect.

Când creezi o clasa sau o funcție ar trebui sa creezi și un test unitar pentru fiecare comportament pe care trebuie sa
îl aibă. Ca un minimum ar trebui sa te asiguri ca este produsa o eroare dacă ii sunt furnizate argumente incorecte și ca
funcționează când sunt primite argumente valide. Asta va asigura ca atunci când mai târziu în ciclul de dezvoltare faci
schimbări în aceasta clasa sau funcție, vechea funcționalitate va continua sa meargă precum ne așteptăm. Singura
alternativa la ar fi var_dump() într-un test.php, ceea ce desigur nu e o opțiune serioasa.

Celalalt uz al testelor unitare este contribuirea la open source. Dacă poți scrie un test care demonstrează
funcționalitate stricata (adică eșuează), și îl și repari, și arăți apoi ca testul trece cu bine, apoi patch-urile vor
avea mult mai multe șanse sa fie acceptate. Dacă conduci un proiect care accepta cereri pull atunci ar trebui sugerezi
asta ca o cerință.

[PHPUnit](http://phpunit.de) este framework-ul de-facto pentru scrierea de teste unitare pentru aplicațiile PHP, dar
exista și alternative

* [atomu](https://github.com/atoum/atoum)
* [Enhance PHP](https://github.com/Enhance-PHP/Enhance-PHP)
* [PUnit](http://punit.smf.me.uk/)
* [SimpleTest](http://simpletest.org)


### Testarea integrării

De la [Wikipedia](http://en.wikipedia.org/wiki/Integration_testing):

> Testarea integrării (uneori numită Integrare și Testare, abreviat "I&T") este faza în testarea software-ului în care
> module individuale sunt combinate și testate ca un grup. Se întâmplă după testarea unitară și înainte de testarea
> validării. Testarea integrării ia ca input modulele care au fost testate unitar, le grupează în agregate mai mari,
> aplică testele definite în planul de test asupra acelor agregate, și livrează ca output sistemul integrat gata pentru
> testarea sistemului.

Multe dintre aceleași unelte care pot fi folosite pentru testare unitară pot fi folosite și pentru testarea integrării
pentru ca multe dintre aceleași principii sunt folosite.

### Testare funcțională

Uneori cunoscută și drept testare a acceptării, testarea funcțională înseamnă folosirea de unelte pentru a crea automat
teste care folosesc cu adevărat aplicația în loc de a verifica doar că bucăți de cod individuale se comportă corect sau
că pot vorbi între ele. Aceste unelte operează de obicei folosind date reale și simulează utilizatorii reali ai
aplicației.

#### Unelte de testare funcțională

* [Selenium](http://seleniumhq.com)
* [Mink](http://mink.behat.org)
* [Codeception](http://codeception.com) este un framework de teste pentru întreaga stivă care include și unelte de testare a acceptării
* [Storyplayer](http://datasift.github.io/storyplayer) este un framework de teste pentru întreaga stiva care include și suport pentru crearea și distrugerea mediilor de test la cerere
