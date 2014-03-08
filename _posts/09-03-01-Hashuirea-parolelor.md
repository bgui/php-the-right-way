---
isChild: true
---

## Hash-uirea parolelor {#password_hashing_title}

Toată lumea construiește o aplicație PHP care se bazează pană la urmă pe autentificarea utilizatorilor. Username-urile
și parolele sunt stocate în baza de date iar mai târziu folosite pentru a autentifica utilizatorii.

E important ca parolele să fie bine [_hash-uite_][3] înainte de salvarea în baza de date. Hash-uirea parolelor este
o funcție ireversibilă, mono-direcțională aplicată pe parola utilizatorului. Aceasta produce un șir de caractere de
lungime fixă care nu poate fi folosit pentru a afla parola originală într-un timp fezabil. Asta înseamnă că poți compara
un hash versus un altul ca să vezi dacă ambele au venit de la aceeași sir sursă, dar nu poți determina șirul original.
Dacă parolele nu sunt hash-uite iar baza ta de date este accesată de un terț neautorizat, toate parolele vor fi atunci
compromise. Unii utilizatori ar putea(din păcate) fii folosit aceeași parolă și la alte servicii. Așadar e important să
iei în serios securitatea.

**Hash-uirea parolelor cu `password_hash`**

În PHP 5.5 a fost introdus `password_hash`. Momentan folosește BCrypt, cel mai puternic algoritm suportat de PHP. Va fi
actualizat în curând pentru a suporta mai mulți algoritmi. Biblioteca `password_compat` a fost creată pentru a o face
disponibilă și pentru PHP >= 5.3.7.

Mai jos hash-uim un string, și apoi verificam hash-ul împotriva unui alt string. Pentru că sursele noastre sunt diferite
('secret-password' vs. 'bad-password') autentificarea va eșua.

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



* [Învață despre `password_hash`] [1]
* [`password_compat` pentru PHP  >= 5.3.7 && < 5.5] [2]
* [Învață despre hashing în legătură cu criptografia] [3]
* [PHP `password_hash` RFC] [4]

[1]: http://us2.php.net/manual/ro/function.password-hash.php
[2]: https://github.com/ircmaxell/password_compat
[3]: http://en.wikipedia.org/wiki/Cryptographic_hash_function
[4]: https://wiki.php.net/rfc/password_hash
