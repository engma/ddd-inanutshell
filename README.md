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
* Used when dealing with legacy subsystems that provide a very messy and fuzzy interface that we have to cope with
* Consists of Facades, Adapters, and translators
* *The Facades* will provide a better interface to the legacy app/system, they will use its model (the model of the legacy app). They will provide the needed functionality and will hide the rest, they will also hide the complicated interface of the other system.
* Facades **must** comply with the other systems model, they are not another layer of modeling, they are merely a friendlier interface
* *The Adapters* will convert requests from our app to the legacy apps interface and then pass them to the *facades*, they will then convert the response to something that our app can understand
* There will one adapter per each service which communicates with the other system
* Adapters only know how to convert requests and responses
* The task of converting between data models is complicated and could be common across our adapters, adapters will typically use one or more data models of the two systems to achieve their job, therefore they use *Translators*
* *Translators* handle conversions between data models of the two systems
#### Notes on Anticorruption Layer
1. If the other system has a clean interface, you may not need the Facades
2. You may need to change your model a little bit to minimize the translations if the two systems are very different, but do it with care and make sure you don't compromise the integrity of your model
3. In case you have access to the other system, doing some refactoring might be useful to support the translations

### 5. Separate Ways
* The apps will not share anything and will have very little to no data exchange, each one of them will function independently from the other apps
* They could share the same access layer or middleware layer, but each of them will execute within its own bounded context
* Used when integration does not provide many benefits to the system and could make the models complex or add a useless translation layer overhead

### 6. Open Host Service
* Provide your app's functionality as a public interface for all the required integration apps
* This interface should be updated and modified regularly to accommodate to new integration needs
* For specific integration requests you can create a separate translation layer for that case only, but the public protocol should stay the same
* Ideal for cases when you have a core service that needs to be accessed by many other services

### 7. Published Language
* When a shared service is accessed by many services, it may need to publish a common language/contract for all of them to understand
* That language would the actual representation of the domain model which satisfies all the services
* Each consuming service would probably have its own idea of what the service's model is, but this understanding could be wrong
* The published language would help the clients of the service reach a common understanding of the domain and use a single representation
* Creating this language is not an easy task, it takes a lot of takes and refinements with the consumers of the service
* In some cases a common language might already exist which we can just use with our clients, like a well-known domain language which is already used between the services clients

------

## Domain Distillation Techniques
The **Core Domain** of your system will be mostly hiding within a lot of other domains which are all important for the system to function correctly but are not the main focus of the system.
Discovering the core domain requires some distillation techniques and tools to uncover it and possible isolated.

### 1. Generic Subdomains
Generic Subdomains are the parts of your system which are challenging and required but they are not the core of the domain.

An example would be a calculation algorithm of some sort, that calculates values for reports in a car rental application. This domain, however important it might seem, is not the core domain of the application. It might seem intriguing to invest our best developers in this algorithm but that would risk our core domain being handled by developers who are not the top notch of their game.

We have several solutions to this problem:

1. **Using of The Shelf Software**: We might be lucky enough to find a generic solution that is readily available which implements our generic problem, for example, in our reporting domain, we might find a generic reporting app that does that calculation for us. The downsides would be

    a. Integration of that piece of software with our system might not be easy
  
    b. It might be too generic and contains more power than we need
  
    c. We might be tied to it without much benefit
2. **Using a Generic/Standardized Domain Model**: If our problem already has a standardized or generic domain model which is battle tested in other software and we can reuse that subdomain in our app, then we can apply that to our model and implement it in this way, the downsides are:
    
    a. We might not be using all of the domain models
    
    b. The domain model might not match our domain completely and our domain model might lose some of its specific capabilities because of this adaptation

3. **Outsourcing The Subdomain**: We might consider outsourcing that part of the app to a third party company to handle it's development for us, thus relieving our top developers from it and focusing our best assets on the core domain, this also has some downsides like
    
    a. Coordination between both teams will take sometime
    
    b. Adaptation of the other team to our domain model might be as adequate as we expect, so we need to have a lot of acceptance tests and automated tests to verify the product
    
    c. Moving the handling of that subdomain to our development will not be easy because they need to understand a new code written by another team
    
    d. Code quality of the product will be good or bad depending on the expertise of the outsource team
    
4. **In-house development**: Finally we can resort to developing those parts ourselves, this will make the development tailored specifically for our problem domain and needs, we don't get any more than we need, integration with our core domain will be smoother as we are the owners of both services, however, this has several disadvantages, mainly:

    a. We will need a team to maintain this service, it will need to be updated and integrated regularly
    
    b. Some readily available software might have solved the problem
    
    
### Domain Vision Statement
* A statement of what the system will be solving and it's expected behaviors
* Must be specific to the domain and not the technicalities
* Acts as a guideline of the overall direction of the system and it's main and core purpose
* Illustrates the core domain of the system and the main business or added value of the domain
* Regularly updated as we get more insights about the domain and update our model

