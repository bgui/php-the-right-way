---
isChild: true
---

## Vagrant {#vagrant_title}

Rularea aplicatiei tale pe diferite medii in dezvoltare si productie poate duce catre aparitia unor bug-uri neobisnuite 
atunci cand are loc lansarea aplicatiei. De asemenea este dificil sa pastrezi actualizate la zi diferite medii de 
dezvoltare cu aceleasi versiuni ale tuturor bibliotecilor folosite atunci cand se lucreaza cu o echipa de dezvoltatori.

Daca dezvolti pe Windows si lansezi pe Linux (sau orice non-Windows) sau dezvolti in echipa ar trebui sa iei in calcul
 folosirea unei masini virtuale. Suna complicat, dar folosind [Vagrant][vagrant] poti construi o masina virtuala simpla
 cu numai cativa pasi. Aceste masini de baza pot fi configurate manual sau poti folosi "provisioning"-software cum sunt
 [Puppet][puppet] sau [Chef][chef] care sa faca asta pentru tine.
Initializarea masinii de baza e o metoda buna de a asigura ca mai multe masini sunt setate intr-o maniera identica si
 elimina nevoia de a avea liste cu comenzi de configurare. De asemenea iti poti distruge masina de baza si o poti
 recrea fara prea multi pasi manuali fiind astfel usor de a crea o instalare proaspata.

Vagrant creeaza directoare comune folosite pentru a pastra in comun codul tau intre gazda si masina virtuala, insemnand
 ca poti crea si edita fisiere pe masina gazda si apoi poti rula codul inauntru masinii virtuale.

### Un pic de ajutor

Daca ai nevoie de putin ajutor pentru a incepe sa folosesti Vagrant exista trei servicii ce ar putea fi utile:

- [Rove][rove]: serviciu care permite sa iti pregenerezi configuratii Vagrant tipice, PHP numarandu-se printre optiuni.
 Initializarea este facuta cu Chef.
- [Puphpet][puphpet]: GUI simplu pentru a seta masini virtuale pentru dezvoltare PHP. **Foarte concentrat pe PHP**.
 In afara masinilor virtuale locale, poate fi folosit si pentru a plasa la servicii cloud. Initializarea e facuta cu Puppet.
- [Protobox][protobox]: este un nivel deasupra lui vagrant si un GUI web pentru a seta masini virtuale pentru dezvoltare
 web. Un singur document YAML controleaza tot ce e instalat pe masina virtuala.

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/
[protobox]: http://getprotobox.com/
