---
isChild: true
---

## Date si Timp {#date_and_time_title}

PHP are o clasa numita DateTime pentru a te ajuta la citirea, scrierea, compararea sau calcularea unor date sau timpi.
Sunt multe functii legate de date si timp in PHP in afara de DateTime, dar ea furnizeaza o interfata usoara si orientata-
obiect pentru majoritatea cazurilor. Poate manevra fusuri orare, dar asta este in afara aceste scurte introduceri.

Pentru a incepe lucrul cu DateTime, transformi un string brut intr-un obiect cu metoda fabrica `createFromFormat()` sau
poti face un `new \DateTime` pentru a obtine data si timpul curente. Folosesti metoda `format()` pentru a transforma
DateTIme inapoi intr-un string pentru afisare.

{% highlight php %}
<?php
$raw = '22. 11. 1968';
$start = \DateTime::createFromFormat('d. m. Y', $raw);

echo 'Start date: ' . $start->format('m/d/Y') . "\n";
{% endhighlight %}

Calcularea cu DateTime este posibila cu clasa DateInterval. DateTime are metode precum `add()` si `sub()` care
primesc un DateInterval ca argument. Nu scrie cod care presupune acelas numar de secunde in fiecare zi, pentru ca
atat ora de iarna si alterarile de fus orar vor invalida aceasta asumptie. Foloseste intervale de data pentru asta.
Pentru a calcula diferenta de data folosete metoda `diff()`. Va returna un nou DateInterval care este super usor de afisat.
{% highlight php %}
<?php
// creeaza o copie a lui $start si adauga o luna si 6 zile
$end = clone $start;
$end->add(new \DateInterval('P1M6D'));

$diff = $end->diff($start);
echo 'Diferenta: ' . $diff->format('%m month, %d days (total: %a days)') . "\n";
// Diferenta: 1 month, 6 days (total: 37 days)
{% endhighlight %}

Pe obiecte DateTime poti folosi comparatii standard:
{% highlight php %}
<?php
if ($start < $end) {
    echo "Start este inainte de sfarsit!\n";
}
{% endhighlight %}

Un ultim exemplu pentru a demonstra clasa DatePeriod. Este folosita pentru a itera prin evenimente recurente.
Poate primi doua obiecte DateTime, start si end, si intervalul pentru care va returna toate evenimentele dintre ele.
{% highlight php %}
<?php
// afiseaza toate Joi-ile dintre $start and $end
$periodInterval = \DateInterval::createFromDateString('first thursday');
$periodIterator = new \DatePeriod($start, $periodInterval, $end, \DatePeriod::EXCLUDE_START_DATE);
foreach ($periodIterator as $date) {
    // afiseaza fiecare data din perioada
    echo $date->format('m/d/Y') . ' ';
}
{% endhighlight %}
1
* [Citeste despre DateTime][datetime]
* [Citeste despre formatarea datelor][dateformat] (operatiuni string formatare date)

[datetime]: http://www.php.net/manual/book.datetime.php
[dateformat]: http://www.php.net/manual/function.date.php
