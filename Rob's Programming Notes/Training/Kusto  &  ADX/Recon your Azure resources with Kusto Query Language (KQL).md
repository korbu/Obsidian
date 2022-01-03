# Recon your Azure resources with Kusto Query Language (KQL)

**Created**: Thursday, July 15, 2021 01:55:40 PM -04:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


[Recon your Azure resources with Kusto Query Language (KQL)](https://www.youtube.com/watch?v=DuWBLsgqhaI)

<iframe width="356" height="200" data-original-src="https://www.youtube.com/watch?v=DuWBLsgqhaI" src="https://www.youtube.com/embed/DuWBLsgqhaI?feature=oembed&autoplay=true"></iframe>

https://aka.ms/LADemo

1. Log Analytics Demo
2. Test data from Microsoft.
3. KQL
    1. Can be used with Resource Graph, Log Analytics
4. SecurityEvent

    | count
5. SecurityEvent

    | take 50
6. SecurityEvent

    | where TimeGenerated &gt;= ago(1d)
7. SecurityEvent

    | where TimeGenerated &gt;= now(-15m)
8. SecurityEvent

    | where TimeGenerated &gt;= now(-15m)

    | project TimeGenerated, Account, Computer, EventID, Activity, IpAddress
9. SecurityEvent

    | where TimeGenerated &gt;= now(-15m) and EventID &gt;= 4000

    | project TimeGenerated, Account, Computer, EventID, Activity, IpAddress
10. SecurityEvent

    | where TimeGenerated &gt;= now(-15m) and EventID == 4624

    | project TimeGenerated, Account, Computer, EventID, Activity, IpAddress

    | summarize Logins = count() by Computer
11. SecurityEvent

    | where TimeGenerated &gt;= now(-15m) and EventID == 4624

    | project TimeGenerated, Account, Computer, EventID, Activity, IpAddress

    | summarize Logins = count() by Computer

    | order by Logins asc
12. SecurityEvent

    | where TimeGenerated &gt;= now(-15m) and EventID == 4624

    | project TimeGenerated, Account, Computer, EventID, Activity, IpAddress

    | summarize Logins = count() by Computer

    | order by Logins asc

    | render piechart // You could pin this to a dashboard
13. Perf

    // | where ObjectName == "System"

    // | where CounterName == "System Up Time" or CounterName == "Uptime"

    // | extend UpTime = CounterValue \* 1s

    // | project TimeGenerated, Computer, UpTime, InstanceName

    | project TimeGenerated, ObjectName, Computer, InstanceName

    // | summarize arg\_max(TimeGenerated, \*) by Computer

    // | order by UpTime desc

    | summarize ObjectTypeCount = count() by ObjectName

    | order by ObjectTypeCount desc

    // System was no longer present as an ObjectName
14.