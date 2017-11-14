# Domain Driven Design in a Nutshell
This is a brief summary of what domain-driven design is and what are it's building blocks, it is meant to serve as a quick reference for DDD, for more detailed information:
* [Domain Driven Design Distelled by Vaughn Vernon](https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/ref=sr_1_sc_1?ie=UTF8&qid=1499649365&sr=8-1-spell&keywords=domain+driven+design+distelled)
* [Domain Driven Design by Eric Evans](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/ref=sr_1_1?ie=UTF8&qid=1499649453&sr=8-1&keywords=domain+driven+design)

______
## Domain Experts
Those are the individuals who have a great deal of familiarity with the domain which the software is trying to solve a problem for. For example, if we were making a software for medical information, then the doctors would be our domain experts, if we were making a software for hotel reservations, the hotel managers would be the experts of this domain.

**They are the ones who carry the knowledge which defines the problem and what the output of the software should be in order to be considered a complete solution, and they can define acceptance tests for this software**

## Ubiquitous Language

The **Language**: Languages are some set of characters/phrases arranged together to define a meaning that is understandable by someone or something that can parse those phrases. When developing software it is important that the *domain experts* and the *developers* would create a language of expressions and common phrases that define the system's model and interactions.

For example, in a hotel booking app, the term *a Booking* would be an agreed upon term that is both understandable for both the experts and the devs, whenever any of them needs to exchange a piece of information about booking manipulation, they would use the term *a booking*, also when a user *books* a *booking* we use the term *books* to refer to this activity.

The Ubiquitous language **MUST be used as it is in our code**. Developers are not allowed to change the terms to more technical one, like using BookingTable or BookingEntity. It must be the same language used by the experts. The same goes for the activities or the interactions which our objects do. So for example, in our code, the user would *book* a booking using the *BookingService*. We could have called it *create* a booking in the code to be a more technical term, but in that case, we lost our domain based language.

The Ubiquitous Langauge guarantees that our code is a complete reflection of what our experts have in mind, it also ensures that the developers know exactly how the system components interact with each other in regards to the real world problem. This will make it easier to spot the gaps or the differences between what we have and the real world, as well as being able to continuously refine our code to get a more concrete representation of the problem domain.

This language will be under constant refining and improvement. It won't be a very understandable or clear language to both parties at the beginning. But with constant knowledge crunching and information gathering, it will become much more robust and standard, and it will make future upgrades easier and quicker to understand.

**The language used to communicate with the domain experts to gather requirements and information, and the terms during our discussions must be reflected as they are in our code**
