---
isChild: true
---

## Vagrant {#vagrant_title}

Rularea aplicației tale pe diferite medii în dezvoltare și producție poate duce către apariția unor bug-uri neobișnuite 
atunci când are loc lansarea aplicației. De asemenea este dificil sa păstrezi actualizate la zi diferite medii de 
dezvoltare cu aceleași versiuni ale tuturor bibliotecilor folosite atunci când se lucrează cu o echipa de dezvoltatori.

Dacă dezvolți pe Windows și lansezi pe Linux (sau orice non-Windows) sau dezvolți în echipa ar trebui sa iei în calcul
 folosirea unei mașini virtuale. Suna complicat, dar folosind [Vagrant][vagrant] poți construi o mașina virtuala simpla
 cu numai câțiva pași. Aceste mașini de baza pot fi configurate manual sau poți folosi "provisioning"-software cum sunt
 [Puppet][puppet] sau [Chef][chef] care sa facă asta pentru tine.
Inițializarea mașinii de baza e o metoda buna de a asigura ca mai multe mașini sunt setate într-o maniera identica și
 elimina nevoia de a avea liste cu comenzi de configurare. De asemenea iți poți distruge mașina de baza și o poți
 recrea fără prea multi pași manuali fiind astfel ușor de a crea o instalare proaspăta.

Vagrant creează directoare comune folosite pentru a păstra în comun codul tău intre gazda și mașina virtuala, însemnând
 ca poți crea și edita fișiere pe mașina gazda și apoi poți rula codul înauntru mașinii virtuale.

### Un pic de ajutor

Dacă ai nevoie de puțin ajutor pentru a începe sa folosești Vagrant exista trei servicii ce ar putea fi utile:

- [Rove][rove]: serviciu care permite sa iți pregenerezi configurații Vagrant tipice, PHP numărându-se printre opțiuni.
 Inițializarea este făcuta cu Chef.
- [Puphpet][puphpet]: GUI simplu pentru a seta mașini virtuale pentru dezvoltare PHP. **Foarte concentrat pe PHP**.
 În afara mașinilor virtuale locale, poate fi folosit și pentru a plasa la servicii cloud. Inițializarea e făcută cu Puppet.
- [Protobox][protobox]: este un nivel deasupra lui vagrant și un GUI web pentru a seta mașini virtuale pentru dezvoltare
 web. Un singur document YAML controlează tot ce e instalat pe mașina virtuala.

[vagrant]: http://vagrantup.com/
[puppet]: http://www.puppetlabs.com/
[chef]: http://www.opscode.com/
[rove]: http://rove.io/
[puphpet]: https://puphpet.com/
[protobox]: http://getprotobox.com/