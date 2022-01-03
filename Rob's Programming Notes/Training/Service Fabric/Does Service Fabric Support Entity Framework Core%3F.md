# Does Service Fabric Support Entity Framework Core?

**Created**: Monday, July 10, 2017 10:37:17 AM -04:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


**<span style="">From:</span>** <span style="">Robert Vettor</span>
<span style=""> 					</span>**<span style="">Sent:</span>** <span style="">Thursday, July 6, 2017 1:59 AM</span>
<span style=""> 					</span>**<span style="">To:</span>** <span style="">Service Fabric Discussions; Entity Framework Discussions</span>
<span style=""> 					</span>**<span style="">Subject:</span>** <span style="">RE: Does Service Fabric Support Entity Framework Core?</span><span style=""> </span>

<span style="">&#160;</span>

<span style="">Update: Got EF Core to work with the ASP.NET Core Stateless Service.</span>

<span style="">&#160;</span>

<span style="">Even though I had added an explicit UserId and Password to the connection string, I found I had to remove the “trusted connection=true” attribute.</span>

<span style="">&#160;</span>

<span style="">The presence of the “trusted connected=true” causes the underlying process to ignore the UserId and Password attributes, which probably makes perfect sense, but is easy to miss.</span>

<span style="">&#160;</span>

<span style="">Would still very much appreciate any examples in which Service Fabric is leveraging Entity Framework.</span>

<span style="">&#160;</span>

<span style="">Thanks!</span>

<span style="">&#160;</span>

*<span style="">Rob</span>*

<span style="">&#160;</span>

**<span style="">Rob Vettor</span>** <span style="">|</span> <span style="">Senior AppDev/Azure PaaS Developer Consultant</span> <span style="">|</span> <span style="">- Modern Apps Domain</span>

<span style="">&#160;</span>
![MCSD_Small](/Attachments/1-8c1a477eb3354364b94424ced6c1895d.png)

![Description: cid:image001.gif@01CC9CCD.D94B9620](/Attachments/1-ff96e49ec0aa45e591e2380a09729021.gif)
<span style="">&#160;</span> <span style="">214-707-0584</span>
![Description: cid:image003.gif@01CC9CCD.D94B9620](/Attachments/1-b5fbe3f9c2184b059ce3ec10ba4f6604.gif)
<span style="">&#160;&#160;</span> robvet@microsoft.com

***<span style="">&#160;</span>***

***<span style="">Co-Author of…</span>***

<span style="">&#160;</span>

[!\[EF6Book\](/Attachments/1-3c333b79e6c74d6ebdd69593b126cb90.jpeg)](http://www.amazon.com/Entity-Framework-Recipes-Brian-Driscoll/dp/1430257881/ref=sr_1_1?ie=UTF8&amp;qid=1438987714&amp;sr=8-1&amp;keywords=entity+framework+6)

<span style="">&#160;</span>

[Check it out on Amazon...](http://www.amazon.com/Entity-Framework-Recipes-Brian-Driscoll/dp/1430257881/ref=sr_1_1?ie=UTF8&amp;qid=1438987714&amp;sr=8-1&amp;keywords=entity+framework+6)

<span style="">&#160;</span>

**<span style="">From:</span>** <span style="">Robert Vettor</span>
<span style="">Sent:</span> <span style="">Wednesday, July 5, 2017 10:45 PM</span>
<span style=""> 				</span>**<span style="">To:</span>** <span style="">Service Fabric Discussions</span> &lt;servicefabrictalk@microsoft.com<span style="">&gt;; Entity Framework Discussions</span> &lt;adonetef@microsoft.com<span style="">&gt;</span>
<span style=""> 				</span>**<span style="">Cc:</span>** <span style="">Robert Vettor</span> &lt;robvet@microsoft.com<span style="">&gt;</span>
<span style=""> 				</span>**<span style="">Subject:</span>** <span style="">Does Service Fabric Support Entity Framework Core?</span>

<span style="">&#160;</span>

<span style="">Am blocked attempting to create a Service Fabric reference architecture that leverages Entity Framework Core.</span>

<span style="">&#160;</span>

<span style="">Created a simple ASP.NET Core Stateful Service in which I scaffolded an Entity Framework context object and entity classes.</span>

<span style="">&#160;</span>

<span style="">To keep it simple as possible, I scaffolded the EF artifacts right into the ASP.NET Core Stateful Service project.</span>

<span style="">&#160;</span>

<span style="">Then, I use the local connection string that the EF scaffolding generated in the DbContext object:</span>

<span style="">&#160;</span>

`        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)`

```
        {
            optionsBuilder.UseSqlServer(@"Server=DESKTOP-5K4SVHG;Database=microjamsapi.productcatalog;Trusted_Connection=True;
            User Id=MicroJamsWriter;Password=P@ssw0rd1;");
        }
 
Here is the error that I get:
 
```
![Edit
project Team Format Layout Architecture
using System. Threading. Tasks;
using Microsoft .AspNetCore .Mvc;
c using webl.lnfrastructure;
•namespace Webl .Contr011ers
public class Homecontroller Controller
public IActionResu1t Index()
return View();
public IActionResu1t About()
Test
NuGet:
ReSharpet
•r: Web
new mic
Help
4
8
28
_ product cat aiogcnntext ctx
-e ctX .A1bums.
ViewData\[&quot;Message&quot;\] &quot;Your
return View();
public IActionResu1t Contact()
foiled for N,ORKCROW.DESKTOP.SKZSVHGS•.•
Details
EM eptim Settings ](/Attachments/1-0671df802461478cab05b2167470323f.jpeg)
<span style="">&#160;</span>

- <span style="">System.Data.SqlClient.SqlException: Login failed for user ‘Workgroup\Desktop-5K4SVHG. Note how it is appending “Workgroup” to the computer name “Desktop-5K4SVHG”.</span>

<span style="">&#160;</span>

<span style="">Couple of thoughts here:</span>

<span style="">&#160;</span>

- <span style="">This code works fine in an ASP.NET Core Application that runs outside of Service Fabric</span>
- <span style="">I’ve searched high and low and cannot find any meaningful references to using Entity Framework Core or Entity Framework 6 with Service Fabric</span>

<span style="">&#160;</span>

<span style="">Would appreciate an example and any input!</span>

<span style="">&#160;</span>

<span style="">Thanks!!</span>

<span style="">&#160;</span>

<span style="">Btw, here’s the entire exception:</span>

<span style="">&#160;</span>
![QuickWatch
Expression:
Value:
Name
Sexceptlon
Class
ClientConnectionId
Data
ErrorCcde
Errors
HResuIt
HelpLink
InnerException
Lin eNumber
Message
Number
Procedure
Server
Source
Stac kTrace
State
TargetSite
Static members
Non-Public members
x
Reevaluate
Add Watch
Value
{&quot;Login failed for user .0
{3a882f7e-c636-4b5g-a96f-7bcfe60cd683}
{System. Collections. ListDictionaryInternaI}
-2146232060
{System. Data.SqICIient.SqIErrorCoIIection}
2146232060
65536
&quot;Login failed for user
18456
&quot;DESKTOP-5K4SVHG&quot;
&quot; .Net SqICIient Data Provider&quot;
at System.DataSqICIient.SqIInternaIConnectionTds..ctor(DbConnectionPooIIdentit,&#39; identity, SqIConnectionString connectionOptions, SqICrecIr •
Systeml
byte
System.(
System. (
Systeml
string
System.E
string
string
string
string
string
byte
{Void .ctor(System.Data.Provider8ase.DbConnectionPooIIdentity, System.DataSqICIlent.SqIConnectionString, System.DataSqICIient.SqICredentiaI, Syst System.F ](/Attachments/1-8704d6bfc48a46f4848d73fc9c6d5708.jpeg)
<span style="">&#160;</span>

<span style="">&#160;</span>

*<span style="">Rob</span>*

<span style="">&#160;</span>

**<span style="">Rob Vettor</span>** <span style="">|</span> <span style="">Senior AppDev/Azure PaaS Developer Consultant</span> <span style="">|</span> <span style="">- Modern Apps Domain</span>