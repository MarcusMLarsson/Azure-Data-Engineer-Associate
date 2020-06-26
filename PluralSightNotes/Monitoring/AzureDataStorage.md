
<h1> Monitoring Microsoft Azure Data Storage </h1>

<img src="https://docs.microsoft.com/sv-se/azure/azure-monitor/insights/media/monitor-azure-resource/metrics.png">


<p> Monitoring is critical to ensure the security, healt and performance of the data. If there are some undetected storage issues, systems may be at risk and performance problems like long delays or excess CPU utilization might follow. It will be difficult to diagnose what is causing the problem, if that storage issue is undetected. Monitoring provides insight into many aspects of storage including performance, it's good to create a performance baseline when I create the solution. Overtime I can compare if the health of the data is degrading. Am I seing any spikes and unexpected errors? This may also include monitoring the end client experiance. </p>

<h3> Types of Montioring Data in Azure </h3>
<img src="https://www.systemcenterautomation.com/wp-content/uploads/2020/01/azure_monitor_twitter.png">
<ul>
 Each service may have different types of monitoring data available, but they fall into three broad categories:
  <li> Metrics: Might give me insight into throughput, capacity, if it was a virtual machine it might be CPU cycles, could be SLA.  </li>
   <li> Logs: These will vary between services, for example SQL server will ahve ah uge number of possible logs. </li>
  <li> Alerts: Alerts are generally  triggered by metrics and logs </li>
  </ul>
  
  <h3> Azure Monitor </h3>
  <p> Azure Montior provides a single source for monitoring of Azure resources. I can think of Azure Monitor as that foundational element providing the first ring of matuirity in the type of insight I want to get about the environment. You might then build on this with for example application insight to get deeper insight into the workings of applications and their health. Azure monitor gives insight into things like
  <ul> 
    <li>Metrics: A metric is insight into the performance. Azure monitor runs in about 1 minute frequency. </li> 
    <li> Activity (Operations performed within the subscription) and Diagnostic Logs (resource level logs):</li> 
    <li> Alets from different sources including Azure Montior, Log Analytics anad Application insight</li> 
  </ul>

<h3> Using Azure Monitor Logs </h3>
<ul>
 <li> This provides the same functionality as Log Analytics</li>
 <li> Provides a location to ingest and store data from almost any source including Azure resources, operating systems and syslog </li>
 <li> Built around a workspace with multiple workspaces supported</li>
 <li> Data can be retained for a configurable duration</li>
 <li> The Kusto Query Language (KQL) is used to query the data stored to provide insight into many aspects of solutions </li>
 <li> Various visualizations and dashboards can also be created </li>
 </ul>
 
 <p> You can create alert based on queries. There are two places you can create alerts, in Azuer Monitor and in Azure Monitor Logs. </p> 
 
 <h3> Diagnostic Log Targets </h3>
 <ul>
 <li> Azure Resources have a common diagnostics setting. </li>
 <li> There may be one or more type of logs and metrics per resource typ </li>
 </ul>
 
 <p> Diagnostic information can be sent to a combination of three possible targets </p>
 <ul>
 <li> Archive to a Storage Accounts - useful for long term, cheap retention </li>
 <li> Send to Log Analytics - for retention of data and to enable rich analysis </li>
 <li> Stream to an Event Hub - a publish/subscribe model used to send logs to external SIEM systems that will subscribe to an event hub</li>
 </ul>
 
 <h3> Using Azure Sentinel </h3>
<img src="https://www.systemcenterautomation.com/wp-content/uploads/2020/05/azure-sentinel-twitter.png"> 

 <p> Storing logs and metrics on its own is useful for forensic analysis post-event. Manually creating alerts based on logs/metrics is not practical in most scenarios to detect security incidents. If you are collecting logs and metrics for security purposes, realise just collecting them is not that useful from an alert aspect. If that is you goal, you need some other type of service. That is Azure Sentinel. Azure Sentinel is 
<ul> 
 <p> Built on top of Azure Monitor Logs </li>
 <p> A cloud-native SIEM (Security Information and Event Management) solution with infinite scale </li>
 <li> Using machine learning and AI to perform analytics against collated signals its getting from your logs, metrics and microsoft security intelligent graph etc</li>
 <li> Cases (the case is the potential threat) are created automatically to collect the associated logs, etc, that have been detected as a threat.
 </ul></p>

<h3> What is SIEM? </h3>

<img src="https://blogvaronis2.wpengine.com/wp-content/uploads/2019/06/siem-process-2.png">

<p> Security Information and Event Management (SIEM) is a software solution that aggregates and analyzes activity from many different resources across your entire IT infrastructure. SIEM collects security data from network devices, servers, domain controllers, and more. SIEM stores, normalizes, aggregates, and applies analytics to that data to discover trends, detect threats, and enable organizations to investigate any alerts. </p>

<h3> Grafana </h3>
<img src="https://upload.wikimedia.org/wikipedia/commons/9/9d/Grafana_logo.png">
 
<p> Grafana provides a rich visualization and analytics set of capabilities. It is note exclusive to Azure, but has a plugin available for Azure Monitor to enable integration.  </p>


<h3> Azure Storage Logs </h3>

<p> Many services integrate tightly with Azure Monitor. This is not the case with Azure Storage, which uses classic logs. Classig logs write information to the $log container of the storage account BLOB service. These logs are enabled per service level. They include metric options at different granularities. And the data retention can be configured. The logs (classic) are hidden in the portal but are available from the API and Azure Storage Explorer. </p>


<h3> Azure Storage Explorer </h3>
<img src="https://dashboard.snapcraft.io/site_media/appmedia/2019/11/storage-explorer.png">

<a href="https://azure.microsoft.com/en-us/features/storage-explorer/"> Download Azure Storage Explorer </a>

<p> Upload, download, and manage Azure blobs, files, queues, and tables, as well as Azure Cosmos DB and Azure Data Lake Storage entities. Easily access virtual machine disks, and work with either Azure Resource Manager or classic storage accounts. Manage and configure cross-origin resource sharing rules. </p>


<h3> Azure Data Lake Storage Gen 2 </h3>

<img src="https://miro.medium.com/max/1078/1*IQ4oFJQaQJGgHS-h0M1fxw.png">
<p> New Service, which sit ontop of blob storage. At the moment, there is no logs for Azure Data Lage Storage Gen 2. </p>

<p> The log storage service colelcts metrics on a best metric basis. If it can not keep up and its going to interupt storage operations, things will rather get missed from the log. In other words, there is logs that could be missed. </p>

<h3> Querying classic storage logs </h3>

<p> How to query the classic storage logs. There is no built-in analysis with the classic logs. The files from $log can be read by a solution and processed, e.g. a SIEM. Integration to Log Analytics is possible through custom solutions. </p>


<h3> Azure Monitor Metrics </h3>
<p> Azure Storage has migrated to Azure Monitor-based metrics. This also applies to ADLS Gen2. This means we are not going to use the classic metrics (or alerts).


<h3> What is HDInsight? </h3>

<img src="https://apifriends.com/wp-content/uploads/2018/05/HDInsightsDetails.png">

<p> HDInsight is the Azure managed offering providing a cloud distribution of Hadoop. There are a number of different open source framework available with HDInsight, including Apache Hadoop, Spark and Kafka. It's primarily an analytics platform for large amounts of data.  </p>

<p> Monitoring for HDInsight requires three areas to be considered. </p>
<ul>
 <li> Cluster health and availability </li>
 <li> Resource utilization and performance</li>
 <li> Job status and logs</li>
</ul>

<p> Ambari comes on every cluster, and there is no additional cost. Ambari is a completely open source management platform for provisioning, managing, monitoring and securing Apache Hadoop clusters. Apache Ambari takes the guesswork out of operating Hadoop. Log analytics has some additional cost, you are going to pay for the data ingestion, pay for the amount of data etc. </p>

<h3> Demo: Monitoring with Azure Monitor Metrics and using Ambari </h3>
