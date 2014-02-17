---
isChild: true
---

## Interfața linie de comandă {#command_line_interface_title}

PHP a fost creat pentru scopul primar de a scrie aplicații web, dar este de asemenea util
pentru scrierea de scripturi pentru linia de comandă (CLI). Programele PHP de linie de comandă
te pot ajuta să automatizezi sarcini comune precum testarea, lansarea, și administrația aplicației.

Programele PHP CLI sunt puternice pentru că poți folosi codul aplicației tale direct fără să fii nevoit să ai un GUI web pentru el.
Doar fii sigur să nu pui scripturile CLI PHP în rădăcina publică.

Încearcă să rulezi PHP din linia de comanda:

{% highlight bash %}
> php -i
{% endhighlight %}

Opțiunea `-i` va afișa configurația ta PHP exact ca funcția [`phpinfo`][phpinfo].

Opțiunea `-a` furnizează un shell interactiv, similar cu IRB-ul lui Ruby sau cu shell-ul interactiv al lui Python.
Există o multitudine de alte de opțiuni[de linie de comandă][cli-options] utile.

Hai să scriem un simplu program CLI "Hello, $name". Ca să îl încercăm, creăm un fișier numit `hello.php`, ca mai jos.

{% highlight php %}
<?php
if ($argc != 2) {
    echo "Uz: php hello.php [name].\n";
    exit(1);
}
$name = $argv[1];
echo "Hello, $name\n";
{% endhighlight %}

PHP setează două variabile speciale bazate pe argumentele cu care este rulat scriptul tău.
[`$argc`][argc] este o variabilă integer ce conține numărul argumentelor și [`$argv`][argv] este un array ce conține
*valoarea* fiecărui argument. Primul argument este totdeauna numele fișierului scriptului tău PHP, în cazul nostru `hello.php`.

Expresia `exit()` este utilizată cu un număr nenul pentru a înștiința shell-ul că comanda a eșuat. Coduri de exit des
uzitate pot fi găsite [aici][exit-codes]

Ca să ne rulăm scriptul de mai sus din linia de comandă:

{% highlight bash %}
> php hello.php
Uz: php hello.php [name]
> php hello.php world
Hello, world
{% endhighlight %}


 * [Învață despre rularea PHP din linia de comandă][php-cli]
 * [Învață despre configurarea Windows pentru a rula PHP din linia de comandă][php-cli-windows]

[phpinfo]: http://php.net/manual/ro/function.phpinfo.php
[cli-options]: http://www.php.net/manual/ro/features.commandline.options.php
[argc]: http://php.net/manual/ro/reserved.variables.argc.php
[argv]: http://php.net/manual/ro/reserved.variables.argv.php
[php-cli]: http://php.net/manual/ro/features.commandline.php
[php-cli-windows]: http://www.php.net/manual/ro/install.windows.commandline.php
[exit-codes]: http://www.gsp.com/cgi-bin/man.cgi?section=3&topic=sysexits