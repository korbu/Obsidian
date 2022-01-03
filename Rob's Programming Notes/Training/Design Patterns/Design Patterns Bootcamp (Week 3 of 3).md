# Design Patterns Bootcamp (Week 3 of 3)

**Created**: Wednesday, June 16, 2021 11:01:38 AM -04:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


Wednesday, June 16th, 2021, 11 am EST

Instructors: [Elisabeth Robson](https://www.amazon.com/Elisabeth-Robson/e/B001H6Q046%3Fref=dbs_a_mng_rwt_scns_share?sa-no-redirect=1&amp;amp;pldnSite=1) and [Eric Freeman](https://www.amazon.com/Eric-Freeman/e/B001H6Q032%3Fref=dbs_a_mng_rwt_scns_share?sa-no-redirect=1&amp;amp;pldnSite=1)

Facilitator: Lindsay Ventimiglia

https://learning.oreilly.com/attend/design-patterns-in-3-weeks/0636920054121/0636920054723/

An Engineering Manager's Guide to Design Patterns

https://learning.oreilly.com/library/view/an-engineering-managers/9781492048671/

[An Engineering Manager&amp;#8217;s Guide to Design Patterns - An Engineering Manager's Guide to Design Patterns.pdf](/Attachments/An-Engineering-Manager&amp;amp;#8217;s-Guide-to-Design-Patterns---An-Engineering-Manager&amp;#39;s-Guide-to-Design-Patterns-1-28c497ffd6624637b194da1aff8d8c20.pdf)

Slides:

https://on24static.akamaized.net/event/30/40/48/3/rt/1/documents/resourceList1622663089929/designpatternsbootcamp3weekspart2padding1622663089079.pdf

[week3designpatternsbootcamp3week1623264322559.pdf](/Attachments/week3designpatternsbootcamp3week1623264322559-1-c10afed329da4c58b0eb3839fa89e971.pdf)
Errata Page:

http://oreilly.com/catalog/0636920367598/errata

Supplemental Content:

https://www.wickedlysmart.com/head-first-design-patterns/

Recording:

https://learning.oreilly.com/attend/design-patterns-in-3-weeks/0636920054121/0636920054723/

1. ![What are two patterns that you are probably already &#xA;using today? (hint: one is a language feature) &#xA;What pattern makes use of a surrogate object? &#xA;What design principle does the decorator pattern most &#xA;make use of? ](/Attachments/1-3d0a4564d3ca41e6a3f03a62d3df8756.png)
2. We are probably using iterator in our code already today.
3. Also observer.
4. Both show up all over the place.
5. Iterator shows up in languages.
6. Observer shows up in language frameworks, Swing, event handlers.
7. Surrogate
    1. Proxy Pattern
8. What uses Decorator pattern
    1. Open Closed
    2. Encapsulate what varies
    3. Composition over inheritance is huge.
9. Singleton Pattern
    1. The one of a kind pattern.
    2. Interview question in Java hey day: implement singleton pattern
10. ![NO.LTIONIS ](/Attachments/1-a4b854c865fb49ad9ef7728550407e22.png)

11. ![How do we create a single object? &#xA;new MyObject(); ](/Attachments/1-f06adb4e560343e0b24a5a02b94cdf24.png)

12. ![How do we create a second object? &#xA;new MyObject(); &#xA;new MyObject(); ](/Attachments/1-cd2021e8888b438d941ad2788d6e0c26.png)
13. Violation!
14. Bugs often result from having more instances than you realize.
15. Never a second instance (or more)
16. ![In Java, a public class typically has &#xA;a public constructor method: &#xA;public MyCIass { &#xA;public MyCIass() { &#xA;// code here &#xA;// other methods here ](/Attachments/1-22631c2c7c85452f91f9a8131c88f903.png)
17. This cannot be a singleton with a public constructor.
18. ![You can make a constructor &#xA;private instead. &#xA;public MyC1ass { &#xA;private MyC1ass() { &#xA;// code here &#xA;// other methods here ](/Attachments/1-b663a46d55c44d4ab6f11aeedaa32473.png)
19. How do you make one of these if the consturctor is private?
20. Attendees suggested using a static method.
21. ![To make an instance, we have to &#xA;call the constructor from MyClass &#xA;public MyC1ass { &#xA;private MyCIass() { &#xA;public static MyC1ass getlnstance() { &#xA;return new MyC1ass(); &#xA;// other methods here ](/Attachments/1-e706564544454bd1ba2f313eb88ff063.png)

22. ![To call a class method: &#xA;public MyCIass { &#xA;private MyCIass() { &#xA;public static MyC1ass getlnstance() { &#xA;return new MyC1ass(); &#xA;myC1ass singleton = MyC1ass.getInstance(); ](/Attachments/1-519953b305cd473c82fe876e9817a572.png)

23. ![Make sure there&amp;#39;s only one! &#xA;public MyC1ass { &#xA;private static MyCIass uniquelnstance; &#xA;private MyC1ass() { } &#xA;public static MyCIass getlnstance() { &#xA;if (uniquelnstance null) { &#xA;uniquelnstance = new MyCIass(); &#xA;return uniquelnstance; ](/Attachments/1-458ae8de625e460494d4896c40f71192.png)
24. This implementation is a B+.
25. Runs into thread safety issues.
26. Two threads could create two instances before uniqueInstance is not null.
27. Rogue singleton.
28. ![Be careful in multi-threaded &#xA;environments &#xA;public MyC1ass { &#xA;private static MyCIass uniquelnstance; &#xA;private MyC1ass() { } &#xA;public static synchronized MyC1ass getlnstance() &#xA;if (uniquelnstance &#xA;null) { &#xA;uniquelnstance &#xA;= new MyCIass(); &#xA;return uniquelnstance; ](/Attachments/1-9b6e45c2dc7c4df1b804d2876c7e8c28.png)
29. This would get you an A.
30. There is a way to get an A+ in Java.
31. Hint: look up volatile.  It's in the book.
32. ![An easier way in Java &#xA;public enum Singleton { &#xA;UNIQUE_INSTANCE; &#xA;public String getDescription() { &#xA;return "I&amp;#39;m a thread safe Singleton! " ; &#xA;public class SingletonC1ient { &#xA;public static void main(String\[\] args) { &#xA;Singleton singleton = &#xA;Singleton. UNIQUE_INSTANCE; &#xA;System. out. println( singleton. getDescription ( ) ) ; ](/Attachments/1-bb9be3c48b52458081616d7c1666b006.png)
33. Be careful with the above if serializing and deserializing.
34. ![Watch your design principles... &#xA;Design Principle &#xA;Strive for loosely coupled &#xA;designs between objects &#xA;that interact. ](/Attachments/1-7c557603c0f6480f845c9c302c937a88.png)
35. Your code may depend on a singleton and changes to it could cause problems throughout your code.
36. Prototype Pattern
    1. Prototypical Creation
    2. Copies objects instead of creating them from scratch.
    3. Clone object.
        1. Customize it?
    4. ![](/Attachments/1-6917345c2646498d98d33a79b3d08e3d.png)
    5. ![What&amp;#39;s good about the &#xA;Prototype Pattern? &#xA;• Separates the client from the details of object &#xA;creation and representation. &#xA;• Helps when the cost of creating an object is &#xA;complex or expensive. Hides complexity of object &#xA;creation. &#xA;• Can allow you to minimize the number of classes &#xA;and reduce need for subclassing. &#xA;• Clients can create new objects without needing to &#xA;know the concrete type. ](/Attachments/1-3796cd24b05b4641a8704498333802ce.png)
    6. ![](/Attachments/1-0128ed11d21541388acc2bcd01e85e7c.png)
    7. ![Prototype Pattern Structure &#xA;Client &#xA;Operation() &#xA;p = prototype. clone ( ) ; &#xA;ConcretePrototype 1 &#xA;clone() &#xA;o &#xA;return copy Of this &#xA;o &#xA;copy Of this ](/Attachments/1-11ef9b8641364ffc94fa7fd339ef9d91.png)
    8. Some patterns are different based on the language you're using.
        1. Singleton and Prototype both fall into this category.
    9. ![How do we Clone? &#xA;Obj b &#xA;a. clone ( ) &#xA;* There are lots of implementation caveats!! ](/Attachments/1-a77a29b5adb84778be2967b5ad7d4a96.png)
    10. Will it be a shallow copy or a deep copy?
    11. Implement cloneable interface.
    12. ![MYC lass &#xA;MyC1ass a = new MyC1ass(); &#xA;// complex set up code &#xA;= new MyC1ass(); &#xA;MyC1ass b &#xA;// repeat complex set up code ](/Attachments/1-95af1a30732f45d3b74994e516c90f1b.png)
    13. Network objects are often complex classes and are complex to set up.
    14. ![MyC1ass &#xA;MyC1ass a = new MyC1ass(); &#xA;// complex set up code &#xA;= a. clone(); &#xA;MyC1ass b &#xA;// no set up needed ](/Attachments/1-8cc2c7efaba449e895ffb4748304dba4.png)
    15. ![Using copies without knowing the &#xA;concrete type &#xA;Client &#xA;Operation() &#xA;o &#xA;p prototype. copy ( ) ; &#xA;Prototype &#xA;C oncretePrototype1 &#xA;copy() &#xA;o &#xA;return clone of this &#xA;Concrete prototype2 &#xA;copy() &#xA;o &#xA;return clone of this ](/Attachments/1-495e49c07c2c4a8a8b8b705a81fbdfb5.png)
    16. Changed from clone to copy because Java has a clone method.
    17. ![Using copies without knowing the &#xA;concrete type &#xA;public class Client { &#xA;public static void args) { &#xA;Prototype pl • new Concreteprototypel(); &#xA;Prototype p2 new ConcretePrototype2(); &#xA;. later . &#xA;operation (PI) ; &#xA;operation(p2) ; &#xA;public static Prototype operation(prototype p) { &#xA;prototype pC0py null; &#xA;try { &#xA;pCopy p.copy(); &#xA;System "Operating With pCopy!"); &#xA;catch (CloneNotSupportedException e) { &#xA;e. printStackTrace() ; &#xA;return pCopy ; ](/Attachments/1-fda3642763834003a8bb010f68dc85bb.png)
    18. Programming to the interface, not the implementation.
37. Factory Pattern
    1. Encapsulating Object Creation
    2. There are 3 forms of Factory Pattern
    3. It would take half a day to cover these.
    4. ![Design Principle &#xA;Program to an interface &#xA;not an implementation. &#xA;Question: We aren&amp;#39;t supposed to program to &#xA;an implementation, but every time we use new, &#xA;that&amp;#39;s exactly what we&amp;#39;re doing, right? ](/Attachments/1-4ee2a797b7bc44eeae0236b10ab48378.png)
    5. Every time you see a new operator, you're violating this to some extent.
    6. ![The new Conundrum ](/Attachments/1-a33bc2f4612240fcbd477c738614f35d.png)
    7. ![The new Conundrum &#xA;Pizza orderPizza() { &#xA;= new Pizza(); &#xA;Pizza pizza &#xA;pizza. prepare() ; &#xA;pizza. bake(); &#xA;pizza. cut(); &#xA;pizza. box(); &#xA;return pizza; &#xA;..but our concrete classes are CheesePizza, VeggiePizza, etc. ](/Attachments/1-50270b7935ae4a56962f8abe8b282b21.png)
    8. ![Coping Strategy &#xA;Pizza orderPizza(String type) { &#xA;Pizza pizza; &#xA;if (type. { &#xA;pizza = new CheesePizza(); &#xA;} else if (type. { &#xA;pizza &#xA;= new PepperoniPizza(); &#xA;} else if (type. { &#xA;pizza = new ClamPizza(); &#xA;} else if (type. { &#xA;pizza = new VeggiePizza(); &#xA;pizza. prepare( ) ; &#xA;pizza. bake(); &#xA;pizza. cut(); &#xA;pizza. box(); &#xA;return pizza; ](/Attachments/1-7bbbe20b07d84885b55922fa520096ac.png)
    9. Change is constant in software development.
    10. ![What about Change? &#xA;Pizza orderPizza(String type) { &#xA;Pizza pizza; &#xA;if (type. { &#xA;pizza = new Cheesepizza(); &#xA;} else if (type .equals( "greek") { &#xA;pizza = new GreekPizza(); &#xA;} else if (type. { &#xA;pizza = new PepperoniPizza(); &#xA;} else if (type { &#xA;pizza = new Veggiepizza(); &#xA;// IMPORTANT CODE HERE (order, prepare, &#xA;etc) ](/Attachments/1-d36df045a922407a9f716830750e6b1e.png)
    11. ![ExeRciSQ &#xA;How might you take all the parts of &#xA;your application that instantiate &#xA;concrete classes and separate or &#xA;encapsulate them from the rest of &#xA;your application? ](/Attachments/1-7db2c7bd9b9045d38cf3faaf1c15648e.png)
    12. ![Let&amp;#39;s Encapsulate &#xA;Object Creation &#xA;if (type. equals("cheese")) { &#xA;pizza &#xA;new Cheesepizza(); &#xA;} else if (type. equals("pepperoni") { &#xA;pizza new Pepperonipizza(); &#xA;} else if (type. equals("veggie") { &#xA;pizza = new Veggiepizza(); &#xA;Pizza orderPizza(String type) { &#xA;Pizza pizza; &#xA;pizza. prepare(); &#xA;pizza. bake(); &#xA;pizza. cut(); &#xA;pizza . box(); &#xA;return pizza; ](/Attachments/1-561ff3ec4fd84f45b004ef57ed9ff461.png)
    13. ![The Pizza Factory &#xA;public class SimplePizzaFactory { &#xA;public Pizza createPizza(String type) { &#xA;Pizza pizza = null; &#xA;if (type { &#xA;= new CheesePizza(); &#xA;pizza &#xA;} else if (type { &#xA;pizza &#xA;= new PepperoniPizza(); &#xA;} else if (type { &#xA;pizza = new VeggiePizza(); &#xA;return pizza; ](/Attachments/1-d04c570220214d57b65d19e5a941148b.png)
    14. ![The New Pizza Store &#xA;public class PizzaStore { &#xA;SimplePizzaFactory factory; &#xA;public PizzaStore(Simp1ePizzaFactory factory) { &#xA;this. factory = factory; &#xA;public Pizza orderPizza(String type) { &#xA;Pizza pizza; &#xA;pizza = factory. createpizza(type); &#xA;pizza. prepare(); &#xA;pizza. bake(); &#xA;pizza.cut(); &#xA;pizza. box(); &#xA;return pizza; ](/Attachments/1-13a14c03b29249b1984b6aea5755cba0.png)
    15. This is the simple factory pattern.
        1. Not one of the original GoF patterns.
        2. That's why pattern is in quotes, below.
        3. But a very common way to create objects.
    16. ![The Simple Factory "Pattern" ](/Attachments/1-e4623c4e3b564526a26cfcdafaff285d.png)
    17. Principles
        1. SRP
        2. Programming to interface
        3. Loose coupling
        4. Encapsulating what varies
    18. ![What if we want to franchise? &#xA;PizzaStoe ](/Attachments/1-229019c6cf36431aad2aaf0467dc3727.png)
    19. The Factory Method pattern will solve this.
    20. ![Factory Method Pattern &#xA;Factory Method Pattern: Define an interface for &#xA;creating an object but let subclasses decide which class &#xA;to instantiate. Factory Method lets a class delegate &#xA;instantiation to the subclasses. ](/Attachments/1-dabed08b785f4c53a03204bf3d7182ca.png)
    21. Similar to overriding methods/algorithms in our classes.
    22. ![The Factory Pattern applied to Pizza &#xA;CheesePizza &#xA;Pizza Store &#xA;orderPizza() &#xA;NYPizzaStore &#xA;createPizza() ](/Attachments/1-3ee002702bb1452e84f59a0fe7050c49.png)
    23. ![A Framework for Pizza Creation ](/Attachments/1-8c572de43edd4293a450faa4f3382a83.png)
    24. Leave common details in the super classes, stays shared.
    25. Abstract Factory Pattern
    26. ![Abstract Factory Pattern &#xA;Abstract Factory Pattern: Provide an interface for &#xA;creating families of related or dependent objects without &#xA;specifying their concrete classes. ](/Attachments/1-d180b47bf6074f9eaae5095fc9f48da5.png)
    27. ![Abstract Factory&amp;#39;s Structure ](/Attachments/1-c46dcd0df72a4969bcabc031917423b3.png)
    28. Client uses the factory.
    29. Isolates concretes classes.
    30. Adds layers of abstraction.
    31. Exchange families of products.
    32. Similarities between simple factory and strategy.
    33. Think back to duck example from first day of class.
    34. Eric's comparison to template method.
    35. Falls into class category of patterns vs. object category of patterns.
38. Builder Pattern
    1. Building objects
    2. Very different from Factory.
    3. More about construction of objects.
    4. ![](/Attachments/1-f6f7e394313543eea5581295a07ad735.png)
    5. The intent is not crystal clear at first.
    6. It wasn't for Eric.
    7. ![Builder Pattern Structure &#xA;constuct() O ](/Attachments/1-0207fcb5a23d48c180fb7fe35be5a334.png)
    8. The key or gist is that it can build different representations.
    9. ![House Builder &#xA;Hase &#xA;atfWaIIsO &#xA;a%WaWWaII w") ](/Attachments/1-b83d4d1213304ad6a757022ba2abd85a.png)
    10. ![House &#xA;public class { &#xA;String name; &#xA;&amp;#39;buseType houseType; &#xA;walls; &#xA;public { &#xA;YR»use addROOf(Roof roof) { &#xA;this. roof • roof; return this; &#xA;House wall) &#xA;this.walls.add(uall); return this; &#xA;ndOw) &#xA;this .windous.add(uindou); return this; &#xA;public String toString() &#xA;n... ](/Attachments/1-0b8092460b1541afb660e52232f5a974.png)
    11. ![HouseBuilder &#xA;public abstract class House8uiIder &#xA;String builderName; &#xA;enum { &#xA;WOOD, CLAY. GINGERBREAD. STONE &#xA;House house = new House(); &#xA;public void setHOuseType(HOuseType houseType) { &#xA;house. setHouseType (houseType ) ; &#xA;// Each method in the Builder returns the guilder so "e can use the Fluent Interface Pattern &#xA;public abstract &#xA;public abstract HouseBuiIder &#xA;public abstract addRCX&amp;#39;f(); ](/Attachments/1-fe2e775706f14245ad881cd2671763c9.png)
    12. ![GingerbreadHouseBuilder &#xA;public class GingerbreadtøuseBuiIder extends &#xA;int • 4 &#xA;int 4; &#xA;String wimio*aterial • &#xA;String &#xA;• •Gingerbread and Icing • ; &#xA;String • Twizzlers•; &#xA;this.builderName •Gingerbread &#xA;Se . GINGERBREAD) &#xA;public ) ( &#xA;for (int i • e; i &#xA;System. out. out of &#xA;return this; &#xA;public HouseBui1der ) ( &#xA;for (int B; i &#xA;System. out. made out of &#xA;return this; &#xA;public House build() &#xA;everything together with icing"); &#xA;re turn ](/Attachments/1-8885f249847e48bcbbbcf6c1659b614e.png)
    13. ![Test the House &#xA;public class HouseDirector { &#xA;public static void args) { &#xA;HouseBui1der woodHouseBui1der new WoodHouseBui1der(); &#xA;House woodHouse &#xA;woodHouseBui Ider. addWa1 Is ( addWindows(). addRoof( ) . build( ) ; &#xA;System. out. printl n (woodHouse) ; &#xA;HouseBui1der clayHouseBui1der = new ClayHouseBuiIder(); &#xA;House clayHouse &#xA;clayHouseBui Ider. addWa1 addWindows( addRoof() . build( ) ; &#xA;System. out. println( clayHouse) ; &#xA;HouseBui1der gingerbreadHouseBui1der = new GingerbreadHouseBui1der(); &#xA;House gingerbreadHouse = &#xA;gingerbreadHouseBui Ider. ( ) . ) . addR00f( ) ; &#xA;System. out. printi n (gingerbreadHouse) ; ](/Attachments/1-0c61cee91e994e8c8b57f9efefb3b506.png)

    14.
    15. ![What design principles does the &#xA;ExegciSe Builder pattern embody? &#xA;00 &#xA;Encapsulate what varies &#xA;• Loose coupling &#xA;Open-Closed ](/Attachments/1-69edf6e2c28f4273ae0c90a06d4226af.png)
    16. Is string builder in Java actually a builder?
    17. ![StringBuilder &#xA;StringBui1der sb new StringBui1der(); &#xA;sb.append("Testing String Builder\n" &#xA;. append ( nyPizza ) &#xA;.insert(e, " &#xA;System. out. Of the String &#xA;Builder: + sb. length()); &#xA;Of the String &#xA;Builder: + sb. tostring()); ](/Attachments/1-53eb522bf77845388b229ea128e9566d.png)
    18. It does not provide abstract API with multiple abstractions.
    19. Not really the builder pattern.
    20. ![Comparing Builder to Decorator &#xA;and Factory &#xA;Builder: Separate the construction of a complex object from its &#xA;representation so that the same construction process can create &#xA;different representations. (Creational) &#xA;Factory Method: Define an interface for creating an object, but let &#xA;subclasses decide which class to instantiate. Factory Method lets &#xA;a class defer instantiation to subclasses. (Creational) &#xA;Decorator: Attach additional responsibilities to an object &#xA;dynamically. Decorators provide a flexible altemative to &#xA;subclassing for extending functionality. (Structural) ](/Attachments/1-71fc6fae1cab42fba08f65c6e4b1fc25.png)
    21. Similarities
    22. Use Builder and Factory in object creation process.
    23. Decorator adds responsibilities to existing objects.
    24. Why not use Decorator for pizza.
        1. It makes a lot of sense.
        2. But Factory is operating at a different level.
        3. Factory doesn't care how it gets created.
        4. Builder makes a good pattern for the build process.
        5. The end representation.
        6. Factory manages different types.
    25. Focus on the intent when choosing a pattern.
    26. They can be more important than you think/realize.
    27. Designing software is an art as well as a science.
    28. One of the later chapters in their book combines a lot of these patterns with the Duck example.
    29. Patterns are discovered, not invented.
    30. After 25 years of the GoF book, there are not 100 patterns.
    31. We're still at about 23 patterns all this time later.
39. Flyweight Pattern
    1. Managing lots of objects
    2. An OO optimization technique.
    3. Not many patterns fit this.
    4. Time and space tradeoffs.
    5. ![Tree Flyweights ](/Attachments/1-f34930d510d546dca878e21f1ab8d578.png)
    6. Designing a college campus.
    7. Want a beautiful landscape.
    8. Thousands of trees.
    9. Very fractal when you include all the leaves.
    10. Very expensive graphical object.
    11. ![The Flyweight Pattern &#xA;The Flyweight Pattern &#xA;Use sharing to support large numbers &#xA;of fine-grained objects efficiently. ](/Attachments/1-18e5a53c5f5e4d3c80464727e9df42cf.png)
    12. ![FLYWEIGHT &#xA;U«• shar•ing to &#xA;f.tting &#xA;editing fm-ilities that Me to Using an &#xA;em-h I—te at &#xA;in and &#xA;to anoW their at &#xA;pat tern&amp;#39;s heavily on how and &#xA;i" s used. the When an Of &#xA;• An a of &#xA;• Me h• of &#xA;• ob#ct state &#xA;• r•plNTd by frw &#xA;state is &#xA;• &amp;#39;t W•ntity. Sim-e fl»eight &#xA;ihtity tests retm-n &#xA;distinct ](/Attachments/1-107d81ea08584a2a8d60fc798b9797c1.png)
    13. Cannot share tree locations.
    14. ![The Flyweight Pattern Structure &#xA;FlyweightFactory &#xA;Operation() &#xA;o &#xA;if (flyweight \[key\] ) &#xA;return it &#xA;else { &#xA;create new flyweight &#xA;add to pool &#xA;return new flyweight &#xA;operation(extrinsicState) &#xA;ConcreteFlyweight &#xA;operation(extrinsicState) &#xA;intrinsicState &#xA;Unsha redConcreteFIyweigh t &#xA;operabon(extrinsicState) &#xA;allState ](/Attachments/1-ee5793cbe2b446c6903330997a5a86d6.png)
    15. extrinsicState is state we cannot share
    16. ![Tree Flyweight Design &#xA;TræFactory &#xA;getTree(type) &#xA;o &#xA;if (tree &#xA;return &#xA;else &#xA;crea &#xA;re turn &#xA;Sts) &#xA;new tree &#xA;new &#xA;Tree &#xA;display(x, y) &#xA;Deciduous Tree &#xA;display(x, y) &#xA;trunk, branches, leaves &#xA;ConiferTre &#xA;display(x, y) &#xA;trunk, branches, needles &#xA;Client ](/Attachments/1-968cc4cbd9de47ccb3bcde4bc22772fc.png)
    17. ![Trees &#xA;public interface Tree { &#xA;public void display(int x, int y); &#xA;public default boolean isWithinRange(LocalDate aDate) { &#xA;Month month &#xA;aDate.getMonth(); &#xA;return (month.getVa1ue() &gt; 2) &amp;amp;&amp;amp; (month.getVa1ue() &amp;lt; 11); &#xA;public class DeciduousTree implements Tree { &#xA;// complex trunk, branch, leaf graphic data &#xA;public void display(int x, int y) { &#xA;System. tree is located at + x + &#xA;if (!this. { &#xA;System.out.print1n("The tree currently has no leaves"); ](/Attachments/1-4ec9b69eb3b3423c8cc0caaf609e2436.png)
    18. ![public interface Tree { &#xA;public void display(int x, int y); &#xA;public default boolean isWithinRange(Loca1Date aDate) { &#xA;Month month = aDate. getMonth(); &#xA;return (month.getVa1ue() &gt; 2) (month.getVa1ue() &amp;lt; 11); &#xA;public class ConiferTree implements Tree { &#xA;// Complex trunk, branch, needle graphic data &#xA;public void display(int x, int y) { &#xA;tree is located at ](/Attachments/1-378485f697d24db3af13fd81b7844142.png)
    19. ![Tree Factory &#xA;public class TreeFactory { &#xA;Tree d, c = null; &#xA;public TreeFactory() { &#xA;this.d = new DeciduousTree(); &#xA;this.c z new ConiferTree(); &#xA;public Tree getTree(String type) throws Exception { &#xA;if (type.equals("deciduous")) { &#xA;return this. d; &#xA;} else if (type. { &#xA;return this.c; &#xA;} else { &#xA;throw new Exception("lnvalid kind of tree"); ](/Attachments/1-8c20817b0e3d4c3ba63965c1ba3900fc.png)
    20. ![Client &#xA;public class Client { &#xA;public static void args) { &#xA;deciduousLocations = &#xA;1}, {33, 5Ø}, &#xA;coniferLocations &#xA;{(10, 87}, {24, 76}, &#xA;TreeFactory treeFactory = new TreeFactory(); &#xA;Tree d, c; &#xA;try { &#xA;d treeFactory. &#xA;c treeFactory. get Tree( "conifer"); &#xA;for (int\[\] location : deciduousLocations) { &#xA;location\[l\]); &#xA;for (int\[\] location : coniferLocations) { &#xA;location\[l\]); &#xA;} catch (Exception e) { &#xA;e. printStackTrace( ) ; &#xA;{løø, 90)}; ](/Attachments/1-ee936148583842629172b8c69b4f3e85.png)
    21. ![• &#xA;Flyweight Recap &#xA;Useful to reduce memory usage by sharing &#xA;common state between many objects. &#xA;Used to support large numbers of similar objects. &#xA;Separates state into extrinsic and intrinsic state &#xA;stored in a flyweight. &#xA;Intrinsic state is immutable. &#xA;More complex design, only use when you really &#xA;need to optimize your design. ](/Attachments/1-ab3b59e88a3641cea95afe08131e719b.png)

    22.
    23. ![What design principles does the &#xA;Exegcise Flyweight pattern embody? &#xA;Program to interfaces, not &#xA;implementations &#xA;Favor composition over &#xA;inheritance &#xA;OO Phi &#xA;hCiples &#xA;Favor &#xA;obJee6 Chat ,hf-eraeé.&amp;#39;hs &#xA;depend &#xA;Only &#xA;tyiends. &#xA;DOh&amp;#39;éeall &#xA;us, &#xA;class &#xA;have one ](/Attachments/1-32462fefbcf0495eb7fd76d58ef9010d.png)
    24. (2nd break)
    25. Mentioned a "Momento Pattern".
        1. [https://www.tutorialspoint.com/design\_pattern/memento\_pattern.htm](https://www.tutorialspoint.com/design_pattern/memento_pattern.htm)
        2. https://refactoring.guru/design-patterns/memento/csharp/example
40. State Pattern
    1. The state of things.
    2. Implements state diagrams.
    3. ![A State Diagram ](/Attachments/1-9b1c878641204936b11694df171a17c2.png)
    4. There is a complete example of this pattern in the book.
    5. We won't cover it all in this class.
    6. ![Typical Implementation &#xA;final static int &#xA;final static int &#xA;final static int &#xA;final static int &#xA;int state SOLD &#xA;SOLD OUT Ø; &#xA;NO_QUARTER 1 &#xA;HAS_QUARTER = 2; &#xA;SOLD - 3; &#xA;OUT ; &#xA;public void insertQuarter() { &#xA;if (state HAS_QUARTER) { &#xA;System. out can&amp;#39;t insert another quarter"); &#xA;} else if (state NO_QUARTER) { &#xA;state HAS_QUARTER; &#xA;System. out . inserted a quarter"); &#xA;else if &#xA;(state SOLD_OUT) { &#xA;System. out .println( "You can&amp;#39;t insert a quarter, the machine is sold out"); &#xA;} else if &#xA;(state SOLD) { &#xA;System. out. wait, we&amp;#39;re already giving you a gumball"); ](/Attachments/1-7e0998df070644e9a6353364e0f1e9bf.png)
    7. ![&amp;#39;(.p.su.dslp &#xA;inq &#xA;) asta &#xA;aro-mos • &#xA;(mos &#xA;• nus) ( &#xA;) (mos a &#xA;) &amp;#39;Vtqnd &#xA;( Lm¯a10S &#xA;asta &#xA;• uns &#xA;"tqnd ](/Attachments/1-d61f080ae8fe45ff8a56d218c75ff5ee.png)
    8. What happens in the presence of change?
    9. ![Feature request! &#xA;be a &#xA;One in Ten &#xA;ßEE ](/Attachments/1-ca50cd668fa4434db6d9ad43ab2add9f.png)
    10. We have to change everything when we mess with this code!
    11. ![Observations about the Code &#xA;A. This code isn&amp;#39;t adhering to the Open Closed Principle. &#xA;B. This code would make a FORTRAN programmer proud. &#xA;C. This design isn&amp;#39;t even very object oriented. &#xA;D. State transitions aren&amp;#39;t explicit; they are buried in the &#xA;middle of a bunch of conditional statements. &#xA;E. We haven&amp;#39;t encapsulated anything that varies here. &#xA;F. Further additions are likely to cause bugs in working code. ](/Attachments/1-d46edc5990954ff2b31d624d5e541a91.png)
    12. You couldn't easily draw the state diagram if the original were lost and all you had left was the code.
    13. ![](/Attachments/1-5a278941cb494f7684f3431be25f9aec.png)
    14. Allow object to change behavior when its state changes.
    15. <mark style="background: #FFF3A3A6;">"The object will appear to change its class."</mark>
    16. This confused Eric.
    17. ![](/Attachments/1-cec83a66576a44c99d383821a170f517.png)
    18. Current state is an object.
    19. Typical composition.
    20. ![m_ib1iC Clagg Gtnba11Machine &#xA;final static &#xA;int SOLD OUT - O; &#xA;final gtatie &#xA;int NO QUARTER - 1; &#xA;final &#xA;int 2; &#xA;final static &#xA;int SOLD - &#xA;int state &#xA;SOLD OUT; &#xA;int • O &#xA;Old &#xA;New &#xA;The code a &#xA;public class GumballMachine &#xA;State soldOutState; &#xA;State &#xA;State hasQuarterState; &#xA;State &#xA;State &#xA;int &#xA;soldState; &#xA;state 301dOutState; ](/Attachments/1-3c90630ab382477aab8b2daf2f843248.png)
    21. ![The Gumball Machine Class &#xA;public class GumballMachine { &#xA;State soldOutState; &#xA;State noQuarterState; &#xA;State hasQuarterState; &#xA;State soldState; &#xA;State state; &#xA;int count e; &#xA;public GumballMachine(int numberGumba11s) { &#xA;soldOutState new SoldOutState(this); &#xA;noQuarterState new NoQuarterState(this); &#xA;hasQuarterState new HasQuarterState(this); &#xA;soldState = new SoldState(this); &#xA;this. count numberGumba11s; &#xA;if (numberGumba11s &gt; ø) { &#xA;state noQuarterState; &#xA;else { &#xA;state — soldOutState; ](/Attachments/1-e65d82e8a6b143eaa9a3af689f3daf57.png)
    22. ![The HasQuarterState Class &#xA;public class HasQuarterState implements State { &#xA;GumballMachine gumballmachine; &#xA;public HasQuarterState(Gumba11Machine gumballMachine) { &#xA;this .gumba11Machine gumballMachine; &#xA;public void insertQuarter() { &#xA;System.out.print1n("You can&amp;#39;t insert another quarter"); &#xA;public void ejectQuarter() { &#xA;returned"); &#xA;gumballMachine. ne. getNOQuarterState( ) ) ; &#xA;public void turnCrank() { &#xA;System .out. println( "You turned... &#xA;gumballMachine. setState (gumballMachine. getS01dState( ) ) ; &#xA;public void dispense() { &#xA;System. Out. gumball dispensed"); ](/Attachments/1-a6fdf5d1dd264e5cb2785f8bb95eaba8.png)
    23. ![The Gumball Machine Class &#xA;public void insertQuarter() { &#xA;state. insertQuarter( ) ; &#xA;public void ejectQuarter() { &#xA;State. ejectQuarter() ; &#xA;public void turnCrank() { &#xA;state. turnCrank() ; &#xA;State. di spense() ; &#xA;void releaseBa11() { &#xA;System. out. gumball comes rolling out the &#xA;if (count e) { &#xA;count = count - 1; &#xA;void setState(State state) { &#xA;this. state state; ](/Attachments/1-988c11c1750f4b64912a50b12fa200d5.png)
    24. ![The State Pattern &#xA;Context &#xA;request() &#xA;state handle() &#xA;ConcreteStateA &#xA;hande() &#xA;State &#xA;handle() &#xA;ConcreteStateB &#xA;handle() ](/Attachments/1-7c40db425e5d4be6942cf8aafe1dcc37.png)
    25. ![Can we easily add the &#xA;winning state now? &#xA;public class WinnerState implements State { &#xA;public void dispense() { &#xA;// logic to dispense two gumballs if the &#xA;// customer is a winner &#xA;public class HasQuarterState implements State { &#xA;public void turnCrank() { &#xA;// logic to randomly pick a winner and &#xA;// transition to Winner state &#xA;// otherwise just go to Sold state ](/Attachments/1-b1d68b2918a245bea63f7570757d8e24.png)
    26. ![Did we solve these issues? &#xA;A. This code isn&amp;#39;t adhering to the Open Closed Principle. &#xA;B. This code would make a FORTRAN programmer proud. &#xA;C. This design isn&amp;#39;t even very object oriented. &#xA;D. State transitions aren&amp;#39;t explicit; they are buried in the &#xA;middle of a bunch of conditional statements. &#xA;E. We haven&amp;#39;t encapsulated anything that varies here. &#xA;F. Further additions are likely to cause bugs in working code. ](/Attachments/1-7f22cf4c851f4fb6b88b185ba11390f1.png)
    27. Does this sound similar to another pattern?
    28. The strategy pattern.
    29. ![,Wait does State look familiar ](/Attachments/1-e34d6e4ba5bd4914aa6d277e7c2f0968.png)
    30. The two patterns differ in intent.
    31. Solutions to different problems in different contexts.
    32. Recognize which intents and which problems are being used to solve.
    33. Class attendee "BS": Real life examples: States of a transaction NEW, IN\_PROGRESS, BLOCKED, CLOSED then action as appropriate
41. Final Pattern: Compound Patterns
    1. ![Patterns are often used together and &#xA;combined within the same design &#xA;solution. &#xA;A compound pattern combines two or &#xA;more patterns into a solution that solves a &#xA;recurring or general problem. ](/Attachments/1-5c8de59779f845558f8094e0ed8cb891.png)
    2. We're going to talk about a combo of 3.
    3. **<span style="">One of the most common patterns in use.</span>**
    4. MVC (Model-View-Controller)
    5. ![A common problem &#xA;View &#xA;M Odel &#xA;Controller ](/Attachments/1-1c6a029d0c014e168da1b45fda7fd928.png)
    6. Think of iTunes
    7. Database of songs
    8. Code communicating between UI and database.
    9. Split app into manageable pieces.
    10. Flexible.
    11. ![Writing a Music Player Controller &#xA;Takes user input figures Nt &#xA;it mea&amp;#39;S to the model. &#xA;Gives you a presentation of the &#xA;model. The view us•nlly gets &#xA;the State ard data it needs to &#xA;display directly from the model. &#xA;user did &#xA;View &#xA;Controller &#xA;MODEL &#xA;The holds all the ±ta. state &#xA;and application The is &#xA;obl•v.ous to the view and controller. &#xA;@ althoue &#xA;it an interface to &#xA;runipu te and retrieve Its state &#xA;Char• aM t can send notifications of state &#xA;charges to obser•vers. &#xA;Model &#xA;I state ](/Attachments/1-7f3c8507d2194bab88697b226b5e507d.png)
    12. ![A Pattern made of Patterns &#xA;Strategy &#xA;Controller &#xA;display &#xA;need state &#xA;Observer &#xA;Model ](/Attachments/1-949802f92a0b4ffe9ea8999f3eafb4ba.png)
    13. ![Observer in MVC &#xA;Observable &#xA;My state has &#xA;changed! &#xA;Model &#xA;I&amp;#39;d like to register &#xA;as an observer &#xA;View &#xA;Observers &#xA;Controller ](/Attachments/1-84e0a9b3b0e04014aca9c03018da1c1c.png)
    14. ![Strategy in MVC &#xA;The user did &#xA;something &#xA;Controller &#xA;View &#xA;Controller ](/Attachments/1-5c4a70e1ace349bbadea0aa1ccd89ec7.png)
    15. This is like the ducks delegating flying and quacking.
    16. ![Composite in MVC &#xA;paint() &#xA;000 &#xA;saBPM: &#xA;View ](/Attachments/1-a448695baf6c42b2b51de011d2c7e7ac.png)
    17. Composite == Tree structures
    18. Attendee "BS": Though Itunes is long gone, observer still applies with spotify as I can switch device where am playing music from and I will continue with the same song, same point in the song
        1. Elisabeth: You have different views
42. Your journey has just begun
    1. ![Shared Vocabularies &#xA;Alice &#xA;I a cream cheese With jelly on White &#xA;bred a chocolate with vanilla ice cream, a &#xA;grilled cheese sandwich with bacon, a fish &#xA;salad on a split With ice cream &amp;amp; sliced &#xA;bamms. and a coffee With a cream and two „ &#xA;Oh, md Nt a hamburw• on the "ill&amp;#39; &#xA;Give me a C J. White. &#xA;a bhck white. a Jack &#xA;Benny. a radio, a house a &#xA;coffee reælar•, and bum one! ](/Attachments/1-e96e8c48dba641cba716473350e8886a.png)
    2. How a team operates when they have a vocabulary like design patterns.
    3. Flo's is much shorter
    4. Semantically the same
    5. Has a shared vocabulary with short order cook
    6. Business domain
    7. ![So I created this broadcast class. It keeps &#xA;track of all the objects listenity to it, and &#xA;anytime a æw piece of data Comes aloty it sends &#xA;a message to each listener. Whafs cool is that the &#xA;listeners Can join the broadcast at any time or &#xA;they can even remove themselves. It is really &#xA;dynamic and loosely coupled! &#xA;Rid ](/Attachments/1-914ca84732884554ad518d048525cb24.png)
    8. ![0 ](/Attachments/1-af673c36f786487281980a34e6423a78.png)
    9. He could have said it much simpler by saying the observer pattern.
        1. Use the shared vocabulary.
    10. It's not just a pattern name.
        1. Qualities, characterics, etc.
    11. Stay in the design longer before heading into coding.
    12. Less room for misunderstandings
    13. Jr devs look up to Sr devs
    14. Sr devs using patterns, jr will want to ramp up and learn from them.
    15. ![Where to go next &#xA;I)esigll 111tt(&amp;#39;111S &#xA;PEevsE NE &#xA;OF FOV2 &#xA;The Des* Pa-keens &#xA;known as Four," ](/Attachments/1-3598527cfb994e44a87be4b1503cce2c.png)
    16. Really useful to have this book.
    17. Very insightful.
    18. The basis for their book.
    19. Examples in C++  and SmallTalk.
    20. Other languages than what they used.
    21. ![Really Learn &#xA;this Stuff &#xA;Head First &#xA;Design &#xA;Patterns ](/Attachments/1-add111f0fadd49e5b0a840d9e4cf8371.png)
    22. A lot of conversation in this book, objects talking to objects, guru.
    23. Pick up the print copy.
    24. Lots of room to write in it.
    25. It's a workbook.
    26. ![Community &#xA;People Projects And &#xA;pa tterns &#xA;Websites &#xA;The Portland patterns Repository, is run by Ward &#xA;Cunningham, is a wiki devoted to all things related to &#xA;patterns. &#xA;The Hillside Group includes information, articles, &#xA;books, and tools related to software design, including &#xA;design patterns. &#xA;O&amp;#39;Reilly Learning has a Wide collection Of books, &#xA;courses, and online training about design patterns. &#xA;103 ](/Attachments/1-7537362c6c6445a493e6b941d4bc193a.png)
    27. Ward Cunningham
    28. Portland Patterns Repo
        1. He also invented wikis.
    29. Be careful about what you read on the Internet.
    30. Some people get it wrong.
    31. Erich Gamma helped with their book.
    32. ![Thinking in Patterns &#xA;• Design Patterns are not a magic bullet. &#xA;• You know you need a pattern when.. &#xA;• Don&amp;#39;t be afraid to remove a pattern from your &#xA;design. &#xA;• If you don&amp;#39;t need it now, don&amp;#39;t do it now. ](/Attachments/1-4b004753e67d4493a0cb59dbf5ad0797.png)
    33. They're not even a bullet.
    34. Other developers have been there before you.
    35. These are time-tested.
    36. ![Head First &#xA;Design Patterns &#xA;WARNING: Overuse Of design patterns can lead &#xA;to code that is downright over-enginæred. &#xA;Always go with the simplest Solution that does &#xA;the job and introduce patterns where the need ](/Attachments/1-2c6544af6e104581b796445a49610c05.png)
    37. Go with simplicity.
    38. ![Your challenge, &#xA;should you &#xA;accept it.. ](/Attachments/1-6bbab9502b3043f3a8e534231e7e3e30.png)
    39. Page 574 of the new edition.
    40. Do this ourselves, fill it out.
    41. Eric likes being reached on LinkedIn.
    42. ![Boy, it&amp;#39;s been great having you. &#xA;We&amp;#39;re going to miss you, for sure. But don&amp;#39;t worry—you can always find us &#xA;at wickedlysmart.com or @erictfree, @elisabethrobson on Twitter. ](/Attachments/1-d1a2797b66ff41fc914a5c2886cabeb0.png)