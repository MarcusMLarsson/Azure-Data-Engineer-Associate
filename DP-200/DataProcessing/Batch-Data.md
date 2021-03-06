<h1> Building Batch Data Processing Solutions in Microsoft Azure </h1>

<p> Batch data processing is where data is proccessed at a scheduled time. In other words, batch processing is the processing of data in a group or a batch. Data is collected, entered, processed and then the batch results are produced (Hadoop is for example focused on batch data processing). While batch processing can be carried out at any time, it is particularly suited to end-of-cycle processing, such as at the end of the business day etc.

<ul>
  <li><b>Batch processing</b>: Working with previously stored data (more tollerance for latency) </li>
<li><b>Stream processing</b>: Working with incoming data in real time.</li>
</ul>

<h3>Developing Batch Processing Solutions with Azure HDInsight </h3>
  <b> Hadoop </b>
<p> Hadoop is a platform for distributed storing and analyzing of very large data sets.  In other words, Hadoop is a framework that allows for the distributed processing of large data sets across clusters of computers using simple programming models. It is designed to scale up from single servers to thousands of machines, each offering local computation and storage. The notion of commodity hardware, means you dont have to pay for super computers
if you are going to spread the workload across enough nodes. For instance you can build a 
Hadoop cluster using rasp-berry pie. </p>

<b> Hadoop history </b> </p>
  In the past, when larger and larger quantities of data needed to be interegated,
businesses would simply write larger and larger checks to their database vendors of choice (Oracle,
IBM, Microsoft). However, in the early of 2000, companies like google were running into a wall. 
There vast quantity of data where simply to large to pump thrue a single database bottleneck.
To address this, the Google labs team developed an algorithm that allowed for their large database
calculations to be chopped up into smaller chunks, and mapped to many computers. They called this algorithm MapReduce. This algorithm were later used to develop an open source project called Hadoop, which allows applications to
run, using the MapReduce algorithm. Simply put, we are processing data in parallel rather than
serial. </p>
  

Hadoop has four main modules. The way these modules are woven together is what makes Hadoop so successful.
<ul>
  <li>Hadoop common </li>
  <li>HDFS </li>
  <li>MapReduce </li>
  <li>YARN </li> 
</ul>

  <img src="https://raw.githubusercontent.com/andkret/Cookbook/master/images/Hadoop-Ecosystem.jpg">
 <b> Hadoop common </b>
<p>
  The Hadoop common libraries and functions are working in the background. That's why I will not go further into them. They are mainly there to support Hadoop's modules. </p>
  
 <b> YARN </b>
<p> Consider YARN as the brain of your Hadoop Ecosystem. It performs all your processing activities by allocating resources and scheduling tasks. </p>
  
  
<b>MapReduce</b>
<p> MapReduce provides the logic of processing. MapReduce has two phases, a Map phase and a reduce phase. The Mappers job is to create or process the
input data. This is usually a file or a directory. This file is stored
on HDFS and is passed into the mapper function. The file is usually passed in line by line, into the
mapper function. The mapper processes this input data to create as few or as many output as needed.
The mappers output is then passed to the reduce phase. The reducers job is to process the data from
the mapper into something useful. Every single value from the mapper is passed into the reduce
function. The reducer will create new output values based on the input from the mapper. The new
output values from the reducer will be saved to HDFS. The technical name for this part is shuffle
and sort phase. Nodes can process data independently, and combine it together.
The cluster is made up of 10, 100 or even 1000 nodes that are connected by a network. A job is 
broken up into smaller part to be run on each node. The mapper works on the smaller parts. The magic
takes the mappers data from every node and brings it together on nodes all alround the cluster. The
reducer runs the node, and knows it has access to everything with the same key. </p>

<b> HDFS </b>
  
<ul>
<li> Hadoop Distributed File System is the core component or you can say, the backbone of Hadoop Ecosystem. </li>
<li>HDFS is the one, which makes it possible to store different types of large data sets (i.e. structured, unstructured and semi structured data). </li>
<li>HDFS creates a level of abstraction over the resources, from where we can see the whole HDFS as a single unit.
It helps us in storing our data across various nodes and maintaining the log file about the stored data (metadata).</li>
</ul>
  
<p>HDFS breaks larger files into smaller chunks (blocks). We get several benefits by breaking up the
terabit files into smaller blocks. When the mapper is operating on the terabite file, its actually
operating on a block and not the entire file. The terabite file is being worked at by several nodes
in the cluster all at once. The various nodes are just operating on different chunks. Once the mapper
is done, the magic takes over. All of the data in the terabite file is combined based on a key.
The reducer runs on different keys.</p> 
  
  
<b> Hadoop Eco System </b>
  
<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2016/10/HADOOP-ECOSYSTEM-Edureka.png">
  
<p> You use Apache Kafka to ingest data, and store the it in HDFS. You do the analytics with Apache Spark and as a backend for the display you store data in Apache HBase.

To have a working system you also need YARN for resource management. You also need Zookeeper, a configuration management service to use Kafka and HBase </p>
  
<b>Distributed storage</b>
<p>
You dont want to be limited by a single hard drive. If you have distributed 
storage you can just keep on adding more and more computers to your cluster. Hadoop is redundant,
if one of the computers is destroyed, Hadoop can handle that as you have backup data in other places
on you cluster. Hadoop was devloped originally by Yahoo! (they were building something called Nutch!)
using Google publically published papers on GFS and MapReduce. Hadoop was primarly driven by
Doug Cutting and Tom White in 2006, it's been evolving ever since. Hadoop was originally used for
batch processing. Now there are stuff built on top of Hadoop which makes it appropriate for
interactive queries aswell (not just for batch processing any more). </p>

<p>
HDFS (Hadoop version of GFS) is the system that allows us to distribute the storage of big data
across our cluster of computer. It makes all of the hard drives on our cluster to look like one 
giant file system. Not only that, it maintaince redundant copies of that data so if one of the 
computer get destroyed, it can recover from that automatically. That is the distributed data storage
piece of Hadoop. Sitting on top of HDFS we have YARN (Yet Another Resource Negotiator): YARN is were the data 
processing is starting to comes to play. YARN is basically the system that manages the resources
on your computing cluster, it what decides what gets to run tests, what nodes are available for 
extra work, which nodes are not available. </p>
<p>
On top of that is MapReduce: initially MapReduce and YARN was kind of the same thing, but got
split up. On top of MapReduce we have technologies like Pig: If you don't want to write JAVA or Python
MapReduce code, you can use Pig, which allows you to write simple scripts that looks alot like SQL.
Hive also sits ontop of MapReduce and solves a similar problem like Pig, but it's more directly
like a SQL database. Database, you can exectute SQL queries on that database. 
Apache Ambari: Sits ontop of everything, basically gives you a view of your cluster. 
Ambari is what Hortonworks uses, there are competing distributens of Hadoops (Hortonworks, Cloudera,
MapR).</p>

<b> Spark </b>
<p>
Spark is sitting at the same level of MapReduce (on top of Yarn), to run queries on your data. Spark is a processing engine that serves as a MapReduce alternative. Sparks goal is to give MapReduce's scale and fault tolerance faster via in-memory processing (rather just disk IO). Spark have API to Scala, Python, Java, R and SQL. If your not using Spark, you are pretty much stuck
with java. Microsoft designed HDinsight in conjunction with Hortonworks (the software company that came from the Apache Hadoop project). In january 2019, Hortonworks merged with Cloudera. Lower compute costs mean Apache Spark is moving to the forefront of big data analysis.  </p>

<img src="https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2016/10/Apache-Spark-Framework-Hadoop-Ecosystem-Edureka-1-528x230.png">

 | MapReduce      | Spark       |
| ------------- |:-------------:|
| Batch processing  | Batch and real-time (streaming) processing |
| Disk data processing    | In-memory data processing      |
| Java API | Scala, R, Python, SQL, JAva APIs       |
| Generally non-interactive  |Interactive emphasis        |
| HiveQL   |Spark SQL       |
| External ML Support (Mahout)  |Native MLlib support|  

  
  | Traditional RDBMS       | Hadoop      |
| ------------- |:-------------:|
| Structured data   | Unstructured (although you can project structure) |
| ACID    | CAP      |
| Lower data throughput, bt faster granular query performance | Higher data thrughput, bot slower granualr query perfromance       |
| Vertically scaled  |Horizontally Scaled        |
| OLTP   |OLAP       |
| SQL Server/Azure SQL Database are licensed and closed source  |(Mostly) free and open source|
  
  
<b> HDInsight </b>  
<p> Azure HDInsight is a managed, full-spectrum, open-source analytics service in the cloud for enterprises. You can use open-source frameworks such as Hadoop, Apache Spark, Apache Hive, LLAP, Apache Kafka, Apache Storm, R, and more. In other words, HDInsight is Microsofts hosted Apache Hadoop cluster environment. So the high level architecture 
is very similar to open soure Apache Hadoop. We got masisivley parallel processing, we got the same
concept under the hood in HDInsight that you would in any other cloud or on-premises Hadoop cluster.
Head Nodes, Worker Nodes, at the bottom we have decoupled storage (Data Lake Store, Azure Storage 
blobs). </p>
<p> HDInsight Cluster Types
  <ul>
    <li>The traditional Hadoop option (Batch query and analysis of HDFS stored data). </li>
<li>HBase (processing for large schmealess NoSQL data). </li>
<li>Interactive Query (In-memory caching for fast Hive queries). </li>
<li>Kafka: Distributed steaming data platform</li>
<li>ML Services: Predictive modeling and machine learning. </li>
<li>Spark: In-memory processing and interactive queries (substitute to MapReduce) </li>
<li>Apache Storm: Real-time event processing</li>
</ul>


<b> HDInsight is hosted Hadoop, and your using the native Hadoop tools, but they are being hosted
in an Azure frame </b> 
<p> Demo: In this demo we are going to create our first HDInsight cluster, we are going to create
an identity that will represent the HDInsight cluster. HDInsight is simply a cloud version of 
Hortonworks data platform (100% Apache Hadoop). Go to gpv2 storage account (Data Lake Gen2 File
System) where Blob Service usually are. Go to access control (IAM) and give our HDInsight permission.
Go add role assignment, use built in Storage Blob Data Contributor. Assign access to User 
assigned managed identity. Let's go to HDInsight tab and press add... Continue demo. </p>

<hr>
<b> Notes </b>
<p> Virtual Machine (VM): Operating systems are software that are able to control the physical
component of a computer. A VM is another type of software that allow us to run more operating systems
within an operating system. Examples are VirtualBox and vmware. </p>

<p> 
In memory processing: is an emerging technology for processing of data stored in an in-memory database.
Older systems has been based on disk storage but these are increasingly regarded as inadequate to meet
BI needs. Because stored data is accessed much more quickly when it is placed in RAM, in-memory 
processing allows data to be analysed in real time, enabling faster reporting. <p>
  
<p>
Everything in a computers memory, takes the form of the basic units called bits, or binary digits.
Each of these are stored in a memory cell, that can switch between two states (0 & 1). Files of 
programs consists of millions of these bits, all processed in the CPU (act as computers brains). As
the number of bits grows constantly, computer desginers face a constant struggle, between size, 
cost and speed. Computers have short term memory for immidiate tasks and long-term memory for more
permanent storage. When you run a program, the operating system allocates area within the short-term
memory. For example, when you press a key in word. Because program instructions must be processed
quickly and continously, all locations within the short-term memory can be accessed in any order (hence
the name Random Access Memory, RAM). The most common type of ram is Dynamic RAM (DRAM). The memory is 
called Dynamic because it only holds charges dynamically, before they leak away. Even it low latency,
is to slow for modern CPUs, so there is also a small high-speed internal memory cache (made from static
RAM). SRAM is the fastest memory and the most expensive. RAM and cache can only hold data as long
as they are powered. For data to remain while the device is turned off, it must be transfered to a long term storage device, which comes in three major types (Magnetic storage, ...)</p>

