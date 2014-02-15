---
isChild: true
---

## Raportarea erorilor {#error_reporting_title}

Log-area (jurnalizarea) erorilor poate fi utila pentru a afla probleme in aplicatia ta, dar, de asemenea,
poate expune informatii despre structura aplicatiei tale lumii externe.
Pentru a-ti proteja aplicatia de probleme ce ar putea fi cauzate de afisarea acestor mesaje,
trebuie sa iti configurezi serverul diferit pentru dezvoltare decat pentru productie (live).

### Dezvoltare
Pentru a arata toate erorile posibile in timpul <strong>dezvoltarii</strong>,
configurati urmatoarele setari din `php.ini`:

    display_errors = On
    display_startup_errors = On
    error_reporting = -1
    log_errors = On


> Pasarea valorii `-1` va arata toate erorile posibile, chiar si cand noi niveluri
si constante sunt adaugate in viitoare versiuni PHP. Constanta `E_ALL` se comporta
in acest fel incepand cu PHP 5.4. - [php.net](http://php.net/manual/function.error-reporting.php)

Nivelul de erori `E_STRICT` a fost introdus in 5.3.0 si nu facea parte din
`E_ALL`, dar totusi a devenit parte din `E_ALL` in 5.4.0. Ce inseamna asta?
In termeni de raportarea fiecarei posibile erori in 5.3 inseamna ca trebuie
sa folosesti ori `-1` ori `E_ALL | E_STRICT`.


**Raportare toate erorile posibile in functie de versiunea PHP**

* &lt; 5.3 `-1` or `E_ALL`
* &nbsp; 5.3 `-1` or `E_ALL | E_STRICT`
* &gt; 5.3 `-1` or `E_ALL`

### Productie

Pentru a ascunde erorile pe mediul vostru de <strong>productie</strong>, configurati-va `php.ini`
precum:

    display_errors = Off
    display_startup_errors = Off
    error_reporting = E_ALL
    log_errors = On

Cu aceste setari in productie, erorile vor fi inregistrate in log-urile de erori de pe serverul web,
dar nu vor fi afisate utilizatorului. Pentru mai multe informatii despre
aceste setari, consultati manualul PHP:

* [error_reporting](http://php.net/manual/errorfunc.configuration.php#ini.error-reporting)
* [display_errors](http://php.net/manual/errorfunc.configuration.php#ini.display-errors)
* [display_startup_errors](http://php.net/manual/errorfunc.configuration.php#ini.display-startup-errors)
* [log_errors](http://php.net/manual/errorfunc.configuration.php#ini.log-errors)
