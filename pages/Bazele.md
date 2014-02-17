---
layout: page
title: Bazele
---

# Bazele

## Operatori de comparație

Operatorii de comparație sunt un aspect deseori trecut cu vederea în PHP, lucru care poate
duce la situații neprevazute. O asemenea problemă izvorăște din comparații stricte
(comparația booleană sau a integer-ilor).

{% highlight php %}
<?php
$a = 5;   // 5 ca integer

var_dump($a == 5);       // compara valoarea; return true
var_dump($a == '5');     // compara valoarea (ignore type); return true
var_dump($a === 5);      // compara tip/valoare (integer vs. integer); return true
var_dump($a === '5');    // compara tip/valoare (integer vs. string); return false

/**
 * Comparații stricte
 */
if (strpos('testing', 'test')) {    // 'test' este găsit la poziția 0, care e interpretat ca booleanul 'false'
    // code...
}

vs.

if (strpos('testing', 'test') !== false) {    // true, întrucât o comparație strictă a fost făcută (0 !== false)
    // code...
}
{% endhighlight %}

* [Operatori de comparație](http://php.net/manual/en/language.operators.comparison.php)
* [Tabel de comparație](http://php.net/manual/en/types.comparisons.php)

## Instrucțiuni conditionale

### Instrucțiuni If

Când folosești instrucțiuni 'if/else' într-o funcție sau clasă, există concepția greșită
că și 'else' trebuie folosit pentru a declara rezultate potențiale. Totuși dacă rezultatul
este de a defini valoarea de return, 'else' nu e necesar întrucât return va întrerupe funcția,
cauzând 'else' să devina superfluă.

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

* [Instrucțiuni if](http://php.net/manual/en/control-structures.if.php)

### Instrucțiuni switch

Instrucțiunile switch sunt o bună metodă de a evita să tastezi if-uri și elseif-uri la nesfârșit,
dar cu câteva condiții de reținut:
- Instrucțiunile switch compară numai valori, și nu tipul (echivalentul lui '==')
- Ele iterează caz după caz pană ce o potrivire este găsită. Dacă nici o potrivire nu e
găsită, atunci default-ul este folosit (dacă e definit)
- Fara un 'break', vor continua să implementeze fiecare caz pana ce ating un break/return
- Într-o funcție, folosirea lui 'return' suplinește nevoia de a folosi 'break' întrucât opreste funcția

{% highlight php %}
<?php
$answer = test(2);    // codul de la 'cazul 2' și 'cazul 3' va fi implementat

function test($a)
{
    switch ($a) {
        case 1:
            // code...
            break;             // break este folosit pentru a sfârși instrucțiunea switch
        case 2:
            // code...         // fără break comparația va continua spre 'cazul 3'
        case 3:
            // code...
            return $result;    // într-o funcție, 'return' va sfârși funcția
        default:
            // code...
            return $error;
    }
}
{% endhighlight %}

* [Instrucțiuni Switch](http://php.net/manual/en/control-structures.switch.php)
* [PHP switch](http://phpswitch.com/)

## Namespace-ul global

Când folosești namespace-uri(spatii de nume), poți descoperi că funcții interne au fost ascunse
de funcții scrise de tine. Pentru a repara asta te poți referi la funcția globală folosind
un backslash înainte de numele funcției.

{% highlight php %}
<?php
namespace phptherightway;

function fopen()
{
    $file = \fopen();    // Numele funcției noastre este identic cu cel al unei funcții interne.
                         // Execută funcția din spațiul global prin adăugarea lui '\'.
}

function array()
{
    $iterator = new \ArrayIterator();    // ArrayIterator este o clasă internă.
                                         // Folosirea numelui său fără un backslash
                                         // va încerca să îl rezolve în namespace-ul tău.
}
{% endhighlight %}

* [Spațiul global](http://php.net/manual/en/language.namespaces.global.php)
* [Reguli globale](http://php.net/manual/en/userlandnaming.rules.php)

## String-uri

### Concatenație

- Dacă linia ta se extinde dincolo de lungimea recomandata(120 de caractere). consideră concatenarea ei.
- Pentru o citire mai ușoară este bine să folosești operatorii de concatenare și nu operatorii de asignare concatenare
- Pe când ești înăuntrul scope-ului original al variabilei, ident-ează atunci când concatenarea
folosește un nou rând

{% highlight php %}
<?php
$a  = 'Multi-line example';    // operator de asignare concatenare (.=)
$a .= "\n";
$a .= 'of what not to do';

vs.

$a = 'Multi-line example'      // operator de concatenare (.)
    . "\n"                     // indentarea noilor rânduri
    . 'of what to do';
{% endhighlight %}

* [Operatori string-uri](http://php.net/manual/en/language.operators.string.php)

### Tipuri de stringuri

Tipurile de stringuri sunt o funcționalitate constantă în comunitatea PHP, dar sperăm că aceasta secțiune
va explica diferențele dintre tipurile de stringuri și beneficiile/utilizările lor.

#### Ghilimele simple

Ghilimelele simple sunt cea mai simplă cale de a defini un string și deseori cea mai rapidă.
Viteza lor pornește din faptul că PHP nu parsează string-ul (nu parsează după variabile).
Sunt cele potrivite pentru:

- String-uri care nu vor fi parsate
- Scrierea unei variabile în text obișnuit

{% highlight php %}
<?php
echo 'Acesta este string-ul meu, privește ce frumos este el.';    // nu e nevoie să fie parsat un simplu string

/**
 * Rezultat:
 *
 * Acesta este string-ul meu, privește ce frumos este el.
 */
{% endhighlight %}

* [Ghilimele simple](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.single)

#### Ghilimele duble

Ghilimelele duble sunt briceagul string-urilor, dar sunt mai lente datorită faptului că string-ul este
parsat. Sunt cele mai potrivite pentru:

- String-uri escape-uite
- Stringuri cu variabile multiple și text simplu
- Condensarea concatenației de multe rânduri, și îmbunătățirea lizibilității

{% highlight php %}
<?php
echo 'phptherightway is ' . $adjective . '.'     // un exemplu cu ghilimele simple care folosește concatenare
    . "\n"                                       // multiplă pentru variabile și string-uri escape-ate
    . 'I love learning' . $code . '!';

vs.

echo "phptherightway is $adjective.\n I love learning $code!"  // În loc de concatenare multipla, ghilimelele
                                                               // duble ne permit să folosim un string parsabil
{% endhighlight %}

Când folosim ghilimele duble care conțin variabile, deseori se poate întâmpla că variabila să atingă
alt caracter. Asta va rezulta în incapacitatea PHP de a parsa variabila întrucât e camuflata. Pentru
a repara aceasta problema, înfășoară variabila cu o pereche de acolade.

{% highlight php %}
<?php
$juice = 'plum';
echo "I drank some juice made of $juices";    // $juice nu poate fi parsat

vs.

$juice = 'plum';
echo "I drank some juice made of {$juice}s";    // $juice va fi parsat

/**
 * Variabile complexe vor fi și ele parsate în acolade
 */

$juice = array('apple', 'orange', 'plum');
echo "I drank some juice made of {$juice[1]}s";   // $juice[1] va fi parsat
{% endhighlight %}

* [Ghilimele duble](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.double)

#### Sintaxa Nowdoc

Sintaxa Nowdoc a fost introdusă în 5.3 și intern se comportă la fel că și ghilimelele simple cu
excepția că este menit pentru string-urile multi-rand fără nevoia de a concatena.

{% highlight php %}
<?php
$str = <<<'EOD'             // inițializat de <<<
Exemplu de string ce se
întinde pe mai multe rânduri
folosind sintaxa nowdoc.
$a nu este parsat.
EOD;                        // 'EOD' de închidere trebuie să fie pe propriul rând, și în cel mai stâng punct posibil

/**
 * Rezultat:
 *
 * Exemplu de string ce se
 * întinde pe mai multe rânduri
 * folosind sintaxa nowdoc.
 * $a nu este parsat.
 */
{% endhighlight %}

* [Sintaxa Nowdoc](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.nowdoc)

#### Sintaxa Heredoc

Sintaxa Heredoc se comportă intern că și ghilimelele duble cu excepția că este menit pentru uzul
string-urilor de mai multe rânduri fără să fie nevoie de concatenare.

{% highlight php %}
<?php
$a = 'Variabilele';

$str = <<<EOD               // inițializat de <<<
Exemplu de string ce se
întinde pe mai multe rânduri
folosind sintaxa heredoc.
$a sunt parsate.
EOD;                        // 'EOD' de închidere trebuie să fie pe propriul rând, și în cel mai stâng punct posibil

/**
 * Rezultat:
 *
 * Exemplu de string ce se
 * întinde pe mai multe rânduri
 * folosind sintaxa heredoc.
 * Variabilele sunt parsate.
 */
{% endhighlight %}

* [Sintaxa Heredoc](http://www.php.net/manual/en/language.types.string.php#language.types.string.syntax.heredoc)

## Operatori ternari

Operatorii ternari sunt o buna cale de a condensa cod, dar deseori sunt folosiți în exces.
Deși operatorii ternari pot fi stivuiți/cuibăriți, este recomandat să fie folosiți unul
pe rând pentru lizibilitate.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? 'yay' : 'nay';

vs.

// ternar stivuit
$b = 10;
echo ($a) ? ($a == 5) ? 'yay' : 'nay' : ($b == 10) ? 'excessive' : ':(';    // stivuire în exces, sacrifică lizibilitatea
{% endhighlight %}

Pentru a returna o valoare cu operatori ternari folosește sintaxa corectă.

{% highlight php %}
<?php
$a = 5;
echo ($a == 5) ? return true : return false;    // acest exemplu va produce o eroare

vs.

$a = 5;
return ($a == 5) ? 'yay' : 'nope';    // acest exemplu va returna 'yay'
{% endhighlight %}

* [Operatori ternari](http://php.net/manual/en/language.operators.comparison.php)

## Declarații de variabile

Uneori, programatorii încearcă să își facă codul "mai clar" declarând variabile predefinite cu un alt nume.
Ceea ce face asta în realitate este de a dubla consumul de memorie al respectivului script.
Pentru exemplul de mai jos, să zicem un string exemplu conține 1MB de date, copiind variabila ai
incrementat execuția scriptului la 2MB.

{% highlight php %}
<?php
$about = 'Un foarte lung string de text';    // folosește 2MB de memorie
echo $about;

vs.

echo 'Un foarte lung string de text';        // folosește 1MB de memorie
{% endhighlight %}

* [Sfaturi pentru performanță](https://developers.google.com/speed/articles/optimizing-php)