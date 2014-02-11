---
isChild: true
---

## Hash-uirea parolelor {#password_hashing_title}

Toata lumea construieste o aplicatie PHP care se bazeaza pana la urma pe autentificarea
utilizatorilor. Username-urile si parolele sunt stocate in baza de date iar mai
tarziu folosite pentru a autentifica utilizatorii.

E important ca parolele sa fie bine [_hash-uite_][3] inainte de salvarea in baza de date.
Hash-uirea parolelor este o functie ireversibila, mono-directionala aplicata pe parola
utilizatorului. Aceasta produce un sir de caractere de lungime fixa care nu poate fi
folosit pentru a afla parola originala intr-un timp fezabil. Asta inseamna ca poti compara
un hash versus un altul ca sa vezi daca ambele au venit de la acelas sir sursa, dar nu
poti determina sirul original. Daca parolele nu sunt hash-uite iar baza ta de date
este accesata de un tert neautorizat, toate parolele vor fi atunci compromise.
Unii utilizatori ar putea(din pacate) fii folosit aceeasi parola si la alte servicii.
Asadar e important sa iei in serios securitatea.

**Hash-uirea parolelor cu `password_hash`**

In PHP 5.5 a fost introdus `password_hash`. Momentan foloseste BCrypt, cel mai puternic
algoritm suportat de PHP. Va fi actualizat in curand pentru a suporta mai multe algoritmuri.
Biblioteca `password_compat` a fost creeata pentru a o face disponibila si pentru PHP >= 5.3.7.

Mai jos hash-uim un string, si apoi verificam hash-ul impotriva unui alt string.
Pentru ca sursele noastre sunt diferite ('secret-password' vs. 'bad-password')
autentificarea va esua.

{% highlight php %}
<?php
                      
require 'password.php';

$passwordHash = password_hash('secret-password', PASSWORD_DEFAULT);

if (password_verify('bad-password', $passwordHash)) {
    // Correct Password
} else {
    // Wrong password
}
{% endhighlight %}  



* [Invata despre `password_hash`] [1]
* [`password_compat` pentru PHP  >= 5.3.7 && < 5.5] [2]
* [Invata despre hashing in legatura cu criptografia] [3]
* [PHP `password_hash` RFC] [4]

[1]: http://us2.php.net/manual/ro/function.password-hash.php
[2]: https://github.com/ircmaxell/password_compat
[3]: http://en.wikipedia.org/wiki/Cryptographic_hash_function
[4]: https://wiki.php.net/rfc/password_hash
