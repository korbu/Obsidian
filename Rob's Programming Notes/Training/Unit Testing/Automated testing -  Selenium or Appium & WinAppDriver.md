# Automated testing: Selenium or Appium/WinAppDriver

**Created**: Tuesday, March 28, 2017 08:51:24 AM -04:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


| **Subject** | **RE: Automated testing: PG contact** |
| --- | --- |
| **From** | Jelle Druyts |
| **To** | Prachi Bora; Carsten Duellmann; WW Communities - Testing; WW Communities - ALM and DevOps |
| **Cc** | Janice Choi |
| **Sent** | March 28, 2017 6:38 AM |

Hi Prachi,

Is there a public statement we can point people at, that explicitly mentions the guidance below about recommending Selenium? The https://blogs.msdn.microsoft.com/visualstudioalm/2016/03/10/visual-studio-team-services-testing-tools-roadmap/ article is less clear in the following statement:

>*Coded UI continues to be our preferred tool for Functional UI Automation for Desktop, Web and Store Apps.  With WebDriver becoming a W3C standard and strong enterprise demand to support Selenium for Web Apps, we will be improving our support for authoring and executing WebDriver based Selenium and Appium tests.  We will do selective feature enhancements to Coded UI such as UWP, Edge support etc. and encourage customers to use Selenium and Appium for Functional UI testing.*

So it seems to say “CUIT is the preferred tool” first, and then “but we encourage customers to use Selenium”. So if we can have a clear cut statement about the recommended way forward as in your email below that would be helpful.

Thanks,

Jelle

**From:** Prachi Bora
**Sent:** donderdag 16 maart 2017 9:08
**To:** Carsten Duellmann &lt;Carsten.Duellmann@microsoft.com&gt;; WW Communities - Testing &lt;wwcomtem@microsoft.com&gt;; WW Communities - ALM and DevOps &lt;wwcomalm@microsoft.com&gt;
**Cc:** Janice Choi &lt;janchoi@microsoft.com&gt;
**Subject:** RE: Automated testing: PG contact

Hi Carsten,

Coded UI remains fully supported for customers that are already using it.

For customers that are starting new projects / automation efforts, our guidance is that they use:

1. <mark style="background: #BBFABBA6;">Selenium for web-apps</mark> 
2. <mark style="background: #BBFABBA6;">For desktop and UWP apps use</mark> <a href="http://appium.io/">Appium</a> <mark style="background: #BBFABBA6;">with the</mark> <a href="https://github.com/Microsoft/WinAppDriver">WinAppDriver</a>. 

Thanks,
Prachi

**From:** Carsten Duellmann
**Sent:** Tuesday, March 14, 2017 2:31 PM
**To:** Prachi Bora &lt;Prachi.Bora@microsoft.com&gt;; WW Communities - Testing &lt;wwcomtem@microsoft.com&gt;; WW Communities - ALM and DevOps &lt;wwcomalm@microsoft.com&gt;
**Cc:** Janice Choi &lt;janchoi@microsoft.com&gt;
**Subject:** RE: Automated testing: PG contact

Hi Prachi,

Thank you very much for your offer! When I see your list below, the question that moves me most currently is this: Whenever I talk to customers about UI Testing the topic comes up whether Coded UI Test is still worth investing into. For Web, I mostly recommend Selenium nowadays, especially if cross browser matters to them (as CUIT itself [delegates to Selenium](https://msdn.microsoft.com/library/jj835758.aspx) for cross browser).

For desktop applications I am not sure what to recommend. What answer should we give a customer asking if they should still start with Coded UI Test?

Thanks
Carsten

**From:** Prachi Bora
**Sent:** Friday, March 10, 2017 4:22 PM
**To:** WW Communities - Testing &lt;wwcomtem@microsoft.com&gt;; WW Communities - ALM and DevOps &lt;wwcomalm@microsoft.com&gt;
**Cc:** Janice Choi &lt;janchoi@microsoft.com&gt;
**Subject:** Automated testing: PG contact

Folks,

I have seen some interesting threads on the aliases related to running automated tests.

I just wanted to reach out and say hello – I am the PM for automated testing experiences in VSTS / TFS.

I will be very happy to address queries / take feedback. Any of the following are fair game, feel free to reach out or loop me in:

1. Selenium tests
2. Appium tests
3. Running tests in build / release (CI/CD)
4. Running tests on-demand from MTM / Test Hub

I would also like to remind that Janice Choi (CC’ed) helps organize a PG sync up on a quarterly basis on automated testing in DevOps.

If you are interested to know what the PG is working on or have feedback to help shape the product backlog, please join these meetings.

Thanks,
Prachi