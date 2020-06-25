
<h1> Monitoring Microsoft Azure Data Storage </h1>

<img src="https://docs.microsoft.com/sv-se/azure/azure-monitor/insights/media/monitor-azure-resource/metrics.png">


<p> Monitoring is critical to ensure the security, healt and performance of the data. If there are some undetected storage issues, systems may be at risk and performance problems like long delays or excess CPU utilization might follow. It will be difficult to diagnose what is causing the problem, if that storage issue is undetected. Monitoring provides insight into many aspects of storage including performance, it's good to create a performance baseline when I create the solution. Overtime I can compare if the health of the data is degrading. Am I seing any spikes and unexpected errors? This may also include monitoring the end client experiance. </p>

<h3> Types of Montioring Data in Azure </h3>
<ul>
 Each service may have different types of monitoring data available, but they fall into three broad categories:
  <li> Metrics: Might give me insight into throughput, capacity, if it was a virtual machine it might be CPU cycles, could be SLA.  </li>
   <li> Logs: These will vary between services, for example SQL server will ahve ah uge number of possible logs. </li>
  <li> Alerts: Alerts are generally  triggered by metrics and logs </li>
  </ul>
  
  <h3> Azure Montior </h3>
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
 
