
<h1> Monitoring Microsoft Azure Data Pipeliens and Processing </h1>

<h3> Control and Data Flow </h3>

<p> The control flow is the orchestration of activities. The data flow is the flow of data within an activity. For example, a control flow is made up of activities. The data flow is the data within the activity Like BLOB to Data Lake Data. This activity consist of Get from Blob and Write to Data Lake. </p>

<h3> Azure Solutions </h3>
<p> Primary technologies that we leverage around the control and data flow. For the control flow, we have Azure Data Factory. This provides the orchestration, it provides the scheduling. Then we have the data flow solutions. There are Azure Databricks and Azure HDInsight (and Azure Data Factory Data Flow).  </p>

<h3> Implementing Monitoring for Data Factory </h3>
<p> Data Factory provides the orchestration and scheduling of processes related to big data such as ETL, i.e. data pipelines.. It is a fully managed service with a graphical user interface. </p>

<p> What to monitor? Primarily for monitoring we think about </p>
  <ul> 
  <li> Triggers runs </li>
  <li> Activity runs </li>
  <li> Pipeline runs </li>
  <li> Integration runtimes </li>
 </ul>
  
  <h3> Data Factory Monitoring Demo </h3>
  <p> Click on monitoring interface. Dashboards, Pipeline runs, Trigger runs.</p>
  <p> Go to metrics (Azure Monitor) tab in Azure Data Factory resource. Go to Diagnostic settings and send data to storage account/event hub/log analytics</p>
  <p> Azure Data Factory Analytics (Preview). Go to market place, search Azure Data Factory. </p>
  
  <h3> Implementing HDInsight Monitoring </h3>
<p> Types of HDInsight Cluster: Batch processes (we care about the jobs), streaming (we care about quanitity), interactive queries (we care about queries). </p>
<ul>
  <li> Batch jobs (for example Spark) </li>
  <li> Streaming (for example kafka) </li>
  <li> Interactive Query (SQLLite)</li>
  </ul>
  
  <p> Monitoring HDINsight: For each cluster we have a monitor solution or we can jump into Embari</p>
