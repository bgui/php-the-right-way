---
isChild: true
---

## Raportarea erorilor {#error_reporting_title}

Log-area (jurnalizarea) erorilor poate fi utilă pentru a afla probleme în aplicația ta, dar, de asemenea,
poate expune informații despre structura aplicației tale lumii externe.
Pentru a-ți proteja aplicația de probleme ce ar putea fi cauzate de afișarea acestor mesaje,
trebuie să iți configurezi serverul diferit pentru dezvoltare decât pentru producție (live).

### Dezvoltare

Pentru a arăta toate erorile posibile în timpul <strong>dezvoltării</strong>,
configurați următoarele setări din `php.ini`:

    display_errors = On
    display_startup_errors = On
    error_reporting = -1
    log_errors = On


> Pasarea valorii `-1` va arăta toate erorile posibile, chiar și când noi niveluri
și constante sunt adăugate în viitoare versiuni PHP. Constanta `E_ALL` se comportă
în acest fel începând cu PHP 5.4. - [php.net](http://php.net/manual/function.error-reporting.php)

Nivelul de erori `E_STRICT` a fost introdus în 5.3.0 și nu făcea parte din
`E_ALL`, dar totuși a devenit parte din `E_ALL` în 5.4.0. Ce înseamnă asta?
În termeni de raportarea fiecărei posibile erori în 5.3 înseamnă ca trebuie
să folosești ori `-1` ori `E_ALL | E_STRICT`.


**Raportare toate erorile posibile în funcție de versiunea PHP**

* &lt; 5.3 `-1` or `E_ALL`
* &nbsp; 5.3 `-1` or `E_ALL | E_STRICT`
* &gt; 5.3 `-1` or `E_ALL`

### Producție

Pentru a ascunde erorile pe mediul vostru de <strong>producție</strong>, configurați-vă `php.ini`
precum:

    display_errors = Off
    display_startup_errors = Off
    error_reporting = E_ALL
    log_errors = On

Cu aceste setări în producție, erorile vor fi înregistrate în log-urile de erori de pe serverul web,
dar nu vor fi afișate utilizatorului. Pentru mai multe informații despre
aceste setări, consultați manualul PHP:

* [error_reporting](http://php.net/manual/errorfunc.configuration.php#ini.error-reporting)
* [display_errors](http://php.net/manual/errorfunc.configuration.php#ini.display-errors)
* [display_startup_errors](http://php.net/manual/errorfunc.configuration.php#ini.display-startup-errors)
* [log_errors](http://php.net/manual/errorfunc.configuration.php#ini.log-errors)