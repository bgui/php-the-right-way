---
isChild: true
---

## Excepții {#exceptions_title}

Excepțiile sunt o parte standard a majorității marilor limbaje de programare, dar sunt deseori trecute cu vederea de
către programatorii PHP. Limbaje precum Ruby se bazează foarte mult pe excepții, așa ca oricând se întâmplă ceva greșit
precum o interogare HTTP care eșuează, sau o interogare SQL, sau o imagine nu poate fi găsită, Ruby (sau gem-ul folosit)
va arunca o excepție pe ecran însemnând că vei știi imediat ca există o greșeală.

PHP este destul de lax în aceasta privință, iar după o apelare la `file_get_contents()` te vei alege cu un `FALSE` și
o avertizare. Multe framework-uri mai vechi precum CodeIgniter vor returna un false, vor scrie un mesaj în jurnalul
propriu și poate te vor lăsa să folosești o metodă precum `$this->upload->get_error()` ca ce eroare a avut loc.
Problema aici este ca tu trebuie să mergi să cauți greșeala și să verifici documentele să vezi care este metoda de
eroare pentru acea clasa în loc ca ea să fie extrem de evidentă.

Altă problemă este când clasele aruncă o eroare automat pe ecran și opresc procesul. Când faci asta înseamnă că oprești
alt programator care s-ar fi ocupat de acea eroare. Excepții ar trebui aruncate pentru a face un programator conștient
de eroare; apoi el va putea să aleagă cum să se ocupe. E.g.:

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
    // Validarea a eșuat
}
catch(Fuel\Email\SendingFailedException $e)
{
    // Driver-ul nu a putut trimite email-ul
}
finally
{
    // Executat chiar și dacă o excepție a fost aruncată și înainte ca
       execuția normală să fie reîncepută
}
{% endhighlight %}

### Excepții SPL

Clasa generică `Exception` pune la dispoziție foarte puțină informație pentru depanare și dezvoltator; totuși,
pentru a remedia asta, este posibil să creezi o excepție specializată prin subclasarea genericei `Exception`:

{% highlight php %}
<?php
class ValidationException extends Exception {}
{% endhighlight %}

Asta înseamnă că poți adăuga multiple blocuri catch și te poți ocupa de diferite Excepții în moduri diferite. Asta poate
duce la crearea multor Excepții personalizate, unele din ele ar fi putut fi evitate folosind excepții SPL disponibile în
[extensia SPL][splext].

Dacă de exemplu folosești metoda magică `__call()` și o metodă invalidă este cerută atunci în loc de aruncarea unei
Excepții standard, care e vagă, sau crearea unei Excepții personalizate numai pentru asta, ai putea pur și simplu să
`throw new BadFunctionCallException;`.

* [Citește despre Excepții][exceptions]
* [Citește despre Excepții SPL][splexe]
* [Stivuirea excepțiilor în PHP][nesting-exceptions-in-php]
* [Bune practici pentru excepții în PHP 5.3][exception-best-practices53]

[exceptions]: http://php.net/manual/ro/language.exceptions.php
[splexe]: http://php.net/manual/ro/spl.exceptions.php
[splext]: /#standard_php_library
[exception-best-practices53]: http://ralphschindler.com/2010/09/15/exception-best-practices-in-php-5-3
[nesting-exceptions-in-php]: http://www.brandonsavage.net/exceptional-php-nesting-exceptions-in-php/
