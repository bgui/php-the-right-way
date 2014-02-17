---
isChild: true
---

## Date și Timp {#date_and_time_title}

PHP are o clasă numită DateTime pentru a te ajuta la citirea, scrierea, compararea sau calcularea unor date sau timpi.
Sunt multe funcții legate de date și timp în PHP în afară de DateTime, dar ea furnizează o interfață ușoară și orientata-
obiect pentru majoritatea cazurilor. Poate manevra fusuri orare, dar asta este în afara aceste scurte introduceri.

Pentru a începe lucrul cu DateTime, transformi un string brut într-un obiect cu metoda fabrică `createFromFormat()` sau
poți face un `new \DateTime` pentru a obține data și timpul curente. Folosești metoda `format()` pentru a transforma
DateTime înapoi într-un string pentru afișare.

{% highlight php %}
<?php
$raw = '22. 11. 1968';
$start = \DateTime::createFromFormat('d. m. Y', $raw);

echo 'Start date: ' . $start->format('m/d/Y') . "\n";
{% endhighlight %}

Calcularea cu DateTime este posibilă cu clasa DateInterval. DateTime are metode precum `add()` și `sub()` care
primesc un DateInterval ca argument. Nu scrie cod care presupune același număr de secunde în fiecare zi, pentru că
atât ora de iarna și alterările de fus orar vor invalida această asumpție. Folosește intervale de date pentru asta.
Pentru a calcula diferența de data folosește metoda `diff()`. Va returna un nou DateInterval care este super ușor de afișat.
{% highlight php %}
<?php
// creează o copie a lui $start și adaugă o lună și 6 zile
$end = clone $start;
$end->add(new \DateInterval('P1M6D'));

$diff = $end->diff($start);
echo 'Diferenta: ' . $diff->format('%m month, %d days (total: %a days)') . "\n";
// Diferenta: 1 month, 6 days (total: 37 days)
{% endhighlight %}

Pe obiecte DateTime poți folosi comparații standard:
{% highlight php %}
<?php
if ($start < $end) {
    echo "Start este inainte de sfarsit!\n";
}
{% endhighlight %}

Un ultim exemplu pentru a demonstra clasa DatePeriod. Este folosită pentru a itera prin evenimente recurente.
Poate primi două obiecte DateTime, start și end, și intervalul pentru care va returna toate evenimentele dintre ele.
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
* [Citește despre DateTime][datetime]
* [Citește despre formatarea datelor][dateformat] (operațiuni string formatare date)

[datetime]: http://www.php.net/manual/book.datetime.php
[dateformat]: http://www.php.net/manual/function.date.php