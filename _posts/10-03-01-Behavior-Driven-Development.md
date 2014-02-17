---
isChild: true
---

## Dezvoltare centrata pe comportament {#behavior_driven_development_title}

Exista doua tipuri diferite de dezvoltare centrata pe comportament (BDD): SpecBDD și StoryBDD.
SpecBDD se concentrează pe comportamentul tehnic al codului, în timp ce StoryBDD se
concentrează pe business sau pe comportamentul funcționalităților sau interacțiunilor.
Exista framework-uri PHP pentru ambele tipuri de BDD.

Cu StoryBDD, tu scrii povestioare citibile de om, care descriu comportamentul aplicației tale.
Aceste povestioare pot fi apoi rulate ca teste efective asupra aplicației tale. Framework-ul
folosit în aplicații PHP pentru StoryBDD este Behat, care este inspirat de proiectul
[Cucumber](http://cukes.info/) din Ruby, și care implementează Gherkin DSL pentru
descrierea comportamentului funcționalităților.

Cu SpecBDD, poți scrie specificații care descriu cum propriul cod trebuie să se comporte.
În loc de a testa o funcție sau o metodă, tu descrii cum acea funcție sau metodă ar trebui să
se comporte. PHP oferă framework-ul PHPSpec pentru aceasta. Acest framework este inspirat de
proiectul [RSpec](http://rspec.info/) pentru Ruby.

### BDD Links

* [Behat](http://behat.org/), framework-ul StoryBDD pentru PHP, inspirat de [Cucumber](http://cukes.info/) din Ruby;
* [PHPSpec](http://www.phpspec.net/), framework-ul SpecBDD pentru PHP, inspirat de proiectul [RSpec](http://rspec.info/) din Ruby;
* [Codeception](http://www.codeception.com) este un framework de întreagă stiva care folosește principii BDD.