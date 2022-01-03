# Design Patterns Bootcamp (Week 2 of 3)

**Created**: Wednesday, June 09, 2021 10:47:50 AM -04:00
**Modified**: Monday, January 03, 2022 10:30:19 AM -05:00


Wednesday, June 2nd, 2021, 11 am EST

Instructors: [Elisabeth Robson](https://www.amazon.com/Elisabeth-Robson/e/B001H6Q046%3Fref=dbs_a_mng_rwt_scns_share?sa-no-redirect=1&amp;amp;pldnSite=1) and [Eric Freeman](https://www.amazon.com/Eric-Freeman/e/B001H6Q032%3Fref=dbs_a_mng_rwt_scns_share?sa-no-redirect=1&amp;amp;pldnSite=1)

Facilitator: Lindsay Ventimiglia

https://learning.oreilly.com/attend/design-patterns-in-3-weeks/0636920054121/0636920054723/

Slides:

https://on24static.akamaized.net/event/30/40/48/3/rt/1/documents/resourceList1622663089929/designpatternsbootcamp3weekspart2padding1622663089079.pdf

[designpatternsbootcamp3weekspart2padding1622663089079.pdf](/Attachments/designpatternsbootcamp3weekspart2padding1622663089079-1-3133012714df4bc1a0215dba36f894ec.pdf)
Errata Page:

http://oreilly.com/catalog/0636920367598/errata

Supplemental Content:

https://www.wickedlysmart.com/head-first-design-patterns/

1. Review of last week.
2. Decorating objects
    1. This uses composition.
    2. ![Starbuzz Coffee &#xA;Il ()ther 1Befi.A rr*ods ](/Attachments/1-0be03df4197943a89dc954130ecdf77d.png)
    3. Italics means abstract
    4. Wants to start adding condiments to add to each type.
    5. Tried creating subclass for every permutation.
    6. ![](/Attachments/1-50116c5251b04164af2fe0409422f5d5.png)
    7. Maintenance nightmare.
    8. ![e•o••*• (4 &#xA;يد ل ص &#xA;(w (دد7 م «ددم &#xA;FOG 9*9qe.S &#xA;R* q..Cqo وددعدد &#xA;مد وحهلاردم إمحيدرل يص ووسد &#xA;4d!7U!SilA 00 &#xA;ي ](/Attachments/1-42e6075c7b604fec8b7a0f39e817f458.png)
    9. Which principles apply?
        1. Encapsulate what varies
        2. Favor composition over inheritance.
    10. ![What about this approach? &#xA;Beverage &#xA;hasMilk() &#xA;seL4ilk() &#xA;setSoy() &#xA;hasMocha() &#xA;setMocha() &#xA;hasWhip() &#xA;Il Offer useful methods.. ](/Attachments/1-b2c4cc87ad304fd391411013744f9143.png)
    11. ![Now let's add in the &#xA;subclasses, one for &#xA;each beverage on &#xA;the menu: &#xA;see.'oda() &#xA;I/ Otter useu ](/Attachments/1-2054e7b2368743cfbb152253478fa636.png)
    12. ![Only five classes, not bad. Although, what problems &#xA;might you encounter with this solution? &#xA;HO&amp;quot; &amp;quot;Blend ](/Attachments/1-1c737cbe5fd94447aba7ca9b47473da6.png)
    13. ![Only five classes, not bad. Although, what problems &#xA;might you encounter with this solution? &#xA;A. Price changes will force us to alter existing &#xA;code. &#xA;B. New condiments will require new methods &#xA;and alter the cost method in the superclass. &#xA;C. New beverages like iced tea will be forced &#xA;to inherit methods that don't make sense. &#xA;D. What if a customer wants a double mocha? ](/Attachments/1-a6126eb37d8c480c843421b3b335a686.png)
    14. We need to encapsulate what varies.
        1. New condiments.
    15. Single Responsibility Principle.
    16. Why have HasMocha for an iced tea since that method doesn&#39;t make sense for iced tea?
    17. Open Closed Principle
    18. What if someone wants a quad shot?
        1. No way to do that right now.
    19. GoF
    20. ![](/Attachments/1-f90c9fa648d74070b449a4bb47c45649.png)
    21. Whip wraps Mocha which wraps Dark Roast.
    22. ![O Now it's time to compute the cost for the customer. We do this &#xA;by calling cost() on the outermost decorator, Whip, and Whip is &#xA;going to delegate computing the cost to the objects it decorates. &#xA;Once it gets a cost, it will add on the cost of the Whip. &#xA;here &#xA;$1.29 &#xA;cos &#xA;.10 &#xA;.20 &#xA;Mocha &#xA;Whip ](/Attachments/1-e3e24c6af0ad4588ad19549e7b46cc4a.png)
    23. ![The Decorator Pattern ](/Attachments/1-4df8fda9b4424f0d8753d42857cac2de.png)
    24. ![Starbuzz Coffee Design ](/Attachments/1-f5670e845e0d4a2892b27df4d94acc14.png)
    25. <mark style="background: #FFF3A3A6;">How does getDescription work if it's concrete in the abstract Beverage class but is abstract in CondimentDecorator?</mark>
    26. ![Components &#xA;public abstract class Beverage { &#xA;String description = &#xA;&amp;quot;Unknown Beverage&amp;quot; ; &#xA;public String getDescription() { &#xA;return description; &#xA;public abstract double cost(); &#xA;public class DarkRoast extends Beverage { &#xA;public DarkRoast() { &#xA;description = &amp;quot;Dark Roast coffee&amp;quot; ; &#xA;public double cost() { &#xA;return .99; ](/Attachments/1-57fea012c629427b89868a9b08e70111.png)
    27. ![Decorators &#xA;public abstract class CondimentDecorator extends Beverage { &#xA;Beverage beverage; &#xA;public abstract String getDescription(); &#xA;public class Whip extends CondimentDecorator { &#xA;public Whip(Beverage beverage) { &#xA;this.beverage = beverage; &#xA;public String getDescription() { &#xA;return beverage.getDescription() + &amp;quot; &#xA;public double cost() { &#xA;return beverage. cost() + .IØ; &#xA;Whip&amp;quot; ; ](/Attachments/1-d713fb25696c4c95815a96174546dc43.png)
    28. ![Decorators &#xA;public class mocha extends condimentDecorator { &#xA;public Mocha(Beverage beverage) { &#xA;this.beverage = beverage; &#xA;public String getDescription() { &#xA;return beverage. getDescription() + &amp;quot; &#xA;public double cost() { &#xA;return beverage. cost() + .20; &#xA;Mocha&amp;quot; ; ](/Attachments/1-095f8379b2c34760a7a9a3bc9dfb6dbd.png)
    29. ![Starbuzz &#xA;public class StarbuzzCoffee { &#xA;public static void main(String args\[\]) { &#xA;Beverage beverage = new DarkRoast(); &#xA;beverage = &#xA;new Mocha(beverage); &#xA;beverage = &#xA;new Mocha(beverage); &#xA;beverage = &#xA;new Whip(beverage); &#xA;System. out. println( beverage. getDescription ( ) &#xA;+ beverage. cost()); ](/Attachments/1-b87f4acb50c44b5395cd3628613d4bbd.png)
    30. Note that it&#39;s a Beverage in the first line, not a DarkRoast.
    31. You could keep all of the decorators in a list.
    32. This example cannot prevent an iced tea from being decorated.
    33. Remember that this is a toy example, so everything may not be appropriate.
    34. Example of Decorator in the real world.
    35. ![Exegcise &#xA;Quick Quiz: can anyone think of a Java &#xA;library that uses the Decorator Pattern? ](/Attachments/1-48481ac6584f4b4a8827eb4f4e4c733e.png)
    36. IO Streams is the answer she was looking for.
    37. ![](/Attachments/1-8a9bcc01a3b04f4eace54dd013a41f98.png)
    38. Think &quot;using&quot; in C#. (Rob&#39;s comment)
    39. See Design Patterns GitHub site for a code example.
3. Surrogate Objects
    1. Aka Proxy Pattern
    2. A stand-in object
    3. ![The Proxy &#xA;Pattern &#xA;PROXY &#xA;Object Structural &#xA;Pnnide a surr•W'te or another to &#xA;access to it. &#xA;Motivation &#xA;One reason for controlling access to an object is to defer the full &#xA;its creation and initialization until actually need to use it. &#xA;Consider a document editor that can embed graphical oliects in a &#xA;d«ument. Some graphical objects can expensive to create. &amp;quot;Ille &#xA;solution is to use another object, an image prosy, that acts as a stand- &#xA;in fir the real image. The proxy acts just like the image and takes &#xA;care of instantiating it when it's required. &#xA;Proxy is applicable wheneser there is a need for a more sersatile &#xA;or g:vhisticated reference to an (A)ject than a simple B'inter. Sorne &#xA;proxies inchKle: &#xA;• A remote proxy prosides a representative fir an object in a &#xA;different address space. &#xA;• A virtual proxy creates expensive otiects on demand. &#xA;• A protection proxy contrrAs access to the original oliect. &#xA;• A smart refrrence that perfirms a€klitional actions when the oliect &#xA;is accessed. ](/Attachments/1-fe88669e037a4576a3a31e086b386d5b.png)
    4. Control access to the object.
    5. Lazy evaluation
    6. A web browser is a document editor
    7. ![-he proxy &#xA;)attern ](/Attachments/1-ae3424e44bd148f7a3b526d4746808c4.png)
    8. Have to get images after we have the text.
    9. Image placeholders
    10. Everything off the page that we have to scroll to.
        1. May never need them if we never scroll to them.
    11. ![•passooov s! &#xA;o atp suopoe IPt109!ppe stuuopod veurs V &#xA;'100!qo ato sto.nuoo Åxo.1d uopommd V . &#xA;•puetuap uo soo!qo astsuadxa smea.ro Åxo.rd V. &#xA;•aoeds ss;uppe &#xA;u! pa(qo tre a.ynnuosa.ldaa v V * ](/Attachments/1-0625647883d747449985e30f902e7fd5.png)
    12. Album cover image loader
    13. Wait to load cover image until user selects album from menu.
    14. Display &quot;Loading album cover. Please wait…&quot; until retrieved.
    15. ![Using Proxy to load images ](/Attachments/1-4265aefe5f754ee6b15c2900db0cf5c8.png)
    16. ![class ImageProxy implements Icon { &#xA;volatile Imagelcon imagelcon; &#xA;final URL imageURL; &#xA;Thread retrieval Thread; &#xA;boolean retrieving false; &#xA;public ImageProxy(URL url) { imageURL url; &#xA;// getters and setters &#xA;public void paintlcon(final Component c, Graphics g, &#xA;if (imagelcon null) { &#xA;imagelcon.paintlcon(c, g, x, y); &#xA;else { &#xA;g. CD cover, please wait. &#xA;if (!retrieving) { &#xA;retrieving true; &#xA;retrievalThread new { &#xA;try { &#xA;ImageProxy &#xA;int x, &#xA;int y) { &#xA;xoeø, Y+19ø); &#xA;&amp;quot;CD Cover&amp;quot;)); &#xA;setlmagelcon(new Imagelcon(imageURL, &#xA;C . repaint(); &#xA;catch (Exception e) { &#xA;e. printStackT race() ; &#xA;retrievalThread. start() ; ](/Attachments/1-11fcd05e8cf44179a1b0db281c8f8584.png)
    17. ![Test the ImageProxy &#xA;public class ImageProxyTestDrive { &#xA;// Swing component properties... &#xA;public static void main (String\[\] args) throws Exception { &#xA;ImageProxyTestDrive testDrive = new ImageProxyTestDrive(); &#xA;public ImageProxyTestDrive() throws Exception { &#xA;// Swing set up.. &#xA;// cds set up--add image URLs to cd objects here &#xA;Icon icon = new Imageproxy(initia1URL); &#xA;imageComponent = new ImageComponent(icon) ; &#xA;frame. getContentPane( ) . add( imageComponent ) ; &#xA;for (Enumeration&amp;lt;String&gt; e cds. keys(); e. hasMoreE1ements();) { &#xA;String name = (String)e.nextE1ement(); &#xA;'Menultem menultem new JMenuItem(name) ; &#xA;menu. add (menultem) ; &#xA;menultem. addActionListener(event -Y { &#xA;imageComponent &#xA;. setlcon(new ImageProxy(getCDUr1(event.getActionCommand()))); &#xA;frame. repaint( ) ; ](/Attachments/1-e368f7abbee54ef982a5cab6c61c4f4e.png)
    18. ![Our Image Proxy Structure &#xA;gdEmWdh() &#xA;parttm() ](/Attachments/1-e4b27398353a4e3598f3767301bc9aa6.png)
    19. ![Types of proxies &#xA;• A virtual proxy controls access to a resource &#xA;that is expensive to create. &#xA;• Remote proxy controls access to a remote &#xA;object. &#xA;• A protection proxy controls access to a &#xA;resource based on access rights. ](/Attachments/1-020ace2af30c4382aadaadafb4f95f9d.png)
    20. ![Exegcise &#xA;Does the Proxy Pattern remind you of &#xA;other patterns (from Bootcamp l)? ](/Attachments/1-d7b7ffd8484e46f094e985e83388c486.png)
        1. Fa&#231;ade
        2. Adapter
            1. Both of these have objects sitting in between and is forwarding requests.
        3. Decorator
        4. Using is-a and has-a together.
        5. The intent of the patterns is different.
            1. Proxy - control access, taking responsibility away from client.
            2. Could argue adding extra behavior.
        6. Look at intent of each pattern and examples for each.
    21. (Break)
4. Observer Pattern
    1. ![Staying Loosely &#xA;Coupled ](/Attachments/1-b664c8b471b74635ba6ad2f988462d18.png)
    2. ![Loose Coupling &#xA;Design Principle &#xA;Strive for loosely coupled &#xA;designs between objects &#xA;that interact. ](/Attachments/1-96ae4b740e0a49aabf7f4dce8fb7671c.png)
    3. Objects are not too dependent on one another.
    4. Leads to a fragile, breakable system.
    5. ![A Common Problem &#xA;42 &#xA;An object with &#xA;an Important &#xA;Value &#xA;VI text &#xA;O &#xA;Object &#xA;O &#xA;VI &#xA;O &#xA;Analytics &#xA;O &#xA;Watchd% object looki'* lcm object &#xA;Objects that need to know &#xA;the Important Value ](/Attachments/1-6cedfa4c4b0b4fed91be2d9b1ae6e48c.png)
    6. Think of this number being the weather temperature.
    7. You don&#39;t want every other object pinging the object for the value all the time.
    8. Don&#39;t poll
        1. Don&#39;t call us, we&#39;ll call you.
    9. ![The Hollywood Principle &#xA;Design Principle &#xA;Don't call us, we'll call you. ](/Attachments/1-d938f1b91fe84863bb7d4d2011a5c952.png)
    10. Observer is like the adapter pattern.
    11. ![Use the Observer Pattern &#xA;• You subscribe to a news &#xA;publisher. &#xA;• Whenever there's a new edition &#xA;of the news (or a new blog &#xA;post), you get it. &#xA;• If you don't want to get the &#xA;paper (or the posts) anymore, &#xA;you unsubscribe. &#xA;• Other subscribers continue to &#xA;get the news. ](/Attachments/1-99f5d8c973fe43ed9b28168db3e0844e.png)
    12. ![A day in the life of the &#xA;Observer Pattern &#xA;Duck ](/Attachments/1-a4d3c894df654095943480dc27334556.png)
    13. The subject is in charge of this important piece of data.
    14. Anyone receiving messages is an observer.
    15. ![A day in the life of the &#xA;Observer Pattern &#xA;Ject ](/Attachments/1-681cb216ef7d41e9aa338a846e9f2b42.png)
    16. Value change
    17. ![A day in the life of the &#xA;Observer Pattern &#xA;ject &#xA;QI'Q, &#xA;Observers ](/Attachments/1-1833e19236404fa895ea0b6fefa7596a.png)
    18. ![A day in the life of the &#xA;Observer Pattern &#xA;.14 &#xA;.. 14 &#xA;Ject &#xA;Ouck ](/Attachments/1-d2ad49838240428b8ea70b9079c9a2c2.png)
    19. ![](/Attachments/1-4500e51dbf06422ba0c8899fc9af49cb.png)
    20. ![The Observer Pattern ](/Attachments/1-c4f9cacd74bf4458996f5294a37e6e7d.png)
    21. Subject will keep a list of observers (to notify).
        1. 0..many
    22. Look at Weather Station example in the book.
    23. ![The Subject Interface &#xA;public interface Subject { &#xA;public void registerObserver(Observer o); &#xA;public void removeObserver(Observer o); &#xA;public void notifyObservers(); ](/Attachments/1-fc350e2bdf98449381a16e1f8d6d3115.png)
    24. ![The Concrete Subject &#xA;public class SimpleSubject implements Subject { &#xA;private ArrayList&amp;lt;Observer&gt; observers; &#xA;private int value = O; &#xA;public SimpleSubject() { &#xA;observers = new ArrayList&amp;lt;Observer&gt;(); &#xA;public void registerObserver(Observer o) { &#xA;observers. add(o) ; &#xA;public void removeObserver(Observer o) { &#xA;// remove observer from the list &#xA;// more code here (next slide) ](/Attachments/1-38ff987f6a894ae29b954934ad402485.png)
    25. ![The Concrete Subject &#xA;public class SimpleSubject implements Subject { &#xA;private ArrayList&amp;lt;Observer&gt; observers; &#xA;private int value = e; &#xA;// other code here &#xA;public void notifyObservers() { &#xA;for (Observer observer : observers) { &#xA;observer. update(value) ; &#xA;public void setvalue(int value) { &#xA;this. value = value; &#xA;notifyObservers ( ) ; ](/Attachments/1-43b4e38fd3cb404aae63f797a913a06a.png)
    26. ![The Observer interface &#xA;public interface Observer { &#xA;public void update(int value); ](/Attachments/1-36b0bc21180744b28801ee5956beb6ad.png)
    27. ![The Concrete Observer &#xA;public class SimpleObserver implements Observer { &#xA;private int value; &#xA;private Subject simplesubject; &#xA;public SimpleObserver(Subject simpleSubject) { &#xA;this . simpleSubject = simpleSubject; &#xA;simpleSubject. registerObserver(this ) ; &#xA;public void update(int value) { &#xA;this. value = value; &#xA;display(); &#xA;public void display() { &#xA;System. out. println( &amp;quot;Value. &#xA;. &amp;quot; + value); ](/Attachments/1-e5295f15978446e3b6cda7f87abba196.png)
    28. You have probably used the observer pattern before.
    29. ![Event handling &#xA;JavaScript: &#xA;buttonE1ement. addEventListener (&amp;quot;click&amp;quot; , &#xA;console. on, do it!&amp;quot;); &#xA;false); &#xA;Java: &#xA;frame = new JFrame(); &#xA;function() { &#xA;3Button button = new I do it?&amp;quot; &#xA;button. addActionListener(event &#xA;System. out .println( &amp;quot;Don't do &#xA;button. addActionListener(event &#xA;System. out. on, &#xA;it, you might regret it! &#xA;do it! ](/Attachments/1-59465cc2a7ab48a6b0b89cd4b9e7a23a.png)
5. Iterator Pattern
    1. ![Encapsulating &#xA;Iteration ](/Attachments/1-b6e9427d2c8a4691b05119a5b94c174e.png)
    1. ![Encapsulate what varies &#xA;Design Principle &#xA;Identify the aspects of your &#xA;application that vary and &#xA;separate them from what stays &#xA;the same. ](/Attachments/1-e46b35d7de3a400685736dc96582ee5d.png)
    1. ![Breaking News: Objectville Piner and &#xA;Objectville Pancake House Merge &#xA;C)/yectvfle Pancake -Nouse ](/Attachments/1-72f6eec17c2a4ab3a34441fe1ba43153.png)
    2. ![We've got different Data Structures &#xA;Menultem\[\] menultems; &#xA;&amp;amp;ttaxe &amp;amp; &#xA;A Ofthe &#xA;menultems; &#xA;299 &#xA;Pancake &#xA;Pmcakes &#xA;Pana*es With &#xA;Pa neakes fresh bk.&amp;amp;mes ](/Attachments/1-8d26d5e9f7e6419f8a2ac9137b0b6318.png)
    3. Waitress code:
    4. ![Iterating with an array list &#xA;for (int i = O; i &amp;lt; breakfastltems. ; i++) { &#xA;Menultem menultem = breakfastltems • &#xA;get(l) &#xA;get(O) &#xA;get (2) get(3) &#xA;ArrayList &#xA;0000 &#xA;euh A-em. ](/Attachments/1-0e6445c5c06b4683b00a792abc3b0444.png)
    5. ![Iterating with an array &#xA;lunchltemslOl &#xA;for (int i &#xA;O; i &amp;lt; lunchltems . ; &#xA;Menultem menultem = lunchltems &#xA;Array &#xA;st2J &#xA;Itemst3J &#xA;We use Che &#xA;kens. ](/Attachments/1-a9171599d03e4610bbf52a9b70844eaf.png)
    6. ![So we have some problems &#xA;with the waitress... &#xA;A. We have duplicate code: a loop for each type of &#xA;menu. &#xA;B. The Waitress has to know how each menu type is &#xA;implemented. &#xA;C. We are coding to concrete implementations, if we &#xA;ever want to replace the data structure we have a lot &#xA;of coding to do (we're not closed for modification!). &#xA;D. Waitress has dual responsibilities (not a single one). ](/Attachments/1-130cbbe0b7564d37981d886875b05d14.png)
    7. For letter C above, code to an interface not to a type.
    8. For letter D above, violates SRP.
    9. The iteration is what&#39;s varying here.
    10. ![](/Attachments/1-6774a3adae9245e88a745058fe5a3b0c.png)
    11. So useful in languages and so common that it&#39;s incorporated right into many languages.
    12. ![ITERATOR &#xA;Object Behavioral &#xA;a to access the ekments an agregate '*jest wnhout expsing its &#xA;underlying representat &#xA;Motivation &#xA;An Qregate oWect such as a list siu»ukl give a way to access its elements without expositw &#xA;ib interrul strtKture. Moreover you might want to trasersc in ways. &#xA;on what you want to accomplish. But you don't want to bloat the List interface wnh operatiotb &#xA;differeM traversals. if you co.dd antic.ate ones &amp;quot;'u will need. &#xA;Iterator pattern kts you au this •nie key in thb pttern is to take the resp«msbility &#xA;for access and traversal of list object put it into an obect. The Iterator clag &#xA;defines an interåce accessing the lisfi elenxnts. An iterator (&amp;quot;ect is responsible K.»r keeping &#xA;track of current ekment; that is. it which elenrnts traver*d already. &#xA;Applicability &#xA;pattern: &#xA;• an aggregate obßcti contents without exposing is &#xA;• to support multiple traversals of agregate objects. &#xA;• to prov*le a unifirm interface for traversirW diffrrent structures. ](/Attachments/1-869ced70c34c4d458556ed94cfd553cd.png)
    13. Aggregate object == a collection.
    14. ![Using an Iterator for ArrayList &#xA;ask {he &#xA;its &#xA;Iterator iterator = breakfastMenu. createlterator ; &#xA;while items &#xA;while (iterator. hasNext ( ) ) &#xA;Menultem iterator. next ( &#xA;next() &#xA;'ec the ike—. &#xA;get(2) &#xA;get(3) &#xA;Jusk &#xA;and &#xA;get(l) &#xA;ArrayList &#xA;get(O) &#xA;0000 ](/Attachments/1-4b2259f7660b4e4eb3cd85b39de4e59c.png)
    15. ![Using an Iterator for Array &#xA;Iterator iterator = ; &#xA;while (iterator. hasNext ( ) ) { &#xA;Menultem menultem = iterator . next() ; &#xA;Array &#xA;lunchItemS(Ol &#xA;Sa—e &#xA;and behind scenes, &#xA;Che &amp;quot;does Eke &#xA;lunch'tems\[2J ](/Attachments/1-ae146bd42b2b4f4197bc0773863ad7a4.png)
    16. ![The new, improved design &#xA;«int«f.ce. ](/Attachments/1-3bb03d4c9ccc42fb847c1a58b8625c51.png)
    17. ![The Iterator Pattern &#xA;Client &#xA;Concrete Aggregate &#xA;Concretelterator ](/Attachments/1-65b2b8aeef554ad5a29b39e3499b2809.png)
    18. ![The Diner Iterator &#xA;public class DinerMenuIterator implements { &#xA;Menultem\[\] list; &#xA;int position = e; &#xA;public list) { &#xA;this.list = list; &#xA;public menultem next() { &#xA;Menultem menultem = list\[position\]; &#xA;position position + 1; &#xA;return menultem; &#xA;public boolean hasNext() { &#xA;if (position list. length Il list\[position\] null) { &#xA;return false; &#xA;return true; ](/Attachments/1-ec5b43e62c9e49e280557dd413408eb0.png)
    19. ![New and improved waitress code &#xA;public class Waitress { &#xA;Menu pancakeHouseMenu; &#xA;Menu dinerMenu; &#xA;public Waitress (Menu pancakeHouseMenu, Menu dinerMenu) { &#xA;this. pancakeHouseMenu = pancakeHouseMenu; &#xA;this. dinerMenu = dinerMenu; &#xA;public void iterator) { &#xA;while (iterator. hasNext()) { &#xA;Menultem menultem = iterator. next(); &#xA;System. out. print(menultem. getName() + &#xA;System. out. print(menultem. getPrice() + &amp;quot; &#xA;System. out. println (menultem. getDescription ( ) ) ; ](/Attachments/1-92491f0052e04c2bbbcc7c79037dfc7e.png)
    20. ![Using built-in iterators &#xA;To create your own menu iterator: &#xA;public Iterator&amp;lt;MenuItem&gt; createlterator() { &#xA;return new PancakeHouseMenuIterator(menuItems); &#xA;To use a built-in iterator: &#xA;public Iterator&amp;lt;MenuItem&gt; createlterator() { &#xA;return menultems . iterator(); ](/Attachments/1-73c6497515cc4056ba50238a9f7c8b1e.png)
6. Composite Pattern
    1. ![](/Attachments/1-11b86430963a494c8e877cb7563c954c.png)
    2. ![](/Attachments/1-b90151eeeee745ea987da9058018b261.png)
    3. DOM model in browser is a great example.
    4. How your page is represented in objects in the browser.
    5. Different types of objects, button, text, form.
    6. Treat them in similar ways in the DOM.
    7. For example, responding to events or adding other elements.
    8. See Chapter 9 in the book for grouping menu items.
    9. Think Decorator
        1. Using both inheritance and composition to get what we want.
    10. Note that Leaf does not implement the methods other than operation.
        1. <mark style="background: #FFF3A3A6;">Feels like a violation.</mark>
    11. Two more encapsulations after the break.
    12. (10 minute break)
7. Command Pattern
    1. ![COMMAND &#xA;Object Behavioral &#xA;Encapsulate a request as an object, then•by letting you parameterize &#xA;clients with different requests, queue or log requests, and support &#xA;undoalk• operations. &#xA;Motivation &#xA;Sometimes it's necessary to issue requests to Objects without knowing &#xA;anything about the operation being requested or the re€x•Åer of the &#xA;request. • I'hc Command pattern lets objects make requests of &#xA;unspecified application objects by turning the request itself into an &#xA;object, which can be stored and passed around like other objects. &#xA;Applicabili ty &#xA;Use the Command pattern when you want to: &#xA;• parameterize objects by an action to perform. Commands are an &#xA;object-oriented replacement for callbacks. &#xA;• specify, queue, and execute requests at different times. A Command &#xA;object can haw a lifetime independent of the original request. &#xA;• support undo. Command's execute operation can store State for &#xA;reversing its effects in the command itself. ](/Attachments/1-5dcf03e086194518b0eb1acbaf841e2e.png)
    2. ![You, the Customer, &#xA;give the Waitress &#xA;your Order, &#xA;O The Short-Order Cook prepares your meal &#xA;from the &#xA;O The Waitress &#xA;takes the Order, &#xA;places it on the &#xA;order counter, &#xA;and says &amp;quot;Order ](/Attachments/1-f45b640fb8dd487e88fc5d7c0a707f15.png)
    3. ![00 ](/Attachments/1-6daaf7ff1fd94b9d9cd2b7db83600045.png)
    4. ![makeBurger(), makeShake() ](/Attachments/1-74cc6d42cf9a49fcaf0451394cc2a83d.png)
    5. ![ORDER &#xA;f ](/Attachments/1-743411e32da34cc6b8fe812646ebccbd.png)
    6. Next waitress could take the pad and complete the order.
    7. Object contains reference to object that needs to prepare it.
    8. This design DOES completely decouple the objects.
    9. ![ΙΙΙ2!Ι2 ](/Attachments/1-7d889ba334b7428da471d567a5e3d53b.png)
    10. Command is our Order object
        1. All actions on the receiver
    11. The Receiver is the Cook
    12. Client is the User or Consumer or Customer
    13. Invoker is the Waitress
    14. ![Customer = client; Waitress = invoker; &#xA;Cook = receiver; Order = command &#xA;aient &#xA;tnvoxef &#xA;Recei ](/Attachments/1-083fe3b3262b4da4a6d74a670b643016.png)
    15. ![Command Pattern Structure &#xA;erecutef) &#xA;receiver. action ( ) ; ](/Attachments/1-5a09facc3e4e49978b8aa80cebd9fcd0.png)
    16. ![The Diner, in code &#xA;public class Diner { &#xA;public static void main(String\[\] args) { &#xA;Cook cook = new Cook(); &#xA;= new Waitress(); &#xA;Waitress waitress &#xA;= new Customer(waitress); &#xA;Customer customer &#xA;customer. createOrder(new BurgerAndFriesOrder(cook)); &#xA;customer. hungry( ) ; ](/Attachments/1-6e8fb0df897246d386c59d547f03f173.png)
    17. ![The Order (Command) &#xA;public interface Order { // Command interface &#xA;public void orderUp(); &#xA;public class BurgerAndFriesOrder implements Order { &#xA;Cook cook; &#xA;public &#xA;BurgerAndFriesOrder(Cook cook) { &#xA;this . cook = cook; &#xA;public &#xA;void orderUp() { &#xA;cook. makeBurger( ) ; &#xA;cook. makeFries(); ](/Attachments/1-db8e3235ba974a7bbac0376d8b665239.png)
    18. ![The Customer (Client) &#xA;public class Customer { &#xA;Waitress waitress; &#xA;Order order; &#xA;public Customer(Waitress waitress) { &#xA;this.waitress = waitress; &#xA;public void createOrder(Order order) { &#xA;this. order = order; &#xA;public void hungry() { &#xA;waitress . takeOrder(order) ; ](/Attachments/1-deaf7fe1522545c29d665c14c3e5734c.png)
    19. ![The Waitress (Invoker) &#xA;public class Waitress { &#xA;Order order; &#xA;public Waitress() { &#xA;public void takeOrder(Order order) { &#xA;this.order = order; &#xA;order. orderUp(); ](/Attachments/1-9bd2cb1f8d904c24aa8a04277fa21d2d.png)
    20. You don&#39;t necessarily need to call Execute right away, i.e. orderUp().
    21. ![The Cook (Receiver) &#xA;public class Cook { &#xA;public Cook() { } &#xA;public void makeBurger() { &#xA;System.out.print1n(&amp;quot;Making a burger&amp;quot;); &#xA;public void makeFries() { &#xA;System.out.print1n(&amp;quot;Making fries&amp;quot;); ](/Attachments/1-30c6b661ad8c4b24b112c630e3146541.png)
    22. ![Command Pattern Intent &#xA;The Command Pattern &#xA;Encapsulates a request as an object, &#xA;thereby letting you parameterize &#xA;other objects with different &#xA;requests, queue or log requests, and &#xA;support undoable operations. ](/Attachments/1-63a4f5994de648569b9dcb661764c9c3.png)
    23. See the book for queuing and logging.
    24. ![)ing Further &#xA;Qnote ](/Attachments/1-85617e2824734a4d827a31d2e711dea2.png)
    25. Chapter 6
    26. The order is like the callback function being passed around.
    27. ![Command in the Real World: &#xA;ActionListener &#xA;onButton. addActionListener(event -Y &#xA;light. setBackground (Color. YELLOW) &#xA;offButton. addActionListener(event &#xA;light. setBackground (Color. LIGHT_GRAY) &#xA;Interface ActionListener &#xA;All Methods &#xA;Modifier and Type &#xA;void &#xA;Method &#xA;actionPerformed (ActionEvent e) ](/Attachments/1-dd76171cb2164ed798e311b6e5ec0784.png)
    28. ![Sometimes objects participate in more &#xA;than one design pattern at a time. What &#xA;design pattern other than Command are &#xA;these objects participating in? &#xA;COO &#xA;onButton .addActionListener(event &#xA;light. setBackground (Color. YELLOW) &#xA;offButton.addActionListener(event &#xA;light. setBackground (Color. LIGHT_GRAY) ](/Attachments/1-2f6a710d3ba14184ac21e04be057243c.png)
    29. Observer!
    30. ![Exegci$e &#xA;on &#xA;Sometimes objects participate in more &#xA;than one design pattern at a time. What &#xA;design pattern other than Command are &#xA;these objects participating in? &#xA;The Observer Pattern! &#xA;onButton. addActionListener(event &#xA;light. setBackground (Color. YEL LOW) &#xA;offButton.addActionListener(event &#xA;light. setBackground (Color. LIGHT_GRAY) ](/Attachments/1-56ca346dcb124decbdce4e0b84b8f1c3.png)
    31. &quot;Listener&quot; is a dead give-away for Observer
8. Template Method Pattern
    1. Encapsulating Algorithms
    2. Different from Strategy
    3. Subclasses provide implementation of aspects of the algorithms.
    4. ![An example with tea &amp;amp; coffee &#xA;public class Tea { &#xA;void prepareRecipe() &#xA;boilWater(); &#xA;steepTeaBag( ) ; &#xA;pourInCup( ) ; &#xA;addLemon() ; &#xA;void boilWater() { • • • } &#xA;void steepTeaBag() &#xA;void pourInCup() { • • • } &#xA;void addLemon() { • • • } &#xA;public class Coffee { &#xA;void prepareRecipe() { &#xA;boilWater( ) ; &#xA;brewCoffeeGrinds ( ) ; &#xA;pourInCup( ) ; &#xA;addSugarAndMiIk( ) ; &#xA;void boilWater() { • • • } &#xA;void brewCoffeeGrinds() } &#xA;void pourInCup() { } &#xA;void addSugarAndMi1k() } ](/Attachments/1-c60d18fb670a43a5bd683be158968411.png)
    5. Same algorithm with a few differences.
    6. ![void prepareRecipe() { &#xA;boilWater(); &#xA;steepTeaBag( ) ; &#xA;pourInCup( ) ; &#xA;addLemon( ) ; &#xA;One solution &#xA;Tea &#xA;void prepareRecipe() { &#xA;boi Iwater() ; &#xA;brewCoffeeGrinds ( ) ; &#xA;pourInCup( ) ; &#xA;addSugarAndMi ( ) ; ](/Attachments/1-b30755835a5b4f978241f90164c33452.png)
    7. We have an Open Closed Principle issue with reimplementing prepareRecipe in both Coffee and Tea.
    8. ![Open-Closed Principle &#xA;Design Principle &#xA;Our code should remain open &#xA;for extension while closed for &#xA;modification ](/Attachments/1-431e8bf607884335a31111750eb33446.png)
    9. ![So we end up with... &#xA;void prepareRecipe ( ) { &#xA;boilWater ( ) ; &#xA;brew ( ) ; &#xA;pourInCup ( ) ; &#xA;addCondiments ( ) ; ](/Attachments/1-d2924b0ffec64eb0b560805963b8cec7.png)
    10. ![Refactoring our work: &#xA;public abstract class CaffeineBeverage { &#xA;final void prepareRecipe ( &#xA;boilWater ( ) ; &#xA;brev() &#xA;pourInCup ( ) ; &#xA;abstract void brew • &#xA;abstract void addCondiments () &#xA;void boilWater ( ) &#xA;System. out.println (&amp;quot;Boiling water&amp;quot;) ; &#xA;void pourInCup ( ) &#xA;System. out.println (&amp;quot;Pouring into cup&amp;quot;) ; ](/Attachments/1-3ad9f8f1dd974d96a1e5ca9164a15b97.png)
    11. Final void means children can&#39;t…???
        1. Subclasses cannot override prepareRecipe()
        2. Final means no modification
        3. Template for algorithm
        4. Can only override certain parts of the algorithm
        5. Algorithm is now poured in concrete
        6. No one can change it
    12. ![Refactoring our work: &#xA;public class Tea extends CaffeineBeverage { &#xA;public void brew ( ) ( &#xA;System. out. printin (&amp;quot;Steeping the tea&amp;quot;) ; &#xA;public void addCondiments { &#xA;System. out. printin (&amp;quot;Adding Lemon&amp;quot;) ; &#xA;public class Coffee extends CaffeineBeverage { &#xA;public void brew ( ) ( &#xA;System. out.println (&amp;quot;Dripping Coffee through filter&amp;quot;) ; &#xA;public void addCondiments ( ) &#xA;System. out. printin (&amp;quot;Adding Sugar and Milk&amp;quot;) ; ](/Attachments/1-c10ad314ae474f039dbc7a62c5e28578.png)
    13. ![What we Did &#xA;fea &#xA;water &#xA;O Steep the the water &#xA;O hurteainaeup &#xA;relies on &#xA;subclass &#xA;for sorne &#xA;Tea steps &#xA;Steep the teabag i&amp;quot; the water &#xA;O Add lemon &#xA;Caffeine Beverage &#xA;O Brew &#xA;O Pour beverage in a eup &#xA;O condiments &#xA;ee &#xA;water &#xA;O Brew theeoffeeørihd' &#xA;Poor coffee a cop &#xA;general &#xA;relies &#xA;subclass &#xA;for some &#xA;Steps &#xA;O brew the coffee &#xA;O Add sugar and Milk ](/Attachments/1-d4dc5304f87b491aaeef1a9669b8e7bd.png)
    14. ![Ihat we &#xA;nlly did &#xA;vas &#xA;mplement &#xA;he Template &#xA;Method &#xA;Design &#xA;Pattern &#xA;TEMPLATE METHOD &#xA;Class Behavioral &#xA;Define the skeleton of an algorithm in an operation, deferring some &#xA;steps to subclasses. Template Method lets subclasses redefine certain &#xA;steps of an algorithm, without changing the algorithm's structure. &#xA;Motivation &#xA;Consider an application framework that provides Application and &#xA;Docurnent classes. By defining some of the steps of an algorithm &#xA;using abstract operations, the template method in an abstract &#xA;Application class fixes their ordering (e.g. for opening and reading &#xA;a document), but it lets Application and Document subclasses vary &#xA;those steps to suit their needs. &#xA;•nie Template Method pattern should be used: &#xA;• to implement the invariant parts of an algorithm once and leave it &#xA;up to the subclasses to implement the behavior that can vary. &#xA;• when common behavior among subclasses should be factored and &#xA;localized in a common class to avoid code duplication. &#xA;• to control subclasses extensions. You can define a template meth«xl &#xA;that calls &amp;quot;hook&amp;quot; operations at specific points, thereby permitting &#xA;extensions only at those points. &#xA;Structure ](/Attachments/1-0f612fb77d92427aad3469c71978fc3c.png)
    15. Contrast this with Strategy
    16. Both behavioral patterns
    17. Strategy was object behavioral
    18. Template method is class behavioral
        1. We get the variation and behavior through template (?) instead of (?)
    19. Getting code reuse through inheritance
        1. Varying behavior
    20. ![The Template Method Structure &#xA;AbstractClass &#xA;templateMethod() &#xA;primitiveOperation I () &#xA;primitiveOperation2() &#xA;ConcreteClass &#xA;prmtjveOperabonl &#xA;prmüveOperatm2() &#xA;prmuveOperauon2(); ](/Attachments/1-154bb472e2334f059342b61751497d49.png)
    21. Pretty easy to wrap your head around this.
    22. Take note of who is calling whom
    23. ![Using Template Method &#xA;CaffeineBeverage &#xA;prepareReape() &#xA;pourlnCup() &#xA;Coffee &#xA;Il other methods &#xA;pourlnCup(), &#xA;addCondtrnents(); &#xA;Tea &#xA;Il other methods ](/Attachments/1-b3f3b0b85cdc41c69e0c780e4f1bbf44.png)
    24. Superclass calls methods in the subclasses
    25. ![Hollywood Principle &#xA;Design Principle: &#xA;The Hollywood Principle &#xA;Don't call us, we'll call you. ](/Attachments/1-f5525e0073c04429b82a256e494099f3.png)
    26. Low level components hook themselves into the system
    27. High level components determine when and how the low level components are needed.
    28. Reduces dependencies
    29. Allows replacement of components.
    30. Similar to Observer, but that&#39;s object based vs. class based
    31. Real world example in Java
    32. ![AbstractList &#xA;AbstractList &#xA;get(3); &#xA;get(it) &#xA;Il ottær methods &#xA;get(nt) ](/Attachments/1-7eab60a720f6464ba0a9b26e024fe2c4.png)
    33. Uses inheritance instead of composition, unlike many other patterns.
    34. Factory method pattern has a similar quality to it.
9. Next week will cover more patterns.
    1. Singleton, etc.
    2. ![The GoF &#xA;Strategy &#xA;Adapter &#xA;Facade &#xA;Decorator &#xA;Proxy &#xA;Observer &#xA;Iterator &#xA;Composite &#xA;Command &#xA;Design Patterns &#xA;Singleton &#xA;Prototype &#xA;Factory &#xA;Builder &#xA;Flyweight &#xA;State &#xA;Compound Patterns &#xA;Template Method ](/Attachments/1-978e8da32520455c9cd20a526c8c1922.png)
    3. Compound pattern is really fun.
        1. One of her favorites
        2. We&#39;ll also talk about patterns best practices.
10. Compare and contrast some of the patterns we&#39;ve already covered.
11. Walk through pattern catalog for review as a homework assignment.

<!-- InkNode is not supported --><!-- InkNode is not supported --><!-- InkNode is not supported --><!-- InkNode is not supported -->