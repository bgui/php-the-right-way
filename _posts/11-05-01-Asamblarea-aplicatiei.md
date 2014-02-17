---
isChild: true
---
 
## Asamblarea și lansarea aplicației tale {#asamblarea_title}
 
Dacă te surprinzi modificând schema bazei de date manual sau rulând testele manual înaintea actualizării
fișierelor tale(manual), mai gândește-te! Cu fiecare task manual adițional necesar pentru lansarea unei noi
versiuni a aplicației tale, șansa unor greșeli fatale crește dacă ai de-a face cu un simplu update,
un proces de construcție complicat sau chiar o strategie de integrare continuă, [automatizarea asamblării]
(http://en.wikipedia.org/wiki/Build_automation) este prietena ta.
 
Printre pașii pe care ai putea dori sa îi automatizezi s-ar putea numără:
 
* Managementul dependințelor
* Compilare, minificatia resurselor tale
* Execuția de teste
* Crearea de documentație
* Împachetare
* Lansare (deployment)
 
 
### Unelte de automatizare a asamblării
 
Unelte pentru asamblarea aplicației pot fi descrise ca o colecție de scripturi care execută instrucțiuni des
întâlnite în dezvoltarea de software. Unealta de asamblare nu este parte a software-ului tău, ea acționează
asupra soft-ului tău din 'afară'.
 
Există multe unelte open source disponibile care te pot ajuta cu automatizarea asamblarii, unele sunt scrise în PHP
iar altele nu. Asta nu ar trebui să te descurajeze din a le folosi, dacă sunt mai bine potrivite pentru
jobul respectiv. Aici sunt câteva exemple:
 
[Phing](http://www.phing.info/) este cea mai ușoară cale de a începe lansare automată în lumea PHP. Cu
Phing tu îți controla împachetarea, transportul sau procesul de testare dintr-un simplu fișier XML. Phing (care e
bazat pe [Apache Ant](http://ant.apache.org/)) pune la dispoziție un bogat set de instrucțiuni de obicei
necesare pentru actualizarea sau instalarea unei aplicații web și poate fi extins cu instrucțiuni
personalizate adiționale, scrise în PHP.
 
[Capistrano](https://github.com/capistrano/capistrano/wiki) este un sistem pentru *programatori intermediari-spre-avansați*
pentru a executa comenzi, într-o manieră structurată și repetabilă pe una sau mai multe mașini externe.
Este pre-configurat pentru lansarea de aplicații Ruby on Rails, dar totuși se pot lansa cu succes
și sisteme PHP cu el. Uzul cu succes al Capistrano depinde de cunoștințe în Ruby și Rake.
 
Blogpost-ul lui Dave Gardner [Lansare PHP cu Capistrano](http://www.davegardner.me.uk/blog/2012/02/13/php-deployment-with-capistrano/)
este un bun punct de plecare pentru dezvoltatorii PHP interesați de Capistrano.
 
[Chef](http://www.opscode.com/chef/) este mai mult decât un framework de lansare a codului, este un puternic system
de integrare bazat pe Ruby care nu numai iți transporta aplicația dar iți poate construi întregul server sau mașini virtuale.
 
Resurse Chef pentru programatori PHP:
 
* [O serie de articole în trei părți despre lansarea unei aplicații LAMP cu Chef, Vagrant, și EC2](http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/)
* [Carte cu rețete Chef care instalează și configurează PHP 5.3 și sistemul de pachete PEAR](https://github.com/opscode-cookbooks/php)
 
Lecturi aprofundate:
 
* [Automatizează-ți proiectul cu Apache Ant](http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/)
* [Maven](http://maven.apache.org/), un framework pentru automatizarea asamblării (build) bazat pe Ant și
[cum să-l folosești cu PHP](http://www.php-maven.org/)
 
### Integrare continuă
 
> Integrarea continua este o practică a dezvoltării software unde membrii unei echipeisi integrează munca frecvent,
> de obicei fiecare persoana integrează cel puțin zilnic — ducând la mai multe integrări pe zi. Multe echipe găsesc
> ca aceasta abordare duce la un număr semnificativ mai mic de probleme de integrare și permite unei echipe să
> dezvolte software consistent mai rapid.
 
 
*-- Martin Fowler*
 
 
Există diferite metode de a implementa integrare continuă pentru PHP. Recent [Travis CI](https://travis-ci.org/) a făcut ca integrarea continua sa devină o realitate chiar și pentru proiecte mici.
Travis CI este un serviciu găzduit de integrare continuă pentru comunitatea open source.
Este integrat cu GitHub și oferă suport de prima mână pentru multe limbaje inclusiv PHP.
 
Lecturi aprofundate:
 
* [Integrare continua cu Jenkins](http://jenkins-ci.org/)
* [Integrare continua cu PHPCI](http://www.phptesting.org/)
* [Integrare continua cu Teamcity](http://www.jetbrains.com/teamcity/)
 
