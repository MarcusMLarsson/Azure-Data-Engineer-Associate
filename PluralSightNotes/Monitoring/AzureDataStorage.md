
<h1> Monitoring Microsoft Azure Data Storage </h1>

<p> Monitoring is critical to ensure the security, healt and performance of the data. If there are some undetected storage issues, systems may be at risk and performance problems like long delays or excess CPU utilization might follow. It will be difficult to diagnose what is causing the problem, if that storage issue is undetected. Monitoring provides insight into many aspects of storage including performance, it's good to create a performance baseline when I create the solution. Overtime I can compare if the health of the data is degrading. Am I seing any spikes and unexpected errors? This may also include monitoring the end client experiance. </p>

<h3> Types of Montioring Data in Azure </h3>
<ul>
 Each service may have different types of monitoring data available, but they fall into three broad categories:
  <li> Metrics: Might give me insight into throughput, capacity, if it was a virtual machine it might be CPU cycles, could be SLA.  </li>
   <li> Logs: These will vary between services, for example SQL server will ahve ah uge number of possible logs. </li>
  <li> Alerts: Alerts are generally  triggered by metrics and logs </li>
  </ul>
  
  <h3> Azure Montior <h3>
  <p> Azure Montior provides a single source for monitoring of Azure resources. I can think of Azure Monitor as that foundational element providing the first ring of matuirity in the type of insight I want to get about the environment. You might then build on this with for example application insight to get deeper insight into the workings of applications and their health. Azure monitor gives insight into things like
  <ul> 
    <li>Metrics: A metric is insight into the performance. Azure monitor runs in about 1 minute frequency. </li> 
    <li> Activity (Operations performed within the subscription) and Diagnostic Logs (resource level logs):</li> 
    <li> Alets from different sources including Azure Montior, Log Analytics anad Application insight</li> 
  </ul></p>
