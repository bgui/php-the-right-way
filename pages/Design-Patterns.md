---
layout: page
title: Șabloane de proiectare
---

# Șabloane de proiectare

There are numerous ways to structure the code and project for you web application, and you can put as much or as little
thought as you like into architecting. But it is usually a good idea to follow common patterns because it will make
your code easier to manage and easier for others to understand.
Exista numeroase moduri in care iti poti structura codul si proiectul aplicatiei tale, si poti
investi cat de mult sau cat te putin efort vrei in arhitectura sa. De obicei e o idee buna
sa adopti sabloane populare pentru ca va fi mai usor sa iti administrezi codul si
va fi mai usor pentru ceilalti sa il inteleaga.


* [Șablon de arhitectura pe Wikipedia](https://en.wikipedia.org/wiki/Architectural_pattern)
* [Șabloane de proiectare Software pe Wikipedia](https://en.wikipedia.org/wiki/Software_design_pattern)

## Factory

Unul dintre cele mai utilizate sabloane de proiectare este cel denumit Factory (fabrica).
In acest sablon, o clasa pur si simplu creeaza obiectul pe care vrei sa il folosesti.
Urmatorul exemplu ilustreaza sablonul:

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

// fabrica va creea obiectul Automobil
$veyron = AutomobileFactory::create('Bugatti', 'Veyron');

print_r($veyron->get_make_and_model()); // afiseaza "Bugatti Veyron"
{% endhighlight %}

Acest cod foloseste o fabrica pentru a creea un obiect automobil. Exista doua posibile beneficii
pentru a construi cod in acest fel; primul este ca daca ai nevoie sa schimbi, sa redenumesti, sau sa inlocuiesti
clasa Automobil mai tarziu, o poti face si nu va trebui decat sa modifici codul din fabrica, in loc de a o face
in fiecare loc din proiect in care e folosita clasa Automobil. Al doilea posibil avantaj este ca daca e
dificil sa construiesti obiectul atunci poti face toata munca in fabrica, in loc de a repeta de fiecare data
cand vrei sa creezi o instanta noua.

Apelul la sablonul fabrica nu este totdeauna necesar (sau intelept). Acest exemplu a fost atat de simplu incat
e posibil ca sablonul sa adauge complexitate inutila. Totusi, daca ai un proiect mare si complex, te poti scuti
de multe probleme mai tarziu folosind fabrici.


* [Șablonul fabrica pe Wikipedia](https://en.wikipedia.org/wiki/Factory_pattern)

## Singleton

Cand construiesti aplicatii web, are deseori sens din punct de vedere conceptual si arhitectural sa permiti
existenta a unei singure si numai unei singure instante a unei anumite clase. Sablonul singleton ne permite
sa facem acest lucru.

{% highlight php %}
<?php
class Singleton
{
    /**
     * Returneaza instanta *Singleton* a acestei clase
     *
     * @staticvar Singleton $instance Instanta *Singleton* a acestei clase.
     *
     * @return Singleton Instanta *Singleton*.
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
     * Constructor privat pentru a preveni crearea unei noi instante prin operatorul `new` din afara acestei clase.
     */
    protected function __construct()
    {
    }

    /**
     * Metoda privata de clonare pentru a preveni clonarea instantei *Singleton*.
     *
     * @return void
     */
    private function __clone()
    {
    }

    /**
     * Metoda privata de deserializare pentru a preveni deserializarea instaintei *Singleton*.
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

Codul de mai sus implementeaza sablonul singleton folosind o variabila [*statica*](http://php.net/language.variables.scope#language.variables.scope.static) si metoda statica de creare `getInstance()`.
Notam urmatoarele:

* Constructorul [`__construct`](http://php.net/language.oop5.decon#object.construct) este declarat ca protected pentru a preveni
crearea unei noi instante a clasei via operatorului `new`.
* Metoda magica [`__clone`](http://php.net/language.oop5.cloning#object.clone) este declarata privata pentru apreveni clonarea unei
instante a clasei via operatorul [`clone`](http://php.net/language.oop5.cloning).
* Metoda magica [`__wakeup`](http://php.net/language.oop5.magic#object.wakeup) este declarata privata pentru a preveni deserializarea
unei instante a clasei via functiei globale [`unserialize()`](http://php.net/function.unserialize).
* O noua instanta este creata via [late static binding](http://php.net/language.oop5.late-static-bindings) in
metoda statica de creare `getInstance()` cu cuvantul cheie `static`. Asta permite subclasarea clasei `Singleton` din exemplu.


Șablonul singleton este util atunci cand avem nevoie sa fim siguri ca avem o singura instanta a clasei pentru
intregul ciclu de viata a aplicatiei noastre web. Aceasta se intampla de obicei pentru obiectele globale
(precum clase de Configurare) sau resurse comune (ca o stiva de evenimente)..

Ar trebui sa fii precaut cand folosesti sablonul singleton, prin natura sa acesta introduce o stare globala
in aplicatia ta, reducand astfel testabilitatea. In majoritatea cazurilor, injectarea dependintelor poate
(si ar trebui) fi folosita in locul unei clase singleton. Folosind injectarea dependintelor inseamna ca nu
introducem cuplari nenecesare in arhitectura aplicatiei noastre, intrucat obiectul ce foloseste resursa
globala sau comuna nu necesita cunostinte despre o clasa definita concret.



* [Șablonul singleton pe Wikipedia](https://en.wikipedia.org/wiki/Singleton_pattern)

## Strategie

Cu sablonul Strategie incapsulezi familii specifice de algoritmi permitant clasei client responsabila de
instantierea unui algoritm particular sa nu aiba cunostinte despre implementarea efectiva.
Exista cateva variatii pe tema sablonului strategie, cea mai simpla dintre ele este expusa dedesubt:

Prima sectiune de cod ilustreaza o familie de algoritmi; ai putea dori un array serializat, ceva JSON
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

Incapsuland algoritmii de mai sus faci in codul tau foarte clar ca alti programatori pot foarte usor adauga
noi tipuri de iesiri fara sa afecteze codul client.

Vei vedea cum fiecare clasa 'output' concreta implementeaza o OutputInterface - iar asta e pentru doua scopuri,
primul este ca astfel se prevede un contract simplu care trebuie respectat de catre orice noua implementare concreta,
iar secund vei vedea in sectiunea urmatoare ca de acum poti utiliza [Type Hinting](http://php.net/manual/en/language.oop5.typehinting.php)
pentru a asigura ca clientul care utilizeaza aceste comportamente este de tipul corect in acest caz 'OutputInterface'.

Urmatorul extras de cod subliniaza cum o clasa client apelanta ar putea folosi unul dintre acesti algoritmi, si,
chiar si mai bine, ar putea hotari comportamentul necesar la timpul rularii:
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

Clasa client apelanta de mai sus are o proprietate privata care trebuie setata la timpul rularii si care trebuie
sa fie de tip 'OutputInterface' odata ce aceasta proprietate e setata o apelare loadOutput() va executa metoda load() din
clasa concreta a tipului de output care a fost setat.
{% highlight php %}
<?php

$client = new SomeClient();

// Vrei un array?
$client->setOutput(new ArrayOutput());
$data = $client->loadOutput();

// Vrei niste JSON?
$client->setOutput(new JsonStringOutput());
$data = $client->loadOutput();

{% endhighlight %}

* [Sablonul strategie pe Wikipedia](http://en.wikipedia.org/wiki/Strategy_pattern)

## Front Controller

Sablonul front controller este acolo unde ai un singur punct de intrare in aplicatia ta web (e.g. index.php)
care se ocupa de toate interogarile. Acest cod este responsabil de incarcarea tuturor dependintelor, de
procesarea interogarii si de trimiterea raspunsului catre browser. Sablonul front controller poate fi benefic
pentru ca incurajeaza cod modular si iti furnizeaza un loc central in care sa poti insera cod care sa fie
rulat pentru fiecare interogare (precum sanitizarea datelor de intrare).

* [Șablonul Front Controller pe Wikipedia](https://en.wikipedia.org/wiki/Front_Controller_pattern)

## Model-View-Controller


Șablonul model-view-controller (MVC) si rudele sale HMVC si MVVM iti permit sa spargi codul in obiecte logice care
servers unor scopuri foarte exacte. Modelele servesc ca nivel de acces de date unde datele sunt recuperate in formaturi
utilizabile prin toata aplicatia. Controller-ele se ocupa de interogare, proceseaza datele returnate de la
modele si incarca view-urile pentru a trimite raspunsul. View-urile sunt template-uri (sabloane de afisare) in html, xml,
etc care sunt trimise in raspuns catre browserul web.

MVC este cel mai comun sablon de proiectare arhitecturala folosit in [framework-urile PHP populare](https://github.com/codeguy/php-the-right-way/wiki/Frameworks).
Afla mai multe despre MVC si rudele sale:

* [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93View%E2%80%93Controller)
* [HMVC](https://en.wikipedia.org/wiki/Hierarchical_model%E2%80%93view%E2%80%93controller)
* [MVVM](https://en.wikipedia.org/wiki/Model_View_ViewModel)
