---
layout: page
title: Șabloane de proiectare
---

# Șabloane de proiectare

Există numeroase moduri în care iți poți structura codul și proiectul aplicației tale, și poți
investi cât de mult sau cât de puțin efort vrei în arhitectura sa. De obicei e o idee bună
să adopți șabloane populare pentru că va fi mai ușor să iți administrezi codul și
va fi mai ușor pentru ceilalți să îl înțeleagă.


* [Șablon de arhitectură pe Wikipedia](https://en.wikipedia.org/wiki/Architectural_pattern)
* [Șabloane de proiectare software pe Wikipedia](https://en.wikipedia.org/wiki/Software_design_pattern)

## Factory

Unul dintre cele mai utilizate șabloane de proiectare este cel denumit Factory (fabrică).
În acest șablon, o clasă pur și simplu creează obiectul pe care vrei să îl folosești.
Următorul exemplu ilustrează șablonul:

{% highlight php %}
<?php
class Automobile
{
    private $vehicle_make;
    private $vehicle_model;

    public function __construct($make, $model)
    {
        $this->vehicle_make = $make;
        $this->vehicle_model = $model;
    }

    public function get_make_and_model()
    {
        return $this->vehicle_make . ' ' . $this->vehicle_model;
    }
}

class AutomobileFactory
{
    public static function create($make, $model)
    {
        return new Automobile($make, $model);
    }
}

// fabrica va crea obiectul Automobil
$veyron = AutomobileFactory::create('Bugatti', 'Veyron');

print_r($veyron->get_make_and_model()); // afișează "Bugatti Veyron"
{% endhighlight %}

Acest cod folosește o fabrică pentru a crea un obiect automobil. Există două posibile beneficii
pentru a construi cod în acest fel; primul este că dacă ai nevoie să schimbi, să redenumești, sau să înlocuiești
clasa Automobil mai târziu, o poți face și nu va trebui decât să modifici codul din fabrică, în loc de a o face
în fiecare loc din proiect în care e folosită clasa Automobil. Al doilea posibil avantaj este că dacă e
dificil să construiești obiectul atunci poți face toată munca în fabrică, în loc de a repeta de fiecare dată
când vrei să creezi o instanță nouă.

Apelul la șablonul fabrică nu este totdeauna necesar (sau înțelept). Acest exemplu a fost atât de simplu încât
e posibil că șablonul să adauge complexitate inutilă. Totuși, dacă ai un proiect mare și complex, te poți scuti
de multe probleme mai târziu folosind fabrici.


* [Șablonul fabrică pe Wikipedia](https://en.wikipedia.org/wiki/Factory_pattern)

## Singleton

Când construiești aplicații web, are deseori sens din punct de vedere conceptual și arhitectural să permiți
existența a unei singure și numai unei singure instanțe a unei anumite clase. Șablonul singleton ne permite
să facem acest lucru.

{% highlight php %}
<?php
class Singleton
{
    /**
     * Returnează instanța *Singleton* a acestei clase
     *
     * @staticvar Singleton $instance Instanța *Singleton* a acestei clase.
     *
     * @return Singleton Instanța *Singleton*.
     */
    public static function getInstance()
    {
        static $instance = null;
        if (null === $instance) {
            $instance = new static();
        }

        return $instance;
    }

    /**
     * Constructor privat pentru a preveni crearea unei noi instanțe prin operatorul `new` din afara acestei clase.
     */
    protected function __construct()
    {
    }

    /**
     * Metoda privata de clonare pentru a preveni clonarea instanței *Singleton*.
     *
     * @return void
     */
    private function __clone()
    {
    }

    /**
     * Metoda privata de deserializare pentru a preveni deserializarea instanței *Singleton*.
     *
     * @return void
     */
    private function __wakeup()
    {
    }
}

class SingletonChild extends Singleton
{
}

$obj = Singleton::getInstance();
var_dump($obj === Singleton::getInstance());             // bool(true)

$anotherObj = SingletonChild::getInstance();
var_dump($anotherObj === Singleton::getInstance());      // bool(false)

var_dump($anotherObj === SingletonChild::getInstance()); // bool(true)
{% endhighlight %}

Codul de mai sus implementează șablonul singleton folosind o variabilă [*statică*](http://php.net/language.variables.scope#language.variables.scope.static) și metoda statică de creare `getInstance()`.
Notăm următoarele:

* Constructorul [`__construct`](http://php.net/language.oop5.decon#object.construct) este declarat ca protected pentru a preveni
crearea unei noi instanțe a clasei via operatorului `new`.
* Metoda magica [`__clone`](http://php.net/language.oop5.cloning#object.clone) este declarată privată pentru preveni clonarea unei
instanțe a clasei via operatorul [`clone`](http://php.net/language.oop5.cloning).
* Metoda magica [`__wakeup`](http://php.net/language.oop5.magic#object.wakeup) este declarată privată pentru a preveni deserializarea
unei instanțe a clasei via funcției globale [`unserialize()`](http://php.net/function.unserialize).
* O nouă instanță este creată via [late static binding](http://php.net/language.oop5.late-static-bindings) în
metoda statică de creare `getInstance()` cu cuvântul cheie `static`. Asta permite subclasarea clasei `Singleton` din exemplu.


Șablonul singleton este util atunci când avem nevoie să fim siguri că avem o singură instanță a clasei pentru
întregul ciclu de viată a aplicației noastre web. Aceasta se întâmplă de obicei pentru obiectele globale
(precum clase de Configurare) sau resurse comune (că o stivă de evenimente).

Ar trebui să fii precaut când folosești șablonul singleton, prin natura să acesta introduce o stare globală
în aplicația ta, reducând astfel testabilitatea. În majoritatea cazurilor, injectarea dependințelor poate
(și ar trebui) fi folosită în locul unei clase singleton. Folosind injectarea dependințelor înseamnă că nu
introducem cuplări nenecesare în arhitectura aplicației noastre, întrucât obiectul ce folosește resursa
globala sau comuna nu necesită cunoștințe despre o clasă definită concret.

* [Șablonul singleton pe Wikipedia](https://en.wikipedia.org/wiki/Singleton_pattern)

## Strategie

Cu șablonul Strategie încapsulezi familii specifice de algoritmi permițând clasei client responsabilă de
instanțierea unui algoritm particular să nu aibă cunoștințe despre implementarea efectivă.
Exista câteva variații pe tema șablonului strategie, cea mai simplă dintre ele este expusă dedesubt:

Prima secțiune de cod ilustrează o familie de algoritmi; ai putea dori un array serializat, ceva JSON
sau poate doar un array de date:
{% highlight php %}
<?php

interface OutputInterface
{
    public function load();
}

class SerializedArrayOutput implements OutputInterface
{
    public function load()
    {
        return serialize($arrayOfData);
    }
}

class JsonStringOutput implements OutputInterface
{
    public function load()
    {
        return json_encode($arrayOfData);
    }
}

class ArrayOutput implements OutputInterface
{
    public function load()
    {
        return $arrayOfData;
    }
}
{% endhighlight %}

Încapsulând algoritmii de mai sus faci în codul tău foarte clar că alți programatori pot foarte ușor adăuga noi tipuri de ieșiri fără să afecteze codul client.

Vei vedea cum fiecare clasă 'output' concretă implementează o OutputInterface - iar asta e pentru doua scopuri,
primul este că astfel se prevede un contract simplu care trebuie respectat de către orice noua implementare concreta,
iar secund vei vedea în secțiunea următoare că de acum poți utiliza [Type Hinting](http://php.net/manual/en/language.oop5.typehinting.php)
pentru a asigura că clientul care utilizează aceste comportamente este de tipul corect în acest caz 'OutputInterface'.

Următorul extras de cod subliniază cum o clasă client apelantă ar putea folosi unul dintre acești algoritmi, și,
chiar și mai bine, ar putea hotărî comportamentul necesar la timpul rulării:
{% highlight php %}
<?php

class SomeClient
{
    private $output;

    public function setOutput(OutputInterface $outputType)
    {
        $this->output = $outputType;
    }

    public function loadOutput()
    {
        return $this->output->load();
    }
}
{% endhighlight %}

Clasa client apelantă de mai sus are o proprietate privată care trebuie setată la timpul rulării și care trebuie
să fie de tip 'OutputInterface' odată ce aceasta proprietate e setata o apelare loadOutput() va executa metoda load() din
clasa concreta a tipului de output care a fost setat.
{% highlight php %}
<?php

$client = new SomeClient();

// Vrei un array?
$client->setOutput(new ArrayOutput());
$data = $client->loadOutput();

// Vrei niște JSON?
$client->setOutput(new JsonStringOutput());
$data = $client->loadOutput();

{% endhighlight %}

* [Șablonul strategie pe Wikipedia](http://en.wikipedia.org/wiki/Strategy_pattern)

## Front Controller

Șablonul front controller este acolo unde ai un singur punct de intrare în aplicația ta web (e.g. index.php)
care se ocupă de toate interogările. Acest cod este responsabil de încărcarea tuturor dependințelor, de
procesarea interogării și de trimiterea răspunsului către browser. Șablonul front controller poate fi benefic
pentru că încurajează cod modular și iți furnizează un loc central în care să poți insera cod care să fie
rulat pentru fiecare interogare (precum sanitizarea datelor de intrare).

* [Șablonul Front Controller pe Wikipedia](https://en.wikipedia.org/wiki/Front_Controller_pattern)

## Model-View-Controller


Șablonul model-view-controller (MVC) și rudele sale HMVC și MVVM îți permit să spargi codul în obiecte logice care
servesc unor scopuri foarte exacte. Modelele servesc ca nivel de acces de date unde datele sunt recuperate în format-uri
utilizabile prin toată aplicația. Controller-ele se ocupă de interogare, procesează datele returnate de la
modele și încarcă view-urile pentru a trimite răspunsul. View-urile sunt template-uri (șabloane de afișare) în html, xml,
etc care sunt trimise în răspuns către browserul web.

MVC este cel mai comun șablon de proiectare arhitecturală folosit în [framework-urile PHP populare](https://github.com/codeguy/php-the-right-way/wiki/Frameworks).
Află mai multe despre MVC și rudele sale:

* [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)

