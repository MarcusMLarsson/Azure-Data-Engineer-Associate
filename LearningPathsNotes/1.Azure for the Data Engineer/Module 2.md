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
<li> <b> Azure Blob: </b>  A scalable object store for text and binary data</li> 
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


  
  
  

