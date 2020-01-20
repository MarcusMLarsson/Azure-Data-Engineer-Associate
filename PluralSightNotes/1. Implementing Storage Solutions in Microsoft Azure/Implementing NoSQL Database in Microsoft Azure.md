<h1> Implementing NoSQL Database in Microsoft Azure </h1>

<h3> Introduction </h3>
<ul>
<i> <li> Learn Azure Cosmos DB</li>
<li>  Learn Azure Multimodel API</li>
<li> Azure Table Storage etc</li> </i>
</ul>

---

<h3> An Introduction on NoSQL Databases. </h3>
<ul>
<p> <b>  Managed NoSQL offeings by Azure </b> </p>
<li> Azure Storage (blob, file, queue, table</li>
 <p> Can be used to store unstructured data in cheap storage. Is accessible from any where in the world over HTTP / HTTPS. </p>
<li> Azure Data Lake </li>
 <p> Using Azure Storage under the hood </p>
<li> CosmosDB (previous called Document DB)</li>
 <p> Globally distributed, multimodel database. 
 <ul>
  <li> If you want to store data as JSON document use the SQL and MongoDB API.</li>
  <li> If your data is stored in key-value pairs use the Azure table API.</li>
  <li> If you want to store your data as wide columns use the Cassandra API </li>
  <li> If you want to store your data as graphs use the Gremlin API</li>
 </ul>
 
 </p>
</ul>

<ul>
<p> <b> CosmosDB API </b> </p>
 <li> SQL API </li>
 <li> Cassandra</li>
 <li> Graph (Gremlin) </li>
 <li> MongoDB </li>
 <li> Table </li>
</ul>

<ul>
<p> <b> What is NoSQL</b> </p>
 <li> Not schema dependent. </li>
  <li> Any database that store data which is not in tabular relationships. </li>
  <li> JSON structure is normal: Key value pair.</li>
  <li> Scales better horizontal scaling. </li>
  <li> NoSQL should not only be recommended to store non-relational data. NoSQL can store relational data aswell. </li>
 <li> Mainly about horizontal scalability, availability and price. </li>
</ul>


<ul>
<p> <b> Manage NoSQL offerings by Azure</b> </p>
 <li> IaaS: Provision VMs and install database engines of your choice. </li>
 <li> PaaS (Platform as a Service): Azure manages the underlying infrastructure for you. We will only talk about PaaS in this course. </li>
</ul>

<b> Demo </b>

<p> Start by provisioning Azure storage account. => More services => Storage => Storage Accounts. Account kind: StorageV2 are used normally. Locally redundant storage is the cheapest one. Cool are for archiving. Choose hot. After creating you can choose 4 different storage types under the storage account umbrella. </p>

<p> Let's provision a CosmosDB. More services => Databases => CosmosDB. Leave API as core SQL</p>

<p>Azure Table Storage </p> 
<p> Ideal for storing structured non-relation data. Imagen you want to save information for a group of people. You know this people will have some attributes which are similar to each other, for example first name, last name, email. Azure table storage is a greate option for this kind of data. If you however have a few JSON files which haven nothing incommon, you should store them in a different type which is best for unstructured data (e.g. Azure Blob Storage). Azure Table storage is not good with complex joins. Access data with using OData protocol and LINQ queries. </p>
<ul>
 
 <p> To be able to use Azure Table Storage, you first need a Azure Storage Account. Inside this storage account you can create a few tables (example Users and Posts). Next you can store your data inside these tables. Each row in the tables are referred to as an entity. These entities can have multiple properties, name, email, phonenumber etc. 
 
 <li> Can store large amount of data</li>
 <li> Is a NoSQL datastore </li>
 <li> Is ideal for storing non-relational data </li>
 </ul>
 
 <b> Azure Blog Storage </b>
 <p> Optimized to store massive amount of unstructured data in the cloud. Servering documents directly to browser. Widley used for data back-up and restore. Many Azure services, for example Azure SQL Database are storing their backup in Azure Blob Storage (-10 years). Audio and video files can be uploaded to Azure Blob storage. The service can also be used to store data for analysis. Azure Blob Storage can automatically scale when the demand increases.</p>
 
 <b> Azure Queue Storage </b> 
 <p> Azure queue storage is a service for storing large numbers of messages. You can access the messages vi authenticated calls using HTTP or HTTPs. E.g. passing messages from a web role to a worker role. Imagen you have a website that converts bitmap images into jpg. Users can upload their files and they will get the jpg image. Converting bitmap img to jpg can be time consuming. And you might not be able to convert 1000 of files at the same time. What you can do is per each bit map conversion request you add a message to your Azure queue storage. You have your converter worker role read these messages and do the conversions.
 
 <b> Azure Files </b>
 <p> Azure files offers fully managed file shares in the cloud that are accessible via the industry standard server message block (SMB) protocol. Most people use shared dirves at work. There is an on-premise file server. Your network administrator is mapping those drives to your machine and than you can simply drag and drop files. <b> Azure files can be used to replace on-premises file  servers </b>. If you are using legacy applications which uses shared files you can lift and shift them to the cloud.  </p>
 
 <b> Securing storage accounts. </b>
<ul>
 <li><b> Management security</b> Who can create a storage account, who can delete tables, blobs or queues within the storage?</li>
 <p> Operations that affect the storage account itself. RBAC (roled base access control) roles for storage (owner role, contributor role, reader) </p>
 <li><b> Data access secuirty </b>Who can access the blob data, or who can update the data </li>
 <p> Access to storage account data is blocked by default. You have two main method to grant access, storage account keys (grants complete access), shared access signature (SAS), give the permission required for a <b> limited amount of time </b>. You can even limit by IP, so if you receive an correct request from wrong IP, it will be rejected. You can also enforce HTTPS.</p>
  <li><b> Encryption for data in transit </b> </li>
 <p> You can use both HTTP and HTTPS when calling the REST APIs or accessing objects in storage. It's recommended to always use HTTPS.
 <li><b> Encryption for data at rest </b> </li>
 <p> Data is rest is refered to the data that is stored in the storage account. There are two methods to encrypt this data. The first one is storage service encryption (SSE), this option is able for all storage accounts and can not be disables. You can also use client side encryption. You can programmatically encrypt the data in a client application then send it across the wire (can be done using the storage account SDK). </p>
  <li><b> Auditing and monitoring access </b> Who accessed your blob storage, and at what time? </li>
 <p> You can enable Azure Storage Analytics to log the authentication method used by clients. This data will be saved in Azure montior logs and can be queried </p> 
 <li><b> CORS for browser clients </b>  </li>
 <p> When a web browser running in one domain makes an HTTP request for a different domain, this is called a cross-origin HTTP request. When calling the Azure Table Storage API that return JSON data to be processed by JavaScript client. You can allow origins, methods and headers. </p>
 </ul>
 
 <b> Demo: Provisioning Table Storage in the Azure Portal </b>
 <ul>
 <li> We are going to provision a storage account in the Azure Portal. We will also configure security. More services => Storage accounts => Add. Account kind: StorageV2 (general purpose v2). Choose locally-redundant storage (LRS) for replication. </li>
 <li> Go to resource => Access keys (under settings). Shared access signature (SAS token)? I can define if the token is only going to be used as a Blob, file storage for example. I can allow user permissions (can they read, write, delete, add, update etc). You can put a time frame on SAS token.</li>
 <li> Generate SAS and connection string (generates a token, a connection string), url for choosen storage type (blob/file/table/queue) </li>
 <li> Encryption: Option to use your own key stored in Azure Key Vault for encryption </li>
 <li> Firewalls and virtual networks: By default all the services within all virtual networks can access my storage account. You can change that by specifying a few selected virtual networks (selected networks). Here I can whitelist IPs which are allowed to access my storage account or even access existing virtual network or create a new virtual network and assign it to my storage account.</li>
 <li> CORS (cross-origin request): Here you can specify CORS for Blob, File, QUeues and Tables separately. Imagine you have a client JavaScript application on domain name x, you should come here and whitelist that domain here. Server-side client can make requests directly to this storage account. You can also whitelist HTTP headers or verbs.</li>
 </ul>
 
 
 
 
 ---
 
 <b> Notes </b>
 
 <p> REST api </p>
 
