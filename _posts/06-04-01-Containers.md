---
isChild: true
---

## Containeri {#containers_title}

Primul lucru pe care ar trebui sa il intelegi despre containeri de injectare de dependinte este
ca ei nu sunt acelas lucru ca injectarea de dependinte. Un container este o utilitate convenienta
care ajuta sa implementan injectarea de dependinte, dar, ei pot fi, si sunt gresit utilizati
prin implementarea unui anti-sablon, Locator-ul de Servicii. Injectarea unui container ca
locator de servicii in clasele noastre creeaza o dependenta mai mare de container decat de
cea pe care incerci sa o inlocuiesti. De asemenea iti face codul mult mai putin transparent si
mai greu de testat.
Majoritatea framework-urilor moderne au propriul container de injectare de dependinte care iti
permite sa iti tii dependintele impreuna prin configuratie.
Ce inseamna asta in practica este ca poti scrie cod de aplicatie care este la fel de curat
si de decuplat ca si framework-ul pe care e cladit.
