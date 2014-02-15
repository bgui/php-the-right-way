---
layout: page
title: Bazele
---

# Bazele

## Operatori de comparatie

Operatorii de comparatie sunt un aspect deseori trecut cu vederea in PHP, lucru care poate
duce la situatii neprevazute. O asemenea problema izvoraste din comparatii stricte
(comparatia booleana sau a integer-ilor).

{% highlight php %}
<?php
$a = 5;   // 5 ca un integer

var_dump($a == 5);       // compara valoarea; return true
var_dump($a == '5');     // compara valoarea (ignore type); return true
var_dump($a === 5);      // compara tip/valoare (integer vs. integer); return true
var_dump($a === '5');    // compara tip/valoare (integer vs. string); return false

/**
 * Comparatii stricte
 */
if (strpos('testing', 'test')) {    // 'test' este gasit la pozitia 0, care e interpretat ca bool-eanul 'false'
    // code...
}

vs.

if (strpos('testing', 'test') !== false) {    // true, intrucat o comparatie stricta a fost facuta (0 !== false)
    // code...
}
{% endhighlight %}

* [Operatori de comparatie](http://php.net/manual/en/language.operators.comparison.php)
* [Tabel de comparatie](http://php.net/manual/en/types.comparisons.php)

## Instructiuni conditionale

### Instructiuni If

Cand folosesti instructiuni 'if/else' intr-o functie sau clasa, exista conceptia gresita
ca si 'else' trebuie folosit pentru a declara rezultate potentiale. Totusi daca rezultatul
este de a defini valoarea de return, 'else' nu e necesar intrucat return va intrerupe functia,
cauzand 'else' sa devina superflua.

{% highlight php %}
<?php
function test($a)
{
    if ($a) {
        return true;
    } else {
        return false;
    }
}

vs.

function test($a)
{
    if ($a) {
        return true;
    }
    return false;    // else nu e necesar
}
{% endhighlight %}

* [Instructiuni if](http://php.net/manual/en/control-structures.if.php)

### Instructiuni switch

Instructiunile switch sunt o buna metoda de a evita sa tastezi if-uri si elseif-uri la nesfarsit,
dar cu cateva conditii de retinut:
- Instructiunile switch compara numai valori, si nu tipul (echivalentul lui '==')
- Ele itereaza caz dupa caz pana o potrivire este gasita. Daca nici o potrivire nu e
gasita, atunci default-ul este folosit (daca e definit)
- Fara un 'break', vor continua sa implementeze fiecare caz pana ating un break/return
- Intr-o functie, folosirea lui 'return' suplineste nevoia de a folosi 'break' intrucat termina functia

{% highlight php %}
<?php
$answer = test(2);    // codul de la 'cazul 2' si 'cazul 3' va fi implementat

function test($a)
{
    switch ($a) {
        case 1:
            // code...
            break;             // break este folosit pentru a sfarsi instructiunea switch
        case 2:
            // code...         // fara break comparatia va continua spre 'cazul 3'
        case 3:
            // code...
            return $result;    // intr-o functie, 'return' va sfarsi functia
        default:
            // code...
            return $error;
    }
}
{% endhighlight %}

* [Instructiuni Switch](http://php.net/manual/en/control-structures.switch.php)
* [PHP switch](http://phpswitch.com/)

## Namespace-ul global

Cand folosesti namespace-uri(spatii de nume), poti descoperi ca functii interne au fost ascunse
de functii scrise de tine. Pentru a repara asta te poti referi la functia globala folosind
un backslash inainte de numele functiei.

{% highlight php %}
<?php
namespace phptherightway;

function fopen()
{
    $file = \fopen();    // Numele functiei noastre este identic cu cel al unei functii interne.
                         // Executa functia din spatiul global prin adaugarea lui '\'.
}

function array()
{
    $iterator = new \ArrayIterator();    // ArrayIterator este o clasa interna.
                                         // Folosirea numelui sau fara un backslash
                                         // va incerca sa il rezolve in namespace-ul tau.
}
{% endhighlight %}

* [Spatiul global](http://php.net/manual/en/language.namespaces.global.php)
* [Reguli lobale](http://php.net/manual/en/userlandnaming.rules.php)

## String-uri

### Concatenatie

- Daca linia ta se extinde dincolo de lungimea recomandata(120 de caractere). considera concatenarea ei.
- Pentru o citire mai usoara este bine sa folosesti operatorii de concatenare si nu operatorii de asignare concatenare
- Pe cand esti inauntrul scope-ului original al variabilei, ident-eaza atunci cand concatenarea
foloseste un nou rand

{% highlight php %}
<?php
$a  = 'Multi-line example';    // operator de asignare concatenare (.=)
$a .= "\n";
$a .= 'of what not to do';

vs.

$a = 'Multi-line example'      // operator de concatenare (.)
    . "\n"                     // indentarea noilor randuri
    . 'of what to do';
{% endhighlight %}

* [Operatori string-uri](http://php.net/manual/en/language.operators.string.php)

### Tipuri de stringuri

Tipurile de stringuri sunt o functionalitate constanta in comunitatea PHP, dar speram ca aceasta sectiune
va explica diferentele dintre tipurile de stringuri si beneficiile/utilizarile lor.

#### Ghilimele simple

Ghilimelele simple sunt cea mai simpla cale de a defini un string si deseori cea mai rapida.
Viteza lor porneste din faptul ca PHP nu parseaza string-ul (nu parseaza dupa variabile).
Sunt cele potrivite pentru:

- String-uri care nu vor fi parsate
- Scrierea unei variabile in text obisnuit

{% highlight php %}
<?php
echo 'Acesta este string-ul meu, priveste ce frumos este el.';    // nu e nevoie sa fie parsat un simplu string

/**
 * Rezultat:
 *
 * Acesta este string-ul meu, priveste ce frumos este el.
 */
{% endhighlight %}

* [Ghilimele simple](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.single)

#### Ghilimele duble

Double quotes are the Swiss army knife of strings, but are slower due to the string being parsed. They're best
suited for:
Ghilimelele duble sunt briceagul string-urilor, dar sunt mai lente datorita faptului ca string-ul este
parsat. Sunt cele mai potrivite pentru:

- String-uri escape-uite
- Stringuri cu variabile multiple si text simplu
- Condensarea concatenatiei de multe randuri, si imbunatatirea lizibilitatii

{% highlight php %}
<?php
echo 'phptherightway is ' . $adjective . '.'     // un exemplu cu ghilimele simple care foloseste concatenare
    . "\n"                                       // multipla pentru variabile si string-uri escape-ate
    . 'I love learning' . $code . '!';

vs.

echo "phptherightway is $adjective.\n I love learning $code!"  // In loc de concatenare multipla, ghilimelele
                                                               // duble ne permit sa folosim un string parsabil
{% endhighlight %}

Cand folosim ghilimele duble care contin variabile, deseori se poate intampla ca variabila sa atinga
alt caracter. Asta va rezulta in incapacitatea PHP de a parsa variabila intrucat e camuflata. Pentru
a repara aceasta problema, infasoara variabila cu o pereche de acolade.

{% highlight php %}
<?php
$juice = 'plum';
echo "I drank some juice made of $juices";    // $juice nu poate fi parsat

vs.

$juice = 'plum';
echo "I drank some juice made of {$juice}s";    // $juice va fi parsat

/**
 * Variabile complexe vor si si ele parsate in acolade
 */

$juice = array('apple', 'orange', 'plum');
echo "I drank some juice made of {$juice[1]}s";   // $juice[1] va fi parsat
{% endhighlight %}

* [Ghilimele duble](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.double)

#### Sintaxa Nowdoc

Sintaxa Nowdoc a fost introdusa in 5.3 si intern se comporta la fel ca si ghilimelele simple cu
exceptia ca este menit pentru string-urile multi-rand fara nevoia de a concatena.

{% highlight php %}
<?php
$str = <<<'EOD'             // initializat de <<<
Exemplu de string ce se
intinde pe mai multe randuri
folosind sintaxa nowdoc.
$a nu este parsat.
EOD;                        // 'EOD' de inchidere trebuie sa fie pe propriul rand, si in cel mai stang punct posibil

/**
 * Rezultat:
 *
 * Exemplu de string ce se
 * intinde pe mai multe randuri
 * folosind sintaxa nowdoc.
 * $a nu este parsat.
 */
{% endhighlight %}

* [Sintaxa Nowdoc](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.nowdoc)

#### Sintaxa Heredoc

Sintaxa Heredoc se comporta intern ca si ghilimelele duble cu exceptia ca este menit pentru uzul
string-urilor de mai multe randuri fara sa fie nevoie de concatenare.

{% highlight php %}
<?php
$a = 'Variabilele';

$str = <<<EOD               // initializat de <<<
Exemplu de string ce se
intinde pe mai multe randuri
folosind sintaxa heredoc.
$a sunt parsate.
EOD;                        // 'EOD' de inchidere trebuie sa fie pe propriul rand, si in cel mai stang punct posibil

/**
 * Rezultat:
 *
 * Exemplu de string ce se
 * intinde pe mai multe randuri
 * folosind sintaxa heredoc.
 * Variabilele sunt parsate.
 */
{% endhighlight %}

* [Sintaxa Heredoc](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.heredoc)

## Operatori ternari

Operatorii ternari sunt o buna cale de a condensa cod, dar deseori sunt folosit in exces.
Desi operatorii ternari pot fi stivuiti/cuibariti, este recomandat sa fie folositi unul
pe rand pentru lizibilitate.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? 'yay' : 'nay';

vs.

// ternar stivuit
$b = 10;
echo ($a) ? ($a == 5) ? 'yay' : 'nay' : ($b == 10) ? 'excessive' : ':(';    // stivuire in exces, sacrifica lizibilitatea
{% endhighlight %}

Pentru a returna o valoare cu operatori ternari foloseste sintaxa corecta.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? return true : return false;    // acest exemplu va produce o eroare

vs.

$a = 5;
return ($a == 5) ? 'yay' : 'nope';    // acest exemplu va returna 'yay'
{% endhighlight %}

* [Operatori ternari](http://php.net/manual/en/language.operators.comparison.php)

## Declaratii de variabile

Uneori, programatorii incearca sa isi faca codul "mai clar" declarand variabile predefinite cu un alt nume.
Ceeace face asta in realitate este de a dubla consumul de memorie al respectivului script.
Pentru exemplul de mai jos, sa zicem un string exemplu contine 1MB de date, copiind variabila ai
incrementat executia scriptului la 2MB.

{% highlight php %}
<?php
$about = 'Un foarte lung string de text';    // foloseste 2MB de memorie
echo $about;

vs.

echo 'Un foarte lung string de text';        // foloseste 1MB de memorie
{% endhighlight %}

* [Sfaturi pentru performanta](https://developers.google.com/speed/articles/optimizing-php)
