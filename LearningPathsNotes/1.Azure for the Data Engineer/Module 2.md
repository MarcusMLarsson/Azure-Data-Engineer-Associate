<h1> Survey the services on the Azure Data platform </h1>

<h3> Introduction </h3>
<ul>
<li> Learn about Azure technologies </li>
<li> Explore common Azure data platform technologies and identify when to use them. </li>
<li> Learn how engineers can choose technologies to meet their business needs </li>
</li>
</ul>

<h3> Structured data: Review </h3>
<ul>
<li> Relational databases: Microsoft SQL Server, Azure SQL Database and Azure SQL Data Warehouse </li> 
<li> Data structure defined at design time, before data is loaded into the system </li> 
<li> Designed in the form of tables </li> 
<li> Reacts slowly to changes because of that the structural database needs to change every time a data requirement change </li>
<li> When new columns are added, you might need to bulk-update all existing records </li>
<li> Typically uses a query language such as Transact-SQL </li>   
</ul>

<h3> Nonstructured data: Review </h3>
<ul>
<li> Examples of nonstructured data include binary, audio and image files. </li> 
<li> Nonrelational systems, commonly called NoSQL systems. </li> 
<li> Data structure isn't defined at deisgn time, loaded in its raw format</li> 
<li> The data structure is defined only when the data is read </li>
<li> Nonrelatonal systems can also support semistructured data such as JSON file formats</li>
</ul>

<h3> Four types of open-source NoSQL databases </h3>
<ul>
<li> <b> Key-value store: </b> Stores key-value pairs of data in a table structure. </li> 
<li> <b> Document database: </b> Stores documents that are tagged with metadata to aid document searches.</li> 
<li> <b> Graph database: </b> Graph database: Find relationship between data points by using a structure that's composed of vertices and edges.</li> 
<li> <b> Column database: </b> Stores data based on columns rather than rows. Columns can be defined at the query's runtime, allowing flexibility in the data that's returned performantly. </li> 
</ul>

<h3> Azure Storage </h3>
<ul>
<li> <b> Azure Blob: </b>  A scalable object store for text and binary data (any kind of file) </li> 
<li> <b> Azure Files: </b> Managed file shares for cloud or on-premises deployments</li> 
<li> <b> Azure Queue: </b> Graph database: A messaging store for reliable messaging between application components</li> 
<li> <b> Azure Table: </b> A NoSQL store for no-schema storage of structured data </li> 
</ul>

<p> You can use Azure Storage as the storage basis when provisioning a data platform such as Azure Data Lake Storage and HDInsight. But you can also provision Azure Storage for standalone use. For example, you provision an Azure Blob store as a standard storage in the form of magnetic disk storage or as premium storage in the form of solid-state drivers (SSDs)

<h3> Azure Blob storage </h3>
<p> If you need to provision a data store that will store but not query data, your cheapest option is to set up a storage account as a Blob store. Blob storage works well with images and unstructured data, and it's the cheapest way to store data in Azure. </p>

<h3> Key features </h3>
<p> Scalable, secure, durable and highly available. Provides REST (Representational state transfer) APIs and SDKs for Azure Storage in various languages. Supported languages include .NET, Java, Node.js, Python, PHP, Ruby, and Go. 
  
<h3> Data ingestion </h3>
<p> To ingest data into your system, use Azure Data Factory, Storage Explorer, the AzCopy toll, PowerShell or Visual Studio. If you use the File Upload feature to import file sizes above 2 GB, use PowerShell or Visual Studio. AzCopy supports a maximum file size of 1 TB and automatically splits data files that exceed 200 GB. </p>

<h3> Queries </h3>
<p> If you create a storage account as a Blol store, you <b> can't </b> query the data directly. To query it, either move the data to a store that supports queries or set up the Azure Storage account for a data lake storage account. </p>

<h3> Data security </h3>
<p> Azure Storage encrypts all data that's written to it. Azure Storage also provides you with fine-grained control over who has acces to your data. You'll secure the data by using keys or shared access signatures. Azure Resource Manager provides a permissions model that uses role-based access control (RBAC). Use this functionality to set permission and assign roles to users, groups, or applications. </p>

<h3> Azure Data Lake Storage </h3>
<p> Azure Data Lake Storage is a Hadoop-compatible data repository that can store any size or type of data. Azure Data Lake is built from the ground up as naitive Hadoop distributed file system or HDFS, working out of the box with the Hadoop echo system. 
The storage service is available as Generation 1 (Gen1) or Generation 2 (Gen2). Gen1 users are not required to
upgrade to Gen2, but they forgo some benifits. </p>

<p> Data Lake Storage Gen2 users take advantage of Azure Blob storage, a hierarchical file system, and performance tuning
that helps them process big-data analyitcs solutions. In Gen2, developers can access data trough either the Blob API or
the Data Lake file API. Gen2 can also act as a storage layer for a wide range of compute platforms,
including Azure Databricks, Hadoop, Azure HDInsight. </p>

<h3> Where to use Data Lake Storage Gen2? </h3>
<p> Data Lake Storage is designed to store massive amounts of data for big-data analytics. Data Lake Store allows you to store unstructured, semi-structured and structured data and does not require a schema to be defined before the data is loaded.
The compute aspec that sits above this storage can vary. The aspec can include platforms like HDInsight, Hadoop,
Cloudera, Azure Databricks, and Hortonworks. </p>

<h3> Key Features </h3>
<ul>
<li> Unlimited scalability </li>  
<li> Hadoop compatibility</li> 
<li> Security support for both access control lists (ACL) </li> 
<li> POSIX compliance </li>
<li> An optimized Azure Blob File System (ABFS) driver that's desinged for big-data analyitcs</li>
<li> Zone-redundant storage</li>
<li> Geo-redundant storage</li>
</ul>

<h3> Data ingestion </h3>
<p>To ingest data into your system, use Azure Data Factory, Apache Sqoop, Azure Storage Explorer, the AzCopy tool, PowerShell or Visual Studio. </p>

<h3> Queries </h3>
<p> In Data Lake storage Gen1, data enginerers query data with U-SQL language.
In Gen2, Azure Blob Storage API or Azure Data Lake System (ADLS) API. </p>

<h3> Data security </h3>
<p> Data Lake Storage supports Azure Active Directory ACLs, security administrators can control data access by using the
familiar Active Directory Security Groups. Role-based access control (RBAC) is available in Gen1.
Built in security groups include ReadOnlyUsers, WriteAccessUsers, and FUllAccessUsers.Data Lake Storage
automatically encrypts data at rest, protecting data privacy. </p>

---
<h3> Notes </h3>

<h3> Hadoop </h3> 
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

<h3> Linus vs Unix </h3>

<p> Unix and Linus has same command lines. Operating systems considered Unix: Solaris (Oracle), BSD, macOS. Systems
considered Linux: Ubuntu, Fedora, Debian, Android.

Neither Linux and Unix refer to an operating system today. Back in the 60s and 70s Unix was an operating system. However, when we call an operatingsystem Unix, what we are really saying is that it's Unix standard compliant. For Linux this story is slightly different. Linux is defined by the kernel. The kernel is the software that lives closes to the hardware. The kernel translates instructions from applications to low-level information, to be read by hardware. The kernel is common to all distributions of Linux. 
Many Unix operating system are proprietary. Linux created for liberty (GPL, general public license), open-source, free, derivate of Unix. </p>  
</p>

<p> POSIX vs SUS </p>
<p> POSIX = Portable Operaing Systems Interface, formal standard to uniform Linux system. </p>
