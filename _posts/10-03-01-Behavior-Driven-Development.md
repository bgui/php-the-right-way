---
isChild: true
---

## Dezvoltare centrata pe comportament {#behavior_driven_development_title}

Exista doua tipuri diferite de dezvoltare centrata pe comportament (BDD): SpecBDD si StoryBDD.
SpecBDD se concentreaza pe comportamentul tehnic al codului, in timp ce StoryBDD se
concentreaza pe business sau pe comportamentul functionalitatilor sau interactiunilor.
Exista framework-uri PHP pentru ambele tipuri de BDD.

Cu StoryBDD, tu scrii povestioare citibile de om, care descriu comportamentul aplicatiei tale.
Aceste povestioare pot fi apoi rulate ca teste efective asupra aplicatiei tale. Framework-ul
folosit in aplicatii PHP pentru StoryBDD este Behat, care este inspirat de proiectul
[Cucumber](http://cukes.info/) din Ruby, si care implementeaza Gherkin DSL pentru
descrierea comportamentului functionalitatilor.

Cu SpecBDD, poti scrie specificatii care descriu cum propriul cod trebuie sa se comporte.
In loc de a testa o functie sau o metoda, tu descrii cum acea functie sau metoda ar trebui sa
se comporte. PHP ofera framework-ul PHPSpec pentru aceasta. Acest framework este inspirat de
proiectul [RSpec](http://rspec.info/) pentru Ruby.

### BDD Links

* [Behat](http://behat.org/), framework-ul StoryBDD pentru PHP, inspirat de [Cucumber](http://cukes.info/) din Ruby;
* [PHPSpec](http://www.phpspec.net/), framework-ul SpecBDD pentru PHP, inspirat de proiectul [RSpec](http://rspec.info/) din Ruby;
* [Codeception](http://www.codeception.com) este o framework de intreaga stiva care foloseste principii BDD.
