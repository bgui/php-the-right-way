---
isChild: true
---

## Containeri {#containers_title}

Primul lucru pe care ar trebui sa îl înțelegi despre containerii de injectare de dependințe este
că ei nu sunt același lucru ca injectarea de dependințe. Un container este o utilitate convenientă
care ajută să implementăm injectarea de dependințe, dar, ei pot fi, și sunt greșit utilizați
prin implementarea unui anti-șablon, Locator-ul de Servicii. Injectarea unui container ca
locator de servicii în clasele noastre creează o dependență mai mare de container decât de
cea pe care încerci să o înlocuiești. De asemenea iți face codul mult mai puțin transparent și
mai greu de testat.
Majoritatea framework-urilor moderne au propriul container de injectare de dependințe care iți
permite sa iți ții dependințele împreună prin configurație.
Ce înseamnă asta în practică este că poți scrie cod de aplicație care este la fel de curat
și de decuplat ca și framework-ul pe care e clădit.
