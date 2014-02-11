---
isChild: true
---

## Exceptii {#exceptions_title}

Exceptiile sunt o parte standard a majoritatii marilor limbaje de programare, dar sunt deseori trecute
cu vederea de catre programatorii PHP.
Limbaje precum Ruby se bazeaza foarte mult pe exceptii, asa ca oricand se intampla ceva
gresit precum o interogare HTTP care esueaza, sau o interogare SQL, sau o imagine nu poate
fi gasita, Ruby (sau gem-ul folosit) va arunca o exceptie pe ecran insemnand ca vei
stii imediat ca exista o greseala.

PHP este destul de lax in aceasta privinta, iar dupa o apelare la `file_get_contents()` te
vei alege cu un `FALSE` si o avertizare.
Multe framework-uri mai vechi precum CodeIgniter vor returna un false, vor scrie un mesaj in
jurnalul propriu si poate te vor lasa sa folosesti o metoda precum `$this->upload->get_error()`
ca sa vezi ce s-a petrecut rau. Problema aici este ca tu trebuie sa mergi sa cauti greseala
si sa verifici documentele sa vezi care este metoda de eroare pentru acea clasa in loc ca ea
sa fie extrem de evidenta.

Alta problema este cand clasele arunca o eroare automat pe ecran si opresc procesul.
Cand faci asta inseamna ca opresti alt programator care s-ar fi ocupat de acea eroare.
Exceptii ar trebui aruncate pentru a face un programator constient de eroare; apoi el
va putea sa aleaga cum sa se ocupe. E.g.:

{% highlight php %}
<?php
$email = new Fuel\Email;
$email->subject('My Subject');
$email->body('How the heck are you?');
$email->to('guy@example.com', 'Some Guy');

try
{
    $email->send();
}
catch(Fuel\Email\ValidationFailedException $e)
{
    // Validarea a esuat
}
catch(Fuel\Email\SendingFailedException $e)
{
    // Driver-ul nu a putut trimite email-ul
}
finally
{
    // Executat chiar si daca o exceptie a fost aruncata si inainte ca
       executia normala sa fie reinceputa
}
{% endhighlight %}

### Exceptii SPL

Clasa generica `Exception` pune la dispozitie foarte putina informatie pentru depanare
pentru dezvoltator; totusi, pentru a remedia asta, este posibil sa creezi o `Exception`
specializata prin subclasarea genericei `Exception`:

{% highlight php %}
<?php
class ValidationException extends Exception {}
{% endhighlight %}

Asta inseamna ca poti adauga multiple blocuri catch si te poti ocupa de diferite
Exceptii diferit. Asta poate duce la crearea de mult Exceptii personalizate, unele
dintre care ar fi putut fi evitate folosind exceptii SPL disponibile in [extensia SPL][splext].

Daca de exemplu folosesti metoda magica `__call()` si o metoda invalida este ceruta
atunci in loc de aruncarea unei Exceptii standard, care e vaga, sau crearea unei
Exceptii personalizate numai pentru asta, ai putea pur si simplu sa
`throw new BadFunctionCallException;`.

* [Citeste despre Exceptii][exceptions]
* [Citeste despre Exceptii SPL][splexe]
* [Stivuirea exceptilor in PHP][nesting-exceptions-in-php]
* [Bune practici pentru exceptii in PHP 5.3][exception-best-practices53]

[exceptions]: http://php.net/manual/ro/language.exceptions.php
[splexe]: http://php.net/manual/ro/spl.exceptions.php
[splext]: /#standard_php_library
[exception-best-practices53]: http://ralphschindler.com/2010/09/15/exception-best-practices-in-php-5-3
[nesting-exceptions-in-php]: http://www.brandonsavage.net/exceptional-php-nesting-exceptions-in-php/
