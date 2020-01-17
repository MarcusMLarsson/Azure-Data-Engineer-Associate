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
