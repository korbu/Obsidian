# Migrating ASP.NET Web Forms to ASP.NET Core

**Created**: Saturday, May 30, 2020 02:20:58 PM -04:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


**<span style="">From:</span>**<span style="">&#160;Ignacio Quijas Palos &lt;Ignacio.Quijas@microsoft.com&gt;</span>

**<span style="">Sent:</span>**<span style="">&#160;Thursday, May 28, 2020 10:49 AM</span>

**<span style="">To:</span>**<span style="">&#160;Mike Becker &lt;Mike.Becker@microsoft.com&gt;; Shiv Sidhu &lt;Shivkanwer.Sidhu@microsoft.com&gt;; WW Communities - Apps Domain &lt;wwcappsdomain@service.microsoft.com&gt;; WW Communities - Development &lt;WWCDevelopment@service.microsoft.com&gt;; .NET Community Discussion &lt;dotnetcommunity-disc@microsoft.com&gt;</span>

**<span style="">Subject:</span>**<span style="">&#160;RE: Migrating ASP.NET Web Forms to ASP.NET Core</span>

<span style="">&#160;</span>

<span style="">Hi&#160;</span>[@Shiv Sidhu](mailto:Shivkanwer.Sidhu@microsoft.com)<span style="">,</span>

<span style="">&#160;</span>

<span style="">There is specific guidance on&#160;</span>[migrating ASP .Net to ASP .Net Core](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Faspnet%2Fcore%2Fmigration%2Fproper-to-2x%2F%3Fview%3Daspnetcore-3.1&amp;data=02%7C01%7CRobert.Bernstein%40microsoft.com%7C16cb5640089b4f494cf308d8031658a0%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637262742122239737&amp;sdata=UxHJeG9Wm7%2B1a9bkmTkhHpqbg4k1KtGLQn7%2Bp2lRyZY%3D&amp;reserved=0)<span style="">&#160;that I have found very useful before. Regarding the specifics of web forms migration to .net core I would suggest this&#160;</span>[guide](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fgithub.com%2Friganti%2Fdotvvm-samples-webforms-migration&amp;data=02%7C01%7CRobert.Bernstein%40microsoft.com%7C16cb5640089b4f494cf308d8031658a0%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637262742122239737&amp;sdata=FXzHKowoK2gABdwQ%2FJ5G0iy8lXL1CGVFYzjgcOHzkwU%3D&amp;reserved=0)<span style="">&#160;by Thomas Herceg.</span>

<span style="">&#160;</span>

<span style="">Telerik also has a&#160;</span>[tool](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fwww.telerik.com%2Fblogs%2Fwebforms-to-razor-view-converter-tool&amp;data=02%7C01%7CRobert.Bernstein%40microsoft.com%7C16cb5640089b4f494cf308d8031658a0%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637262742122249732&amp;sdata=jdp5y4ZvZevRJ%2BRS8%2BNriET6JdNgSRm%2BNU8halOJKwo%3D&amp;reserved=0)<span style="">&#160;to convert WebForms to Razor that you could try on&#160;</span><span style="">&#128522;</span>

<span style="">&#160;</span>

<span style="">You should also considering&#160;</span>[breaking changes](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fdotnet%2Fcore%2Fcompatibility%2Ffx-core&amp;data=02%7C01%7CRobert.Bernstein%40microsoft.com%7C16cb5640089b4f494cf308d8031658a0%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637262742122249732&amp;sdata=A2ewWdMmfpnZh%2FmilW%2BJxIyH7ALBdbIcydV8VbYqC0Q%3D&amp;reserved=0)<span style="">&#160;can be present and must be addressed.</span>

<span style="">&#160;</span>

<span style="">Regards</span>

<span style="">&#160;</span>

**<span style="">From:</span>**<span style="">&#160;Mike Becker &lt;Mike.Becker@microsoft.com&gt;&#160;</span>

**<span style="">Sent:</span>**<span style="">&#160;Thursday, May 28, 2020 2:25 AM</span>

**<span style="">To:</span>**<span style="">&#160;Shiv Sidhu &lt;Shivkanwer.Sidhu@microsoft.com&gt;; WW Communities - Apps Domain &lt;wwcappsdomain@service.microsoft.com&gt;; WW Communities - Development &lt;WWCDevelopment@service.microsoft.com&gt;; .NET Community Discussion &lt;dotnetcommunity-disc@microsoft.com&gt;</span>

**<span style="">Subject:</span>**<span style="">&#160;RE: Migrating ASP.NET Web Forms to ASP.NET Core</span>

<span style="">&#160;</span>

<span style="">+WWC Dev, dotent DL for experience exchange</span>

<span style="">&#160;</span>

<span style="">Sent from&#160;</span>[Mail](https://go.microsoft.com/fwlink/?LinkId=550986)<span style="">&#160;for Windows 10</span>

<span style="">&#160;</span>

**<span style="">From:&#160;</span>**[Shiv Sidhu](mailto:Shivkanwer.Sidhu@microsoft.com)

**<span style="">Sent:&#160;</span>**<span style="">Thursday, May 28, 2020 8:59 AM</span>

**<span style="">To:&#160;</span>**[WW Communities - Apps Domain](mailto:wwcappsdomain@service.microsoft.com)

**<span style="">Subject:&#160;</span>**<span style="">Migrating ASP.NET Web Forms to ASP.NET Core</span>

<span style="">&#160;</span>

<span style="">Hi All,</span>

<span style="">&#160;</span>

<span style="">One of our Partners is in process of modernizing a legacy ASP.NET Web Forms application. They have decided to go for ASP.NET Core as the target platform. Once the application is modernized it is going to be hosted on Azure. I have following queries for which I need your assistance:</span>

- <span lang="en-IN"><span style="">Is there a case study available which is related with such migration (ASP.NET Web Forms to ASP.NET Core) that can be shared with the Partner?</span></span>
- <span lang="en-IN"><span style="">Is there a tool (Microsoft or 3</span><sup style="color:#323130">rd</sup><span style="">&#160;Party) that can help the partner in reducing the migration effort? (I checked&#160;</span><a href="https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fwww.dotvvm.com%2Fmodernize%23products&amp;data=02%7C01%7CRobert.Bernstein%40microsoft.com%7C16cb5640089b4f494cf308d8031658a0%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637262742122259728&amp;sdata=dVZrQTyg98%2BCf6pNVWs6XHHJuoE6%2F2Tnh8xwPTgedAM%3D&amp;reserved=0">DotVVM</a><span style="">&#160;and it looks promising)</span></span>
- <span lang="en-IN"><span style="">Are there any documents/templates available that contain some pre-defined set of questions which can be used by the partner as a starting point for capturing inputs from the customer and forming a migration strategy?</span></span>

<span style="">&#160;</span>

<span style="">Thanks &amp; Regards,</span>

**<span style="">Shivkanwer Singh Sidhu</span>**

<span style="">Partner Technical Consultant – Azure</span>

<span style="">Microsoft Global Partner Services</span>
![Microsoft](/Attachments/1-ac4f0fc6d5f90daa3554563fda1ad2cb.png)
<span style="background-color:white">﻿&#160;</span>