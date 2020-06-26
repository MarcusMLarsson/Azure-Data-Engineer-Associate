
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
  
  
  <h3> Azure Monitor </h3>
 
 <img src="https://www.systemcenterautomation.com/wp-content/uploads/2020/01/azure_monitor_twitter.png">
  <p> The goal of Azure Monitor is to provide a single source for the monitoring of <b> Azure resources </b>. In Azure Monitor you can look at metrics from multiple resources in the same chart. If, I press metrics in the user interface for a resource, that resource will already be selected. Azure monitor gives insight into
<ul>
  <li> Metrics </li>
  <li> Activity (directly accessed to Azure Monitor) and Diagnostic Logs (integrate with Azure Monitor Logs to view the content)  </li>
  <li> Alerts: from different sources including Azure Monitor, Log Analytics and Application insight (not covered in this course)</p>
  
  
  <p> Azure Monitor Logs integrates log analytics capabilities. In Azure Monitor, select logs. The view is now going to shift into that of log analytics. Any logs that you sent to the log analaytics workspace you can now query from within here with KQL queries. </p> 
  
  <h3> Diagnostic log targets </h3>
  <p> There may be one or more type of logs and metrics per resource type. These diagnostic inforamtion can be sent to a combiantion of three possible targets. Metrics are always availabile with the Azure Monitor view. But the logs we are talking about, there is not native way to interact with those via the Azure Portal. I need to send them to some service that can consume those logs and give us a way to interact with them. There might be for some services multiple places I need to configure the diagnostic log settings. For example, in an Azure SQL Database, go to Diagnostic settings under monitoring. Then you can configure by adding a new diagnostic setting. In the diagnostic setting, you can send it to either 
<ul>
  <li> Archive to a storage account </li>
  <li> Stream to an event hub </li>
  <li> Send to log analytics </li>
  </ul>
  </p>
  <p> if the database is part of a elastic pool, this elastic pool has it owns diagnostic settings. For pool level information you need to send somewhere aswell. Same options are included as before </p>
