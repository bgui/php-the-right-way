---
isChild: true
---

## Constructia si lansarea aplicatiei tale {#build_title}

Daca te surprinzi modificand schema bazei de date manual sau ruland testele manual inaintea actualizarii
fisierelor tale(manual), mai gandeste-te! Cu fiecare task manual aditional necesar pentru lansarea unei noi
versiuni a aplicatiei tale, sansa unor greseli fatale creste. Daca ai de-a face cu un simplu update,
un proces de constructie complicat sau chiar o strategie de integrare continua, [automatizarea constructiei]
(http://en.wikipedia.org/wiki/Build_automation) este prietena ta.

Printre pasii pe care ai putea dori sa ii automatizezi s-ar putea numara:

* Managementul dependintelor
* Compilare, minificatia resurselor tale
* Executia de teste
* Crearea de documentatie
* Impachetare
* Lansare (deployment)


### Unelte de automatizare a constructiei

Unele pentru constructia aplicatiei pot fi descrise ca o colectie de scripturi care executa instructiuni des
intalnite in dezvoltarea de software. Unealta de constructie nu este parte a software-ului tau, ea actioneaza
asupta soft-ului tau din 'afara'.

Exista multe unelte open source disponibile care te pot ajuta cu automatizarea constructiei, unele sunt scrise in PHP
iar altele nu. Asta nu ar trebui sa te descurajeze din a le folosi, daca sunt mai bine potrivite pentru
jobul respectiv. Aici sunt cateva exemple:

[Phing](http://www.phing.info/) este cea mai usoara cale de a incepe lansare automata in lumea PHP. Cu
Phing tu iti controla impachetarea, transportul sau procesul de testare dintr-un simplu fisier XML. Phing (care e
bazat pe [Apache Ant](http://ant.apache.org/)) pune la dispozitie un bogat set de instructiuni de obicei
necesare pentru actualizarea sau instalarea unei aplicatii web si poate fi extins cu instructiuni
personalizate aditionale, scrise in PHP.

[Capistrano](https://github.com/capistrano/capistrano/wiki) este un sistem pentru *programatori intermediari-spre-avansati*
pentru a executa comenzi, intr-o maniera structurata si repetabila pe una sau mai multe masini externe.
Este pre-configurat pentru lansarea de aplicatii Ruby on Rails, dar totusi se pot lansa cu succes
si sisteme PHP cu el. Uzul cu succes al Capistrano depinde de cunostinte in Ruby si Rake.

Blogpost-ul lui Dave Gardner [Lansare PHP cu Capistrano](http://www.davegardner.me.uk/blog/2012/02/13/php-deployment-with-capistrano/)
este un bun punct de plecare pentru dezvoltatorii PHP interesati de Capistrano.

[Chef](http://www.opscode.com/chef/) este mai mult decat un framework de lansare a codului, este un puternic system
de integrare bazat pe Ruby care nu numai iti transporta aplicatia dar iti poate construi intregul server sau masini virtuale.

Resurse Chef pentru programatori PHP:

* [O serie de articole in trei parti despre lansarea unei aplicatii LAMP cu Chef, Vagrant, si EC2](http://www.jasongrimes.org/2012/06/managing-lamp-environments-with-chef-vagrant-and-ec2-1-of-3/)
* [Carte cu retete Chef care instaleaza si configureaza PHP 5.3 si sistemul de pachete PEAR](https://github.com/opscode-cookbooks/php)

Lecturi aprofundate:

* [Automatizeaza-ti proiectul cu Apache Ant](http://net.tutsplus.com/tutorials/other/automate-your-projects-with-apache-ant/)
* [Maven](http://maven.apache.org/), un framework pentru automatizarea constructiei (build) bazat pe Ant si
[cum sa-l folosesti cu PHP](http://www.php-maven.org/)

### Integrare continua

> Integrarea continua este o practica a dezvoltarii software unde membrii unei echipeisi integreaza munca frecvent,
> de obicei fiecare persoana integreaza cel putin zilnic — ducand la mai multe integrari pe zi. Multe echipe gasesc
> ca aceasta abordare duce la un numar semnificativ mai mic de probleme de integrare si permite unei echipe sa
> dezvolte software consistent mai rapid.


*-- Martin Fowler*


Exista diferite metode de a implementa integrare continua pentru PHP. Recent [Travis CI](https://travis-ci.org/) a facut ca integrarea continua sa devina o realitate chiar si pentru proiecte mici.
Travis CI este un serviciu gazduit de integrare continua pentru comunitatea open source.
Este integrat cu GitHub si ofera suport de prima mana pentru multe limbaje inclusiv PHP.

Lecturi aprofundate:

* [Integrare continua cu Jenkins](http://jenkins-ci.org/)
* [Integrare continua cu PHPCI](http://www.phptesting.org/)
* [Integrare continua cu Teamcity](http://www.jetbrains.com/teamcity/)
