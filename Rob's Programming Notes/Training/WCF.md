# WCF

**Created**: Wednesday, June 02, 2021 09:56:18 PM -04:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


Day 1: 03/28/2006

=================

aaron@pluralsight.com

http://www.pluralsight.com/aaron/courses/2006-03-wcf

Channel Stack =&gt; Under the service side (vs. client)

Under Dispatcher =&gt; Message transform logic

Share schema and contract, not implementation =&gt; XML

- Message passing

- Not calling interfaces

XML - Data Structure

XSD - Schema Definition

WSDL - Describes the contract

SOAP - Package and send messages

- v1.2 not an acronym any more

- v0.9 the goal was just to make COM work on the Internet

- Now: objects are bad!

SOAP

----

&lt;soap:Envelope xmlns:soap="http://..."&gt;

&lt;soap:Header&gt;

...

&lt;/soap:Header&gt;

&lt;soap:Body&gt;

...

&lt;/soap:Body&gt;

&lt;/soap:Envelope&gt;

REST, Plain Old XML =&gt; HTTP

SOAP =&gt; decouple from HTTP

- Transport neutrality

WS-I =&gt; The W3C Police

- Test

- Write up a document (i.e. a Profile) pointing out errors and incompatibilities

- "Do this", "Don't do that"

SRT = Security, Reliability, Transactions

Lots of specs are still being written

- Lots of churn

SO = Decoupling + reuse

Service = Passive

Client = Initiate

Client

- Should it expect a response?

WSDL is the universal language for sharing endpoints + policy (inside WSDL)

a b c = address, binding, contract

svcutil.exe =&gt; generate code from metadata (i.e. WSDL)

(Tony suggested looking at www.ikvm.net)

In some of the labs, try running two clients at the same time

Day 2: 03/29/2006

=================

TcpTrace

Hosting

.Net Reflector: http://www.aisto.com/roeder/dotnet/

COM+ is one legacy element that will move forward

- You can wrap it in a WCF component

SvcCfgEditor =&gt; File / Integrate...

- C:\WINDOWS\WinFX\v3.0\Windows Communication Foundation

- You can choose which methods to expose

- Cmd Line: comsvcconfig.exe

When you create a Windows NT Service, do not add an installer project

- Go to the Service Design Surface (gray component page), right-click, and choose "Add Installer"

- Then at the cmd line, use installutil

On-demand activation

- Services are run when their ports are touched

Run the IIS administration console

- Apps are isolated directories: Virtual Directory

- Apps have different icons from std virt dirs.

- Icon has spinning-ball look like COM+ (but doesn't spin)

- Think of apps as separate processes

Application Pools

- Select isolation mode

In order to get IIS to redirect requests to our code, need to tell the HTTP Listener Adapter

Make sure that the service is in the bin directory of your IIS app dir

- Obviously, only http bindings work in IIS 5.1/6.0

- Use WAS for IIS 7

Create a WinFX Service project in VS2005

IIS 7 is just the HTTP Adapter

- Everything else has been moved out and into the Kernel and the WAS

- WAS wakes up and redirects requests

In lab 4 when you install your service, make sure you specify the username as machinename\username.

XML Miniclass (Day 2 Lunch)

===========================

He worked for FranklinCovey; built their PIM for Windows

Ini Files

[Distributor]

Name=

Id=

Sponsor=FID

...

[...]

XML arrived ~1998

The key to XML is that everyone agreed on a format around the same time

- Ubiquity

- Developer doesn't have to write the parsing code anymore

- Lots of Daves in the XML parser

=&gt; Then you need to write about 1/2 the code! (He did)

The XML Infoset: UML description of an XML document

- XmlReader in .Net

- With things like XPath, the order of the fields becomes irrelevant; can ask for fields by Name instead

- XML Query is like SQL

- XML Schema -- explicit; with ini files, schema was implicit;

- With schemas, you can validate that data conforms

If you use a standard XML encoding, you don't need to use the XML declaration (i.e. &lt;?xml version...&gt;)

- XML declaration MUST be the first thing in the file

- Serialization depends upon the character encoding

- UTF-8 and UTF-16 must both be implemented encodings

- What is the difference between UTF-8 and UTF-16?

- BOM (Byte Order Mark) MUST be present if the XML Declaration is not specified

Element is top level (e.g. StockQuote), attributes are part of an Element (e.g. symbol):

&lt;StockQuote symbol="MSFT"&gt;

&lt;CurrentPrice&gt;24.4&lt;/CurrentPrice&gt;

&lt;StartPrice&gt;20.0&lt;/StartPrice&gt;

&lt;Timestamp&gt;2006-03-29&lt;/Timestamp&gt;

&lt;/StockQuote&gt;

&lt;StockQuote symbol="GOOG"&gt;

&lt;CurrentPrice&gt;24.4&lt;/CurrentPrice&gt;

&lt;StartPrice&gt;20.0&lt;/StartPrice&gt;

&lt;Timestamp&gt;2006-03-29&lt;/Timestamp&gt;

&lt;/StockQuote&gt;

- Elements are meant to be viewable (i.e. the data)

- Attributes are meant to be metadata (not displayed)

Rename .xml to .htm and open the file in the browser.  You will just see the elements.

These days, you would typically put everything in elements.  Protocols would use attributes.

- But you can use either; it's up to you.

Is this a well-formed XML document?

- No.  Why?

- Only one top-level element

- No overlapping elements

XML is strict and simple -- makes it easy to write the parsers

XmlReader is like a depth-first search of the tree nodes of our document

Low-level XML Reader:

XmlReader r = XmlReader.Create(filename);

while (r.Read())

Console.Writeline("{0} -- {1}", r.Name, r.Value);

or a higher-level reader:

XmlDocument doc = new XmlDocument();

doc.Load(@"filename");

// XPath expression

XmlNodeList results =

doc.SelectNodes("/Quotes/StockQuote[CurrentPrice &gt; 25]");	// Quotes: Not global namespace, NO namespace

// use "//StockQuote[..." to find them once x: is defined

foreach (XmlNode n in results)

Console.Writeline("{0}: {1}",

n.SelectSingleNode("@Symbol").Value,	// @ means attribute

n.SelectSingleNode("CurrentPrice").InnerText);

Look into XSLT (no time now)

Namespaces

- Uniquely identify an element

- When receiving documents from different sources

- Two different "StockQuote" elements in two different documents, NS lets you differentiate

- e.g. Different endpoint versions with different structures

- Allows us to qualify our elements with a unique name

&lt;Quotes xmlns="http://pluralsight.com/stocks"&gt;

&lt;x:Quotes xmlns:x="http://pluralsight.com/stocks"&gt;

...

- Now, only the root element is in a namespace.  The rest of the elements are in NO namespace

XmlNamespaceManager ns = new XmlNamespaceManager(doc.NameTable);

ns.AddNamespace("z", "http://pluralsight.com/stocks");

XmlNodeList results =

doc.SelectNodes("/z:Quotes/z:StockQuote[z:CurrentPrice &gt; 25]", ns);

foreach (XmlNode n in results)

Console.Writeline("{0}: {1}",

n.SelectSingleNode("@Symbol", ns).Value,	// @ means attribute

n.SelectSingleNode("z:CurrentPrice", ns).InnerText);

Back to xml file:

&lt;s:Quotes xmlns:s="http:..."&gt;

&lt;...&gt;

You can qualify just the root element or you can qualify everything with a namespace

- You can do a mixture

SOAP only has three elements: Envelope, Body, Header

- Each one of those will have elements that you define

Schemas:

Create an XSD in VS2005

- Specify "unqualified" for local elements (i.e. not the root element)

- Once you define a schema, Intellisense will kick in for VS2005 xml docs

- Will inform you when you have invalid XML

MTOM uses MIME -- binary data

Serialization is the key =&gt; XML is a data model

XML Schema lays types on top of XML

Think C#: You can either fully qualify items with their namespace, or

you can use a using statement.

&lt;x:StockQuotes x="PS.Namespace"&gt;

In XML, specify xmlns in the root element and then entire document falls into the unnamed namespace

Lecture 5

=========

WCF can translate XSD into .NET classes

It can also translate .NET classes from XSD

- svcutil.exe /dataContractOnly

- xsd.exe /classes

DataContractSerializer and NetDataContractSerializer

- These used to be called XmlFormatter

- Can only do attributes with XmlSerializer

- There are three classes XmlDictionaryReader/Writer: Text, Binary, MTOM

- They can all be used with XmlSerializer

You can only serialize the public types (only exposed elements of the contract)

In XSD, strings can be null and have minOccurs="0" to represent that

- Actually means reference (0) versus value (1) types

XmlSerializer REQUIRES a public default constructor!

XmlSerializer adds xsi and xsd namespaces, but they are not used

- You can delete them

- Just helping you if you need them later

XmlSerializer ignore all of the attributes added by WCF (e.g. [DataContract], etc.)

- Uses XmlRoot, XmlAttribute, XmlElement

If you add junk or change names of your elements, XmlSerializer will ignore added stuff

and will revert to default values for elements it cannot find (e.g. "0")

Downsides: Opt-out can be a security risk

DataContractSerializer is a small subset of XSD

- Opt-in

- Replaces all old remoting code

[Serializable]

- All fields are serialized (e.g. to a remote system)

- Properties are not because they would just be duplicates of fields

- Primarily used to bring old .NET remoting code forward to WCF

- IXmlSerializable lets you break out of this model completely

- Totally customizable

[DataContract]

- This is what MS wants you to use

- Everything should use DataContract

NetDataContractSerializer

- Looks up type at runtime, sends it over the wire

- Type, AssmemblyName show up in the XML

- Microsoft strongly discourages using this

- Hard to turn it on; he'll show us how

Advanced Topics

- Everything in the type hierarchy must be serializable (e.g. an Address type inside a Person type)

- What if you don't have the source?

- Use IDataContractSurrogate

- You create a method that pulls out all relevant data and copies it to a known, serializable object type

XmlSerializerFormat attribute

Lab 5

=====

Be careful about displaying your object with WriteLine(myObj).  Only the items specified in the overridden ToString will be displayed.

DataContractSerializer includes anything annotated with DataContract or DataMember

Serializable includes all fields, but never properties.

Note that [System.SerializableAttribute()] is the same as [Serializable]

- The compiler translates this behind the scenes

Lecture 6

=========

'c' is underlined because it is the c of the abc model

Always request/response by default

- You will know if there are exceptions

parameters is circled because:

- holdover from asmx

- only one type going in and one going out

- Tempting to use a parameter list, though

- Behind the scenes, if you look at the messages, there is a single element that has multiple attributes that map to your parameters

- Creates a wrapper element that takes the whole thing

- Once you run it through a code generator, you will see how it translated your code + parameter list

- There is a way to "wink" at the code generator that will turn the parameter class back into a list of parameters

- Try it with "parameter" and "parameters" =&gt; very different results

Message represents what's going to go out on the wire

- You can display this

- It's the SOAP envelope

MessageContract is more of an advanced feature

- Usually your parameters, etc. will go in the SOAP body

- However, you can use this to put parameters in the SOAP header

- Or other data in the header

One-Way =&gt; No SOAP faults returned (obviously)

Request-Reply =&gt; Could be fault info returned

Duplex =&gt; Bidirectional

Duplex contracts will almost definitely fail when exchanging WSDL contracts with Java

- Duplex uses two one-way contracts; one input, one output

- The output corresponding to the input used is just dropped on the floor

- The input corresponding to the output used is also just dropped on the floor

Cannot map faults for web services in .NET 1.1 to different types

- No classifications

- Just one catch-all

Fault Exceptions do not send unhandled exceptions back to the client by default

- This would be a security issue

- There is a knob to turn this back on =&gt; "returnUnknownExceptionsAsFaults"

Sessions

- Requires a binding at run-time

- Demands support for sessions

Day 3: 03/30/2006

=================

Lab

http://localhost:8080/auction?wsdl=wsdl1

url?wsdl       = Concrete Definitions

url?wsdl=wsdl1 = Abstract Definitions

http://localhost:8080/auction?xsd=xsd0

AddListing instead of AddNewListing

Lecture 7 - Bindings

====================

Bindings are all about the wire

Transport Security Binding Elements

- Windows is Kerberos

Prebuilt bindings are pretty constrained

- Customizing lets you tweak the existing ones or create entirely new ones

Note that the WindowsStreamSecurityBindingElement goes

after BinaryMessageEncodingBindingElement

The Protocol Binding Elements have lots of properties you can set

- Especially security; it's pretty complicated

When connecting to Java web services where the bindings don't match

exactly, which is almost exactly the case, the WSDL will translate

into custom binding classes.

Lecture 8 - Behaviors

=====================

Service behaviors affect the whole runtime

A or X, A=Attribute, X = XML \_ELEMENT\_

You can write your own behaviors

For PerCall, runtime ignores all threading issues (whether you request them or not)

PerSession is related to channels

- The instance will be released as soon as the channel is closed

Shareable

- Client 1 must pass the session information to Client 2

- There is a programmatic method for doing this

- This mode may be yanked before WCF is RTM'd

- Aaron doesn't see a lot of use for this

- Uses InstanceID's in each message

To have clients call a specific method before any others, you

would mark all methods with IsInitiating = false except for

the one method that needs to be called first.

IsTerminating = true means session is no longer valid

- Further calls will raise exceptions; i.e. can't make any more calls

- Only way to truly dispose of the object is to delete the ChannelFactory

Sessions can be problematic

- Good for .NET remoting or COM+ situations

- Not good for Enterprise-scaled operations

- Might use sessionful binding, though

Lab

===

Step 6f: you still get an exception, but it is not handled as we did above (rfb)

Lecture 9

=========

Slide 5: Reliable messaging is implemented at the SOAP layer

Transactions

- If one thing goes wrong, you want a collection of things to be rolled back

- DTS are all about this; DTC - dist xact coord

- MSMQ

- State Management Resource

Queues

- Provide durability

- What if server goes down after submitting msg?

- Client on an airplane: work offline

- Messages move from queue-to-queue

Dropped connections will be reestablished

- Tries a specified number of times (8?)

- Has a timeout, so tries for a period each time

He did a demo showing how tcptrace.exe acted as a router, closed tcptrace,

it hung instead of exceptioning out while it was retrying to connect.  Then

he reopened tcptrace, and the app picked up where it left off.  This is

similar to a router going down on your network.

COM+ was transactional

- This was the benefit of COM+

- DTC did the coordination

Transactions are hard over the Internet

- Web services may go down

Look up a great transactional book (see end of lecture)

Exiting the using body for TransactionScope without calling Complete

causes the transaction to rollback

- You can say Scope=true and autocomplete=true and it takes care of everything for you

This class in C# 2.0 makes lightweight transactions easy

If an exception occurs on the client after the server has finished its tasks

and has returned control, the client will automatically notify the server

and the server will roll everything back!  Cool!

Queues

- Think TicketMaster

- Flooded when concert tickets become available

- Other times, absolutely silent

Day 4: 03/31/2006

=================

You definitely still want to install the COM+ update hotfix for the WinFX runtime if you

are going to "migrate" COM+ components (e.g. if you are going to try some of the COM+

lab exercises)

Lecture 10

==========

Transport security tends to be a lot faster than message security

- Transport is focused on raw bytes; message is XML, all text - must base64 encode first

Federation and Infocard are introduced in Vista

- Single Sign-on?

TCP/NP = TCP or Named Pipes

- These are Windows stream security in WCF

Message Security

- Messages become about 10x larger with all the extra encoding and security stuff

TCP and NP bindings use Windows authn (i.e. Kerberos)

SSL

- Server is authenticating itself to the client

- If client doesn't recognize the server's credentials, it will either fail or you

will get a warning =&gt; Are you sure?

Certificate means mutual certificate authentication

Issued Token means Federated Identity (Infocard)

- Infocard is intended to be a replacement for Passport

- Certificates are hard to manage =&gt; PKI Infrastructure

Slides 15 and 16 are equivalent (programmatic vs. a behavior, i.e. declaratively)

- Impersonation is the server running code as the client

AzMan is a Role Provider

- Roles are like application-specific groups

WCF uses claims

- Think about your driver's license

- Makes claims about you: brown hair, etc.

Keith Brown recommended running as Network Service

- Could deploy as Network Service

- However, with a custom acct, you have finer-grained control

Input Validation Tutorials

http://channel9.msdn.com/wiki/default.aspx/SecurityWiki.InputValidationTrainingModules

Lecture 11 - Interoperability

=============================

Integration on Windows

- You probably don't even need to touch the original code

- Wrap it with WCF (e.g. COM+)

- All about pain thresholds, money available

Interop really means "on the wire"

WCF supports SOAP v1.1 and v1.2

- v1.2 may not work with a lot of existing toolkits that are out there

Streaming bodies onto the transport almost definitely won't work with other

implementations

BizTalk is an integration server

- Integrate legacy systems through adapters

- Integrates with ASMX and WSE today

- Over 100 BTS adapters; could be converted to WCF channels in the future (and not need BTS)

eBay has a really wacky SOAP API

- Built on Java

- Does not interoperate well with WCF

- Always uses SSL

- Have to build up a funky URL (requestURL in his code)

- They're not using SOAP the way it was meant to be

- They are following the REST model more than SOAP

- Custom element must be present in the body of each SOAP message

- Simplest function in eBay API is GetEbayOfficialTimeRequest

- Expected it to be simple; set his bar low

- WSDL is so huge, you cannot display it in IE

- The XSLT engine hangs!

- The eBayAPISoapBinding was imported from the WSDL

- Cater to the REST, Plain Old XML crowd

WCF will try to use the default address

- This won't work because the URL needs to have all the credential junk in it

eBay doesn't put quotes around charset, which should have them

- MS implemented a fix to get around this, but it disappeared

- This is either the encoding or the transport; the encoding

- See MessageEncoder class

"The Law of Leaky Abstractions" - Joel Spolsky

- An abstraction is not a reason to not understand how something works under the covers

Church of the SubGenius

SRT - Security, Reliable Messaging, Transactioning

One WCF service per COM class

Explicit boundaries

.NET Enterprise Services are hosted in COM+

- See ServicedComponent class (i.e. COM)

- gacutil /i AuctionComponent.dll = &gt; Installs into C:\Windows\Assembly (i.e. The GAC)

- regsvcs AuctionComponent.dll =&gt; installs into COM+

- COM+ can be hosted as a server app or a library app

- Look at COM+ Activation tab in Component Services control panel applet

- Typically hosting within IIS =&gt; Library app

- Publish it as a WFC service =&gt; use ComSvcConfig.exe

- /hosting:complus for an app or /hosting:was for website

- This provides a really nice wizard

- Can add a MEX endpoint

- Web site: use Web Sharing tab in Windows Explorer to create a virtual directory (i.e. web site)

- .svc file and .config file are generated

- Notice &lt;comContract&gt; extension XML tag

You can put your entire WSDL in the service moniker "string" (?)

We can also call COM clients to affect our WCF services

- contract="COM+ GUID" in lab exercise

- This is in a .js file

- Annotate interface with a GUID

- Make sure to register the assembly with the GAC

- Make sure to call regsvcs on the COM+ component (use /tlb to get the type library) (?) - didn't work

- Maybe regasm? - also didn't work

- Something is wrong in the lab, because these are the steps he told us to take in the lab

- Needed to specify the output file for the tlb (?)

- He got it working

MSMQ

- LCE = Loosely Coupled Events

Lecture 12

==========

Use ByteArrays in your data contracts

- ASMX and WCF will correctly handle this

- Will convert to BASE64

Reference by URI

- This is instead of embedding binary in XML

- More efficient

- Out-of-band

- End-user may not have access to some of the URL's referenced in the XML document (firewalls)

- May be queueing the messages for later access

Different methods of packaging have been tried

- SOAP with attachments

- DIME =&gt; was introduced in WSE

- No one implemented but Microsoft

- Dying =&gt; no interop

- Going away in WSE 3.0

- Don't use it

SOAP Infosets =&gt;  ByteArrays

XOP is a standard as of early last year

- Defines the transformation

- XOP works with any XML, not just SOAP (i.e. just the transformation)

MTOM "glues" XOP to SOAP

Slide 16: Using EITHER XML 1.0 \*or\* MTOM

MessageEncoding (which is part of the binding) affects whether we use XML 1.0 or MTOM

Lab

He separated out IListingImages from the IAuctionService so he can use a different encoding, such

as MTOM, for images.  Otherwise, everything would have to use MTOM.

WCF uses buffered messages for everything

- This is not good for sending large files around (e.g. movie files, 100 MB)

Chunking

- You break message up into smaller pieces and send each piece separately

- You have to break it up and reassemble it manually

- You will want to use RM to accomplish this

Streaming

- Use System.IO.Stream in your data contract

- Server side writes directly to the transport, just like sockets

- Client reads from stream, like a socket

- Not very interoperable

- Set TransferMode "knob" to "StreamedResponse"

ChunkChannel was a sample shown at PDC

- You can download this

Lecture 13

==========

Cannot use an attribute to add an endpoint behavior

- Must be added at runtime

MessageEncoders are implemented differently from other low-level customizations

- Look at his eBay code