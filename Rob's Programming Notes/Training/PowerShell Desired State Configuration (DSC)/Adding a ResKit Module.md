# Adding a ResKit Module

**Created**: Monday, November 03, 2014 06:32:08 PM -05:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


Download the DSC Resource Kit (All Modules) from here:

https://gallery.technet.microsoft.com/scriptcenter/DSC-Resource-Kit-All-c449312d

Download the xWebAdministration DSC module from here:

https://gallery.technet.microsoft.com/scriptcenter/xWebAdministration-Module-3c8bb6be

1. Download the appropriate zip file from the web site, e.g. xWebAdministration\_1.3.2.zip
2. Unzip the subdirectory contained within it to the $env:ProgramFiles\WindowsPowerShell\Modules folder.
    1. The unzipped module files must exist on the machine where you are running the PowerShell DSC script to generate the .mof files.
    2. The unzipped module files must exist on the target server which you are configuring.
3. Your finished path should look similar to the following:
    1. C:\Program Files\WindowsPowerShell\Modules\xWebAdministration
4. Now run Get-DscResource from the PSH prompt to ensure that the new modules appear, e.g. xWebsite.
5. http://www.powershellmagazine.com/2013/09/02/copying-powershell-modules-and-custom-dsc-resources-using-dsc/
6. http://blogs.msdn.com/b/powershell/archive/2014/02/07/need-more-dsc-resources-announcing-dsc-resource-kit-wave-2.aspx
7. [https://gallery.technet.microsoft.com/site/search?query=dsc%20resource%20kit&f%5B0%5D.Value=dsc%20resource%20kit&f%5B0%5D.Type=SearchText&ac=2](https://gallery.technet.microsoft.com/site/search?query=dsc%20resource%20kit&amp;f%5B0%5D.Value=dsc%20resource%20kit&amp;f%5B0%5D.Type=SearchText&amp;ac=2)

# File copy permissions problem

http://newdelhipowershellusergroup.blogspot.com/2014/05/powershell-and-dsc-using-file-resource.html

**<span style="background-color:white">What happen?</span>** <span style="background-color:white">Why it not able to Copy the files from local share to the Server?, we run the ISE as “Administrator”</span> **<span style="background-color:white">it should be working!</span>**<span style="background-color:white"> </span><span style="background-color:white">No</span><span style="background-color:white">?</span>

**<span style="background-color:white">NO!</span>**

<span style="background-color:white">The problem is (</span> [thanks to PowerShellMagazine.com](http://www.powershellmagazine.com/2013/09/02/copying-powershell-modules-and-custom-dsc-resources-using-dsc/)<span style="background-color:white">) DSC Local Configuration Manager runs as the</span> **<span style="color:red;background-color:white">SYSTEM</span>** <span style="background-color:white">account and</span> **<span style="color:red;background-color:white">won’t have access to network resources</span>**<span style="background-color:white">. We have to give permission to them.</span>

**`To solve this, we have to add both, the client computer and the Sever computer account to the network share directory and give them read only access.`**

**<span style="background-color:white">How to add Computer account to the share?</span>**

<span style="background-color:white">It’s simple, Right click on your</span> **<span style="background-color:white">Share Folder</span>**<span style="background-color:white">, Click on</span> **<span style="background-color:white">Properties,</span>** <span style="background-color:white">in</span> **<span style="background-color:white">Security</span>**<span style="background-color:white"> </span>**<span style="background-color:white">Tab</span>**<span style="background-color:white">, click on</span> **<span style="background-color:white">edit</span>**<span style="background-color:white">, in</span> **<span style="background-color:white">Object</span>** <span style="background-color:white">Type , select “</span>**<span style="background-color:white">Computers</span>**<span style="background-color:white">”, click on “</span>**<span style="background-color:white">OK</span>**<span style="background-color:white">” and then in “</span>**<span style="background-color:white">enter the Object Name Box</span>**<span style="background-color:white">”, type your both computer names and add them.</span>

From &lt;http://newdelhipowershellusergroup.blogspot.com/2014/05/powershell-and-dsc-using-file-resource.html&gt;

`dir cert:\localmachine\my`

From &lt;http://www.iis.net/learn/manage/powershell/powershell-snap-in-configuring-ssl-with-the-iis-powershell-snap-in&gt;

When importing the certificate, check the box "Mark Exportable". Works fine now.

From http://forums.iis.net/t/1149042.aspx

Get-WindowsFeature

dir Cert:\LocalMachine\WebHosting | ? { $\_.Subject -eq "CN=robernst-gcc12.redmond.corp.microsoft.com" }