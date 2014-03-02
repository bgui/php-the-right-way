---
isChild: true
---

## Fișiere de configurare {#configuration_files_title}

Când creezi fișiere de configurare, bunele practici recomandă ca una dintre următoarele metode să fie folosită:

- Este recomandat să îți stochezi informațiile de configurare unde nu pot fi accesate direct sau extrase prin sistemul
  de fișiere
- Dacă trebuie sa îți stochezi fișierele de configurație în directorul rădăcină, denumește-le cu extensia `.php`. În
  acest fel te asiguri că chiar dacă scriptul este accesat direct, nu va fi afișat ca text.
- Informațiile din fișierele de configurare ar trebui protejate, ori prin criptare, ori prin setarea corespunzătoarea
  a permisiilor sistemului de fișiere
