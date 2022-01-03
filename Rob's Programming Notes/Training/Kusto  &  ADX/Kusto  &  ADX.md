# Kusto / ADX

**Created**: Monday, April 26, 2021 09:29:50 AM -04:00
**Modified**: Monday, January 03, 2022 10:30:18 AM -05:00


1. Checked out an Azure subscription from here: https://subscriptionlibrary.azure.net/#/AvailableSubscriptions?teamId=63

    | xstore_public_rd_sharedsub_009 | 5e0ad271-584f-456c-8410-61f256067022 | 4/26/2021, 9:29:31 AM | 4/29/2021, 9:29:31 AM |
    | --- | --- | --- | --- |

2. Following this tutorial:
    1. https://docs.microsoft.com/en-us/azure/data-explorer/create-cluster-database-portal
3. Create a new cluster:
    1. RG: robernst-kusto
    2. Cluster Name: robernstkusto
    3. Region: East US
    4. Workload: Storage Optimized
    5. Size: Medium (8 cores)
    6. Compute Specs: Standard\_DS13\_v2+1TB\_PS
    7. Create Start time: 4/26/2021, 9:36:46 AM
    8. Create End time: 4/26/2021, 9:48:21 AM (11 minutes 34 seconds)
    9. /subscriptions/5e0ad271-584f-456c-8410-61f256067022/resourceGroups/robernst-kusto/providers/Microsoft.Kusto/Clusters/robernstkusto
4. Create a database:
    1. TestDatabase
    2. Retention Period: 3650 days
    3. Cache Period: 31 days
5. Data Ingestion
    1. When creating the database finished, it presented me with the "Ingest new data" or "Create data connection" buttons.
    2. Instead, the tutorial said to click on Query to try things.
6. Query
    1. .show databases
        1. Returned valid info.
    2. .show tables
        1. Returned an empty result set.
7. Stop and Restart the Cluster
    1. Click Stop in the Azure Portal on the Overview tab.
        1. Your Azure Data Explorer cluster is currently in state: Stopping
        2. ❗<mark style="background: #FFF3A3A6;">This took a while, about 9 minutes!</mark>
    2. Click Start.
        1. ❗<mark style="background: #FFF3A3A6;">It then takes about 10 minutes to become available!</mark> 😮
8. [Add help cluster](https://docs.microsoft.com/en-us/azure/data-explorer/web-query-data)
    1. Go to https://dataexplorer.azure.com/
    2. In the upper left of the application, select Add Cluster.
    3. In the Add cluster dialog box, enter the URI https://help.kusto.windows.net, then select Add.
    4. Expand the Samples database and open the Tables folder to see the sample tables that you have access to.
    5. We use the StormEvents table later in this quickstart, and in other Azure Data Explorer articles.
9. Add Your Cluster
    1. Now add the test cluster you created.
    2. Select Add Cluster.
    3. In the Add Cluster dialog box, enter your test cluster URL in the form https://robernstkusto.eastus.kusto.windows.net/, then select Add.
10. Run queries
    1. You can now run queries on both clusters (assuming you have data in your test cluster).
        1. For this article, we'll focus on the help cluster.
    2. In the left pane, under the help cluster, select the Samples database.
    3. Copy and paste the following query into the query window. At the top of the window, select Run.

            StormEvents
            | sort by StartTime desc
            | take 10

    4. Copy and paste the following query into the query window, below the first query. Notice how it isn't formatted on separate lines like the first query.

            StormEvents | sort by StartTime desc
            | project StartTime, EndTime, State, EventType, DamageProperty, EpisodeNarrative | take 10

    5. Select the new query. Press <mark style="background: #BBFABBA6;">Shift+Alt+F</mark> to **format the query**.
    6. Select Run or press<mark style="background: #BBFABBA6;">Shift+Enter</mark> to **run a query**. This query returns the same records as the first one, but includes only the columns specified in the project statement.
    7. Select <mark style="background: #BBFABBA6;">Recall</mark> (F8) at the top of the query window to show the result set from the first query **without having to rerun the query**.
        1. Often during analysis, you run multiple queries, and Recall allows you to retrieve the results of previous queries.
        2. <mark style="background: #FFF3A3A6;">This didn't work for me.</mark>
    8. Let's run one more query to see a different type of output.

            StormEvents
            | summarize event_count=count(), mid = avg(BeginLat) by State
            | sort by mid
            | where event_count > 1800
            | project State, event_count
            | render columnchart

        1. Note the <mark style="background: #BBFABBA6;">summarize</mark> and <mark style="background: #BBFABBA6;">render</mark> keywords.
    9. My Queries

            StormEvents
            | where BeginLat > 0
            | sort by StartTime desc
            | take 10

            StormEvents
            | summarize event_count=count() by State
            | sort by event_count desc
            | render columnchart

11. Expand a Cell
    1. Expanding cells is useful to view long strings or dynamic fields such as JSON.
    2. Double-click a cell to open an expanded view. This view allows you to read long strings, and provides a JSON formatting for dynamic data.
    3. Click on the icon on the top right of the result grid to switch reading pane modes. Choose between the following reading pane modes for expanded view: inline, below pane, and right pane.
![Icon to change reading pane for expanded view mode - Azure Data Explorer WebUI query results](/Attachments/1-2155143750f34c9ea509366e32f502d3.png)    4. ⭐ Rob: This was very useful!
12. Expand a Row
    1. Click on the arrow \> to the left of the row you want to expand.
13. Group column by results
    1. Within the results, you can group results by any column.
    2. Run the following query:

            StormEvents
            | sort by StartTime desc
            | take 10

    3. Mouse-over the State column, select the menu, and select <mark style="background: #BBFABBA6;">Group by State</mark>.
    4.  In the grid, double-click on California to expand and see records for that state. This type of grouping can be helpful when doing exploratory analysis.
    5. Mouse-over the Group column, then select <mark style="background: #BBFABBA6;">Reset columns</mark>. This setting returns the grid to its original state.
14. Use value aggregation
    1. After you have grouped by a column, you can then use the value aggregation function to calculate simple statistics per group.
    2. Select the menu for the column you want to evaluate.
    3. Select Value Aggregation, and then select the type of function you want to do on this column.
    4. ❓<mark style="background: #FFF3A3A6;">I'm not sure where to see the results of this calculation.</mark> 
15. Filter columns
    1. You can use one or more operators to filter the results of a column.
    
            StormEvents
            | sort by StartTime desc
            | take 10

    2. To filter a specific column, select the menu for that column.
    3. Select the filter icon.
    4. In the filter builder, select the desired operator.
    5. Type in the expression you wish to filter the column on. Results are filtered as you type.
        1. Note: The filter isn't case sensitive.
    6. Type "alabama" in the State column.
    7. To create a multi-condition filter, select a boolean operator to add another condition
    8. Select OR and type "missouri" in the State column.
    9. To remove the filter, delete the text from your first filter condition.
16. Where clause

        StormEvents
        | take 100000
        | where State in ('ALABAMA', 'MISSOURI', 'FLORIDA')

    1. The values in the where clause **ARE case sensitive**.
17. Run cell statistics
    1. Run the following query.

            StormEvents
            | sort by StartTime desc
            | where DamageProperty > 5000
            | project StartTime, State, EventType, DamageProperty, Source
            | take 10

    2. In the results grid, **select a few of the numerical cells**. The table grid allows you to select multiple rows, columns, and cells and calculate aggregations on them. The Web UI currently supports the following functions for numeric values: **Average, Count, Min, Max, and Sum.**
18. Filter to query from grid
    1. Another easy way to filter the grid is to add a filter operator to the query directly from the grid.
    2. Select a cell with content you wish to create a query filter for.
    3. Right-click to open the cell actions menu. Select <mark style="background: #BBFABBA6;">Add selection as filter</mark>.
    4. A query clause will be added to your query in the query editor:
19. Pivot
    1. The pivot mode feature is similar to Excel’s pivot table, enabling you to do advanced analysis in the grid itself.
    2. Pivoting allows you to take a columns value and turn them into columns. For example, you can pivot on State to make columns for Florida, Missouri, Alabama, and so on.
    3. On the right side of the grid, select Columns to see the table tool panel.
    4. Select <mark style="background: #BBFABBA6;">Pivot Mode</mark>, then drag columns as follows: EventType to Row groups; DamageProperty to Values; and State to Column labels.
    5. <mark style="background: #FFF3A3A6;">Rob: I still need to think about this more, but it looks VERY useful.</mark>
20. Search in the results table
    1. You can look for a specific expression within a result table.
    2. Run the following query:

            StormEvents
            | where DamageProperty > 5000
            | take 1000
    3. Click on the Search button on the right and type in "Wabash"
    4. All mentions of your searched expression are now highlighted in the table. You can <mark style="background: #BBFABBA6;">navigate between them by clicking Enter</mark> to go forward or <mark style="background: #BBFABBA6;">Shift+Enter</mark> to go backward, or you can use the up and down buttons next to the search box.
21. Share queries
    1. In the query window, select the first query you copied in.
    2. At the top of the query window, select Share.
    3. The following options are available in the drop-down:
        1. Link to clipboard
        2. [Link query to clipboard](https://docs.microsoft.com/en-us/azure/data-explorer/web-query-data#provide-a-deep-link)
        3. Link, query, results to clipboard
        4. [Pin to dashboard](https://docs.microsoft.com/en-us/azure/data-explorer/web-query-data#pin-to-dashboard)
        5. <mark style="background: #FFF3A3A6;">Query to Power BI</mark>: https://docs.microsoft.com/en-us/azure/data-explorer/power-bi-imported-query
22. Use Kusto/ADX with LINQPad.
    1. https://docs.microsoft.com/en-us/azure/data-explorer/kusto/api/tds/clients#linqpad
    2. Select Add connection.
    3. Set Build data context automatically.
    4. Set Default (LINQ to SQL), the LINQPad driver.
    5. Set SQL Azure.
    6. For the server, specify the name of the Azure Data Explorer cluster. For example, mykusto.kusto.windows.net.
        1. help.kusto.windows.net
        2. <mark style="background: #FFF3A3A6;">Do NOT include the https://.</mark>
    7. Set Windows Authentication (Active Directory), for signing in.
    8. Select Test to verify connectivity.
    9. Select OK. The browser window displays the tree view with the databases.
    10. You can browse through the databases, tables, and columns.
        1. <mark style="background: #FFF3A3A6;">This failed for me.</mark>
    11. You can run SQL queries in the query window. Specify the SQL language, and select a connection to the database.
    12. You can also run LINQ queries in the query window. For example, select a table in the browser window. Select Count, and let it run.
23. <mark style="background: #FFF3A3A6;">There's much more to explore on this page, but this is a good start.</mark>
