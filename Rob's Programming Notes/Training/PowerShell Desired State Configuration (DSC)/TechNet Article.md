# TechNet Article

**Created**: Tuesday, October 28, 2014 07:23:24 AM -04:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


DSC is a new management platform in Windows PowerShell that enables deploying and managing configuration data for software services and managing the environment in which these services run.

From &lt;http://technet.microsoft.com/en-us/library/dn249912.aspx&gt;

DSC provides a set of Windows PowerShell language extensions, new Windows PowerShell cmdlets, and resources that you can use to declaratively specify how you want your software environment to be configured. It also provides a means to maintain and manage existing configurations.

DSC introduces a new keyword called **<span style="">Configuration</span>**. To use DSC to configure your environment, first define a Windows PowerShell script block using the **<span style="">Configuration</span>** keyword, then follow it with an identifier, then with braces (**<span style="">{}</span>**) to delimit the block.

From &lt;http://technet.microsoft.com/en-us/library/dn249918.aspx&gt;

Inside the configuration block you can define node blocks that specify the desired configuration for each node (computer) in your environment. A node block starts with the **<span style="">Node</span>** keyword. Follow this keyword with the name of the target computer, which can be a variable. After the computer name, use braces **<span style="">{}</span>** to delimit the node block.

From &lt;http://technet.microsoft.com/en-us/library/dn249918.aspx&gt;

Note: Do NOT run this on Windows 10 Technical Preview at this time.  If you want to, see:

- http://powershell.org/wp/forums/topic/beware-windows-10-technical-preview/

```
PS C:\Users\robernst\Documents> Start-DscConfiguration -Wait -Verbose -Path .\MyWebConfig
VERBOSE: [ROBERNST-GCC12]:                            [[File]MyFileExample] The system cannot find the file specified.
VERBOSE: [ROBERNST-GCC12]:                            [[File]MyFileExample] The related file/directory is: C:\Octopus Samples.
VERBOSE: [ROBERNST-GCC12]:                            [[File]MyFileExample] The path cannot point to the root directory or to the root of a net share.
VERBOSE: [ROBERNST-GCC12]:                            [[File]MyFileExample] The related file/directory is: C:\Octopus Samples.
VERBOSE: [ROBERNST-GCC12]:                            [[File]MyFileExample] SourcePath must be specified if you want to configure the destination directory recursivel
y. Make sure that SourcePath is a directory and that it is accessible.
SourcePath must be specified if you want to configure the destination directory recursively. Make sure that SourcePath is a directory and that it is accessible.
    + CategoryInfo          : InvalidArgument: (:) [], CimException
    + FullyQualifiedErrorId : MI RESULT 4
    + PSComputerName        : robernst-gcc12

VERBOSE: [ROBERNST-GCC12]: LCM:  [ End    Set      ]
The SendConfigurationApply function did not succeed.
    + CategoryInfo          : InvalidArgument: (root/Microsoft/...gurationManager:String) [], CimException
    + FullyQualifiedErrorId : MI RESULT 4
    + PSComputerName        : robernst-gcc12

VERBOSE: Operation 'Invoke CimMethod' complete.
VERBOSE: Time taken for configuration job to complete is 0.332 seconds
```

Help for this issue:

- http://www.powershellmagazine.com/2013/09/02/copying-powershell-modules-and-custom-dsc-resources-using-dsc/

1. Copy the xWebAdministration folder to C:\Program Files\WindowsPowerShell\Modules\ on the client where deployment is being executed.
2. Copy the xWebAdministration folder to C:\Program Files\WindowsPowerShell\Modules\ on the server that is the deployment target.
3. <span>~~<span style="">&amp; &#39;.\GETS Plus DSC Deployment.ps1&#39;</span>~~</span>
4. Load script in ISE.
5. Hit F5 to execute the script.
6. GETSPlus -ConfigurationData .\DevOneBox.psd1
7. Start-DscConfiguration -Wait -Verbose -Path .\GETSPlus

# Testing on the Server

1. import-module WebAdministration
    1. This will create the IIS: drive in PSH.
2.

`$Session = New-CimSession -ComputerName "robernst-gcc12" -Credential ACCOUNTS\PattiFuller`

`Get-DscConfiguration -CimSession $Session`

`Restore-DscConfiguration -CimSession $Session`

`Test-DscConfiguration -CimSession $Session`

# Composite Resources

Reusing Existing Configuration Scripts in PowerShell Desired State Configuration

From &lt;http://blogs.msdn.com/b/powershell/archive/2014/02/25/reusing-existing-configuration-scripts-in-powershell-desired-state-configuration.aspx&gt;