
<h1> Microsoft Azure Database Monitoring Playbook </h1>

<p> Why is monitoring important? Data is the foundation of any import process. Most corporate data are stored in database services. Monitoring is critical to ensure secuirty, health and performances of those database services. When I think about monitoring, I need bench marking. With becnhmarking I can show what is the peformance today compared to a good known state. </p>

<p> Monitoring provides insight into many aspects of databases </p>
<ul>
  <li> Performance (including comparision to an established baseline) </li>
  <li> SLA adherence and service health </li>
  <li> Spikes and unexpected errors (including from clients/queries) </li>
  <li> Capacity (storage and quotas) </li>
  
  </ul>
  
  <p> Quatoas is very important with Azure Services. On premises, we look at the physical box. The physical box has limits, limits on CPU, limits on memory, limits on IOPS. In the cloud that is not really our concern, the physical limit of a disk does not matter. In the cloud I might have DTUs with my Azure SQL Database that gives me a certain amount of IO. As I appoach that thresholds, I might see my IO being queued. </p>
  
  <h3> Types of monitoring data in Azure </h3>
  <p> Each service may have different types of monitoring data available </p>
  <ul>
  <li> Metrics: Values I can get about resources, CPU use, DTU utilization etc </li>
  <li> Logs: Logs are either generated at the azure resource level (activity logs, a resource was created, it was modified etc) or inside the resource (diagnostic logs)</li>
  <li> Alerts: From the metrics and logs, we can generate alerts. </li>
  </ul>
  
  <ul>
  <p> We can monitor Data in Azure from three different sources </p>
  <li> Azure subscriptions/tenant </li>
  <li> Azure resources </li>
  <li> Guest componetns such as OS and applications </li>
  </ul>
  
  <h3> Azure Monitor </h3>
 
 <img src="https://www.systemcenterautomation.com/wp-content/uploads/2020/01/azure_monitor_twitter.png">
  <p> The goal of Azure Monitor is to provide a single source for the monitoring of <b> Azure resources </b>. In Azure Monitor you can look at metrics from multiple resources in the same chart. If, I press metrics in the user interface for a resource, that resource will already be selected. Azure monitor gives insight into
<ul>
  <li> Metrics </li>
  <li> Activity (directly accessed to Azure Monitor) and Diagnostic Logs (integrate with Azure Monitor Logs to view the content)  </li>
  <li> Alerts: from different sources including Azure Monitor, Log Analytics and Application insight (not covered in this course)</p>
  </ul>
  
  <p> Azure Monitor Logs integrates log analytics capabilities. In Azure Monitor, select logs. The view is now going to shift into that of log analytics. Any logs that you sent to the log analaytics workspace you can now query from within here with KQL queries. </p> 
  
  <h3> Diagnostic log targets </h3>
  <p> There may be one or more type of logs and metrics per resource type. These diagnostic inforamtion can be sent to a combiantion of three possible targets. Metrics are always availabile with the Azure Monitor view. But the logs we are talking about, there is not native way to interact with those via the Azure Portal. I need to send them to some service that can consume those logs and give us a way to interact with them. There might be for some services multiple places I need to configure the diagnostic log settings. For example, in an Azure SQL Database, go to Diagnostic settings under monitoring. Then you can configure by adding a new diagnostic setting. In the diagnostic setting, you can send it to either 
    </p>
<ul>
  <li> Archive to a storage account </li>
  <li> Stream to an event hub </li>
  <li> Send to log analytics </li>
  </ul>
  <p> if the database is part of a elastic pool, this elastic pool has it owns diagnostic settings. For pool level information you need to send somewhere aswell. Same options are included as before </p>
  
<h3> Implementing Monitoring for Azure SQL Database and Azure Synapse Analytcis </h3>
<p> Benefits of PaaS Database </p>
<ul>
  <li> Automated backups </li>
  <li> Built-in resiliency options </li>
  <li> Evergreen (always new)</li>
  <li> Increased scalability and agility </li>
  <li> Auto-tuning of indexes </li>
  <li> Better monitoring </li>
</ul>

<p> Azure SQL Database deployment types </p>
<ul> 
  <li> Single Database </li>
  <li> Elastic Pool </li>
  <li> Managed instance </li>
  </ul>


<h3> Monitoring Plan of Attack </h3>
<ul>
<li> Start int he portal, if we can get the answer here it is the most simple solution </li>
<li> After that move to advanced tools </li>
</ul>

<h3> SQL Diagnostic Settings </h3>
<ul>
  <li> For Elastic Pool and Manage instance there are diagnostic at the pool/managed instance level that can be enabled </li>
  <li> For single database, database in elstic pool and instance database there are diagnostics that are enabled per database </li>
  </ul>
  <p>
  
  <h3> Monitoring SQL Performance </h3>
  <ul>
  <li> Azure SQL Intelligent Insight provides continuous feedback on SQL performance using AI to help detect and resolve performance challanges </li>
  <li> Azure SQL Analytics (search market place and install) is monitoring solution for Log Analytics which provides advanced cloud monitoring for multiple databases </li>
  <li>
    
<h3> Monitoring Query Performance </h3>
<ul>
  <li> Most interactions with SQL Database will be via various types of queries </li>
  <li> Insight into the queries can provide guidance to tune the queries and the database </li>
  <li> Tuning the application is critical </li>
  <li> Azure SQL Database provides two tools to aid with query performance (Query performance Insight & SQL Database Advisor) </li>
  </ul>
  
 
<h3> Azure Cosmos DB State of the Union </h3>
<ul>
  <li> Azure Cosmos DB was built as a cloud database </li>
  <li> It is probably the purest form of a managed database </li>
  <li> Nearly all aspects are automatically tuned and optimized </li>
  <li> There are metrics available, however these are all via Azure Monitor </li>
  <li> The biggest use of metrics is to optimize partitioning and to identify request unit exhaustion </li>
  <li> Useful metadata is also returned as part of each operation </li>
</ul>

<p> Data explorer, look at request units </p>


<h3> Metrics for Cosmos DB </h3>
<ul>
  <li> Cosmos DB supports a number of models </li>
  <li> There are a set of core, standard metrics which can be view through Azure Monitor </li>
  <li> Some metrics vary depending on the type of model </li>
  <li> Cosmos DB Metrics view has a number of tabs highlighting and visualizing metrics related to different areas </li>
  </ul>
  
  <p> Within a container in Cosmos DB, we have items. In this case we will focus on documents, but it can be another type of container. When we create the container, we specify a partition key. The partition key could be a name, a a region (some element within the JSON document). Let's say we pick name. Partition Set 1 will be Clark, Partition Set 2 will be Bruce, Partition Set 3 will be Barry. The dataset is now distributed across physical nodes that can then be used to perfrom queries on them. The goal is to spread the dataset over the physical nodes so we can distribute the workload. It's very important to get this partition key correct. </p>
  
  
  <p> Http 429, number of requests exceeded capacity.
  
  
  <h3> Logs for Cosmos DB </h3>
  <ul>
  <li> Like most Azure resources, the diagnostic settings enables log and metrics to be sent to the normal targets. </li>
  <li> Activities such as key interaction is written to the Activity log </li>
  </ul>
  
