---
isChild: true
---

## Interfata linie de comanda {#command_line_interface_title}

PHP a fost creat pentru scopul primar de a scrie aplicatii web, dar este de asemenea util
pentru scrierea de scripturi pentru linia de comanda (CLI). Programele PHP de linie de comanda
te pot ajuta sa automatizezi sarcini comune precum testarea, lansarea, si administratia aplicatiei.

Programele PHP CLI sunt puternice pentru ca poti folosi codul aplicatiei tale direct fara sa fii nevoit sa ai un GUI web pentru el.
Doar fii sigur sa nu pui scripturile CLI PHP din radacina publica.

Incearca sa rulezi PHP din linia de comanda:

{% highlight bash %}
> php -i
{% endhighlight %}

Optiunea `-i` va afisa configuratia ta PHP exact ca functia [`phpinfo`][phpinfo].

Optiunea `-a` furnizeaza un shell interactiv, similar cu IRB-ul lui Ruby sau cu shell-ul interactiv al lui Python.
Exista o multitudine de alte de optiuni[command line options][cli-options] utile.

Hai sa scriem un simplu program CLI "Hello, $name". Ca sa il incercam, creem un fisier numit `hello.php`, ca mai jos.

{% highlight php %}
<?php
if ($argc != 2) {
    echo "Uz: php hello.php [name].\n";
    exit(1);
}
$name = $argv[1];
echo "Hello, $name\n";
{% endhighlight %}

PHP seteaza doua variabile speciale bazate pe argumentele cu care este rulat scriptul tau.
[`$argc`][argc] este o variabila integer ce contine numarul argumentelor si [`$argv`][argv] este un array ce contine
*valoarea* fiecarui argument. Primul argument este totdeauna numele fisierului scriptului tau PHP, in cazul nostru `hello.php`.

Expresia `exit()` este utilizata cu un numar nenul pentru a instiinta shell-ul ca comanda a esuat. Coduri de exit des
uzitate pot fi gasite [aici][exit-codes]

Ca sa ne rulam scriptul de mai sus din linia de comanda:

{% highlight bash %}
> php hello.php
Uz: php hello.php [name]
> php hello.php world
Hello, world
{% endhighlight %}


 * [Invata despre rularea PHP din linia de comanda][php-cli]
 * [Invata despre configurarea Windows pentru a rula PHP din linia de comanda][php-cli-windows]

[phpinfo]: http://php.net/manual/ro/function.phpinfo.php
[cli-options]: http://www.php.net/manual/ro/features.commandline.options.php
[argc]: http://php.net/manual/ro/reserved.variables.argc.php
[argv]: http://php.net/manual/ro/reserved.variables.argv.php
[php-cli]: http://php.net/manual/ro/features.commandline.php
[php-cli-windows]: http://www.php.net/manual/ro/install.windows.commandline.php
[exit-codes]: http://www.gsp.com/cgi-bin/man.cgi?section=3&topic=sysexits
