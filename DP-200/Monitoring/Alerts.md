
<h1> Microsoft Azure Alert Configuration Playbook </h1>
<p> Type of Alert </p>
<ul>
  <li> Flag in Dashboard </li>
  <li> Email</li>
  <li> SMS/Voice</li>
  <li> ITSM</li>
  <li> Automation (Automation Runbook, LogicApp, Azure Function, Webhook)
    </ul>
    
  <h3> Action Groups </h3>
<ul>
  <li> Azure Monitor has a standardized alerting experience that is focused around action groups. </li>
  <li> Alert groups enable sets of actions to be defined that can be used across altering mechansim </li>
  <li> An action group supports multiple sets of actions</li>
 </ul>  
 
 
 <p> Go to Azure Montiro and click on alerts. Click on manage actions. If we select the dropdown all of the availaible actions are available (Email, SMS, Azure Functions, LogicAPP, Webhook, ITSM, Automation Runbook etc). </p>
 
 <h3> Smart Groups</h3>
 <ul>
  <li> Alerts may generate a lot of noise </li>
  <li> Smart groups uses AI to group like alerts together to minimize noise </li>
  <li> Show a common potential cause and enable response to be performed against all alerts in the group </li>
  </ul>
  
  <h3> Action Rules </h3>
  <p> Normally, we create an alert rule which has a certain target (e.g. resource group), I can optionally add actions. I can then sepperatley think about action rules. An Action role has a scope, it can be a particular resource group or even the whole subscription. Let's say I want the same action for a specific resource group/subscription</p>
 
<h3> Service Helath Alerts </h3>
<p> While built on Activity Logs, service health has its own  interface. It uses the same  alerting operations as Azure metrics. Can create ealerts based on specific services, regions and types of event. </p>

<h3> Azure Monitor Logs Alerting </h3>
<ul>
  <li> Utilizes Log Analytics </li>
  <li> Requires the data to be sent to Log Analytics via the resource Diagnostic Settings </li>
  <li> Kusto queries can be authored and used to create alerts that trigger alert groups. </li>
  
  <p> First is to create a query that we want to alert. Then click the new alert rule. </p>
  
  
  <h3> Azure Storage Alerting </h3>
  <p> Within the storage account, go to alerts. Create a new alert rule, then we can add the condition. </p>
  
  <h3> Azure SQL Database and Azure Synapse Analytics </h3>
  <p> The activity log and metrics we can configure the alerts from Azure monitor. For diagnostic logs we can use log analytics to create alerts. </p> 
  
  <h3> Azure Cosmos DB alerting </h3>
  <p> The activity log and metrics we can configure the alrets from Azure monitor. For diagnostic logs we can use log analytics to create alerts. </p>
  
  
  <h3> Azute Data Factory alerting </h3>
  <p> The activity log and metrics we can configure the alrets from Azure monitor. For diagnostic logs we can use log analytics to create alerts. </p>
 
