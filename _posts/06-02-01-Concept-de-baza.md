---
isChild: true
---

## Concept de bază {#concept_de_baza_title}

Putem demonstra conceptul cu un simplu, deși naiv exemplu.

Aici avem clasa `Database` care necesită un adaptor ca să vorbească cu baza de date. Instanțiem adaptorul în constructor
și creăm o dependință explicită. Asta face testarea dificilă și înseamnă că clasa `Database` este strâns cuplată de
adaptor.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct()
    {
        $this->adapter = new MySqlAdapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

Acest cod poate fi rescris (refactored) pentru a folosi injectarea de dependințe și așadar să flexibilizeze dependința.

{% highlight php %}
<?php
namespace Database;

class Database
{
    protected $adapter;

    public function __construct(MySqlAdapter $adapter)
    {
        $this->adapter = $adapter;
    }
}

class MysqlAdapter {}
{% endhighlight %}

Îi dam acum lui `Database` propria lui dependință față de atunci când îl lăsam pe el sa și-o creeze singur. Am putea
chiar crea o metodă care ar accepta un argument al dependinței și ar seta-o astfel, sau dacă proprietatea `$adapter` ar
fi publică am putea-o seta direct.
