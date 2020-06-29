
<pre> Which Cosmos DB APIs offer a wide-column NoSQL Database?</pre>
<ul>
	<li><b>Table and Cassandra API</b></li>
	<li> SQL (Core) API</li>
	<li> Gremlin API </li>
	<li> MongoDB API </li>
</ul>

<pre> Which generation of Azure Data LAke Storage is cheaper and why?</pre>
<ul>
	<li>Gen1 because it is based on the cheap Azure Blobs</li>
  <li> <b>Gen2 because it is based on the cheap Azure Blobs </b></li>
	<li> Gen1 because it is using the HDFS</li>
	<li> Gen2 because it does not implement the hierarchical directory structure </li>
</ul>



<pre> Which managed NoSQL offering by Azure is a good option for big data analytics with Hadoop</pre>
<ul>
	<li>Azure Cosmos DB Gremlin API</li>
  <li> <b>GAzure Data Lake Storage</b></li>
	<li>Azure Cosmos DB Table API</li>
	<li> Azure Table Storage </li>
</ul>



<pre> How many custom properties can be added to an Azure Table Storage entity</pre>
<ul>
  <li> <b>252 properties </b></li>
  <li> Three properties </li>
	<li> 255 properties</li>
	<li> Unlimited number of properties can be assigned</li>
</ul>


<pre> You already have provisioned your Cosmos DB in the East-US region. Now you have custoemrs in West-US. What should you do?</pre>
<ul>
  <li> Provision a new instance of Cosmos DB with West-US and East-US regions and transfer your data</li>
  <li> Create a new instance in West-US and setup replication between your seperate instances </li>
	<li> <b>Simply add West-US as a new region to your Cosmos DB Instance </b></li>
	<li> No action is required. Azure Cosmos DB will automatically add West-US as a new region</li>
</ul>

<pre> You are creating a new Cosmos DB project. Which Cosmos DB API is recommended?</pre>
<ul>
  <li> SQL or Table API</li>
  <li> Cassandra or MongoDB API </li>
	<li> <The SQL (core) API</li>
	<li> <b> SQL or Gremlin API based on your scenario. </b></li>
</ul>


<pre> You chose a wrong PartitionKey for one of your migrated collections. Waht can be done after migration?</pre>
<ul>
  <li> Simply update your collections with the new PartitionKey</li>
  <li> Simply add a new region to your Cosmos DB instance </li>
	<li> <b>You need to re-create your colelctions with the new PartitionKey and repeat the migration </b></li>
	<li> Azure Cosmos DB will automatically adjust the PartitionKey</li>
</ul>


<pre> Why would you migrate from Azure Table Storage to Azure Cosmos DB Table API?</pre>
<ul>
  <li> Azure Table Storage does not offer any indexing on any property</li>
  <li> <b>To take advantage of better SLAs and other premium features such as secondary indexing </b></li>
	<li>The Table SDK has interface limitations</li>
	<li> Azure Table Storage has storage size limitations which Cosmos DB does not have</li>
</ul>


<pre> Which Cosmos DB API can be used to persist a graph?</pre>
<ul>
	<li> <b>Gremlin API</b></li>
  <li> Core (SQL) API</li>
	<li>Cassandra API</li>
	<li> Table API</li>
</ul>

<pre> Model the following sentence into a property graph: John uses a silver laptop</pre>
<ul>
	<li> Person and laptop are edges, uses is the vertex, john and silver are properties</li>
  <li> John and laptop are vertices, uses is the edge, silver is a property</li>
	<li> <b>Person and laptop are vertices, uses is the edge, John and silver are properties </b></li>
	<li> John and laptop are vertices, uses and silver are properties.</li>
</ul>

<pre> You are looking for a cheap, easy o use wide-column NoSQL database in Azure. Premium SLA is not too important for you. Which of the following is a good option?</pre>
<ul>
	<li> <b>Azure Table Storage </b></li>
  <li> Azure Cosmos DB Cassandra API </li>
	<li> Azure Cosmos DB Table API</li>
	<li> Azure Data Lake Storage</li>
</ul>



<pre> You need to auto-expire some items in your Cosmos DB afer 12 hours. What is the easiest method to do it?</pre>
<ul>
	<li> <b>Setup TTL (time-to-live) at the item level </b></li>
  <li> Create a scheduled Azure Function to cleanup Cosmos DB items </li>
	<li> Setup TTL (time-to-live) at the container level</li>
	<li> Create an Azure Automation runbook to cleanup Cosmos DB Items</li>
</ul>




<pre> Which concistency level provides the lowest latency</pre>
<ul>
	<li> Session</li>
  <li> Bounded Staleness </li>
	<li> <b>Eventual </b></li>
	<li> Strong</li>
</ul>



<pre> How do you prevent creation of hot partitions?</pre>
<ul>
	<li> By configuring the multi-homing API</li>
  <li> By choosing the right document id </li>
	<li> By choosing the right timestamp</li>
	<li> <b>By choosing the right PartitionKey </b></li>
</ul>



<pre> Which of the following steps is a MongoDB API post-migration step</pre>
<ul>
	<li> Estimate the throughput needed for your workload</li>
  <li> Create an Azure Cosmos DB Account </li>
	<li> Choose the right PartitionKey for every collection</li>
	<li><b>Configure database consistency level</b></li>
</ul>



<pre> You have underestimated the throughput for your migrated collections. What can be done after migration?</pre>
<ul>
	<li> Simply add a new region to your Cosmos DB instance</li>
  <li> Azure Cosmos DB will automatically adjust the throughput</li>
	<li> <b>Simply assing more throughput to the database or the collection </b></li>
	<li> You need to re-create your collections with the new throughput ad repeat the migration</li>
</ul>
