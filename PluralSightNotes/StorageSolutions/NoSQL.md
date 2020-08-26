<h1> Implementing NoSQL Database in Microsoft Azure </h1>
<p><b> What is NoSQL and why use it?  </b></p>
<ul> 
<li> NoSQL is any database that store data which is not in tabular relationships (not schema dependent). </li>
<li> Mainly about horizontal scalability, availability, price and agile development (in contrary relational databases are designed to run on a single serie in order to maintaine the integrity of the table mappings and requires consistency) </li>
<li> NoSQL databases are designed to handle unstructured data (such as texts, social media posts, photos, videos, email) </li>
</ul>

<p> <b>  Managed NoSQL offeings by Azure </b> </p>
<ul>
<li> Azure Storage (blob, file, queue, table)</li>
 <p> Can be used to store unstructured data (csv, video, image etc) in cheap storage. Is accessible from anywhere in the world over HTTP / HTTPS. </p>
<li> Azure Data Lake </li>
 <p> Uses Azure Storage under the hood. </p>
<li> CosmosDB (previous called Document DB)</li>
 <p> Globally distributed, multimodel database. </p>
 </ul>
<p> <b> Options are available for </b> </p>
<ul>
 <li> IaaS (Infrastructure as a Servce): Provision VMs and install database engines of your choice. </li>
 <li> PaaS (Platform as a Service): Azure manages the underlying infrastructure for you. We will only talk about PaaS in this course.</li>
</ul>

<h3> <a href="http://www.sigops.org/s/conferences/sosp/2011/current/2011-Cascais/11-calder-online.pdf"> Azure Storage Account</a></h3>
<li> A storage account is an cloud repository for data (Blob, File, Queue, Table) </li>
<li> Notice that, a storage account is not a NoSQL service or a database, its a container for various file and storage services</li>
<li>A storage account is just to store data. A database does not only store data, but makes the data easily accessible to users, for example with queries</li>
<br>

<b> Azure Table Storage </b> 
<p> Ideal for storing structured non-relation data. Imagen you want to save information for a group of people. You know this people will have some attributes which are similar to each other, for example first name, last name and email. Azure table storage is a great option for this kind of data. If you however have a few JSON files which haven nothing incommon, you should store them in a different storage account, which is better suited for unstructured data (e.g. Azure Blob Storage). Azure Table storage is not good with complex joins. Think of this like a large excel sheet. </p>

 <p> To be able to use Azure Table Storage, you first need an Azure Storage Account. Inside this storage account you can create a few tables. Next you can store your data inside these tables. Each row in the tables are referred to as an entity. These entities can have multiple properties, name, email, phonenumber etc. 
  
 <b> Azure Blog Storage (Binary Large Object) </b>
 <p> Blob Storage is optimized to store massive amount of unstructured data (e.g. audio, video, csv) in the cloud, servering documents directly to the browser. Blob Storage is widely used for data back-ups and restores. Many Azure services (for example Azure SQL Database) are storing their backup in Azure Blob Storage. The service can also be used to store data for analysis. Azure Blob Storage can automatically scale when the demand increases.</p>
 
 <b> Azure Queue Storage </b> 
 <p> Azure queue storage is a service for storing large numbers of messages. You can access the messages via authenticated calls using HTTP or HTTPs. Imagen you have a website that converts bitmap images into jpg. Users can upload their files and they will get the jpg image. Converting bitmap imgages to jpg can be time consuming, and you might not be able to convert 1000 of files at the same time. What you can do is per each bit map conversion request you add a message to your Azure queue storage. You than have your converter worker role read these messages and do the conversions. </p>
 
 <b> Azure Files </b>
 <p> Azure files offers fully managed file shares in the cloud that are accessible via the industry standard server message block (SMB) protocol. Most people use shared dirves at work using an on-premise file server. Your network administrator is mapping those drives to your machine and than you can simply drag and drop files. <b> Azure files can be used to replace on-premises file  servers </b>. If you are using legacy applications which uses shared files you can lift and shift them to the cloud.  </p>
 
 <b> Securing storage accounts </b>
<ul>
 <li><b> Management security</b> </li> <p> Represents who can create a storage account, who can delete tables, blobs or queues within the storage. That is operations that affect the storage account itself. <b> RBAC (roled base access control) </b> roles for storage (owner role, contributor role, reader) </p>
 <li><b> Data access secuirty </b> </li> <p> Represents who can access the blob data, or who can update the data. Access to storage account data is blocked by default. You have two main method to grant access, <b>storage account keys</b> (grants complete access) and <b> shared access signature (SAS)</b>, which gives the permission required for a <b>limited amount of time</b>. You can even limit by IP, so if you receive an correct request from wrong IP address, the request will be denied. You can also enforce HTTPS.</p>
  <li><b> Encryption for data in transit </b> </li>
 <p> You can use both HTTP and HTTPS when calling the REST APIs or accessing objects in storage. It's recommended to always use HTTPS.
 <li><b> Encryption for data at rest </b> </li>
 <p> Data at rest is refered to the data that is stored in the storage account. There are two methods to encrypt this data. The first one is <b> storage service encryption (SSE) </b>, this option is enabled for all storage accounts and can not be disables. You can also use client side encryption. You can programmatically encrypt the data in a client application then send it across the wire (can be done using the storage account SDK). </p>
  <li><b> Auditing and monitoring access </b> </li> <p> Who accessed your blob storage, and at what time? 
 You can enable <b> Azure Storage Analytics </b> to log the authentication method used by clients. This data will be saved in Azure montior logs and can be queried </p> 
 <li><b> CORS (Cross-Origin Resource Sharing) for browser clients </b>  </li>
 <p> <b> CORS </b> is a mechanism that uses additional HTTP headers to tell browsers to give a web application running at one origin, access to selected resources from a different origin. You can allow origins, methods and headers, when calling the Azure Table Storage API that return JSON data to be processed by the JavaScript client. </p>
 </ul>
 
 
  <b> Azure Storage redundancy </b>
  <p> Azure Storage always stores multiple copies of your data so that it is protected from planned and unplanned events, including transient hardware failures, network or power outages, and massive natural disasters. Redundancy ensures that your storage account meets the Service-Level Agreement (SLA) for Azure Storage even in the face of failures. </p>
  <ul>
 <li> Locally redundant storage (LRS) </li>
 <p> copies your data synchronously three times within a single physical location in the primary region. LRS is the least expensive replication option, but is not recommended for applications requiring high availability. LRS protects your data against server rack and drive failures. However, if a disaster such as fire or flooding occurs within the data center, all replicas of a storage account using LRS may be lost or unrecoverable.  </p>
 <li> Zone redundant storage</li>
 <p> copies your data synchronously across three Azure availability zones in the primary region. For applications requiring high availability, Microsoft recommends using ZRS in the primary region, and also replicating to a secondary region. With ZRS, your data is still accessible for both read and write operations even if a zone becomes unavailable. Microsoft recommends using ZRS in the primary region for scenarios that require consistency, durability, and high availability. We also recommend using ZRS if you want to restrict an application to replicate data only within a country or region because of data governance requirements. However, ZRS by itself may not protect your data against a regional disaster where multiple zones are permanently affected. For protection against regional disasters, Microsoft recommends using geo-zone-redundant storage   </p>
 <li> Geo-redundant storage</li>
 <p> copies your data synchronously three times within a single physical location in the primary region using LRS. It then copies your data asynchronously to a single physical 
 <li> Read-access geo-redudant storage</li>
 <p> Geo-redundant storage (with GRS or GZRS) replicates your data to another physical location in the secondary region to protect against regional outages. However, that data is available to be read only if the customer or Microsoft initiates a failover from the primary to secondary region. When you enable read access to the secondary region, your data is available to be read at all times, including in a situation where the primary region becomes unavailable.</p>
  <li>Geo-zone-redundant storage</li>
 <p> copies your data synchronously across three Azure availability zones in the primary region using ZRS. It then copies your data asynchronously to a single physical location in the secondary region.s </p>
 <li>Read-access geo-zone-redundant storage</li>
 </ul>

 <h3> Azure Cosmos DB </h3>
 <ul>
<li> Cosmos DB is a globally distributed multi-model database </li>
<li> A multi-model database is designed to support multiple data models against a single, integrated backend. Relational (SQL), NoSQL (MongoDB), Graph (Gremlin), wide column store (Cassandra), key-value pairs (Table) models are examples of data models that are supported by Cosmos DB. </li>
<li> Cosmos DB is a unit of management for a set of containers </li>
</ul>
<p> <b> What back-end to pick </b></p>
 <ul>
  <li> If you want to store data as JSON document use the SQL and MongoDB API.</li>
  <li> If your to store the data in key-value pairs use the Azure table API.</li>
  <li> If you want to store your data as wide columns use the Cassandra API </li>
  <li> If you want to store your data as graphs use the Gremlin API</li>
 </ul>
 
 <b> Cosmos DB Concepts - Global Distribution and Multi-homing </b>
 <p> Multi-homing APIs </p> 
 <ul>
 <li> Your application is aware of the nearest region and can send requests to that region </li>
 <li> Nearest region is identified without any configuration changes. </li>
 <li> When a new region is added or removed, the connection string stays the same. </li>
 </ul> 


 <b> Time-to-live</b>
 <p> With time-to-live (TTL) you can set an expire date on some of your objects saved into the database. You don't need to clean up your database and delete when the time has come. You can set the expiry time on Cosmos DB data items; the setting is called TTL and is set in seconds. Cosmos DB will automatically remove the items after this time period, since the last modififed time. </p>
 
<b> Database Consistency</b>
<p> Imagen you have a distributed database. One replica exist  in West US, and the other replica exists in East US, and there is a global replication going on between these two. So every 5 seconds, the data in West US will be replicated to East US. This database holds information of a few bank clients, and the information we are interest in is the credit score of these clients. Let's say credit score goes from 750 to 700 for on customer in West US database. 
<pre>UPDATE History Set
CreditScore = 750
WHERE ID = 10 </pre>

Now someone in the East US needs to access the credit score of the customer updated in West US (id = 10). So he runs the query. 
<pre>SELECT CreditScore FROM History,
WHERE ID = 10 </pre>

What score do the observer get? 700 or 750? The observer is not suppose to see the old credit score. This is the concept around data consistency. Relational Databases make sure you always get the consistent version of the data, even if you have to wait for some time. Azure Cosmos DB gives the option to add consistency to your database. 
</p>
 
 
 <b> Cosmos DB Concepts - Consistency Levels </b>
 
<p> There is always a trade off between data consistency and data availability & latency. Most distributed databases ask you to choose between the two extreme consistency levels: strong and eventual consistency. Strong means you always see the latest version of the data, even if you have to wait for a few milliseconds or seconds. Eventual consistency, meaning, the database enginge doesn't guarantee that you see the latest data, but at the same time, the data, is returned very quickly. Azure Cosmos DB offers 5 consistency levels to choose from, including the 2 extremes. Moving from up to down you get higher latency and throughput at the price of weaker consistency. </p>
<ul>
 <li><b> Strong</b></li>
 Strong always guarantes consistency level.
  <li> <b>Bounded staleness</b></li>
 For the bounded staleness you specify a window of staleness, and this windows is defined in time and number of operations. For example, you are going to say, I want my Window of staleness to be 10 minutes and for 1000 operations. So any observer accessing Cosmos DB outside this staleness Windows is going to see a strong consistency. For the observers accessing Cosmos DB within this staleness window, they are only guaranteed consistent prefix consistency level, meaning they are guaranteed to see in order updates, but not necessarily the latest and most consistent version of the data.
  <li><b>Session</b></li>
 Session consistency level is in the middle ground. It's the default consistency level when you are povisioning a new instance of Cosmos DB. Same as bounded staleness, you are going to have two different consistency levels, but instead of a staleness window, you are dealing with a session. So if you observer is accessing Cosmos DB within the same session that writes data, they are going to see a strong consistency; however for other obsvers accessing Cosmos DB from other sessions, they are going to only see consistent prefix.
  <li><b>Consistent prefix</b></li>
 For consistent Prefix the only thing Cosmos DB is guaranteeing is that your observer is always going to see in the correct order of updates. If they see update N, they are going to see all the ones before as well, but consistent Prefix does not guarantee N is the latest version. 
  <li> <b>Eventual</b></li>
 Finally we have the Eventual consistency level. This is the weakest consistency level. For Eventual consistency level you might see out of order updates.
 </ul>
  
 <b> Cosmos DB Concepts - Data Partitioning </b>
 
 <p> An Azure Cosmos database is a unit of management for a set of containers. A single database consist of a set of schema-agnostic container. The data you store inside containers can be partioned based on their partition key. A logical partition consists of a set of items that have the same partition key. Data that's added to the container is automatically partitioned across as set of logical partitions. Logical partitions are mapped to physical partitions that are distributed among several machines. Throughput provisioned for a container is divided evenly among physical partitions. </p>
 
 <p> Don't pick an partition key that result in "hot spots" within your applications. In other words, choose a partition key that has a wide range of values, so your data is evenly spread across logical partitions. If you are saving data about people in their cities, chosing city as the partition key might be a good idea because this way you make sure your data is roughly spread evenly among different logical partitions (assuming the cities you are choosing have roughly the same amount of population). For partition keys, try to use properties that appear frequently as a filter in queries; including the partition key in the filter predicate improves query performance.  A single logical partition has a limit of 10 GB of storage </p>


 <b> Security </b>
 <ul>
 <li> RBAC (Roll based access control) to grant access to users, groups or applications. </li>
 <li> Use Firewall to limit clients who can access Cosmos DB </li>
 <li> Deploy Cosmos DB into a VNet & use NSGs: Azure Cosmos DB can be integrated with a virtual network. This way, you can use network security groups to control inbound and outbound traffic for your Cosmos DB </li>
 <li> CORS (Cross-origin resource control) can be whitelisted for Azure Cosmos DB as well. So if you have a client-side application which is directly calling Cosmos DB APIs to get data back, you can whitelist those applications in Azure Cosmos DB so those requests can be made from the browser.  </li>
 <li> Read-only and read-write keys </li>
</ul>

<b> Working with Azure Cosmos DB - MongoDB API</b>

<p>
 MongoDB is a cross-platform document-oriented database program. MongoDB is a NoSQL database. Documents are stored in JSON format. The conecpt of containers is called collection for MongoDB. </p>
 <p>
 Why would you wan't to migrate your already working MongoDB database to Cosmos DB? You can get financially backed <b> SLAs (service level agreement) </b> for the NoSQL APIs powered by Cosmos DB. Cosmos DB provides global distribution with multi-master replication. You can have multiple nodes around the world and all of them can write to your database. If you have more traffic, you can elastically scale the provisioned throughput and storage for your Cosmos database. You pay only for the throughput and storage you need. 
 </p>
<ul> 
 <p> Let's take alook at the pre-migrating steps before migrating your data. 
</p>
 <li> Create an Azure Cosmos AB account </li>
 <p> See previous demo </p>
 <li> Estimate the throughput needed for your workload (you can change this later) </li>
 <p> Throughput can be provisioned on both collection & database. You can choose database-level throughput if not sure. Throughput is measured in Request Units (RUs) / second. RU is an abstraction of physical resources (Memory, CPU, IOPs). The concept of RUs is very similar to the concept of DTUs in Azure SQL Database.  </p>
 <p> Key factors affecting needed RUs (Memory, CPU, IOPS), The size of an item effects the number of RUs consumed to read/write the item. The number of RUs consumed to write an item increases as the item property count increases. The frequency of CRUD (create, read, update, delete). The complexity of queries (query pattern). Azure has a capacity calculator which can help you estimate throughput. </p>
 
 <li> Pick an optimal partition key for your data (can't be changed if you don't recreate the collection)</li>
 <p> Cosmos DB uses partitioning to scale individual containers in a database to meet the scalability and performance needs of the application. Follow best practices to avoid "hot" partitions. Choose a partition key so your data is divided equally.</p>
 
 <li> Understand the indexing policy that you can set on your data </li>
 <p> Azure Cosmos DB indexes all the data field upon ingestion. However, it is recommended to turn off indexing when migrating data. We are going to use Azure Data Migration Service (DMS) to migrate data from MongoDB to Cosmos DB. This services can migrate MongoDB indexes with unique indexes. However, the unique indexes must be created in destination before the migration. It's important to note that you can not create unique indexes, when there is already data in collections. We are going to use Azure Database Migration service to migrate a MongoDB  collection to Azure Cosmos DB.  </p>
</ul>

<p>
 Post-migration steps: After your data is migrated to the destination you need to connect your application with the connection string. The other three steps are optional steps. You can optimize the indexing policy, you can globally distribute your data and you can set concistency level of your choice.
 </p>

<b> Working with Azure Cosmos DB - Table API </b>

<p> So you already have your data in Azure Table Storage. Why would you migrate to Cosmos DB Table API? Azure Cosmos DB offers global distribution. Azure Table Storage is fast but you don't get SLAs around latency. Azure Cosmos DB provides less than 10 millisecond latency for reads. Azure Table Storage has a maximum throughput of 20,000 operations/s, which is not the limit for Azure Cosmos DB (more operations/s). Azure Table Storage only provide primary index on partition key and row key. There are no secondary index. For Azure Cosmos DB you get automatic and complete indexing on all properties by default. Meaning queries will run faster as they can utilize these indexes. With Azure Table Storage you get strong consistency within primary region and eventual consistency within secondary region. For Azure Cosmos DB you have five well-defined consistency level. You get higher SLAs with Azure Cosmos DB.
 

Azure Cosmos DB containers are named table for Azure Table API. If you have your data migrated to Azure Cosmos DB Table API there are multiple ways for you to query your data. You can query data using partition key and row key. Alternativly you can query your data by using an OData filter. Finally, you can query by using LINQ (.NET SDK).

<pre> 

Using PartitionKey and Rowkey. The combination of PartitionKey and Rowkey forms an entity's primary key.

https://<table-endpoint>/People(PartitionKey='Boston', RowKey='1000')
 
OData Filter, looking for an item, with the PartitionKey of Boston and the Email address of Reza@test.com. The property name, operator and constant value must be separated by URL-encoded spaces (%20). All parts of the filter string are case-sensitive. 

https://<endpoint>/People()?$filter=PartitionKey%20eq%20'Boston'%20and%20Email%20eq%20'Reza@test.com'
 
Finally, you can use the LINQ (.NET SDK) syntax. To do so, you need to install the correct version of .NET Framework SDK (using Microsoft.Azure.Cosmos.Table).
</pre>

<b> Working with Azure Cosmos DB - Gremlin (graph) API. </b>

<p> What are the graph data model components and what are uses cases in the real world? Azure Cosmos DB Gremlin API can be used as a graph data base. What is a graph data model? Real world data is naturally connected. Traditional data modelling focuses on entities not relationships. For many applications, there's need to model both entities and relationships. A graph database persists relationships in the storage layer. This leads to highley efficient graph retrieval operations. Graph data models are included within the NoSQL or non-relational category, sinnce there is no dependency on a schema or constrained data model. </p>

<p> A property graph is a structure that's composed of vertices (circle) and edges (connections). Both vertex and edge can have properties. Vertices are discrete entities such as a person, a place or an event. Edges are relationships between vertices. Finally we have properties. These are information about the vertices e.g. name or age. Real world applications of a graph data model are social networks, recommendation engines, geospatial, IoT. </p>

<p> Apache Gremlin is a graph traversal (query) language. You can use Gremlin to add, update, delete and query graph items. These items include vertices, edges and properties. There are multiple ways to interact with your graphs in Azure Cosmos DB Gremlin API. You can use the Gremlin SDK, which is available for .NET, Java, Node.js, Python or you can use Gremlin to interact with your graph. You can download the Apache Gremlin console and use that, or alternatively, run your Gremlin queries from within the Azure Portal. </p>

<p> Graph is similar to container. Use a partition key. </p>

<pre> 

<p> Imperative traversal</p>

g.V().has("name", "gremlin").    // Get the vertex with name "gremlin"
   out("knows").                 // Traverse to the people that Gremlin knows.
   out("knows).                  // Traverse to the people those people know.
   values("name")                // Get those people's names.
     </pre>
     
<pre>

<p> Declarative traversal</p>

g.V().match(
  as("a").out("knows").as("b"),        // there exists some "a" who knows "b"
  as("a").out("created").as("c"),        // there exists some "a" who created "c"
  as("b").out("created").as("c"),      // there exists some "b" who created "c"
  as("c").in("created").count().is(2)) // there exists some "c" created by 2 people.
     select("c").by("name")
</pre>

<b>Working with Azure Cosmos DB - Cassandra API </b>

<p> Apache Cassandra: A wide column store is a type of NoSQL database. Unlike a relational database, the names and format of the columns can vary from row to row in the same table. A few others wide column store databases are Apache Cassandra, Hbase and Azure Tables. Cosmos DB Cassandra API can be used as the data store for apps written for Apache Cassandra. Existing Cassandra applications using CQLv4 compliant drivers, can communicate with the Cosmos DB Cassandra API. You can easily switch from Apache Cassandra to Cosmos DB Cassandra API by just updating the connection string. Use the CQL (Casandra Query Language), Cassandra-based tools and Cassandra client drivers you're already familiar with. </p>

<p> Benefits of using Cosmos DB Cassandra API includes no operations management (PaaS), low latency reads and writes, you can use existing code and tools to work with Cosmos DB, throughput and storage elasticity, global distribution and availability, choice of five well-defined consistency levels </p>

<p> You can choose different tools for interacting with the Cosmos DB Cassandra API. You can use Cassandra-based tools (e.g. cqlsh, SQL Shell), you can use the data explorer and finally you can interact programmatically, using the SDK (CassandraCSharpDriver). In the data explorer, you need to define a keyspace. The keyspace is a container or namespace, if you will, and the tables you create will be inside this keyspace. </p>

<b> Working with Azure Data Lake Storage Gen2 </b>

<p> Azure Data Lake Storage is a hyper-scale repository for big data analytic workloads. You can use this service to capture data of any size, type and ingestion speed. Storage can be accessed from Hadoop (available with HDInsight cluster). Using the WebHDFS-compatible REST APIs. Includes enterprise-grade capabilties: security, manageability, scalability, reliability, and availability. Azure Data Lake Storage is a set of capabilities dedicated to big data analytics, built on top of the Azure Blob storage. </p>

<p> Demo: Provisioning Azure Data Lake Storage Gen2 using the portal. Uploading documents using AzCopy. 

Step 1: Create a storage account
Step 2: Create a file system (?) 
Step 3: Download Azure Storage Explorer 

You can upload files to the Data Lake with the RESTful API or the DistCp tool. Since Azure Data Lake Storage Gen2 is built on top of Azure Blob Storage, you can also use the AzCopy tool to copy documents into this storage. With AzCopy we can have different file formats (csv, xlsx, JSON, xml, sql, accdb, zip etc) </p>



---

<h3> Notes </h3>

<b> Instance </b>
<p> In object-oriented programming (OOP) an "instance" is synonymous with "object". The creation of an instance is called instantiation </p> 

<b> Azure Container Instance </b>
<p> Azure Container Instances is a service that enables a developer to deploy containers on the Microsoft Azure public cloud without having to provision or manage any underlying infrastructure. The service -- which supports both Linux and Windows containers -- eliminates the need for a developer to provision virtual machines, or implement a container orchestration platform, such as Kubernetes, to deploy and run containers. Instead, with Azure Container Instances (ACI), an organization can spin up a new container via the Azure portal or command-line interface (CLI), and Microsoft automatically provisions and scales the underlying compute resources.</p>

<b> Provisioning </b>
<p> Provisioning is the enterprise-wide configuration, deployment and management of multiple types of IT system resources. </p> 


<b> Wide column store </b>
<p> A wide column store is a type of NoSQL database. It uses tables, rows, and columns, but unlike a relational database, the names and format of the columns can vary from row to row in the same table. A wide column store can be interpreted as a two-dimensional key-value store. </p>

<b> HTTP Headers </b>
<p> When you type a url in your address bar, your browser sends an HTTP request and it may look like this </p>
<pre>GET /tutorials/other/top-20-mysql-best-practices/ HTTP/1.1
Host: net.tutsplus.com
User-Agent: Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US; rv:1.9.1.5) Gecko/20091102 Firefox/3.5.5 (.NET CLR 3.5.30729)
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Keep-Alive: 300
Connection: keep-alive
Cookie: PHPSESSID=r2t5uvjq435r4q7ib3vtdjq120
Pragma: no-cache
Cache-Control: no-cache</pre> 

<p> First line is the "Request Line" which contains some basic info on the request. And the rest are the HTTP headers.</p>

<p> After that request, your browser receives an HTTP response that may look like this </p>

<pre>HTTP/1.x 200 OK
Transfer-Encoding: chunked
Date: Sat, 28 Nov 2009 04:36:25 GMT
Server: LiteSpeed
Connection: close
X-Powered-By: W3 Total Cache/0.8
Pragma: public
Expires: Sat, 28 Nov 2009 05:36:25 GMT
Etag: "pub1259380237;gz"
Cache-Control: max-age=3600, public
Content-Type: text/html; charset=UTF-8
Last-Modified: Sat, 28 Nov 2009 03:50:37 GMT
X-Pingback: https://net.tutsplus.com/xmlrpc.php
Content-Encoding: gzip
Vary: Accept-Encoding, Cookie, User-Agent
 
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>Top 20+ MySQL Best Practices - Nettuts+</title>
<!-- ... rest of the html ... --> </pre> 
 
 <p>The first line is the "Status Line", followed by "HTTP headers", until the blank line. After that, the "content" starts (in this case, an HTML output). When you look at the source code of a web page in your browser, you will only see the HTML portion and not the HTTP headers, even though they actually have been transmitted together as you see above.</p>

<b> Classes, Objects, Instance </b>

<p>A car is a class, different cars has different features, cars with similar features can be grouped as objects (car with this color, how takes this many passanges, can reach this speed). An instance is a specific object created from a particular class. </p>


<b> Latency </b>
<p> It is an expression of how much time it takes for a packet of data to get from one designated point to another. Latency depends on the speed of the transmission medium (e.g., copper wire, optical fiber or radio waves) and the delays in the transmission by devices along the way (e.g., routers and modems).	

Latency is the amount of time a message takes to traverse a system.

In a computer network, it is an expression of how much time it takes for a packet of data to get from one designated point to another. It is sometimes measured as the time required for a packet to be returned to its sender.

Latency depends on the speed of the transmission medium (e.g., copper wire, optical fiber or radio waves) and the delays in the transmission by devices along the way (e.g., routers and modems). A low latency indicates a high network efficiency.

Latency and throughput are the two most fundamental measures of network performance. They are closely related, but whereas latency measures the amount of time between the start of an action and its completion, throughput is the total number of such actions that occur in a given amount of time. </p>

<b> Containers </b>
<p>Having code and scripts that only work on your machine is no longer sustainable. You need to be able to share your work and have other teams be able to repeat your results. The idea of a container is that it is an isolated environment in which you can set up the dependencies that you need in order to perform a task. Containers are an alternative to virtual machines, which are a great solution to isolation, but require substantial overhead. With a container framework, you specify the dependencies that your code needs, and let the framework handle the legwork of managing different execution environments. Docker is the defacto standard for containers, and there is substantial tooling built around Docker. </p>

<b> REST api </b>
<p> Representational state transfer (REST) is a software architectural style that defines a set of constraints to be used for creating Web services. Web services that conform to the REST architectural style, called RESTful Web services, provide interoperability between computer systems on the Internet. REST determines how the API looks like. It stands for “Representational State Transfer”. It is a set of rules that developers follow when they create their API. One of these rules states that you should be able to get a piece of data (called a resource) when you link to a specific URL. REST or RESTful API design (Representational State Transfer) is designed to take advantage of existing protocols. While REST can be used over nearly any protocol, it usually takes advantage of HTTP when used for Web APIs. This means that developers do not need to install libraries or additional software in order to take advantage of a REST API design.</p>
 
 <b> Latency </b>
 <p> Latency is a networking term to describe the total time it takes a data packet to travel from one node to another.  </p>
 
 <p> data latency is the time between the creation of data in a source system and the exact time at which the same data is available for end users on the business intelligence platform.</p>


<b>Setup LocalDB server using sqllocaldb (Microsoft SQL Server Management Studio</b>

<a href="https://www.youtube.com/playlist?list=PLWsYJ2ygHmWgGDLIGe0w5nA5QyMDB3-OU"> Youtube playlisy </a>

<pre> sqllocaldb

sqllocaldb info

sqllocaldb create "LocalDBDemo" </pre>

<p> Servername: (LocalDb)\LocalDBDemo
 Authentication: Windows Authentication
 </p> 


<hr> 

<h3> Demo </h3>
<b> <i>The demo section can't be followed by only using my notes </b></i> 

<p> Start by provisioning an Azure storage account. => More services => Storage => Storage Accounts. Account kind: StorageV2 (normally used). Locally redundant storage is the cheapest one. Cool is for archiving, choose hot. After creating a storage account you can choose 4 different storage types under the storage account umbrella. </p>

<p> Let's provision a CosmosDB. More services => Databases => CosmosDB. Leave API as core SQL</p>

<b> Demo: Provisioning Table Storage in the Azure Portal </b>
 <ul>
 <li> We are going to provision (configuration, deployment and management) a storage account in the Azure Portal. We will also configure security. More services => Storage accounts => Add. Account kind: StorageV2 (general purpose v2). Choose locally-redundant storage (LRS) for replication. </li>
 <li> Go to resource => Access keys (under settings). I can define if the token is going to be used as a Blob/File/queque/table storage. I can allow user permissions (can they read, write, delete, add, update etc). You can put a time frame on SAS token.</li>
 <li> Generate SAS and connection string (generates a token, a connection string), url for choosen storage type (blob/file/table/queue) </li>
 <li> Encryption: Option to use your own key stored in Azure Key Vault for encryption </li>
 <li> Firewalls and virtual networks: By default all the services within all virtual networks can access my storage account. You can change that by specifying a few selected virtual networks (selected networks). Here I can whitelist IPs which are allowed to access my storage account or even access existing virtual network or create a new virtual network and assign it to my storage account.</li>
 <li> CORS (cross-origin request): Here you can specify CORS for Blob, File, Queues and Tables separately. Imagine you have a client JavaScript application on domain name x, you should come here and whitelist that domain here. Server-side client can make requests directly to this storage account. You can also whitelist HTTP headers or verbs.</li>
 </ul>
 
<b> Demo: Working with Azure Storage Explorer</b>
<p> 
 
 
There are two different options (desktop version and the online version) to work with <b> Azure Storage Explorer </b>. We will be using the online version of the Storage Explorer (preview) in this demo. In Azure Storage Explorer I have the option to create a blob, file, queue or tables storage. Let's start with creating a Table Storage add a new entity to the table. RowKey and PartionKey are created automatically. Remember, that RowKey, PartionKey and TIMESTAMP are three properties which are system properties and mandatory for every entity. The TIMESTAMP will be managed by Azure, so you don't need to worry about that. However, it's your responsibility to provide the value for PartionKey and RowKey. It's also your responsibility to choose the right PartitionKey so your data is divided into appropriate size. Now when the system properties are defined, press add property. Press insert  </p>

<b> Demo: Working with Azure Table Storage .NET SDK (Software development kit)</b>
<p><a href="https://github.com/Azure/azure-sdk-for-net">Azure SDK for .NET </a></p>
<p><a href="https://github.com/Azure/azure-sdk-for-python"> Azure SDK for Python </a></p>
 <p> We are going to write a small .NET application which connects to this storage account and reads an entity from our existing table. First, let's take a look at our data. => Storage Explorer => Tables. Start a console application in Visual Studio. Download WindowsAzure.Storage NuGet package. Grab the connection string under Access keys.    </p>
 
<pre>using Microsoft.WindowsAzure.Storage;                  <i> //importing package from SDK </i>
using Microsoft.WindowsAzure.Storage.Table;             

namespace AzureStorageSDK                                   <i> //namespaces are used to organize classes </i>             
{
    class Program                                           <i> //A class is a blueprint for creating objects </i> 
    {                                                            
      static void Main(string[] args)    <i> // Void returns nothing, static means that there's only one (don't belong to an object) </i>                         
        {
            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=namestorageaccount;AccountKey=lYMyjeY0YFvEKIdy/IRJyLwxKQWTEi7y0VZFLGV9rHVxDDcKfGKmF9uM4YGOTXAhNRj+g5SCEXN6NXyxDBRGEA==;EndpointSuffix=core.windows.net";

           <i> // A connection string includes the authorization information required for your application to access data in an Azure   Storage account </i> 

            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);
            
           <i> // CloudStorageAccount is a class, account is an object, storageConnectingString represents our storage credentials </i>
           <i> // Parse is a method which parses a connection string and returns a CloudStorageAccount created from the connectiong string. </i>
          CloudStorageAccount </a> </i>

            CloudTableClient serviceClient = account.CreateCloudTableClient();       
           <i> // CloudTableClient is a class, serviceClient is an object </i>

            CloudTable table = serviceClient.GetTableReference("TableTest");

            var opperation = TableOperation.Retrieve<TableTest>("Sweden", "1");

            var jobResult = table.ExecuteAsync(opperation);

            var entity = jobResult.Result;
        }
    }
}
</pre>

<pre>using Microsoft.WindowsAzure.Storage.Table;

namespace AzureStorageSDK                 <i> // namespace are used to organize classes </i>
{
    internal class TableTest : TableEntity       <i> // Class TableTest is inheriting from TableEntity </i>
    {

        public TableTest()
        {

        }

        public TableTest(string pk, string rk)
        {
            PartitionKey = pk;
            RowKey = rk;
        }


        public string Name { get; set; }

        public string Email { get; set; }

        public string Phone { get; set; }
    }
}</pre>


<b> Demo: Provisioning a new Cosmos DB instance, Containers, and TTL </b>
 <p> Let's start with creating an Cosmos DB. Go tomore Services => Cosmos Db. Overview => Add container. Remember an Cosmos DB is the management unit for a group of containers. You have the option to create a new database or use an existing database within this Azure Cosmos DB account. Name the container, People and pick /City as partinione key. Add a new item (we will use JSON format). When you click save, "_rid", "_self", "_etag":, "_attachments", "_ts" are added automatically.</p>
   
 <b> Demo: Cosmos DB Security </b>
 <p>
If I only need the clients to be able to see the data, but not to update the data,  you can give them Read-only keys (not Read-write keys). Under Firewall and virtual networks you can whitelist by selecting selected networks. CORS (cross-origin resource sharing) is an HTTP feture that enables a web application running under one domain to acces resource in another domain.</p>

 <b> Working with Azure Cosmos DB - SQL (Core) API </b>
 
 <p> Review: An Azure Cosmos container is the unit of scalability for throughput and storage. The container items and the throughput are distributed across a set of logical partitions. Logical partitions are created based on partition keys. An Azure Cosmos container can scale elastically. </p> 
 
 <ul>
 <p> Container name for different APIs </p>
 <li> <b> SQL API:</b> Collection</li>
 <li> <b>Table API:</b> Table</li>
 <li> <b>MongoDB API:</b> Collection</li>
 <li> <b>Cassandra API:</b> Table</li>
 <li> <b>Gremlin API:</b> Graph</li>
 </ul>
 <br>
 
 <p> Use Data Explorer: Azure Cosmos DB SQL API supports querying JSON items using SQL.
<pre>
"firstname": "Marcus",
"lastname": "Larsson,
"email": "mla@mail.se",
"address": { 
    "streetAdress": "Gatan",
    "city": "Stockholm",
    "country": "Sweden",
},
"phone": "+46703 ....."
</pre>

<pre>
SELECT *
FROM People as p
WHERE p.lastname = "Marcus"
</pre>

<p> You can also query nested properties </p>
<pre>
SELECT *
FROM People as p
WHERE p.address.city = "Stockholm"
</pre>

<p> I can select fields of my items into new JSON objects</p>

<pre>
SELECT {"Name":p.id, "City":p.address.city} AS Person
FROM People AS p
WHERE p.address.city = "Gothenburg"
</pre>

<b> Demo: Working with Data Explorer, Partition Keys, and Unique Constraints </b>

<p> Create CosmosDB => Create container => add items </p>

<pre>
{
    "id": "1000",
    "name" : "Reza",
    "email" : "reza@test.com",
    "city" : "Toronto"
}
</pre> 

<pre>
{
    "id": "1001",
    "name": "John",
    "email": "John@test.com",
    "city": "Boston",
}
</pre>

<b> Demo: Using Azure Cosmos DB Data Migration Tool </b>

<p> Let's import some data from another data source to Azure Cosmos DB. I already have an Azure SQL database instance with some sample data in it. Let's go ahead and check it out. </p>

<p> Create a SQL server & Database in Azure. Populate it with data with the help of the pre-compiled binary.

<a href = "https://aka.ms/csdmtool"> pre-compiled binary </a>

<b> Demo: Working with the Azure Cosmos DB Client Library 3.x for .NET </b>

<pre>using System;
using System.Collections.Generic;
using Microsoft.Azure.Cosmos;

namespace ConsoleApp1
{
    class Program
    {
        static void Main(string[] args)
        {
            CosmosClient cosmosClient;                
            Database database;
            Container container;

            cosmosClient = new CosmosClient("AccountEndpoint=https://mlacosmos.documents.azure.com:443/;AccountKey=x73LhWDOWB4zDSoMUlqQUaJHWpB2cSURpnm1DyXvtl79hXlsuHNYJDIVggnnngE4O5mHnw8D9Uj5mcM22PGH4A==;");                 // Create a cosmosClient object by passing connection string
            database = cosmosClient.GetDatabase("db01");             // Using the cosmosClient object, create a database object (getting a refrence to the database)  
            container = database.GetContainer("Items");               // Access the container I need inside this database.   

            var sqlQueryText = "SELECT * FROM dbo.Product";          // Sql query
            QueryDefinition queryDefinition = new QueryDefinition(sqlQueryText);          // create object queryDefinition with the help of QueryDefinition class (pass query to a constructor)
            FeedIterator<Product> queryResultSetIterator = container.GetItemQueryIterator<Product>(queryDefinition);   // create object queryResultSetIterator (create a query result iterator)

            List<Product> redProducts = new List<Product>();                   // an empty list of the product object that I'm going to fetch


            while (queryResultSetIterator.HasMoreResults)  // as long as we have data to fetch =>
            {
                FeedResponse<Product> currentResultSet = queryResultSetIterator.ReadNextAsync().Result;  // => it is going to fetch the data =>
                foreach(Product product in currentResultSet)
                {
                    redProducts.Add(product);                                 // => add them to the result list =>
                    Console.WriteLine("\tRead {0}\n", product.ProductNumber); // => and also put the product console into the consol
                }

            }
        }
    }
}
</pre>

<pre> 
namespace ConsoleApp1
{
    internal class Product
    {

        public int ProductID { get; set; }
        
        public string Name { get; set;  }

        public string ProductNumber { get; set; }

        public Category Category { get; set; }

    }

    public class Category
    {
        public int CategoryId { get; set; }
    }

}

</pre>


<hr>


<b> Demo: Create a sample MongoDB database in MongoDB Atlas </b>
<p> MongoDB Atlas: Create free tier (M0 Sandbox). Click on three dots, load sample dataset. Define a database user. Under security, click on database access, click on add new user, and create a new user. Download Studio 3T mongoDB client  </p>

<pre> 
using MongoDB.Driver;
using System;

namespace MongoDBAPI
{
    class Program
    {
        static void Main(string[] args)
        {
            IMongoCollection<Company> companiesCollection;

            MongoClient client = new MongoClient("mongodb+srv://marcuslarsson:Britney123@cluster0-rmtx6.azure.mongodb.net/test?retryWrites=true&w=majority"); 

            // Create an instance of MongoClient object using MongoDB connection string to this constructure.

            var database = client.GetDatabase("sample_training"); // get a reference to the database that we are going to work with. 

            companiesCollection = database.GetCollection<Company>("companies"); //name of the collection

            var myCompanies = companiesCollection.Find<Company>(company => company.founded_year > 2000).Limit(100).ToList();


            foreach (var company in myCompanies)
            {
                Console.WriteLine($"{company.name} founded in { company.founded_year}.");
                    
            }

            Console.WriteLine("press a key to exit ...");
            Console.ReadKey();
        }
    }
}

</pre>

<pre>
using MongoDB.Bson;
using MongoDB.Bson.Serialization.Attributes;

namespace MongoDBAPI
{
    internal class Company
    {

        [BsonId]
        [BsonRepresentation(BsonType.ObjectId)]
        public string id { get; set; }

        public int founded_year { get; set; }

        public string name { get; set; }

        public string homepage_url { get; set; }
    }
}
</pre>

<hr>

<p> Demo: Provisioning a Cosmos DB Table API instance. </p>

<pre>
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Table;

namespace TableAPI
{
    class Program
    {
        static void Main(string[] args)
        {


            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=mlacosmosdb;AccountKey=3DUoTtcwo7whnUkawB7DuejVEL7HWkCwR3Y2erou891Caa6O0Fd2sQimMBPgrXAaCUDIA3DOwKTClRjvUzHhWw==;TableEndpoint=https://mlacosmosdb.table.cosmos.azure.com:443/;";


            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            CloudTableClient serviceClient = account.CreateCloudTableClient();

            CloudTable table = serviceClient.GetTableReference("people");

            var opperation = TableOperation.Retrieve<Person>("canada", "1");


            var jobResult = table.ExecuteAsync(opperation);


            var entity = jobResult.Result;
        }
    }
}

</pre>
