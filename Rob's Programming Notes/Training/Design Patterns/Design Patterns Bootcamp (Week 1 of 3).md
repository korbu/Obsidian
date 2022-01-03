# Design Patterns Bootcamp (Week 1 of 3)

**Created**: Wednesday, June 02, 2021 11:03:41 AM -04:00
**Modified**: Monday, January 03, 2022 10:30:21 AM -05:00


Wednesday, June 2nd, 2021, 11 am EST

Instructors: [Elisabeth Robson](https://www.amazon.com/Elisabeth-Robson/e/B001H6Q046%3Fref=dbs_a_mng_rwt_scns_share?sa-no-redirect=1&amp;amp;pldnSite=1) and [Eric Freeman](https://www.amazon.com/Eric-Freeman/e/B001H6Q032%3Fref=dbs_a_mng_rwt_scns_share?sa-no-redirect=1&amp;amp;pldnSite=1)

Facilitator: Lindsay Ventimiglia

https://learning.oreilly.com/attend/design-patterns-in-3-weeks/0636920054121/0636920054723/

![O&amp;#39;REILLY &#xA;Design Patterns in 3 Weeks &#xA;Presented by Elisabeth Robson and Eric Freeman &#xA;RETURN TO O&amp;#39;REILLY &#xA;Media Player &#xA;Live Online Training &#xA;All of the O&amp;#39;Reilly live training sessions are recordedNou will receive an e &#xA;with the recording within 2448 hours. You will also be able to the &#xA;recording by visiting the link that you used to join this session. &#xA;Resource List &#xA;o &#xA;Github &#xA;An Engineering Manager&amp;#39;s Guide to &#xA;Design Patterns &#xA;Slides - Week 1 Download here &#xA;with Eric Freeman &amp;amp; Elisabeth Robson &#xA;LIVE &#xA;e &#xA;DAY 1 &#xA;o ](/Attachments/1-933e5e7278e14b7c9e3e133a89f29255.png)
![All of the O&amp;#39;Reilly live training sessions are recorded. You will receive an email &#xA;with the recording within 24-48 hours. You will also be able to access the &#xA;recording by visäing the link that you used to join this session. ](/Attachments/1-2912f0cd71df417ea8034c8d2fa4e1d2.png)

GitHub:

https://github.com/bethrobson/Head-First-Design-Patterns

Book: &quot;An Engineering Manager's Guide to Design Patterns&quot;

https://learning.oreilly.com/library/view/an-engineering-managers/9781492048671/

Slides:

https://on24static.akamaized.net/event/30/40/47/9/rt/1/documents/resourceList1622135823035/week1designpatternsbootcamp3week1622135822545.pdf

1. [week1designpatternsbootcamp3week1622135822545 - slides.pdf](/Attachments/week1designpatternsbootcamp3week1622135822545---slides-1-91bb92fb7ff641d6881b31f25c3a88c2.pdf)
2. [week1designpatternsbootcamp3week1622135822545.pdf](/Attachments/week1designpatternsbootcamp3week1622135822545-1-91bb92fb7ff641d6881b31f25c3a88c2.pdf)

Recommended Preparation:

5. [Learning Object-Oriented Programming](https://www.oreilly.com/library/view/learning-object-oriented-programming/9781785289637/) (Calibre)
6. [Head First Design Patterns](https://www.oreilly.com/library/view/head-first-design/0596007124/)

Recommended Follow-up:

10. Take&#160;[Design Patterns Boot Camp II](https://learning.oreilly.com/live-training/courses/design-patterns-boot-camp-ii/0636920354826/)&#160;(live online training course with Eric Freeman and Elisabeth Robson)

From &lt;https://www.oreilly.com/attend/design-patterns-boot-camp/0636920057253/0636920351719/&gt;

14. Just changed from two day back to back course to a three week course.
15. https://WickedlySmart.com
16. Design patterns help with the structure of your application.
17. Your software needs to live for a lifetime.
    1. That lifetime tends to be much longer than you expect.
18. Elevator Pitch: Think of a design pattern as a general solution for a common object oriented problem.
19. They go into your brain before they go into your code.
    1. Once you understand them, bring them into your code.
20. They are general solutions.
21. Programmers have discovered these from very hard problems.
22. This is not about using code from other developers, but using a design from other developers.
23. This topic is like peeling an onion.
24. He would ask: what is in this for me?
    1. What can I expect to gain from this commitment?
    2. (See slide)
    3. Don't reinvent the wheel.
        1. We will see a design that gives us problems in a few minutes.
        2. Sometimes it takes a few iterations of your code or your entire product to get it right.
        3. We're leveraging the hard work of others to help ourselves.
    4. Designs are more maintainable and resilient to change.
        1. Change is the constant in software development.
        2. Design patterns protect you from changes to your code base in the future.
        3. Interesting side effect of design patterns: design principals.
            1. Little guidelines, pieces of advice.
            2. Basics of OO programming.
            3. Abstraction, inheritance.
            4. These are a layer above that.
        4. Encounter these patterns in other frameworks.
    5. When you and your team encounter this, all better.
        1. Shared knowledge.
25. Class (Cost?) diagrams
    1. Loosely diagrammed in UML.
    2. We don't always add the types to the properties.
    3. Subclassing, inheritance.
        1. Hollow arrow head.
    4. Overriding methods, adding new methods.
    5. Is a relationships.
    6. A dog is an animal.
    7. Abstract method in a class to leave out implementation.
        1. Italics in class diagram.
        2. Animal  can no longer be instatiated.
        3. Dotted line to other class.
    8. You can create an interface with a walk method.
        1. Not define walk.
        2. No properties in interfaces
26. Composition / Aggregation
    1. &quot;Has a&quot; relationship
    2. Filled in arrow head.
    3. Can an owner exist without an animal?
    4. Think animal and owner
    5. Think body and leg.
27. SimUDuck example
    1. Where do we need patterns?
    2. Ducks figure prominently in early design pattern literature.
    3. Abstract class Duck (name in italics)
    4. On the surface, it looks like a decent design.
    5. He thinks it's a decent design so far.
    6. It's not a disaster.
    7. Change in software design: a new requirement comes in.
        1. Make ducks fly.
        2. Your manager said no problem by next shareholder meeting.
    8. Something went horribly wrong, rubber ducks don't fly.
        1. Rubber duck may not be a great example, realistic, reasonable.
        2. Baby ducks cannot fly, maybe a better example.
        3. Demonstrates something else.
        4. Quack has been overridden to Squeak.
            1. Not a great solution.
    9. Where did this design go wrong?
        1. What are ways to solve this issue?
        2. Add flying and non-flying ducks.
        3. Two interfaces, one with flying and one with non-flying.
    10. Another change request comes in.
        1. Add a decoy duck, which is a wooden duck.
        2. Does not fly or quack.
        3. Override both methods to prevent bad behavior.
        4. May have to override to do nothing.
        5. Not great for reuse.
        6. Class answers:
            1. Inheritance hell.
            2. Not maintainable.
            3. Code duplication.
            4. Redundant code.
        7. Instructor answers:
            1. Code duplicated across subclasses.
            2. Runtime behavior changes are difficult.
                1. Behavior is hard-wired.
            3. Hard to gain knowledge
                1. Have to look at implementations of ALL ducks.
            4. Changes can unintentionally affect other ducks.
                1. No global view.
    11. Interfaces will help.
        1. Flyable
        2. Quackable
        3. Can be implemented by each child class.
        4. This seems like an improvement in some ways.
        5. What is biggest issue?
            1. We're shooting ourselves in the foot.
            2. Code duplication is the big issue here.
        6. Lots of subclasses have to reimplement methods from interfaces.
        7. We lost everything we were getting from inheritance.
        8. Our design is now more complex.
        9. That's okay if we get a lot out of it.
        10. But, we've gone sideways.
        11. Where does this leave us?
            1. Not all subclasses should have flying and quacking behavior.
            2. Inheritance is not the right answer.
            3. Destroyed code reuse.
            4. Maintenance nightmare.
        12. This is about as simple as it gets and we already have lots of problems.
    12. Someone out there has already documented this problem.
    13. <mark style="background: #BBFABBA6;">Design Principle: Identify the aspects of your application that vary and separate them from what stays the same.</mark> 
        1. Reuse where we can, but allow for variation.
        2. This applies to anything that changes when each new requirement comes in.
        3. Take the parts of your app that vary and separate them.
            1. This will stop affecting anything that is not strongly connected.
    14. Let's identify what's varying in the design now.
        1. We want to reuse quack and fly when it makes sense, but still allow ducks to quack and fly.
        2. There is a way to do this!
        3. (Quick break)
        4. Identify aspects of ducks that are varying.
    15. Create two sets of classes
        1. Flying behaviors
        2. Quacking behaviors
        3. Assign the correct version of each that applies to each duck.
        4. Create interfaces.
            1. FlyBehavior
            2. QuackBehavior
        5. These are interfaces that behaviors will implement, NOT that ducks will implement.
        6. FlyWithWings
        7. FlyNoWay
        8. Quack
        9. Squeak
        10. MuteQuack
    16. How do we put it all back together?
    17. Design Principle: Favor composition over inheritance.
        1. &quot;Has a&quot; is better than &quot;is a&quot;.
    18. What have we achieved?
        1. See slides.
        2. Much more flexible design.
        3. Easier to change.
        4. This is the Strategy pattern.
    19. The behaviors are algorithms to fly or quack.
    20. The duck is a client of these behaviors.
    21. Catalogs
    22. There is a spectrum of design patterns from abstract to not abstract.
        1. Strategy is very abstract.
        2. We'll look at Adapter soon and it's very easy to understand.
    23. Let's look at some code.
        1. Composition.
        2. The duck is delegating its fly and quack behaviors to other objects.
        3. Can change behaviors dynamically at run time if we wish, which is a good improvement.
        4. Good example of strategy pattern: tax app which handles different states.
        5. <mark style="background: #FFF3A3A6;">Search web for </mark><a href="https://www.bing.com/search?q=strategy+pattern+examples&amp;amp;cvid=f209421b3946400eb0e13333129affb3&amp;amp;aqs=edge..69i57j0l3.289j0j1&amp;amp;pglt=163&amp;amp;FORM=ANNAB1&amp;amp;PC=U531">strategy pattern examples</a>.
        6. Dependency injection.
            1. Pass behaviors in constructor.
28. Design Patterns: The Big Picture
    1. Christopher Alexander invented these.
    2. He's an architect.
    3. He wants to foster community in an apartment building.
    4. How can you build high density, but still have people interact.
    5. Patterns that occur over and over in our environment.
    6. Ward Cunningham and Kent Beck in late 80's started looking at this.
    7. OO programming was getting popular.
    8. Some of these problems needed solutions.
    9. The GoF wrote the book.
    10. This class is going to focus on the 23 patterns covered in this book, this catalog.
    11. There are also Enterprise Patterns books, etc.
29. Patterns in a catalog
    1. High level design that you can modify for your problem.
    2. See strategy pattern in slides.
    3. Categories for patterns.
        1. Creational
        2. Behavioral
        3. Structural
            1. Composition
        4. (These 3 are used in GoF book)
    4. (10 minute break)
30. How to be Adaptive
    1. Adaptor Pattern
    2. Think of a wall outlet.
    3. Can plug an adapter in to use a British wall outlet.
    4. What is this doing, in object oriented terms?
    5. Transforming
    6. Converting
    7. Interfacing
    8. Changing interface
    9. Delegating
    10. Mapping
    11. It's like a translator.
    12. Converting from one interface to another.
    13. Neither plug knows there's a translation going on.
    14. You can do this the wrong way (see slide)
        1. ![](/Attachments/1-9eeee1eb9d504213a0dfbdd278e892bc.png)
        2. Could be fragile or dangerous!
    15. Can connect your existing system to talk to vendor class.
        1. Insert an adaptor.
        2. ![Your &#xA;Existing &#xA;System &#xA;Your &#xA;Existing &#xA;Systm &#xA;Your &#xA;Existing &#xA;System &#xA;Adapter &#xA;Adapter &#xA;Vendor &#xA;Class &#xA;Vendor &#xA;Class &#xA;Vendor &#xA;Class ](/Attachments/1-602a600df4264a3b8d92be85d648ef47.png)
        3. Could require multiple calls to meet the original interface.
    16. Homework
        1. <mark style="background: #FFF3A3A6;">Check out the façade pattern.</mark>
        2. Wraps a complicated subsystem.
        3. Make it simple to use for customers.
        4. Customer just interacts with the fa&#231;ade, not the actual interfaces.
        5. Fa&#231;ade helps to isolate customer from changes in the original APIs.
31. Design Principles
    1. What are design principles?
        1. General guidelines to avoid bad OOP designs.
        2. Keep your designs flexible, resilient, reusable.
        3. Some are more important than others.
    2. OO Basics vs. Principles
        1. ![ssep &#xA;sQ\sea OO ](/Attachments/1-45985290dda04f52a4890ef9a99a4532.png)
        2. Dependency inversion principle.
        3. Last one is single responsibility principle.
            1. If a class has multiple responsibilities, then more pressure on that class.
32. Program to Interfaces
    1. Program to an interface, not an implementation.
33. Open/Closed Principle
    1. Classes should be open for extension but closed for modification.
    2. We spent a lot of time getting this code correct and bug free.  Don't modify it!
    3. There are clever OO techniques for this.
    4. Patterns that work.
    5. The next pattern in the next class is the decorator pattern, which demonstrates this.
34. Loose Coupling
    1. Strive for loosely coupled designs between objects that interact.
    2. You can create a fragile and breakable system.
    3. Also see the Observer pattern.
    4. You may have used it even without knowing it.
    5. Notifications, events, state changes.
    6. Objects can go away without breaking something.
35. Single Responsibility Principal
    1. A class should have only one reason to change.
    2. Keep classes focused on one thing.
    3. Try to make class responsible for just one thing.
    4. May have to change this, but won't have to make changes all over our code if we do.
36. We're going to see examples where we move from designs where we do too much in a single class and move to single responsibility principal.
37. SOLID Principles
    1. Well known set of principals
    2. ![Single Responsibility Principle &#xA;Open/Closed Principle &#xA;LISkov Substitution Principle &#xA;Interface Segregation Principle &#xA;Dependency Inversion Principle ](/Attachments/1-9d5ca7663ab841a185712cd3ceb8edff.png)
    3. Liskov - don't make a special case out of one of the subclasses.
    4. Interface - don't make code in subclasses that we don't use
    5. Dependency inversion - depend on abstractions, not concrete classes.
        1. Abstraction is like a super type.
    6. We don't talk about DRY in this course at all, but you should learn about it.