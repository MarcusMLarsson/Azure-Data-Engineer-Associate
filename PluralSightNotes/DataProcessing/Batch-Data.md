<h1> Building Batch Data Processing Solutions in Microsoft Azure </h1>

<p> <b>The Four V's of Big Data </b>
<ul> 
  <li>Volume (the flow of data, size matrix like Peta bites or Exa bites) </li>
<li>Velocity (Processing frequency, what is your tollerance for latency)</li>
<li> Data Variety (is your data structured, semi-structured or unstructured)</li>
<li>Veraciy (Data trustworthiness, Noise, bias). </li></ul> </p>

<p> Structured data (SQL table, data is fully modeled, each entity (table) is sorted into a number
of columns, and relationships among tables are explicitly defined.
Semi-structured data (JSON, XML), JSON is same as key value pair, for XML you have the possibility
for a schema. Unstructured data (CSV, PNG, EXE (blob)). </p>

<p> For a Data Warehouse, the datas purpose is defined (structured and highly transformed). For a
Data Lake the datas purpose is not yet determined. 
<ul> 
<li> ETL (Extract, transform load. Data is transformed in flight between source and destination. Does not scale particulary well.</li> 
<li> ELT (Extract, load, transform). Data is transformed after it is extracted (Azure usually uses ELT as its a great fit
  for the cloud given limitless compute and storage resources). </li>
</ul>

<table>
<tr>
  <th> Batch processing </th> <th>Working with 
previously stored data (more tollerance for latency)</th></tr>
<tr>
   <th> Stream processing </th> <th> Working with incoming
data in real time.</th></tr>
<tr>
   <th>Data processing </th> <th>Situationg data into a usable format. </th></tr>
<tr>
   <th>Data analysis </th> <th>Asking questions of the prepared data </th></tr>
</table>




| Azure SQL Database       | Azure SQL Data Warehouse      |
| ------------- |:-------------:|
| OLTP (Online transaction processing)/CRUD (CREATE READ UPDATE DELETE)    | OLAP(Online analytical processing)/querying and reporting  |
| SMP    |  MPP      |
| Vertical scale | Horizontal scale      |
| No polybase | Polybase       |




<p> To make a storage account a (Enable the hierachical namespace) a datalake storage gen2 account.
Notice under services, instead of Blob Storage its now called Data Lake Gen2 file system. So from
now on this storage account is going to be a datalkae store with HDFS compatible file systems. Select
that service and collect a file system. If we go into the file system we get a prompt that let's use
Azure Storage Explorer. </p>

<p> PolyBase: is a Microsoft technology to open up the ability of Azure SQL Data Warehouse to access 
external data while still giving you the ability to use transct-SQL. PolyBase means you can get
data from different source like Azure Blob storage, Azure Data Lake Storage (Hadoop). You can be in
your data warehouse and you can create an external table which pulls data from for example a
Hadoop cluster and you can bring in the data. It provides a higher degree of cross-platform
compatibility. </p>

<p> Demo: Use the polly based feature to create an external table from data that resides from outside
the warehouse. We can now work with this data from within the Data Warehouse as nativley as these
external tables were permentaly appart of the Data Warehouse. </p>

<p> Data Analysis Options: Excel, in the Azure cloud you got Azure Analysis Services (cloud based 
variant of SSAS), Power BI. </p>

<p> Demo: Azure Data Factory, Code-free data integration solution, informerly we can call it
cloud bases SSIS. You use Azure Data Factory to build pipelines (hybid ETL and ELT) with a visual
design surface. There is over 80 pre-built connectors to differet data sources. 

In this demo we will use Azue Data Factory to perform a copy activity, we are going to take the
dbo.weather table in SSMS and we are going to place it in our Data Lake Storage Gen2.

<p> Developing Batch Processing Soltuions with Azure HDInsight </p>
<p> Hadoop: Have you every woner how facebook can quickly deal with it's large quantity of 
information? In the past when larger and larger quanteties of data needed to be interegated,
businesses would simply write larger and larger checks to their database vendors of choice (Oracle,
IBM, Microsoft). However, in the early of 2000, companies like google were running into a wall. 
There vast quantity of data where simply to large to pump thrue a single database bottleneck.
To address this, the Google labs team developed an algorithm that allowed for their large database
calculations to be chopped up into smaller chunks, and mapped to many computers. Then when the
calculations were done, be brought back together. They called this algorithm MapReduce. This algorithm
were later used to develop an open source project called Hadoop, which allows applications to
run, using the MapReduce algorithm. Simply put, we are processing data in parallel rather than
serial. 

MapReduce: Two phases, Map phase and reduce phase. The Mappers job is to create or process the
input data. As shown in the diagram, this is usually a file or a directory. This file is stored
on HDFS and is passed into the mapper function. The file is usally passed in line by line, into the
mapper function. The mapper processes this input data to create as few or as many output as needed.
The mappers output is then passed to the reduce phase. The reducers job is to process the data from
the mapper into something useful. Every single value from the mapper is passed into the reduce
function. The reducer will create new output values based on the input from the mapper. The new
output values from the reducer will be saved to HDFS. The technical name for this part is shuffle
and sort phase (also called the magic). Nodes can process data independently, and combine it together.
The cluster is made up of 10, 100 or even 1000 nodes that are connected by a network. A job is 
broken up into smaller part to be run on each node. The mapper works on the smaller parts. The magic
takes the mappers data from every node and brings it together on nodes all alround the cluster. The
reducer runs the node, and knows it has access to everything with the same key. 

HDFS breaks larger files into smaller chunks (blocks). We get several benefits by breaking up the
terabit files into smaller blocks. When the mapper is operating on the terabite file its actually
operating on a block and not the entire file. The terabite file is being worked at by several nodes
in the cluster all at once. The various nodes are just operating on different chunks. Once the mapper
is done, the magic takes over. All of the data in the terabite file is combined based on a key.
The reducer runs on different keys.

Distributed storage. You dont want to be limited by a single hard drive. If you have distributed 
storage you can just keep on adding more and more computers to your cluster. Hadoop is redundant,
if one of the computers is destroyed, Hadoop can handle that as you have backup data in other places
on you cluster. Hadoop was devloped originally by Yahoo! (they were building something called Nutch!)
using Google publically published papers on GFS and MapReduce. Hadoop was primarly driven by
Doug Cutting and Tom White in 2006, it's been evolving ever since. Hadoop was originally used for
batch processing. Now there are stuff built on top of Hadoop which makes it appropriate for
interactive queries aswell (not just for batch processing any more). 

HDFS (Hadoop version of GFS) is the system that allows us to distribute the storage of big data
across our cluster of computer. It makes all of the hard drives on our cluster to look like one 
giant file system. Not only that, it maintaince redundant copies of that data so if one of the 
computer get destroyed, it can recover from that automatically. That is the distributed data storage
piece of Hadoop.
Sitting on top of HDFS we have YARN (Yet Another Resource Negotiator): YARN is were the data 
processing is starting to comes to play. YARN is basically the system that manages the resources
on your computing cluster, it what decides what gets to run tests, what nodes are available for 
extra work, which nodes are not available.
On top of that is MapReduce: ----, initially MapReduce and YARN was kind of the same thing, but got
split up.
On top of MapReduce we have technologies like Pig: If you don't want to write JAVA or Python
MapReduce code, you can use Pig, which allows you to write simple scripts that looks alot like SQL.
Hive also sits ontop of MapReduce and solves a similar problem like Pig, but it's more directly
like a SQL database. Database, you can exectute SQL queries on that database. 
Apache Ambari: Sits ontop of everything, basically gives you a view of your cluster. 
Ambari is what Hortonworks uses, there are competing distributens of Hadoops (Hortonworks, Cloudera,
MapR).
Spark: Sitting at the same level of MapReduce (on top of Yarn), to run queries on your data. Requires
some programming, use Spark script with Python, Java, Scala. It's very fast and under alot of 
active development. If you want to quickly process data on your Hadoop cluster, Spark is a good 
choice. 
Kafka: Data ingestion, collect data of any sort from a cluster of pc and broadcast that into your
hadoop cluster. 


<p> What is Apache Hadoop: Open-source framework for distributed big data processing and 
analysis. The notion of commodity hardware, means you dont have to pay for super computers
if you are going to spread the workload across enough nodes. For instance you can build a 
Hadoop cluster using rasp-berry pie. 


<ul>
<p> Traditional RDBMS : Hadoop </p>
<li> RDBMS : Hadoop </li>
<li> Structured data : Unstructured (although you can project structure) </li>
<li> ACID : CAP </li>
<li> Lower data throughput, bt faster granular query performance : Higher data thrughput, bot slower granualr query perfromance </li>
<li> Vertically scaled : Horizontally Scaled </li>
<li> OLTP : OLAP </li>
<li> SQL Server/Azure SQL Database are licensed and closed source : (Mostly) free and open source,
Cloudera and Microsoft offers managed services, paying for hosted environment and integration with 
HDinsight </li>
<p> HDInsight is Microsoft hosted Apache Hadoop cluster environment. So the high level architecture 
is very similar to open soure Apache Hadoop. We got masisivley parallel processing, we got the same
concept under the hood in HDInsight that you would in any other cloud or on-premises Hadoop cluster.
Head Nodes, Worker Nodes, at the bottom we have decoupled storage (Data Lake Store, Azure Storage 
blobs). </p>
<p> HDInsight Cluster Types: The traditional Hadoop option (Batch query and analysis of HDFS stored data). HBase (processing for large schmealess NoSQL data). Interactive Query (In-memory caching for
fast Hive queries). Kafka: Distributed steaming data platform, ML Services: Predictive modeling and 
machine learning. Spark: In-memory processing and interactive queries (substitute to MapReduce), 
Apache Storm: Real-time event processing




<b> HDInsight is hosted Hadoop, and your using the native Hadoop tools, but they are being hosted
in an Azure frame </b> 
<p> Demo: In this demo we are going to create our first HDInsight cluster, we are going to create
an identity that will represent the HDInsight cluster. HDInsight is simply a cloud version of 
Hortonworks data platform (100% Apache Hadoop). Go to gpv2 storage account (Data Lake Gen2 File
System) where Blob Service usually are. Go to access control (IAM) and give our HDInsight permission.
Go add role assignment, use built in Storage Blob Data Contributor. Assign access to User 
assigned managed identity. Let's go to HDInsight tab and press add... Continue demo. </p>


<p> Azure Data Factory Integration: ? </p>

<p> Combine HDInsight with Hive to do a batch processing job. We are going to download our
dataset (CSV), populate it into our HDInsight cluster, Transform the data using Hive, Create a table
in an Azure SQL Database, and than export the processed data to Azure SQL Database using scoop. </p>

<p> About Apache Spark: Spark is a processing engine that serves as a MapReduce alternative. Goal to 
give MapReduce's scale and fault tolerance faster via in-memory processing (rather just disk IO). Spark
open ups API to Scala, Python, JAva, R and SQL. If your not using Spark, you are pretty much stuck
with java. Microsoft designed HDinsight in conjunction with Hortonworks (the software company that came from the Apache Hadoop project). In january 2019, Hortonworks merged with Cloudera.
Lower compute costs mean Apache Spark is moving to the forefront of big data analysis.  </p>

<p> Databricks: is a hosted Apache Spark environment. Databricks is not originally Microsoft, but 
Microsoft worked with the Databricks team to create Azure Databricks (microsofts hosted value). This
mean you have native compatibility with other Azure products. Demo: Create a Spark HDInsight cluster, 
we will ingest csv data, create a notebook, and than we query the result. </p>

<p> Developing Batch ProcessingSolutions with Azure Databricks </p>

<p> Databricks is a hosted Apache Spark environment and  Azure databricks are Microsofts hosted Databricks environment (Azure Databricks is not the same as Databricks). We are still using most of
Apacahe Hadoop tools, but rather than using the original MapReduce algorithm, we are using Spark. And Spark is known to be super fast, because it does it distributed data processing in-memory. 
The problem with doing Databricks in an on-premis enviornment is that you have the capex of purchasing the clusters host. Doing this in the cloud, gives us cloud compute and cloud scale.
Azure Databricks added value: Auto scale the cluster and place the database cluster in any region. Multio-modal notebook model (programmer can look at code, business people can look at charts).
Built in machine learning libaries, and full Azure integration (RBAC, Azure AD, Tie-in with other Azure resource). 

<ul>

<p> MapReduce : Spark </p>
<li> Batch processing : Batch and real-time (streaming) processing </li>
<li> Disk data processing : In-memory data processing </li>
<li> Java API : Scala, R, Python, SQL, JAva APIs </li>
<li> Generally non-interactive : Interactive emphasis </li>
<li> HiveQL : Spark SQL </li>
<li> External ML Support (Mahout) : Native MLlib support </li> 
</ul>

<p> Demo: We are going to do a ETL job with Azure Databricks. We are going to ingest unstructured data (log files, csv files, media). We are going to Databricks ingest that data into a
reposityory (really ELT not ETL), than using Databricks to perform some transformation on the data, and than load it to Azure SQL Data Warehouse. </p>


<p> Let's look at stream processing with Azure Databricks. An Azure Event hub is a hosted PaaS solution for high-volume data streaming and event ingestion. Event hub can receive and process
millions of events per second. The idea is that we can than take the streams out of Event Hub and ingest them selectivlty into Data Lake Storage Gen2. Azure Event Hub forms the "front door" to Azure
event pipelines. </p>

<p> Demo: We are taking data out of twitter feed and an Azure Event Hub is going to catch that telemetry. </p>


<p> Azure Batch: a hosted way to do MPP with VMs. </p>


<p> Open source python CLI that Microsoft publishes called the Azure Distributed Data Engineering Toolkit (aztk). It allows you to provision on-demand Spark clusters. This is not Databricks, this is more
of the traditional Hadoop/Spark/HDInsight cluster. You can also programatically submit Spark job. Builtatop Azure Batch. Employes (BYO) Docker containers. Low-priority VMs offer 80% discount. 



---




<h1> Notes </h1>

<p> Virtual Machine (VM): Operating systems are software that are able to control the physical
component of a computer. A VM is another type of software that allow us to run more operating systems
within an operating system. Examples are VirtualBox and vmware. </p>

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
as they are powered. For data to remain while the device is turned off, it must be transfered to a long term storage device, which comes in three major types (Magnetic storage, ...)

In memory processing: is an emerging technology for processing of data stored in an in-memory database.
Older systems has been based on disk storage but these are increasingly regarded as inadequate to meet
BI needs. Because stored data is accessed much more quickly when it is placed in RAM, in-memory 
processing allows data to be analysed in real time, enabling faster reporting. <br> <br>

With the hitherto prevalent disk-based technolgoy, data is loaded to the computer's hard drive in the
form of multiple tables and multi-dimensonal structures against which queries are run. Disk-based
technologies are relational database management systems (RDMS), often based on the
SQL language. To improve query performance, multidimensonal databases or OLAP cubes are constructed.
Designing a cube is an elaborate and lengthy process, and changing the cubeäs structure to adapt
to dynamically changing business needs may be cumbersome. Cubes are pre-populated with data to answer
specific queries and altough they increase performance, they are still not suitable for answering
ad-hoc queries. <br> <br> Reading data from the hard disk is much slower (possibly hundreds of times)
when compared to reading the same data from RAM. Memory processing can be accomplished via traditional
databases such as Microsoft SQL Server of via NoSQL offerings. With in-memory databases is initially
loaded into memory RAM instead of hard disks. </p>

<p> Semiconductur: Sillicone is insulating at room temperatur but conducts electricity when it's very
hot. It's a semiconductor who's conductivity change based on the environment. This special ability make
semicondcuturs the perfect brain for electronic devices. Circuits of small semiconductor switches,
called transistors, are at the heart of computer chips, and enable them to do math and run programs. </p> 

