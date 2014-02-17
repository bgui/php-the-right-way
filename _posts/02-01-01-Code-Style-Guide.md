# Ghid stil cod  {#code_style_guide_title}

Comunitatea PHP este mare, diversă, și este compusă din nenumărate biblioteci, framework-uri și componente. Este comun ca
dezvoltatorii să aleagă câteva dintre acestea și sa le combine într-un singur proiect. E important ca, codul PHP să adere
(pe cât posibil) la un stil de programare comun pentru a fi ușor pentru dezvoltatori să amestece diferite biblioteci
pentru proiectele lor.

[Framework Interop Group][fig] a propus și a probat o serie de recomandări de stil. Nu toate sunt legate de stilul codului
dar acelea care sunt [PSR-0][psr0], [PSR-1][psr1], [PSR-2][psr2] si [PSR-4][psr4]. Aceste recomandări sunt doar un set de reguli
pe care unele proiecte precum Drupal, Zend, Symfony,  CakePHP, phpBB, AWS SDK, FuelPHP, Lithium, etc au început să le adopte. Le poți folosi
în proiectele tale sau poți continua folosirea propriului stil personal.

Ideal ar fi să scrii cod PHP care aderă la un standard cunoscut. Aceasta ar putea fi orice combinație de PSR-uri, sau unul
dintre standardele de codare făcute de PEAR sau Zend. Aceasta înseamnă că alți dezvoltatori pot citi și lucra cu codul tău cu ușurință,
iar aplicațiile care implementează componente pot avea consecvență chiar și atunci când lucrează cu mult cod din terțe părți.



* [Citește despre PSR-0][psr0]
* [Citește despre PSR-1][psr1]
* [Citește despre PSR-2][psr2]
* [Citește despre PSR-4][psr4]
* [Citește despre standardele PEAR][pear-cs]
* [Citește despre standardele Zend][zend-cs]
* [Citește despre standardele Symfony][symfony-cs]

Poți folosi [PHP_CodeSniffer][phpcs] pentru a verifica codul față de oricare din aceste recomandări, iar module plugin pentru
editoarele de text precum [Sublime Text 2][st-cs] iți pot da indicii în timp real.

Folosește [PHP Coding Standards Fixer][phpcsfixer] al lui Fabien Potencier pentru a modifica automat sintaxa codului tău așa încât
ea să se conformeze acestor standarde salvându-te pe tine de la rezolvarea fiecărei probleme manual.

Engleza este preferată pentru toate numele de simboluri. Comentariile pot fi scrise în orice limba ușor accesibilă tuturor părților ce vor
lucra cu bucata de cod.



[fig]: http://www.php-fig.org/
[psr0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md
[pear-cs]: http://pear.php.net/manual/ro/standards.php
[zend-cs]: http://framework.zend.com/wiki/display/ZFDEV2/Coding+Standards
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/