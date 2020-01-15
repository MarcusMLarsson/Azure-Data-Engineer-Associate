<h1> Survey the services on the Azure Data platform </h1>

<h3> Introduction </h3>
<p> This module will cover the following Azure technologies </p>
<ul>
<i> <li> Azure Storage </li>
<li> Azure Data Lake Storage </li>
  <li> Azure Cosmos DB </li>
  <li> Azure SQL Database </li>
  <li> Azure SQL Data Warehouse </li>
  <li> Azure Stream Analytics </li>
  <li> Azure HDInsight </li>
  <li> Other Azure services </li>
</li> </i>
</ul>

<h3> Review </h3>
<p> <b> Structured data </b> <p>
<ul>
<li> Relational databases: Microsoft SQL Server, Azure SQL Database and Azure SQL Data Warehouse </li> 
<li> Data structure defined at design time, before data is loaded into the system </li> 
<li> Designed in the form of tables </li> 
<li> Reacts slowly to changes because of that the structural database needs to change every time a data requirement change </li>
<li> When new columns are added, you might need to bulk-update all existing records </li>
<li> Typically uses a query language such as Transact-SQL </li>   
</ul>

<p> <b> Nonstructured data</b> </p>
<ul>
<li> Examples of nonstructured data include binary, audio and image files. </li> 
<li> Nonrelational systems, commonly called NoSQL systems. </li> 
<li> Data structure isn't defined at deisgn time, loaded in its raw format</li> 
<li> The data structure is defined only when the data is read </li>
<li> Nonrelatonal systems can also support semistructured data such as JSON file formats</li>
</ul>

<p> <b> Four types of open-source NoSQL databases </b> </p>
<ul>
<li> <b> Key-value store: </b> Stores key-value pairs of data in a table structure. </li> 
<li> <b> Document database: </b> Stores documents that are tagged with metadata to aid document searches.</li> 
<li> <b> Graph database: </b> Graph database: Find relationship between data points by using a structure that's composed of vertices and edges.</li> 
<li> <b> Column database: </b> Stores data based on columns rather than rows. Columns can be defined at the query's runtime, allowing flexibility in the data that's returned performantly. </li> 
</ul>

---

<h3> Azure Storage </h3>
<p> <a href="https://www.youtube.com/watch?v=UzTtastcBsk"> Video Explanation </a> </p>
<ul>
<li> <b> Azure Blob: </b>  A scalable object store for text and binary data (any kind of file). Blog storage
  is seprated into containers which contains files </li> 
<li> <b> Azure Files: </b> Managed file shares for cloud or on-premises deployments. File storage is separated into different shares which contains files and folders. </li> 
<li> <b> Azure Queue: </b> is a service for storing large numbers of messages. Storage Queues are separated into Queues and each queue contain multiples messages. Simple messaging service.</li> 
<li> <b> Azure Table: </b> A NoSQL store database in the cloud (for no-schema storage). Storage tables are seperated into tables,
  which each contains rows of data. </li> 
</ul>

<p> You can use Azure Storage as the storage basis when provisioning a data platform such as Azure Data Lake Storage and HDInsight. But you can also provision Azure Storage for standalone use. For example, you provision an Azure Blob store as a standard storage in the form of magnetic disk storage or as premium storage in the form of solid-state drivers (SSDs)

<h3> Azure Blob storage </h3>
<p> If you need to provision a data store that will store but not query data, your cheapest option is to set up a storage account as a Blob store. Blob storage works well with images and unstructured data, and it's the cheapest way to store data in Azure. </p>

<b> Key features </b>
<p> Scalable, secure, durable and highly available. Provides REST (Representational state transfer) APIs and SDKs for Azure Storage in various languages. Supported languages include .NET, Java, Node.js, Python, PHP, Ruby, and Go. 
  
<b> Data ingestion </b>
<p> To ingest data into your system, use Azure Data Factory, Storage Explorer, the AzCopy toll, PowerShell or Visual Studio. If you use the File Upload feature to import file sizes above 2 GB, use PowerShell or Visual Studio. AzCopy supports a maximum file size of 1 TB and automatically splits data files that exceed 200 GB. </p>

<b> Queries </b>
<p> If you create a storage account as a Blob store, you <b> can't </b> query the data directly. To query it, either move the data to a store that supports queries or set up the Azure Storage account for a data lake storage account. </p>

<b> Data security </b>
<p> Azure Storage encrypts all data that's written to it. Azure Storage also provides you with fine-grained control over who has acces to your data. You'll secure the data by using keys or shared access signatures. Azure Resource Manager provides a permissions model that uses role-based access control (RBAC). Use this functionality to set permission and assign roles to users, groups, or applications. </p>


---

<h3> Azure Data Lake Storage </h3>
<p> <a href="https://www.youtube.com/watch?v=2uSkjBEwwq0"> Video Explanation </a> </p>
<p> Azure Data Lake is a data storage solution designed for <b> big data analytics </b>. Each data lake has a container (file system) underneath. Just like any filesystem it has folders and files within it. Because the service is designed for data analytics, the file system is called Azure Blob File System (ABFS). The file system is Hadoop compatible. Azure Data Lake is built from the ground up as naitive Hadoop distributed file system or HDFS, working out of the box with the Hadoop echo system. 
The storage service is available as Generation 1 (Gen1) or Generation 2 (Gen2). Gen1 users are not required to
upgrade to Gen2, but they forgo some benifits. </p>

<p> Data Lake Storage Gen2 users take advantage of Azure Blob storage, a hierarchical file system, and performance tuning
that helps them process big-data analyitcs solutions. In Gen2, developers can access data trough either the Blob API or
the Data Lake file API. Gen2 can also act as a storage layer for a wide range of compute platforms,
including Azure Databricks, Hadoop, Azure HDInsight. </p>

<b> Where to use Data Lake Storage Gen2? </b>
<p> Data Lake Storage is designed to store massive amounts of data for big-data analytics. Data Lake Store allows you to store unstructured, semi-structured and structured data and does not require a schema to be defined before the data is loaded.
The compute aspec that sits above this storage can vary. The aspec can include platforms like HDInsight, Hadoop,
Cloudera, Azure Databricks, and Hortonworks. </p>
</p>

<b> Key Features </b>
<ul>
<li> Unlimited scalability </li>  
<li> Hadoop compatibility</li> 
<li> Security support for both access control lists (ACL) </li> 
<li> POSIX compliance </li>
<li> An optimized Azure Blob File System (ABFS) driver that's desinged for big-data analyitcs</li>
<li> Zone-redundant storage</li>
<li> Geo-redundant storage</li>
</ul>

<b> Data ingestion </b>
<p>To ingest data into your system, use Azure Data Factory, Apache Sqoop, Azure Storage Explorer, the AzCopy tool, PowerShell or Visual Studio. </p>

<b> Queries </b>
<p> In Data Lake storage Gen1, data engineers query data with U-SQL language.
In Gen2, Azure Blob Storage API or Azure Data Lake System (ADLS) API. </p>

<b> Data security </b>
<p> Data Lake Storage supports Azure Active Directory ACLs, security administrators can control data access by using the
familiar Active Directory Security Groups. Role-based access control (RBAC) is available in Gen1.
Built in security groups include ReadOnlyUsers, WriteAccessUsers, and FUllAccessUsers. Data Lake Storage
automatically encrypts data at rest, protecting data privacy. </p>

---

<h3> Azure Cosmos DB </h3>
<p><a href ="https://www.youtube.com/watch?v=R_Fi59j6BMo"> Video Explanation </a> </p>
<ul>
<p> Azure Cosmos DB is a globally distributed, multimodel database. It's simply a document data base. Document is a JSON format (Key: Value pair. An open standard for transfering data. You can deploy it by using several API models) </p>
<li> SQL API (a core API) </li>
<li> MongoDB API (NoSQL) </li>
<li> Cassandra API (NoSQL)</li>
<li> Gremlin API (Graph) </li>
<li> Azure Table Storage API (NoSQL) </li>
</ul>

<p> Multimodel database puts alla data into one database. You can query as a graph, as a document or SQL. You can also match
these in the same query. Imagen you have three different datastores; Swift (SQlite), Cassandra (NoSQL) and SAP HANA (Relational), now you need to interface with three different system, meaning three different SQL syntaxes. A multi-model database  can serve all these with one integrated enginge. 
</p>


<b> Key Features </b>
<ul>
<li> Global Distribution </li>
<li> Regional presence - available in 54+ regions </li>
<li> Always On 99.999% </li>
<li> Elastic Scale - from thousands to hundreds of millions of requests/sec </li>
<li> Low latency guarantee - under 10ms read/write for 99 percentile </li>
<li> Consistency options </li>
<li> No Schema or index management </li>
</ul>

<p> Cosmos DB stores "items" in "containers", with these two concepts being surfaced differentyl depending on the API (these would be
"documents" in "collections" using MongoDB). Cosmos DB is a NoSQL Database as a Service (higher SLA 99.999% Service Level Agreement). Cosmos DB supports 99.999 percent uptime.  </p>

<b> Data ingestion </b>
<p> To ingest data into Azure Cosmos DB you can either use Azure Data Factory, create an application that writes data into Azure Cosmos DB
through its API, upload JSON documents, or directly edit the document. </p>

<b> Queries </b>
<p> You can create stored procedures, triggers and user-defined functions (UDFs). Or use the JavaScript query API </p>

<b> Data security </b>
<p> Azure Cosmos DB supports data encryption, IP firewall configurations, and access from virtual networks. Data is encrypted automatically. User authentication is based on tokens, and Azure Active Directory provides role-based security. </p>

---

<h3> Azure SQL Database </h3>
<p><a href = "https://www.youtube.com/watch?v=BgvEOkcR0Wk"> Video Explanation </a></p>
<p>This unit focuses on Azure SQL Database, the platform as a service (PaaS) database offering. Azure SQL Database is a managed relational database service. It supports structures such as relational data and unstructured formats such as spatial and XML data. SQL Database provides online transaction processing (OLTP) that can scale on demand. </p>

<b> When to use SQL Database </b>

<p> Use SQL Database when you need to scale up and scale down OLTP systems on demand. SQL Database is a good solution when your organization wants to take advantage of Azure security and availability features. Organizations that choose SQL Database also avoid the risks of capital expenditures and of increasing operational spending on complex on-premises systems. SQL Database is backed up by the Azure service-level agreement (SLA). </p>

<b> Key features </b>
<p> SQL Database delivers predictable performance for multiple resource types, service tiers, and compute sizes. Requiring almost no administration, it provides dynamic scalability with no downtime, built-in intelligent optimization, global scalability and availability, and advanced security options. You no longer have to devote precious time and resources to managing virtual machines and infrastructure.</p>

<b> Ingesting and processing data </b>
<p> SQL Database can ingest data through application integration from a wide range of developer SDKs. Allowed programming languages include .NET, Python, Java, and Node.js. Beyond applications, you can also ingest data through Transact-SQL (T-SQL) techniques and from the movement of data using Azure Data Factory.</p>

<b> Queries</b>
<p> Use T-SQL to query the contents of a SQL Database.</p>

<b> Data security </b> 
<ul> 
<p> Azure SQL Database provides a range of built-in secuirty and compliance features. </p>
<li> Advanced Threat Protection </li>
<li> SQL Database auditing </li>
<li> Data encryption </li>
<li> Azure Active Directory Authentication </li>
<li> Multifator authentication </li>
<li> Compliance certification </li>
</ul>

---

<h3> SQL Data Warehouse </h3>
<p> <a href="https://www.youtube.com/watch?v=wjIuWBvD4_I"> Video Explanation </a> </p>
<p>Azure SQL Data Warehouse is a cloud-based enterprise data warehouse. It can process massive amounts of data and answer complex business questions. </p>

<b> When to use SQL Data Warehouse </b>

<p> 
Data loads can increase the processing time for on-premises data warehousing solutions. Organizations that face this issue might look to a cloud-based alternative to reduce processing time and release business intelligence reports faster. But many organizations first consider scaling up on-premises servers. As this approach reaches its physical limits, they look for a solution on a petabyte scale that doesn't involve complex installations and configurations.
</p>

<b> Key features</b>
<ul>
  <li> SQL Data Warehouse uses massively parallel processing (MPP) to quickly run queries across petabytes of data.  </li>  
  <li> Storage is separated from the compute nodes, you can scale the compute nodes independently </li>  
  <li> Data Movement Service (DMS) coordinates and transports data between compute nodes </li>  
  <li> QL Data Warehouse supports two types of distributed tables: hash and round-robin. </li>  
  <li> can also pause and resume the compute layer, you pay only for the computation you use. </li>  
</ul>


<b> Ingesting and processing data </b>
<p> SQL Data Warehouse uses the extract, load, and transform (ELT) approach for bulk data. 
SQL professionals are already familiar with bulk-copy tools such as bcp and the SQLBulkCopy API.
Data engineers who work with SQL Data Warehouse will soon learn how quickly PolyBase can load data.
Developers use PolyBase to apply stored procedures, labels, views, and SQL to their applications.</p>

<b> Queries </b>
<p> ou can use the familiar Transact-SQL to query the contents of SQL Data Warehouse 
Load data fast by using PolyBase with additional Transact-SQL constructs such as CREATE TABLE and AS SELECT.</p>

<b> Data security </b> 
<p>  supports both SQL Server authentication and Azure Active Directory. </p>

---

<h3> Azure Stream Analytics </h3>

<p> <a href ="https://www.youtube.com/watch?v=rrODKaB7XSY"> Video Explanation </a> </p>
<p> Broadcasting continous event data is known as data streaming. Streaming data is high volume and has a ligther payload (Payload is the part of transmitted data that is the actual intended message. Headers and metadata are sent only to enable payload delivery.) than
  nonstreaming systems. You can use Stream Analytics for Internet of Things (IoT) monitoring, web logs, remote patient monitoring and 
  point of sale (POS) systems. </p>
  
<b> When to use Stream Analytics </b>
<p> UJse Steram Analyitcs if your organization must respond to data events in real time or analyze large batches of data in a continous time-bound stream. Your organization must decide whether to work with streaming data or batch data</p>

<p> Data is ingested from IoT devices and gateways into an event hub or IoT hub. The difference between an IoT Hub and a Event Hub is that Event Hub only take in data while IoT hub can also send data (e.g. firmware updates). The Event / IoT hub then streams data into Steam Analytics for real-time analysis. Batch systems (Non-Streaming) process groups of data that are stored in Azure Blob store. They do this in a single job that runs at a predefined interval. Don't use batch systems for business intelligence systems that can't tolerate the predefined interval. An autonomous vehicle can't wait for a batch system to adjust its driving. Similarly, a fraud-detection system must decline a questionable financial transaction in real time and therefore needs stream data. </p>

<b> Data ingestion </b>
<p> Set up data ingestion in Stream Analytics by configuring data inputs from first-class integration sources. These sources include Azure Event Hubs, Azure IoT Hub, and Azure Blob storage. An IoT hub is the cloud gateway that connects IoT devices. IoT hubs gather data to drive business insights and automation. Azure Event Hubs provides big-data streaming services. It's designed for high data throughput, allowing customers to send billions of requests per day. Event Hubs uses a partitioned consumer model to scale out your data stream. This service is integrated into the big-data and analytics services of Azure. These include Databricks, Stream Analytics, Azure Data Lake Storage, and HDInsight. Event Hubs provides authentication through a shared key.
</p> 

<b> Data processing </b>
<p> To process streaming data, set up Stream Analytics jobs with input and output pipelines. Inputs are provided by Event Hubs, IoT Hubs, or Azure Storage. Stream Analytics can route job output to many storage systems. These systems include Azure Blob, Azure SQL Database, Azure Data Lake Storage, and Azure Cosmos DB.

After storing the data, run batch analytics in Azure HDInsight. Or send the output to a service like Event Hubs for consumption. Or use the Power BI streaming API to send the output to Power BI for real-time visualization. </p>

<b> Queries </b>
<p> To define job transformations, use a simple, declarative Stream Analytics query language. The language should let you use simple SQL constructs to write complex temporal queries and analytics. The Stream Analytics query language is consistent with the SQL language. If you're familiar with the SQL language, you can start creating jobs.</p>

<b> Data security </b>

<p> Stream Analytics handles security at the transport layer between the device and Azure IoT Hub. Streaming data is generally discarded after the windowing operations finish. Event Hubs uses a shared key to secure the data transfer. If you want to store the data, your storage device will provide security.</p>

---

<h3> Azure HDInsight </h3>
<p> <a href="https://www.youtube.com/watch?v=phKiAIHMLAI"> Video Explanation </a> </p>
<p> <a href ="https://www.youtube.com/watch?v=x3o7aG9kyxg"> Video Explanation </a> </p>

<p> Azure HDInsight provides technologies to help you ingest, process, and analyze big data. It supports batch processing, data warehousing, IoT, and data science. <b> Azure HDInsight is simply a cloud version of Hoortonworkds data platform (100 % Apache Hadoop). Azure HDInsight can also be described as Apache Haddop running on Microsoft Azure.
  
 Azure will create cluster for us. Azure is creating the cluster with help of configurations from HortonWorks platform.  
  
  </b> </p>

<ul>
  <li><b> Hadoop </b> includes Apache Hive, HBase, Spark and Kafka. Hadoop stores data in a file system (HDFS). Spark stores 
  data in memory. This difference in storage makes Spark about 100 times faster. </li>
  <li> <b> HBase </b> is a NoSQL database built on Hadoop. It's commonly used for search engines. HBase offers automatic failover.</li>
  <li> <b> Storm </b> is a distributed real-time streamlining analytics solution. </li>
  <li> <b> Kafka </b> is an open-source platform that's used to compose data pipelines. It offers message queue functionality, 
  which allows users to publish or subscribe to real-time data streams. </li>
</ul>

<b> Ingesting data </b> 

<p> As a data engineer, use Hive to run ETL operations on the data you're ingesting. Or orchestrate Hive queries in Azure Data Factory. </p>
<b> Data processing </b> 
<p> In Hadoop, use Java and Python to process big data. Mapper consumes and analyzes input data. It then emits tuples that Reducer can analyze. Reducer runs summary operations to create a smaller combined result set.
  
<b> Queries </b> 
<p>In Hadoop supports Pig and HiveQL languages. In Spark, data engineers use Spark SQL. </p> 


<b> Data security </b>
<p> Hadoop supports encryption, Secure Shell (SSH), shared access signatures, and Azure Active Directory security.</p>
  

Spark processes streams by using Spark Streaming. For machine learning, use the 200 preloaded Anaconda libraries with Python. Use GraphX for graph computations.

Developers can remotely submit and monitor jobs from Spark. Storm supports common programming languages like Java, C#, and Python.</p>

<b> Computer Memory vs Computer Storage </b>
<p> 
Memory is used in the computer to tempory store information (tempory stored in RAM, random access memory) until you click save.
And then its saved to your harddrive were its keept. 
  

</p>


---

<h3> other Azure data services </h3>

<ul>
  <li> Azure Databricks </li>  
  <li> Data Factory </li>
  <li> Data Catalog</li>
</ul>

<b> Databricks </b>

<p> Databricks is a serverless platform that's optimized for Azure. It provides one-click setup, streamlined workflows, and an interactive workspace for Spark-based applications.

Databricks adds capabilities to Apache Spark, including fully managed Spark clusters and an interactive workspace. You can use REST APIs to program clusters. In Databricks notebooks you'll use familiar programming tools such as R, Python, Scala, and SQL. Role-based security in Azure Active Directory and Databricks provides enterprise-grade security.</p>

<b> Data Factory </b>

<p> Data Factory is a cloud-integration service. It orchestrates the movement of data between various data stores. You can create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation. Use Data Factory to create and schedule data-driven workflows (called pipelines) that can ingest data from data stores. Data Factory processes and transforms data by using compute services such as Azure HDInsight, Hadoop, Spark, and Azure Machine Learning. Publish output data to data stores such as Azure SQL Data Warehouse so that business intelligence applications can consume the data.  </p>

<b> Data Catalog </b>

<p> Data Catalog features a crowdsourcing model of metadata and annotations. In this central location, an organization's users contribute their knowledge to build a community of data sources that are owned by the organization.Data Catalog is a fully managed cloud service. </p>

---

<h3>Check Your knowledge </h3>

1. Which data platform technology is a globally distributed, multimodel database that can perform queries in less than a second?
<pre>- Azure SQL Database (OLTP)
- <b>AZURE COSMOS DB</b> </pre>
- Azure SQL Data Warehouse (ETL) 

2. Which data store is the least expensive choice when you want to store data but don't need to query it?
<pre>- Azure Stream Analytics
- Azure Databricks
- <b>AZURE STORAGE</b> </pre>
 
3. Which Azure service is the best choice to store documentation about a data source?
<pre>- Azure Data Factory
- <b>AZURE DATA CATALOG</b></pre>
- Azure Data Lake Storage
---
<h3> Notes </h3>

<b> Hadoop </b> 
<p> Hadoop can be thought of a set of open source programs and procedures which anyone can use
as the backbone of their big data operations.

<p> Hadoop is developed for anybody to be able to store and analyze datasets far larger than can be
practically be stored and accessed on one physical storage device (such as a hard disk). Hadoop
is based on the idea that many smaller devices working in parallel are more efficient that
one larger one. Released in 2005 by the Apache Software Foundation, a non-profit organization
which produces open source software. </p>

<ul>
<p> Hadoop is made up of "modules", each of which carries out particular task essential for a computer
  system designed for big data analytics. </p>
  
 <p> HDFS (Hadoop Distributed File System) is the filesystem of the Hadoop framework. HDFS is designed to store and manage big data
  in a efficient manner. Developed by people at Google. HDFS is a Userspace File System. HDFS is not embedded within the operating system
  kernel. On a traditional file system, the block size is of 4-8kbytes. On HDFS the default block size is 64MB. HDFS is not suitable for files which are small in size. Not suitable for reading data from a random position in the file.    
  
<p> <a href="https://www.youtube.com/watch?v=aNeEsfOI5cU"> Video Explanation </a> </p> 

<li> 1. -Distributed File-System </li>
<p> A file system is the method used by a computer to store data. Normally this is determined by the 
OS, however Hadoop system uses its own file system which sits "above" the file system of the host
computer, meaning it can be accessed using any computer running any supported OS </p>
<li> 2. -MapReduce </li>
<p> Two basic operations, Reading data from the database, putting it 
into a format suitable for analysis (map) and performing mathematical operations </p>
<li> 3. -Hadoop Common </li>
<p> Provides the tools (in Java) needed for the user's computer system to read data stored under the
Hadoop file system. </p>
<li> 4. -YARN </li>
<p> Manages resources of the systems storing the data and running the analyisis </p>
</ul>  

<b> Spark </b>


<b> Linus vs Unix </b>

<p> Unix and Linus has same command lines. Operating systems considered Unix: Solaris (Oracle), BSD, macOS. Systems
considered Linux: Ubuntu, Fedora, Debian, Android.

Neither Linux and Unix refer to an operating system today. Back in the 60s and 70s Unix was an operating system. However, when we call an operatingsystem Unix, what we are really saying is that it's Unix standard compliant. For Linux this story is slightly different. Linux is defined by the kernel. The kernel is the software that lives closes to the hardware. The kernel translates instructions from applications to low-level information, to be read by hardware. The kernel is common to all distributions of Linux. 
Many Unix operating system are proprietary. Linux created for liberty (GPL, general public license), open-source, free, derivate of Unix. </p>  
</p>

<b> POSIX vs SUS </b>
<p> POSIX = Portable Operaing Systems Interface, formal standard to uniform Linux system. </p>


<b> Memory Size </b>
<p> Computers stores data with the binary system (0,1). Bit = Binary digit, smallest unit of data (1 or 0). The number of Bits we use determines how much we can store. 8 Bits (e.g. 01011011) is equal to 1 Byte. 1 Byte is equal to store one letter in the alphabet. </p>
<ul>
<li> Bits </li>  
<li> Bytes </li> 
<li> Kilobytes (1k) ~Two pages of text </li> 
<li> MegaBytes (1M) ~5 large books or one photo, or one minute of music</li> 
<li> GigaBytes (9Z ~400 books, 1000 photos, 16 hours music, one very short film, low resolution, 1GB flash drive ~5 dollars) </li> 
<li> TeraBytes (12Z, 1 million pictures, 2 year of music, 10 4-k movies, </li> 
</ul>


<b> Graph database </b>

<p> Relational databse use a ledger-style structure. A thing (level of entity) is a row in a table. Foreign key constraint represent
a relationship. Multilevel joins are slow and complex. Graph are much simpler. Things are nodes. Nodes have properties (often key: "values" pairs). Nodes have labels (similar to table name). This node is person

Example of node: n: Person, id: 1234, first_name: "Ed", last_name: "Finkler". Nodes are connected by relationships or edges. Relationship have a type, direction and can have properties. Typicall graph database dont enforce schema. Summarizing it's only dots and lines. </p>


<b> Filesystem: </b>

<p> There exist text files, music files, video files etc. How does files works and how do computer keep files order with file system.
 File formats are a huge list of numbers stored as a binary. Meta data is stored at the front of the file, ahead of the actual data.
 
 Let's think of storage as a long line of little buckets that store values. It's possible to store more than one file at a time. 
 The simplest option is to store files back to back. E.g. Directory file, File A, File B, File C, File D. How does the computer know where files begin and end. Storage devices have no notion of files. They are just a mechanism to store alot of bits. Therefore we need a speciall file, which record where other ones are located. A good general term is directory file. The directory files stores Name, "todo.txt", "theme.wav", "script.doc", where the files begin and end and how long they are and meta data (when they were created and last modified). The directory file and the maintanance of it is an example of a very simple file system. The part of the operating system that manages and tracks stored files. This particular example is called a flat file system.  
 
Moderns file system stores files in blocks and uses slack space. All file system are aligned to a common size, which simplifies management.

 </p>     

