# Ghid stil cod  {#code_style_guide_title}

Comunitatea PHP este mare, diversa, si este compusa din nenumarate biblioteci, framework-uri si componente. Este comun ca
dezvoltatorii sa aleaga cateva dintre acestea si sa le combine intr-un singur proiect. E important ca, codul PHP sa adere
(pe cat posibil) la un stil de programare comun pentru a fi usor pentru dezvoltatori sa amestece diferite biblioteci
pentru proiectele lor.

[Framework Interop Group][fig] a propus si a probat o serie de recomandari de stil. Nu toate sunt legate de stilul codului
dar acelea care sunt sunt [PSR-0][psr0], [PSR-1][psr1], [PSR-2][psr2] si [PSR-4][psr4]. Aceste recomandari sunt doar un set de reguli
pe care unele proiecte precum Drupal, Zend, Symfony,  CakePHP, phpBB, AWS SDK, FuelPHP, Lithium, etc au inceput sa le adopte. Le poti folosi
in proiectele tale sau poti continua folosirea propriului stil personal.

Ideal ar fi sa scrii cod PHP care adera la un standard cunoscut. Aceasta ar putea fi orice combinatie de PSR-uri, sau unul
dintre standardele de codare facute de PEAR sau Zend. Aceasta inseamna ca alti dezvoltatori pot citi si lucra cu codul tau cu usurinta,
iar aplicatiile care implementeaza componente pot avea consecventa chiar si atunci cand lucreaza cu mult cod din terte parti.



* [Citeste despre PSR-0][psr0]
* [Citeste despre PSR-1][psr1]
* [Citeste despre PSR-2][psr2]
* [Citeste despre PSR-4][psr4]
* [Citeste despre standardele PEAR][pear-cs]
* [Citeste despre standardele Zend][zend-cs]
* [Citeste despre standardele Symfony][symfony-cs]

Poti folosi [PHP_CodeSniffer][phpcs] pentru a verifica codul fata de oricare din aceste recomandari, iar module plugin pentru
editoarele de text precum [Sublime Text 2][st-cs] iti pot da indicii in timp real.

Foloseste [PHP Coding Standards Fixer][phpcsfixer] al lui Fabien Potencier pentru a modifica automat sintaxa codului tau asa incat
ea sa se conformeze acestor standarde salvandu-te pe tine de la rezolvarea fiecarei probleme manual.

Engleza este preferata pentru toate numele de simboluri. Comentariile pot fi scrise in orice limba usor accesibila tuturor partilor ce vor
lucra cu bucata de cod.



[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[pear-cs]: http://pear.php.net/manual/en/standards.php
[zend-cs]: http://framework.zend.com/wiki/display/ZFDEV2/Coding+Standards
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
