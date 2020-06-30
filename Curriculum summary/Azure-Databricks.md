<h3>Azure SQL Database </h3>

<b> PaaS offerings </b>
<ul>
 <li> Single Database </li>
 <p> Isolated database that is perfect for applications that need a single data source </p>
  <li> Elastic Pools </li>
 <p> Collection of Single databases with a shared set of resources such as CPU or memory </p>
  <li> Manage Instance </li>
 <p>  Easy migration of on-premis databases </p>
</ul>

<b> Service Tiers </b>
<ul>
 <li> General Purpose </li>
 <p>  IO and basic availability requirements, Reliability of Azure Blob storage, separte compute and storage, 1 replica, no read-scal,  99.99% HA SLA  </p>
  <li> Business Critical </li>
 <p> Fast IO and high availability requirements, local SSD storage, Combines Compute / Storag </p>
  <li> Hyperscale </li>
 <p>  Supports up to 100 TB of data, ensure 99.99% availability</p>
</ul>

<b> Purchasing models </b>
<ul>
 <li> DTU (Database Throughput Unit)  </li>
 <p>  DTUs are based on a blended measure of CPU, memory, reads, and writes.  </p>
  <li> vCore</li>
 <p> Gives you the option to choose between generations of hardware, number of cores, memory and storage size</p>
</ul>

<b> Monitor using Dynamic Management Views (DMVs) </b>
<p> DMVs are a great tool to help troubleshoot performance related issues. All queries executed on SQL pool are logged to sys.dm_pdw_exec_requests. This DMV contains the last 10,000 queries executed. The request_id uniquely identifies each query and is the primary key for this DMV.

<b> Performance Recommendations </b>
<p> You can use the Azure portal to find performance recommendations that can optimize performance of your database in Azure SQL Database or to correct some issue identified in your workload. The Performance recommendation page in the Azure portal enables you to find the top recommendations based on their potential impact. Recommendations are sorted by their potential impact on performance into the following categories, high, medium and low. It is possible to apply individual recommendations. You can also set your database to implment recommendations automatically (auto tuning) </p>

<b> Query performance insight </b>
<p> Query Performance Insight provides intelligent query analysis for single and pooled databases. It helps identify the top resource consuming and long-running queries in your workload. Review top CPU consuming queries, view individual query details. </p>


<b> Geo replica</b>
<p> Active geo-replication is an Azure SQL Database feature that allows you to create readable secondary databases of individual databases on a server in the same or different data center (region). </p>

<b> Failover Groups</b>
<p>  Are similar to geo replica but are for differt things. Automatic failover. Can fail over multiple databases simultaneously. Failover groups are supported for managed instance, which is not the case for Geo replciation.  </p>

<b> Alwasy Encrypted </b>
<p> Always Encrypted is a feature designed to protect sensitive data, stored in Azure SQL Database or SQL Server databases from access by database administrators (e.g. the members of the SQL Server sysadmin or db_owner roles), administrators of machines hosting SQL Server instances,), and Azure SQL Database (cloud) administrators. Always Encrypted leverages client-side encryption: a database driver inside an application transparently encrypts data, before sending the data to the database. Similarly, the driver decrypts encrypted data retrieved in query results.  </p>

<b> Transparent Data Encryption </b>
 <p> TDE is intended to add a layer of security to protect data at rest from offline access to raw files or backups, common scenarios include datacenter theft or unsecured disposal of hardware or media such as disk drives and backup tapes. </p>
 
 <b> Data Masking </b>
 <p> Dynamic data masking limits sensitive data exposure by masking it to non-privileged users. Dynamic data masking helps prevent unauthorized access to sensitive data by enabling customers to designate how much of the sensitive data to reveal with minimal impact on the application layer. It’s a policy-based security feature that hides the sensitive data in the result set of a query over designated database fields, while the data in the database is not changed.</p>
 


 <b> SQL Data Sync </b>
<p> SQL Data Sync is a service built on Azure SQL Database that lets you synchronize the data you select bi-directionally across multiple databases, both on-premises and in the cloud. Data Sync is based around the concept of a sync group. A sync group is a group of databases that you want to synchronize. Data Sync uses a hub and spoke topology to synchronize data. You define one of the databases in the sync group as the hub database. The rest of the databases are member databases. Sync occurs only between the hub and individual members. 
<ul>
 <li> The Hub Database must be an Azure SQL Database. </li>
 <li>  The member databases can be either databases in Azure SQL Database or in instances of SQL Server. </li>
 <li>  The Sync Database contains the metadata and log for Data Sync. The Sync Database has to be an Azure SQL Database located in the same region as the Hub Database. The Sync Database is customer created and customer owned. </li>
</ul>

<p>The Sync Direction can be bi-directional or can flow in only one direction. That is, the Sync Direction can be Hub to Member, or Member to Hub, or both.  The Sync Interval describes how often synchronization occurs. SQL Data sync may appeal to customers who are considering moving to the cloud and would like to put some of their application in Azure.</p>

</p>

<b> Data base migration service </b>
<p> 
Azure Database Migration Service is a tool that helps you simplify, guide, and automate your database migration to Azure. Easily migrate your data, schema, and objects from multiple sources to the cloud at scale.
 </p>


<hr>

<h3>Azure SQL Data Warehouse </h3>
<ul>
<li>Distributions, Partitioning, Resource Classes, Polybase, External Tables, CTAS, Performance Monitoring (DMVs), Authentication & Security, etc. </li>
</ul>

<hr>

<h3>Azure Stream Analytics </h3>
<ul> 
 <Li>Cloud vs Edge, Inputs, Outputs, UDAs, UDFs, Window Functions, Stream vs Reference, Partitioning, Performance, Scaling. </li>
</ul>

<hr>
<h3>Azure Data Factory </h3>
<ul>
<li>Pipelines & Activities, Datasets, Linked Services, Integration Runtimes, Triggers, Authoring/Monitoring Experience. </li>
 </ul>

<hr>

<h3>Azure Storage</h3>
<ul>
 <li>Blobs vs ADLS Gen2, Data Redundancy, Security, Performance Tiers, Storage Lifecycle, Migration. </li>
</ul>

<hr>

<h3>Azure Key Vault</h3>
<ul>
 <li>Keys, Secrets, Certs, and Access Policies. </li>
</ul>

<hr>

<h3>Azure Event Hubs </h3>
<ul>
<li>Use Cases in Architecture, Terminology, Availability, Consistency, Scalability. 
 </ul>

<hr>

<h3>Azure Event Grid</h3>
<ul>
<li> Sources, Topics, Subscriptions, Handlers, Use Cases in Architecture.</li>
</ul>

<hr>

<h3> Azure IoT Hub </h3>
<ul>
<li>Use Cases in Architecture. </li>
</ul>

<hr>

<h3>Azure Cosmos DB </h3>
<ul>
 <li>Use Cases for APIs, Consistency Levels, Distribution, Partitioning.</li>
</ul>

<hr>

<h3>Azure Databricks</h3>
<ul>
<li>Use Cases in Architecture, Clusters, Secrets, Connecting to Data Sources, Performance Metrics.</li>
</ul>

<hr>

<h3>Azure Monitor </h3>
<ul>
 <li>Application, Alerts, Log Analytics. </li>
</ul>
