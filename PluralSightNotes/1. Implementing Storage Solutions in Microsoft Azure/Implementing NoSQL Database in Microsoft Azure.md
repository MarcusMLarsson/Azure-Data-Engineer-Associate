<h1> Implementing NoSQL Database in Microsoft Azure </h1>

<h3> Introduction </h3>
<p> In this lession, we will</p>
<ul>
<i> <li> Learn Azure Cosmos DB</li>
<li>  Learn Azure Multimodel API</li>
<li> Azure Table Storage etc</li> </i>
</ul>

---

<h3> An Introduction to NoSQL Databases. </h3>
<ul>
<p> <b>  Managed NoSQL offeings by Azure </b> </p>
<li> Azure Storage (blob, file, queue, table)</li>
 <p> Can be used to store unstructured data in cheap storage. Is accessible from any where in the world over HTTP / HTTPS. </p>
<li> Azure Data Lake </li>
 <p> Uses Azure Storage under the hood </p>
<li> CosmosDB (previous called Document DB)</li>
 <p> Globally distributed, multimodel database. 
 <ul>
  <li> If you want to store data as JSON document use the SQL and MongoDB API.</li>
  <li> If your to store the data in key-value pairs use the Azure table API.</li>
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
  <li> JSON structure is normal.</li>
  <li> Scales better horizontally. </li>
  <li> NoSQL should not only be recommended to store non-relational data. NoSQL can store relational data aswell. </li>
 <li> Mainly about horizontal scalability, availability and price. </li>
</ul>


<ul>
<p> <b> Manage NoSQL offerings by Azure </b> </p>
 <li> IaaS (Infrastructure as a Servce): Provision VMs and install database engines of your choice. </li>
 <li> PaaS (Platform as a Service): Azure manages the underlying infrastructure for you. We will only talk about PaaS in this course. </li>
</ul>

<b> Demo </b>

<p> Start by provisioning Azure storage account. => More services => Storage => Storage Accounts. Account kind: StorageV2 are used normally. Locally redundant storage is the cheapest one. Cool are for archiving. Choose hot. After creating you can choose 4 different storage types under the storage account umbrella. </p>

<p> Let's provision a CosmosDB. More services => Databases => CosmosDB. Leave API as core SQL</p>

<b> Azure Table Storage </b> 
<p> Ideal for storing structured non-relation data. Imagen you want to save information for a group of people. You know this people will have some attributes which are similar to each other, for example first name, last name, email. Azure table storage is a greate option for this kind of data. If you however have a few JSON files which haven nothing incommon, you should store them in a different storage account which is better suited for unstructured data (e.g. Azure Blob Storage). Azure Table storage is not good with complex joins. </p>
<ul>
 
 <p> To be able to use Azure Table Storage, you first need an Azure Storage Account. Inside this storage account you can create a few tables (example Users and Posts). Next you can store your data inside these tables. Each row in the tables are referred to as an entity. These entities can have multiple properties, name, email, phonenumber etc. 
  
 <b> Azure Blog Storage </b>
 <p> Blob Storage is optimized to store massive amount of unstructured data in the cloud, servering documents directly to the browser. Blob Storage is widely used for data back-up and restore. Many Azure services (for example Azure SQL Database) are storing their backup in Azure Blob Storage. Audio and video files can be uploaded to Azure Blob storage. The service can also be used to store data for analysis. Azure Blob Storage can automatically scale when the demand increases.</p>
 
 <b> Azure Queue Storage </b> 
 <p> Azure queue storage is a service for storing large numbers of messages. You can access the messages via authenticated calls using HTTP or HTTPs. E.g. passing messages from a web role to a worker role. Imagen you have a website that converts bitmap images into jpg. Users can upload their files and they will get the jpg image. Converting bitmap img to jpg can be time consuming. And you might not be able to convert 1000 of files at the same time. What you can do is per each bit map conversion request you add a message to your Azure queue storage. You have your converter worker role read these messages and do the conversions. </p>
 
 <b> Azure Files </b>
 <p> Azure files offers fully managed file shares in the cloud that are accessible via the industry standard server message block (SMB) protocol. Most people use shared dirves at work using an on-premise file server. Your network administrator is mapping those drives to your machine and than you can simply drag and drop files. <b> Azure files can be used to replace on-premises file  servers </b>. If you are using legacy applications which uses shared files you can lift and shift them to the cloud.  </p>
 
 <b> Securing storage accounts. </b>
<ul>
 <li><b> Management security</b> </li> <p> Who can create a storage account, who can delete tables, blobs or queues within the storage?
Operations that affect the storage account itself. RBAC (roled base access control) roles for storage (owner role, contributor role, reader) </p>
 <li><b> Data access secuirty </b> </li> <p> Who can access the blob data, or who can update the data. Access to storage account data is blocked by default. You have two main method to grant access, storage account keys (grants complete access) and shared access signature (SAS), which gives the permission required for a <b> limited amount of time </b>. You can even limit by IP, so if you receive an correct request from wrong IP, it will be rejected. You can also enforce HTTPS.</p>
  <li><b> Encryption for data in transit </b> </li>
 <p> You can use both HTTP and HTTPS when calling the REST APIs or accessing objects in storage. It's recommended to always use HTTPS.
 <li><b> Encryption for data at rest </b> </li>
 <p> Data at rest is refered to the data that is stored in the storage account. There are two methods to encrypt this data. The first one is storage service encryption (SSE), this option is able for all storage accounts and can not be disables. You can also use client side encryption. You can programmatically encrypt the data in a client application then send it across the wire (can be done using the storage account SDK). </p>
  <li><b> Auditing and monitoring access </b> </li> <p> Who accessed your blob storage, and at what time? 
You can enable Azure Storage Analytics to log the authentication method used by clients. This data will be saved in Azure montior logs and can be queried </p> 
 <li><b> CORS (Cross-Origin Resource Sharing) for browser clients </b>  </li>
 <p> CORS is a mechanism that uses additional HTTP headers to tell browsers to give a web application running at one origin, access to selected resources from a different origin. You can allow origins, methods and headers, when calling the Azure Table Storage API that return JSON data to be processed by the JavaScript client. </p>
 </ul>
 
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
<p> There are two different options (desktop version and the online version) to work with Azure Storage Explorer. You can download the desktop version of Azure Storage Explorer from Microsoft's website. After that, you can view and edit blob, queues, tables and files. On top of that, you will be able to work with your Cosmos DB Storage. You can also obtain shared access signatures (SAS keys). Also, in the Azure Portal, you have access to the online version of the Storage Explorer (preview). Here I have the option to create a blob, file, queue or tables storage. Add a new entity to the table. RowKey and PartionKey are created automatically. Remember, that RowKey, PartionKey and TIMESTAMP are three properties which are system properties and mandatory for every entity. The TIMESTAMP will be managed by Azure, so you don't need to worry about that. However, it's your responsibility to provide the value for PartionKey and RowKey. It's also your responsibility to choose the right PartitionKey so your data is divided into appropriate size. Put Sweden for the PartionKey and for the RowKey I'm going to put 1. Now when the system properties are defined, press add property. Add Name: Marcus, Email: mla. Press insert  </p>

<b> Demo: Working with Azure Table Storage .NET SDK (Software development kit)</b>
<p><a href="https://github.com/Azure/azure-sdk-for-net">Azure SDK for .NET </a></p>
<p><a href="https://github.com/Azure/azure-sdk-for-python"> Azure SDK for Python </a></p>
 <p> We are going to write a small .NET application which connects to this storage account and reads an entity from our existing table. First, let's take a look at our data. => Storage Explorer => Tables =>.. Start a console application in Visual Studio. Download WindowsAzure.Storage NuGet package. Grab the connection string under Access keys.    </p>
 
<pre>using Microsoft.WindowsAzure.Storage;                  <i> //importing package from SDK </i>
using Microsoft.WindowsAzure.Storage.Table;             

namespace AzureStorageSDK                                   <i> //namespaces are used to organize classes </i>             
{
    class Program                                           <i> //A class is a blueprint for creating objects </i> 
    {                                                            
      static void Main(string[] args)    <i> // Void returns nothing, static means that there's only one (don't belong to an object) </i>                         
        {
            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=namestorageaccount;AccountKey=lYMyjeY0YFvEKIdy/IRJyLwxKQWTEi7y0VZFLGV9rHVxDDcKfGKmF9uM4YGOTXAhNRj+g5SCEXN6NXyxDBRGEA==;EndpointSuffix=core.windows.net";

            <i> //A connection string includes the authorization information required for your application to access data in an Azure   Storage account </i> 

            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);
            
            <i> //CloudStorageAccount is a class, account is an object, storageConnectingString represents our storage credentials </i>
            <i> // Parse is a method which parses a connection string and returns a CloudStorageAccount created from the connectiong string. </i>
            <i> // <a href ="https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.storage.cloudstorageaccount?view=azure-dotnet"> CloudStorageAccount </a> </i>

            CloudTableClient serviceClient = account.CreateCloudTableClient();       
            <i> //CloudTableClient is a class, serviceClient is an object </i>


            CloudTable table = serviceClient.GetTableReference("TableTest");

            var opperation = TableOperation.Retrieve<TableTest>("Sweden", "1");

            var jobResult = table.ExecuteAsync(opperation);

            var entity = jobResult.Result;
        }
    }
}
</pre>

<pre> using Microsoft.WindowsAzure.Storage.Table;

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

        /* */
        public string Phone { get; set; }
    }
}</pre>
 
 
 <b> Azure Cosmos DB Overview </b>
 <ul>
 <li> Global distribution & multi-homing </li>
 <li> Consistency levels </li>
 <li> Auto-expire using time-to-live (TTL) </li>
  <li> Data partitioning & best practices </li>
 </ul>
 
 <b> Cosmos DB Concepts - Global Distribution and Multi-homing </b>
 <p> Multi-homing APIs </p> 
 <ul>
 <li> Your application is aware of the nearest region and can send requests to that region </li>
 <li> Nearest region is identified without any configuration changes. </li>
 <li> When a new region is added or removed, the connection string stays the same. </li>
 </ul> 
 <br>
<p> Imagine you have two regions for your Cosmos DB account, one instance in West US and another instance in East US. You have created two versions of your web application and deployed on to an app service in West US and another app service in the East US region so your users can experience the least amount of latency. Now let's see what happends when there is a request for your application. You must probably have a traffic manager accepting the requests from the clients. The traffic managers knows the location of the client. In this case, the request is originated from Los Angeles, so the traffic manager is going to redirect the request to the app service located in the West US region, and my app service is using a connection string to connect to the Cosmos DB. So the question is, how my app service knows to which instance of Cosmos DB it should connect to; West US or East US? Because we don't have different connection strings for West US Cosmos DB and East US Cosmos DB, the multi-homing API sovles this problem. The multi-homing API is going to figure out which instance of Cosmos DB is closest to my app service and redirect the data request to that instance, and this is the idea behind the multi-homing API </p>


 <b> Time-to-live</b>
 <p> With time-to-live (TTL) you can set an expire date on some of your objects saved into the database. You don't need to clean up your database and delete when the time has come. You can set the expiry time on Cosmos DB data items; the setting is called TTL and is set as seconds. Cosmos DB will automatically remove the items after this time period, since the last modififed time. </p>
 
<b> Database Consistency</b>
<p> Imagen you have a distributed database. One replica exist  in West US, and the other replica exists in East US, and there is a global replication going on between these two. So every 5 seconds, the data in West US will be replicated to East US. This database holds information of a few bank clients, and the information we are interest in is the credit score of these clients. Let's say credit score goes from 750 to 700 for on customer in West US database. 
<pre>UPDATE History Set
CreditScore = 750
WHERE ID = 10 </pre>

Now someone in the East US need to access the credit score of the customer updated in West US (id = 10). So he runs the query. 
<pre>query SELECT CreditScore FROM History,
WHERE ID = 10 </pre>

What score do the observer get? 700 or 750? The observer should not see the old credit score (lag 5 second). This is the concept around data consistency. Relational Databases make sure you always get the consistent version of the data, even if you have to wait for some time. Azure Cosmos DB gives the option to add consistency to your database. 
</p>
 
 
 <b> Cosmos DB Concepts - Multi-writes and Consistent Prefix Reads </b>
 
<ul>
 <li> Data consistency versus data availability & latency </li>
 <li> Most distributed databases ask you to choose between the two extreme consistency levels: strong and eventual consistency. Strong means you always see the latest version of the data, even if you have to wait for a few milliseconds or seconds. Eventual consistency, meaning, the database enginge doesn't guarantee that you see the latest data, but at the same time, the data, is returned very quickly. </li>
 <li> Azure Cosmos DB offers 5 consistency levels to choose from, including the 2 extremes. </li>
 <li> Strong, bounded staleness, session, consistent prefix, eventual</li>
 </ul>
 <br>
 
 <p> Imagine I have a record in my Cosmos DB database. This is a person record and has five properties. givenname, lastname, email, phone, spouse. My Cosmos DB is distributed to East-US and West-US region. At 10 AM my East-US replica is going to update the email address to john@test.com. Two mintues later, the West-US replica goes ahead and updates the phone number. So far, I have two distinguished writes to the same record. At 10:04 AM., my observer queries my Cosmos DB instance for this record, and let's say this database instance guarantees consistent prefix rates. Now let's see which version of the data in the database this observer will se. So is my observer going to see only the first update, meaning, the email address? Or is he going to see both updates side by side? So having in mind that this database guarantees consistent prefix of the list, it is okey for my observer to see either email, the new email, and the new phone, or none of them. So you might ask, what is not okay for this observer to see having in mind that we have consistent prefix consistency level guaranteed? It is not okay to see the second update, but not the first update.   </p>
 
 <b> Cosmos DB Concepts - Consistency Levels (Strong, Session, Eventual, and Others) </b>
 
 <p> Strong, Bounded Staleness, Session, Consistent Prefix, Eventual</p>
 <p> Moving from left to right you get higher latency and throughput put at the price of weaker consistency. Strong always guarantes consistency level. For the bounded staleness you specify a window of staleness, and this windows is defined in time and number of operations. For example, you are going to say, I want my Window of staleness to be 10 minutes and for 1000 operations. So any observer accessing Cosmos DB outside this staleness Windows is going to see a strong consistency. For the observers accessing Cosmos DB within this staleness window, they are guaranteed only consistent prefix consistency level, meaning they are guaranteed to see in order updates, but not necessarily the latest and most consistent version of the data. Session consistency level is in the middle ground. It's the default consistency level when you are povisioning a new instance of Cosmos DB. Same as bounded staleness, you are going to have two different consistnecy level, but instead of a staleness window, you are dealing with a session. So if you observer is accessing Cosmos DB within the same session that writes data, they are going to see a strong consistency; however for other obsvers accessing Cosmos DB from other sessions, they are going to only see consistent prefix, meaning they are going to see in order writes only. For consistent Prefix the only thing Cosmos DB is guaranteeing is that you observer is always going to see in the correct order of updates. If they see update N, they are going to see all the ones before as well, but does not guarantee N is the latest version. Finally we have the Eventual consistency level. This is the weakest consistency level. You might see out of order updates.   </p>
  
 <b> Cosmos DB Concepts - Data Partitioning </b>
 
 <p> Databases and Containers: An Azure Cosmos database is a unit of management for a set of containers. A single database consist of a set of schema-agnostic container. The data you store inside containers can be partioned based on their partition key. A logical partition consists of a set of items that have the same partition key. Data that's added to the container is automatically partitioned across as set of logical partitions. Logical partitions are mapped to physical partitions that are distributed among several machines. Throughput provisioned for a container is divided evenly among physical partations. </p>
 
 <p> Don't pick an partition key that result in "hot spots" within your applications. In other words, choose a partition key that has a wide range of values, so your data is evenly spread across logical partitions. If you are saving data about people in their cities, chosing city as the partition key might be a good idea because this way you make sure your data is almost spread evenly among different logical partitions if the cities you are choosing have almost the same amount of population. For partition keys, try to use properties that appear frequently as a filter in queries; including the partition key in the filter predicate improves query performance.  A single logical partition has a limit of 10 GB of storage </p>
 
 <p> A partition key can be used by Azure Cosmos DB to divide my data into logical partitions. These logical partitions later will be mapped to physical partition and will be saved onto different machines around the globe.    </p>
 
 <b> Cosmos DB APIs and Security </b>
 <ul>
 <li> SQL API </li>
  <li> MongoDB API</li>
  <li> Table API </li>
  <li> Cassandra API</li>
  <li> Gremlin API</li>
 </ul>
 <br>
 
 <b> Security </b>
 <ul>
 <li> RBAC (Roll based access control) to grant access to users, groups or applications. </li>
 <li> Use firewall to limit clients who can access Cosmos DB </li>
 <li> Deploy Cosmos DB into a VNet & use NSGs: Azure Cosmos DB can be integrated with a virtual network. This way, you can use network security groups to control inbound and outbound traffic for your Cosmos DB </li>
 <li> CORS (Cross-origin resource control) can be whitelisted for Azure Cosmos DB as well. So if you have a client-side application which is directly calling Cosmos DB APIs to get data back, you can whitelist those applications in Azure Cosmos DB so those requests can be made from the browser.  </li>
 <li> Read-only and read-write keys </li>
</ul>
<br>

 <b> Demo: Provisioning a new Cosmos DB instance, Containers, and TTL </b>
 <p> More Services => Cosmos Db. Overview => Add container (multiple options). Database is the management unit for a group of containers. You have the option to create a new database or use an existing database within this Azure Cosmos DB account. Name the container People and /City as partinione key. Add a new item (under people). Add to JSON file. When you click save, "_rid", "_self", "_etag":, "_attachments", "_ts" are added automatically.</p>
   
 <b> Demo: Cosmos DB Security </b>
 <p> => Keys 
If I only need my clients to see the data, not update it I give them Read-only keys, not Read-write keys. Under fiewall and virtual networks I can whitelist by selecting selected networks. CORS (cross-origin resourcesharing (CORS) is an HTTP feture that enables a web application running under one domain to acces resource in another domain.</p>
 ---
 
 <b> Notes </b>
 
 <b> REST api </b>
 
 <b> Latency </b>
 <p> Latency is a networking term to describe the total time it takes a data packet to travel from one node to another.  </p>
 
 <p> data latency is the time between the creation of data in a source system and the exact time at which the same data is available for end users on the business intelligence platform.</p>
 
 
 <b> Working with Azure Cosmos DB - SQL (Core) API </b>
 
 <p> Each Cosmos API has its own terminology for the container concepts. You might expect Azure Cosmos DB SQL API to support the SQL syntax, and you are correct. We are going to take a look at a few SQL queries, which you can use to work with your data in Cosmos DB. After that, we are going to talk about Azure Cosmos DB .NET SDK. We will see which NuGet Packages you need to install to be able to use the latest and greatest version of the Azure Cosmos DB .NET SDK.  </p>
 
 <p> Review: An Azure Cosmos container is the unit of scalability for throughput and storage. The container items and the throughput are distributed across a set of logical partitions. Logical partitions are created based on partition keys. An Azure Cosmos container can scale elastically. </p> 
 
 <ul>
 <li> SQL API: Collection</li>
 <li> Table API: Table</li>
 <li> MongoDB API: Collection</li>
 <li> Cassandra API: Table</li>
 <li> Gremlin API: Graph</li>
 </ul>
 
 <p> Use Data Explorer: Azure Cosmos DB SQL API supports querying JSON items using SQL.
<pre>
"firstname": "Marcus",
"lastname": "Larsson,
"email": "mla@ocean.se",
"address": { 
    "streetAdress": "gatan",
    "city": "Gothenburg",
    "country": "Sweden",
},
"phone": "+46703 ....."
</pre>

<pre>
SELECT *
FROM People as p
WHERE p.givenname = "John"
</pre>

<p> You can also query nested properties </p>
<pre>
SELECT *
FROM People as p
WHERE p.address.city = "Gothenburg"
</pre>

<p> I can select fields of of my itmems into new JSON objects</p>

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

<a href ="https://docs.microsoft.com/en-us/azure/cosmos-db/import-data"> Link </a>

<a href ="https://github.com/azure/azure-documentdb-datamigrationtool"> GitHub </a>

<a href = "https://aka.ms/csdmtool"> pre-compiled binary </a>

<b> Demo: Working with the Azure Cosmos DB Client Library 3.x for .NET </b>

<p> </p>

<h3> notes </h3>

---

<b> Instance </b>
<p> In object-oriented programming (OOP) an "instance" is synonymous with "object". The creation of an instance is called instantiation </p> 

<b> Azure Container Instance </b>
<p> Azure Container Instances is a service that enables a developer to deploy containers on the Microsoft Azure public cloud without having to provision or manage any underlying infrastructure. </p>

<b> Provisioning </b>
<p> Provisioning is the enterprise-wide configuration, deployment and management of multiple types of IT system resources. The service -- which supports both Linux and Windows containers -- eliminates the need for a developer to provision virtual machines, or implement a container orchestration platform, such as Kubernetes, to deploy and run containers. Instead, with Azure Container Instances (ACI), an organization can spin up a new container via the Azure portal or command-line interface (CLI), and Microsoft automatically provisions and scales the underlying compute resources. </p> 


<b> Wide column store </b>
<p> A wide column store is a type of NoSQL database. It uses tables, rows, and columns, but unlike a relational database, the names and format of the columns can vary from row to row in the same table. A wide column store can be interpreted as a two-dimensional key-value store. </p>

<b> HTTP Headers </b>
<p> When you type a url in your address bar, your browser sends an HTTP request and it may look like this </p>
<pre> GET /tutorials/other/top-20-mysql-best-practices/ HTTP/1.1
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
