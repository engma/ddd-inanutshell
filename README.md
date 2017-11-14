# Domain Driven Design in a Nutshell
In this very simple introduction I try to distell and give you a very quick overview of what Domain Driven Design is, if you would like to check more informative and detailed resources please check:
* [Domain Driven Design Distelled by Vaughn Vernon](https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/ref=sr_1_sc_1?ie=UTF8&qid=1499649365&sr=8-1-spell&keywords=domain+driven+design+distelled)
* [Domain Driven Design by Eric Evans](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/ref=sr_1_1?ie=UTF8&qid=1499649453&sr=8-1&keywords=domain+driven+design)

______
## Domain Experts
Those are the individuals who have a great deal of familarity with the domain which the software is trying to solve a problem for. For example if we were making a software for medical information, then doctors would be our domain experts, if we were making a software for hotel booking, then hotel managers would be the experts of this domain.

## Ubiqutious Language

the **Language**: Languages are usually some set of characters/phrases grouped together to define a meaning understandable by someone or something that can parse those phrases. When developing software it is important that the *domain experts* and the *developers* would create a language of terms and common phrases that defines the system's model and interactions.

For example, in a hotel booking app, the term *a Booking* would be an agreed upon term that is both understandable for both the experts and the devs, whenever any of them needs to exchange a piece of information about it they use the term *a booking*, also when a use *books* a *booking* we use the term *books* to signify that we are taking about this activity.

The Ubiqutious language **MUST be use as it is in code**. Developers are not allowed to change the terms to another more technical one, like BookingTable or BookingEntity. It must be used as it is. The same goes for the activities or the interactions which our objects do. So for example, in our code the user would *book* a booking using the *BookingService*. We could have called it *create* a booking in the code to be a more technical term, but in that case we lost our domain based language.

This language will be under constant refining and enhacement. It will start as a very understandble or clear language to both parties. But with constant knowledge crunching and information gathering, it will be come mush more robust and standard, and it will make future upgrades easier and quicker to understand.

**The language used to communicate with the domain experts to gather requirements and information, and the terms during our discussions, must be reflected as they are in our code**

