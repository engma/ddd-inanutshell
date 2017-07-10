# Domain Driven Design in a nutshell
In this very simple introduction I try to distell and give you a very quick overview of what Domain Driven Design is, if you would like to check more informative and detailed resources please check:
* [Domain Driven Design Distelled by Vaughn Vernon](https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/ref=sr_1_sc_1?ie=UTF8&qid=1499649365&sr=8-1-spell&keywords=domain+driven+design+distelled)
* [Domain Driven Design by Eric Evans](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/ref=sr_1_1?ie=UTF8&qid=1499649453&sr=8-1&keywords=domain+driven+design)

______


## Buzzwords

Now before we begin we need to state some definitions to some of DDD's most famous buzzwords that we will use

1. **Domain**: Obviously our first word is the "Domain", now that exactly is the domain? DDD takes a more business inclined methodology to how we develop, which means instead of concentrating on naming our classes and dividing our projects based on technology terminologies, we would name and distribute our code and projects based on what the business "Domain" is, hence the word "domain", so here your development is guided and defined by the domain on which you are working on.

      For example, if we were building an online shopping site, then our domain would be "Online Shopping", now all our terminology would be from this domain and our language would be only from this domain context, so instead of "*ListAggregator*" we would use something like "*ShoppingItemsAggregator*" this makes more clear to both developers and domain experts what exactly this part of the app does.
      This domain might be a rather big one that contains various small subdomains by itself, so we divide it into smaller domains, like the *Shopping Cart* Domain, the *Payment* Domain, the *Inventory* Domain ...etc. each one of those could be divided into smaller domains, until we reach a **Bounded Context**

2. **Bounded Context** A bounded context is a self contained part of the domain, it needs no direct depencies on other parts and provide a single set of functionality

3. **Ubiquitous Language** We use a common language and terminology in communication and naming our classes and other parts of our system, now it's a "language" on its own, it's more of a predefined and agreed upon terminology that we will use in our system, that is both understadable by the developers and the domain experts
