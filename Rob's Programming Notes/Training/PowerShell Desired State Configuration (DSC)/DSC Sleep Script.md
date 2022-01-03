# DSC Sleep Script

**Created**: Thursday, December 11, 2014 05:37:17 PM -05:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


# Good examples of script resource:

#    https://github.com/jeffpatton1971/Desired-State-Configuration/blob/master/configurations/Setup-DSCPullServer.ps1

#    http://readsource.co.uk/blog/2013/7/9/using-powershell-dsc-script-resource-provider

#    http://www.wefixbugs.com/blog/DSC-can39t-load-WebAdministration-module-54965.html#.VIn0-Hl0yUk

Script WaitForZipFileToBeUnlocked

{

GetScript = {

Return = @{ Result = ("") }

}

TestScript = {

Return $true

}

SetScript = {

Start-Sleep -Seconds 1

}

DependsOn = "[Archive]UnzipResKit"

}