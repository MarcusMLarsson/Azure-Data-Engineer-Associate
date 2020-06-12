<h1> Integrating Data in Microsoft Azure </h1>

<h3> Azure Data Factory </h3>
<p>Azure Data Factory is a fully managed cloud-based data integration platform. Its used to create data-driven workflows and to integrate data from different data sources in a multi-cloud environment. </p>

<b> Why should you use Azure Data Factory? </b>
<ul>
  <li> Simplifies ETL at scale. </li>
  <li> Enables modern data integration.</li>
<li> Easy drag and drop interface (no code/ low amount of code is needed). </li>
  <li>Over 80 connections available. </li>
  <li> Easy migration from On-premise data stores to Azure </li>
  <li> Different cloud providers supported </li></p>
</ul>

<b> Understanding Azure Data Factory Pipelines </b>
<p> A data factory can contain one or more pipelines. A pipeline is a logical grouping of activities that perform a given task. It allows managing activities as a set instead of individual actions. An activity represents a processing step in the pipeline and they define actions to be performed on the data. One activity in the pipeline can for example be to ingest data, transform data and store data. Activities in the pipeline can be linked together and can be exectued either sequentially or run in pararellel. </p>  
  
<p> <b>Azure Data Factory supports three types of activities </b></p>
<ul>
  <li> Data movement activities</li>
  Copy data located on-premises or in the cloud. Some of the data stores include Azure Blob Storage, Azure Cosmos DB, Amazon Redshift, Google BigQuery, Hive, MariaDB, Oracle, SQL Server, MongoDB, Amazon S3 and more.
  <li> Data transformation activities</li>
  Helps you transform and enrich data. Some of the supported transformation activities include Hive, Pig, MapReduce, Spark and Azure Data Bricks. 
  <li> Control activities</li>
  Allows us to control the flow in the pipeline. Some examples of control activities includes ForEach and Web activity.  
</ul>


<p><b> Azure Data Factory Datasets </b></p>
<p> A dataset is a namned view that points or references the data you want to use in your activities. They identify data inside data stores such as files, folders, documents and tables. For example, if you have a pipeline activity that needs to access data hosted inside an Azure SQL Server database table, you will create a dataset that references this data. </p> 
  
<p> <b> Linked Services </b> </p>
 <p>Before we create a dataset, we need to create a linked service. Datasets and Linked Services go hand in hand. A linked service connects a data store, like SQL Server, to the data factory. Then the dataset uses the linked service to conncet to the data stores. Linked services are similar to connection strings which represents the connection information needed for Data Factory to connect to external resources. These external resources can either be data stores, such as Azure SQL server or a computer resources, e.g. Spark Cluster, that can host the execution of an activity. For example, data bricks notebook running on a Spark computer environment.    </p>

<p> <b> Creating a Pipeline to Ingest Data in Azure Data Factory </b> </p>
There are three steps to ingest data
<ul>
  <li> Create Datasets </li>
  <li> Create Linked Services </li>
  <li> Create a Copy Data Activity </li>
</ul>


<hr>

<h3> Data Migration Assistant </h3>
<ul>
  <li> Helps us with on-premis data migration</li>
  <li> Helps migrating schema and data </li>
  <li> Detects compatibility issues between data sources</li>
  <li> Detects unsupported or partially supported features</li>
</p>
</ul>

<b> Copy Data Tool </b>
<p> Allows data engineers to easily and quickly create data pipelines to move data from different services </p>  

<p> For large migrations Azure Database Migration Service is recommended</p>
<ul>
  <li> Fully managed </li>
  <li> Helps migrate databases at scale</li>
  <li> Minimal downtime</li>
</p>
</ul>

<p> Migrating SQL Server Data, Copying data between Amazon S3 package and Azure Blob Storage. Creating data integration pipelines using Azure Factory and Azuree Databricks. Creating real-time pipelines. </p>


<p> Create an Azure SQL Server, allow firewall settings. Data migration assistant. Helps pgrade infrastructure to a 
modern data platform. Detects compability and migration issues. Detects unsupported or partially supported feautures.
Provides guidance and support. In this module we use Data Migration Assistant to detect compatibility issues between
the on-pemise SQL Server and Azure SQL Server. Need to download the file.
