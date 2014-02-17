# Management-ul dependințelor {#dependency_management_title}

Există o tonă de biblioteci PHP, framework-uri, și componente din care să alegi. Proiectul tău va folosi
cel mai probabil câteva dintre acestea — acestea sunt dependințele proiectului. Pană recent PHP nu a
avut o metodă bună de a administra aceste dependințe ale proiectului. Chiar și dacă le administrai
manual, tot trebuia să te îngrijești de autoload-eri. Nu mai e cazul.

Curent există două sisteme de management de pachete în PHP - Composer și PEAR. Care e mai bun? Ambele!

 * Folosește **Composer** când administrezi dependințele pentru un singur proiect.
 * Folosește **PEAR** când administrezi dependințele PHP pentru întregul tău sistem.

În general, pachetele Composer sunt disponibile numai în proiectele pe care le specifici tu explicit, pe când
un pachet PEAR este disponibil pentru toate proiectele. Deși aparent PEAR sună mai ușor, există avantaje în
folosirea abordării per-proiect.