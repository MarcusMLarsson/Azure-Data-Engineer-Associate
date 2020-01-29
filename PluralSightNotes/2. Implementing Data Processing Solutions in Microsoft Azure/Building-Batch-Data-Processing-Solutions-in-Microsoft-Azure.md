<h1> Building Batch Data Processing Solutions in Microsoft Azure </h1>

<p> The Four V's of Big Data: Volume (the flow of data, size matrix like Peta bites or Exa bites),
Velocity (Processing frequency, what is your tollerance for latency), Data Variety (is your data
structured, semi-structured or unstructured), Veraciy (Data trustworthiness, Noise, bias). </p>

<p> Structured data (SQL table, data is fully modeled, each entity (table) is sorted into a number
of columns, and relationships among tables are explicitly defined.
Semi-structured data (JSON, XML), JSON is same as key value pair, for XML you have the possibility
for a schema. Unstructured data (CSV, PNG, EXE (blob)). </p>

<p> For a Data Warehouse the datas purpose is defined (structured and highly transformed). For a
Data Lake the datas purpose is not yet determined. ETL (Extract, transform load. Data is transformed
in flight between source and destination. Does not scale particulary well. ELT (Extract, load, 
transform). Data is transformed after it is extracted (Azure usually uses ELT as its a great fit
for the cloud given limitless compute and storage resources). Batch processing: Working with
previously stored data (more tollerance for latency). Stream processing: Working with incoming
data in real time. Data processing: Situationg data into a usable format. Data analysis: Asking questions of the prepared data. </p>

<ul>

<p> Azure SQL DAtabase : Azure SQL Data Warehouse </p>
<li> OLTP (Online transaction processing)/CRUD (CREATE READ UPDATE DELETE) : OLAP(Online analytical processing)/querying and reporting </li>
<li> SMP : MPP </li>
<li> Vertical scale : Horizontal scale </li>
<li> : Can pause the virtual server to save costs </li>
<li> No polybase : Polybase </li>


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
<p> Demo: 
