# Domain Driven Design in a Nutshell
This is a brief summary of what domain-driven design is and what are it's building blocks, it is meant to serve as a quick reference for DDD, for more detailed information:
* [Domain Driven Design by Eric Evans](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/ref=sr_1_1?ie=UTF8&qid=1499649453&sr=8-1&keywords=domain+driven+design)
* [Domain Driven Design Distilled by Vaughn Vernon](https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/ref=sr_1_sc_1?ie=UTF8&qid=1499649365&sr=8-1-spell&keywords=domain+driven+design+distelled)

______
## Domain Experts
Those are the individuals who have a great deal of familiarity with the domain which the software is trying to solve a problem for. For example, if we were making a software for medical information, then the doctors would be our domain experts, if we were making a software for hotel reservations, the hotel managers would be the experts of this domain.

**They are the ones who carry the knowledge which defines the problem and what the output of the software should be in order to be considered a complete solution, and they can define acceptance tests for this software**

## Ubiquitous Language

**The Language**: Languages are some set of characters/phrases arranged together to define a meaning that is understandable by someone or something that can parse those phrases. When developing software it is important that the *domain experts* and the *developers* would create a language of expressions and common phrases that define the system's model and interactions.

For example, in a hotel booking app, the term *a Booking* would be an agreed upon term that is both understandable for both the experts and the devs, whenever any of them needs to exchange a piece of information about booking manipulation, they would use the term *a booking*, also when a user *books* a *booking* we use the term *books* to refer to this activity.

The Ubiquitous language **MUST be used as it is in our code**. Developers are not allowed to change the terms to more technical one, like using `BookingTable` or `BookingEntity`. It must be the same language used when communicating with the experts and the language that the experts would understand. The same goes for the activities or the interactions which our objects do, those interactions need to be labeled with the same terms that we use during our communications. So for example, in our code, the user would `book` a booking using the `BookingService`. We could have called it `create` a booking using the `BookingDB` class in the code to be more technical, but in that case, we lost our domain based language. And the information that we acquired from the experts is no longer visible in our code.

The Ubiquitous Langauge guarantees that our code is a complete reflection of what our experts have in mind, it also ensures that the developers know exactly how the system components interact with each other in regards to the real world problem. This will make it easier to spot the gaps or the differences between what we have implemented and the real world representation of the model, as well as being able to continuously refine our code to get a more concrete representation of the problem domain.

This language will be under constant refining and improvement. It won't be a very understandable or clear language to both parties at the beginning. But with constant knowledge crunching and information gathering, it will become much more robust and standard, and it will make future upgrades easier and quicker to understand.

**The language used to communicate with the domain experts to gather requirements and information, and the terms during our discussions must be reflected as they are in our code**


## Bounded Contexts
Bounded contexts are, in their hearts, the application of the **Separation of Concerns** principle on the domain level.
Mainly we would group and collect together relative parts of the overall domain model which represent a single complete context or functionality of the system. 

Continuing with our hotel booking app example, here we have two separate functionalities, which are 1)searching for a room 2) and booking a room in a hotel. So you have two separate contexts one of them is the *search* context and the other is the *booking* context. Each of them would have its own model representation and domain objects. 

Although they may share some concepts, they will have a different representation of those concepts. For example, they both have the concept of a **room**, but in the context of *searching*, the room is an item in a list which adheres to the search criteria provided. While for the *booking* context a room is an item booked for a certain period by a certain client with certain options or added features. The search doesn't need to represent the client-room relation, but it needs to represent all the room's features in order to query them. On the other hand, the booking doesn't need to represent all the room's features which are necessary for searching, it can just use a room type and night rate to represent it's room data, but it's more concerned with the user's info and the payment method for example.

These subtle distinctions between what a room is in different contexts are really important in defining the context's boundaries and the relations between different contexts.
Those two contexts will need to share some data between each other in order to complete the overall system functionality which is booking a hotel room. This will call for some translations between the two contexts, which we will discuss in the next section.

## Context Maps

Bounded context will always need to communicate and/or exchange information, to achieve this we have several patterns which can apply, not all the patterns will be applicable to your situation, so it needs a lot of work and design analysis to choose a pattern.

### 1. Shared Kernel

* Involves sharing a piece of functionality between two contexts, this can be a library or a shared piece of code
* The two contexts will share a subset of the domain, as well as Database design and all the related shared functionality
* Changes to this shared kernel is not easy because it involves discussions and communications between the teams involved
* All the teams should be in a homogeneous relation and their work should be easily coordinated, ideally they should be close in range to each other and part of the same department/group
* The **Shared** part should be as limited as possible, so that it's impact would be small to the changes and needs of both apps
* Continous integration must be done regularly with all apps involved with every change made to the shared kernel

### 2. Customer/Supplier 

* One app context will be the provider of the data and the other will be the customer of this data. The upstream will treat the downstream team as a customer which has specific needs to be provided
* The downstream team will always be treated as a customer and its requirements will be considered as customer requirements
* The upstream team will use some automated tests to ensure that each change doesn't break the downstream apps
* Discussion involving changes in functionality will likely include a representative of the downstream teams as the customers of the app
* Different demands of different customers to the supplier app have to be balanced and standardized during the discussions

### 3. Conformist
* The upstream app cannot be modified to the needs of the downstream
* The upstream app is vital for the downstream
* The downstream app has a shared model with the upstream
* The downstream app will conform to the model of the upstream in how it is represented
* This could lead to better design for the downstream app that matches the domain model in a more coherent way

### 4. Anticorruption Layer
