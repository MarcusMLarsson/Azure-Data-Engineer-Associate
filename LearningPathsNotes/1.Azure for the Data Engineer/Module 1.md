<h1> Module 1 </h1>

<h3> Introduction </h3>
<ul>
<li> Evolving data systems generates exponential growth in data, which is changing the landscape for data professionals. </li>
<li> To generate value, anyone working with data needs to understand how the data landscape has changed and how roles and technologies are evolving. </li>
<li> Azure provides a rich set of data technologies. As data formats evolve, Microsoft releases new technologies to the Azure platform. </li>
</ul>

<h3> Structured or Unstructured</h3>
<ul>
<p> <b>  Structured Data  </b> </p>
<li> Relational databases contains structured data. </li>
<li> Store data distributed across multiple tables, which is connected by relations </li>
<li> You need to know ahead of time how the data is going to look like. </li>
<li> A schema needs to exist. </li> 
<li> Designed decision are made when the database is first formed. </li> 
<li> Changing data down the track can be difficult. </li>
<li> Horizontal scaling is hard </li>
<li> e.g. Azure SQL Database, Azure SQL Data Warehouse </li>
</ul>

<ul>
<p> <b> Unstructured Data </b> </p>
<li> NoSQL databases contains unstructured or semistructured data. </li>
<li> Dynamic schemas </li>
<li> Fits better with agile development </li>
<li> For MongoDB, tables are collections, rows in tables are documents </li>
<li> Scales horizontally (Sharding) </li>
<li> Azure Cosmos DB, Azure HDInsight, MongoDB </li>
</ul>

<p> Schema: All columns have to follow the Schema in relation database. 
A schema is a collection of database tables (objects) associated
with one particular database username. 
This username is the so called the schema owner. Based on a user's privileges within the database, the user has control over 
objects that are created, manipulated, and deleted. </p>

<h3> Compliance </h3>
Data systems should be complient with:

<p> <b> GDPR (General Data Protection Regulation) </b> </p>
<ul>
<li> Applies for any company doing business in EU </li>
<li> Requried to lay out what data is collected and ask for consent</li>
<li> Data has to be protected when stored </li>
<li> Access data on demand or delete on request </li>
</ul>

<p> <b> PCI DSS (Payment Card Industry Data Security Standard) </b> </p>
<ul>
<li> Developed to encourage cardholder data security </li>
<li> Organisations that handle card payment must comply or risk financial penalties </li>
<li> Launched in 2004, result of collaboration between American Express, Mastercard, Visa, JCV, Discover</li>
</ul>

<h3> On-premises Environemnt </h3>
<ul>
<p> On prem environment requires </p>
<li> Physical equipment, Physical servers </li> 
<li> Network infrastructure </li>
<li> Storage </li>
<li> Power, cooling and periodic maintenance by qualified personnel. </li>
<li> A server needs at least one operating system installed. </li>
</ul>

<b> Maintenance </b>
<p>On-premis systems require maintenance for the hardware, firmware (software to perform specific task on hardware), drivers, BIOS (basic input/output system), operating system
software, and antivirus software. </p>

<b> Scalability </b>
<p> To scale on-premis server horizontally, server administrators adds another server node to a cluster.
Clustering uses either a hardware load balancer or a software load balancer to distribute 
incomming network requests to a node of the cluster A limitation of server clustering is that the hardware for each server in the cluster
must be identical. When the server cluster reaches maximum capacity, a server administrator
must replace or upgrade each node in the cluster. </p>

<b> Availability </b>
<p> High-availability systems must be available most of the time. 
Service-level agreements (SLAs) specify your organization's availability expecations.

System uptime can be expressed as three nines, four nines and five nines.
These expressions indicate system uptimes of 99.9 percent, 99.99 percent or 99.999 percent.
For on-premises servers, the more uptime the SLA requires, the higher cost.
To calculate system uptime in terms of hours, 
multpliy these percentages by number of hours in a year (8760) </p>
<ul>
<li> 99.9%, uptime: 8,751.24, downtime: 8.76h </li>
<li>99.99% uptime: 8,759.12 downtime: 0.88h </li>
<li>99.999% uptime: 8,759.91 downtime: 0.09h </li>
</ul>

<b> Support </b>
<p> Hundred of vendors sell physical server hardware. Server admins might need to know different platforms
Might be hard to find server admin to hire. </p>

<b> Multilingual support </b>
<p> Multilingual support might be difficult and expensive for On-premis SQL Server system. </p>

<b> Total cost of ownership (TCO) </b>
<p> Total cost of ownership (TCO) describes the final cost of owning a given technology.
Total cost of ownership for a on-premises systems includes cost for </p>
<ul>
<li> Hardware </li>
<li>Software licensing </li>
<li>Labor (installtion, upgrades, maintenance) </li>
<li>Datacenter overhead (power, telecommunications, building, heating and cooling) </li>
</ul>

<p>
Normally difficult to aling on-premis expenses with actual usage. Organizations buy servers that have extra 
capacity so they can accomodate future growth. Excess capacity is to be expected.
When an on-premises server is at maximum capacity, even an incremental increase in resource demand will require the purchase of more hardware. </p>

<p> Costs for on-premis server systems are often capitalized while cost for cloud is expensed. </p>

<h3> Cloud Environemnt </h3>
<p> Cloud environments require no capital investment. Pays only for what is used. 
Moving servers and services to the cloud also reduces operational costs.
Storage types include Azure Blob storage, Azure Files storage and Azure Disk storage. </p>

<b> Maintenance </b>
<p> Microsoft manages physical hardware, computer networking, firewalls and network security
datacenter fault tolerance, compliance, physical security of the buildings. </p>

<b> Scalability </b>
<p> Scalability in the cloud can be as simple as a mouse click. Scalability in the cloud
is typically measured in compute units. </p>

<b> Availaiblity </b>
<p> Many services uses SLAs (service level agreements) to ensure that customers know the capabilities. </p>

<b> Support </b>
<p> When Microsoft updates a proudct, the update applies to all consumer of the product. </p>

<b> Multilingual support </b>
<p> Cloud system often store data as a JSON file that includes the language code identifier (LCID) </p>

<b> Total cost of ownership </b>
<p> Track costs by subscriptions. A subscription can be based on usage that's measured in compute
units, hours, or transactions. The cost includes hardware, software, disk storage and labor.
Due to economices of scale, on-premises system can rarely compete with the cloud
in terms of the measurement of the service usage. </p>

<b> Lift and shift </b>
<p> When moving to the cloud, many customers migrate from physical or virtualized on-premises servers
to Azure Virtual Machines. This strategy is known as lift and shift. 
Server adminst lift and shift an application from physical environment to Azure Virtual Machines. </p>


<h3> Check Your knowledge </h3>
1. Which data processing framework will a data engineer use to ingest data onto
cloud data platforms in Azure
<pre> Online transaction processing (OLTP)
Extract, transform, and load (ETL) 
EXTRACT, LOAD, AND TRANSFORM (ELT) </pre>

2. The schema of what data type can be defined at query time?
<pre> Structured data
Azure Cosmos DB
UNSTRUCTURED DATA </pre>
 
3. Duplicating customer content for redundancy and meeting service-level agreements (SLAs) in Azure 
meets which cloud technical requirement?
<pre>Maintainability
HIGH AVAILABILITY
Multilingual support</pre>
