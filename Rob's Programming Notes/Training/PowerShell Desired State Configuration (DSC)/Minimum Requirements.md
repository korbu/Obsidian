# Minimum Requirements

**Created**: Tuesday, October 28, 2014 07:29:44 AM -04:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


| OS | Windows 7 SP1 x64 and x86,<br /><br />Windows 8.1,<br /><br />Windows Server 2008 R2 SP1,<br /><br />Windows Server 2012,<br /><br />Windows Server 2012 R2 | You cannot install this software on computers that are running Windows 8.<br /><br /><br />Windows PowerShell 4.0 is available as part of Windows 8.1.<br /><br /><br />Enable WinRM |
| --- | --- | --- |
| .NET Framework | v4.5 | <br /> |
| PowerShell Version | v4.0 | DSC is new to v4.0. |
| Windows Management Framework | v4.0 | http://www.microsoft.com/en-us/download/details.aspx?id=40855 |
| Built-In Windows PowerShell Desired State Configuration Resources | <br /> | http://technet.microsoft.com/en-us/library/dn249921.aspx |
| DSC Resource Kit Additions | <br /> | https://gallery.technet.microsoft.com/DSC-Resource-Kit-All-c449312d |
| Download ResKit | <br /> | Invoke-WebRequest -Uri 'https://gallery.technet.microsoft.com/DSC-Resource-Kit-All-c449312d/file/131371/1/DSC%20Resource%20Kit%20Wave%209%2012172014.zip' -OutFile "C:\Files\DSC-Wave9.zip" |
| PowerShell.org DSC Tools and Documentation | <br /> | https://github.com/PowerShellOrg/DSC/tree/master/ |
| <br /> | <br /> | http://sdmsoftware.com/group-policy-blog/desired-state-configuration/an-in-depth-walkthrough-of-desired-state-configuration-in-powershell-windows-management-framework-v4/ |
| DSC Forum | <br /> | http://powershell.org/wp/forums/forum/dsc-desired-state-configuration/ |
| DSC Snippets | <br /> | http://jdhitsolutions.com/blog/2014/05/dsc-resource-snippets/ |
| List all installed DSC commands and their options (i.e. a template) | <br /> | http://jdhitsolutions.com/blog/2014/05/creating-a-dsc-configuration-template/ |
| DSC Logging | <br /> | http://blogs.msdn.com/b/powershell/archive/2014/02/11/dsc-diagnostics-module-analyze-dsc-logs-instantly-now.aspx |
| Enforce NTFS permissions | <br /> | http://www.vexasoft.com/blogs/powershell/9561687-powershell-4-desired-state-configuration-enforce-ntfs-permissions |
| SQL Database Permissions when the IIS App Pool runs as "ApplicationPoolIdentity". | <br /> | Had to give permissions to "IIS APPPOOL\GETS Plus API AppPool"!<br /><br />- http://stackoverflow.com/questions/454497/iis7-sql-2008-and-asp-net-mvc-security<br /><br /><br />http://www.powershellmagazine.com/2013/05/17/pstip-adding-local-users-to-sql-server-logins-using-smo |
| Multiple "DependsOn"s | <br /> | https://social.technet.microsoft.com/Forums/scriptcenter/en-US/f8a293c7-31f7-4f17-bc41-2cf99752886c/dsc-multiple-dependson?forum=winserverpowershell |
| Sample Script block | <br /> | <br /><br />```<br />Script SetTimezone￼<br />{￼    GetScript = { return @{ Timezone = ("{0}" -f (tzutil.exe /g)) } }￼    TestScript = { return (tzutil.exe /g) -ieq "GMT Standard Time" }￼    SetScript = { tzutil.exe /s "GMT Standard Time" }￼}￼<br />```<br /><br /><br />From &lt;http://readsource.co.uk/blog/2013/7/9/using-powershell-dsc-script-resource-provider&gt; |
| PowerShell DSC Forum | <br /> | http://powershell.org/wp/forums/forum/dsc-desired-state-configuration/ |

Find all DSC command options:

1. Get-DscResource
2. Get-DscResource xWinEventLog | Select-Object -ExpandProperty Properties
3. Get-DscResource xWinEventLog -Syntax

Good examples of script resource:

1. https://github.com/jeffpatton1971/Desired-State-Configuration/blob/master/configurations/Setup-DSCPullServer.ps1
2. http://readsource.co.uk/blog/2013/7/9/using-powershell-dsc-script-resource-provider
3. http://www.wefixbugs.com/blog/DSC-can39t-load-WebAdministration-module-54965.html#.VIn0-Hl0yUk

http://readsource.co.uk/blog/2013/7/9/using-powershell-dsc-script-resource-provider