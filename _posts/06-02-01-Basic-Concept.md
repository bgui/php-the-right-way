---
isChild: true
---

## Concept de baza {#basic_concept_title}

Putem demonstra conceptul cu o simpla, desi naiv exemplu.

Aici avem clasa `Database` care necesita un adaptor ca sa vorbeasca cu baza de date. Instantiem
adaptorul in constructor si cream o dependinta explicita. Asta face testarea dificila si inseamna
ca clasa `Database` este strans cuplata de adaptor.

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

Acest cod poate fi refactorizat pentru a folosi injectarea de dependinte si asadar sa flexibilizeze dependinta.

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

Ii dam acum lui `Database` propria lui dependinta fata de atunci cand il lasam pe el sa si-o creeze singur.
Am putea chiar creea o metoda care ar accepta un argument al dependintei si ar seta-o astfel, sau daca proprietatea
`$adapter` ar fi publica am putea-o seta direct.

