---
isChild: true
---

## Fisiere de configurare {#configuration_files_title}

Cand creezi fisiere de configurare, bunele practici recomanda ca una dintre
urmatoarele metode sa fie folosita:

- Este recomandat sa iti stochezi informatiile de configurare unde nu pot fi
accesate direct sau extrase prin sistemul de fisiere
- Daca trebuie sa iti stochezi fisierele de configuratie in directorul radacina,
denumeste-le cu extensia `.php`. Asta asigura ca chiar daca scriptul este
accesat direct, nu va fi afisat ca text.
- Informatiile din fisierele de configurare ar trebui protejate, ori prin
criptare, ori prin permisiunile sistemului de fisiere