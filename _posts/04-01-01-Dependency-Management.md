# Management-ul dependintelor {#dependency_management_title}

Exista o tona de biblioteci PHP, framework-uri, si componente din care sa alegi. Proiectul tau va folosi
cel mai probabil cateva dintre acestea — acestea sunt dependintele proiectului. Pana recent PHP nu a
avut o metoda buna de a administra aceste dependinte ale proiectului. Chiar si daca le administrai
manual, tot trebuia sa te ingrijesti de autoloaderi. Nu mai e cazul.

Curent exista doua sisteme de management de pachete in PHP - Composer si PEAR. Care e mai bun? Ambele!

 * Foloseste **Composer** cand administrezi dependintele pentru un singur proiect.
 * Foloseste **PEAR** cand administrezi dependintele PHP pentru intregul tau sistem.

In general, pachetele Composer sunt disponibile numai in proiectele pe care le specifici tu explicit, pe cand
un pachet PEAR este disponibil pentru toate proiectele. Desi aparent PEAR suna mai usor, exista avantaje in
folosirea abordarii per-proiect.
