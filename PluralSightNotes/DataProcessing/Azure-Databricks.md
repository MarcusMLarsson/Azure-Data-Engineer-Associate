<h1> Implementing an Azure Databricks Environment in Microsoft Azure </h1>

<p> <b>What is Azure Databricks?</b> It's a scalable apache spark based analytics platform that is optimized for Azure. Designed in
collaboration with the founders of Apache Spark, Azure Databricks provides streamline workflow in an interactive workspace that
enables collaboration between your data scienties, your data engineers etc. </p>

<img src="https://miro.medium.com/max/800/1*qn2gItW3lIvbDtrKlQgtww.jpeg">

<ul> 
<li> Ingest: Kafka, Event Hub, IoT Hub </li>
<li> Store: Blobs, Data Lake </li>
<li> Prep & Train: Databricks (Machine Learning) </li>
<li> Model & Serve: Cosmos DB, SQL Database, SQL Data Warehouse </li>
<li> Intelligence: Analytical Dashboards, predictive apps </li>
</ul>

<b> Apache Spark </b>
<p> Apache Spark is an open-source distributed general-purpose cluster-computing framework. Spark provides an interface from
programming entire clusters with implicit data parallelism and fault tolerance. The purpose of Apache Spark is to process
large amount of data and Spark is suitable for batching and streaming processing. Spark was created to address the limitations to MapReduce, by doing processing in-memory, reducing the number of steps in a job, and by reusing data across multiple parallel operations. With Spark, only one-step is needed where data is read into memory, operations performed, and the results written back—resulting in a much faster execution. Spark also reuses data by using an in-memory cache to greatly speed up machine learning algorithms that repeatedly call a function on the same dataset. Data re-use is accomplished through the creation of DataFrames, an abstraction over Resilient Distributed Dataset (RDD), which is a collection of objects that is cached in memory, and reused in multiple Spark operations. This dramatically lowers the latency making Spark multiple times faster than MapReduce, especially when doing machine learning, and interactive analytics. </p> 

<img src="https://d1.awsstatic.com/Data%20Lake/what-is-apache-spark.b3a3099296936df595d9a7d3610f1a77ff0749df.PNG">

<p> Azure Databricks comprises the complete set of Apache Spark open source technology capabilities. 
 <ul>
<li> Spark SQL is the Spark module for working with structured data within Azure Databricks. A Dataframe is a distributed collection of data organized into name columns. It's conceptionally equivalent to a table or a dataframe in Python. </li>
<li> Than we have streaming support, which provides real time data processing and analysis for analytic and interactive applications. It integrate with things like HDFS, flume and Apache Kafka. </li> 
<li> Next, we have the MLLib (Machine Learning libary), which consist of common learning algorithms for classification,
  regression etc. </li>
<li>Next, we have the GraphX, which provides graphs and graphs computation for a broad scope of use cases.</li>
   <li>Last we have the Spark core API (includes support for R, SQL, Python, Scala, Java).</li></p></ul>
   
   
<b> Spark vs Hadoop </b>

<img src="https://raw.githubusercontent.com/andkret/Cookbook/master/images/Table-Hadoop-and-Spark.jpg">

<p> Hadoop is used to store data in the Hadoop Distributed File System (HDFS). It can analyse the stored data with MapReduce and manage resources with YARN. However, Hadoop is more than just storage, analytics and resource management. There's a whole eco system of tools around the Hadoop core. Compared to Hadoop, Spark is "just" an analytics framework. It has no storage capability. Although it has a standalone resource management, you usually don't use that feature. </b>

<b> Working with Azure Databricks </b>
<p>When working with Azure Databricks you need to understand a few components. First are the collaborative Workspaces that
contain all of your assets. Than you have Apache Clusters, these do the heavy lifting of your analysis work. Next, we have the
Notebooks which provides a collaborative space for traning and preparing your data and creating your data pipelines. We have
Tables which provide datastructures in your work spaces and last are the jobs for scheduling jobs in your work spaces. Now let's take
alook at these by their own. </p>

<p> <b>Workspace</b>: A workspace is an environment for assesing all of your Azure Databricks assets. It organizes notebooks, libaries,
dashboards, and experiments into folders. By default the workspace and all it content is available to all the user who have
access to the workspace. Each user however have their private folder which is note shared. You can create and manage workspaces
using UI, CLI or Workspace API. Folders hold everything within the workspace (like a folder on your local computer). There exist
three folders; Workspace, Shared and Users. Workspace is a special root folder for all of your assets, the Shared folder is for 
sharing objects across your organization. The user folder is for each user. </p>

<p> <b>Demo: Creating an Azure Databricks workspace </p></b>

<p> Search for Databricks, Add (new workspace), pricing tier: standard allows you to secure with Azure AD, while premium allows
Role-based access control (RBAC). Create, Launch workspace, click on user profile, admin console, add user. You can also use 
groups, for example create a group for data science etc. 

<b>Create Workspace</b>: Workspace, Workspace, create, folder. Right click folder and modify permission. 

<b> Demo: Getting started with the Databricks CLI </b>

<p>We will be using Azure Cloud Shell, a webb based CLI for accessing Azure.
You can also setup the CLI locally. CLI stands for command-line interface. First, I need to generate a new token for my user to able access
my workspacing using the databricks cli. Copy the token, and go into https://shell.azure.com. Let's create an virtual environment for
my Data Bricks CLI to live in. </p>

<pre>
virtualenv -p /user/bin/python2.7

I want to enter that virtual environment

source databrickscli/bin/activate

I want to install Data Bricks CLI into my virtual environment.

pip install databricks-cli

The next thing is to configure the virtual environment to go to the workspace

databricks confgiure --token

Copy URL

databricks -h
</pre>

<p> <b>Demo: Working with Spark clusters </p></b>

<p> Go down to the common task, and click new cluster or go over to the cluster icon. Click create cluster. Leave enable autoscaling,
it will automatically scale the minimum and maximum number of nodes based on loads. For worker type, you can choose a number off different
virtual machines. For the type of driver, you can pick the same as a worker. This is how you create a cluster with the UI. </p>

<p> <b>How to create a cluster with the shell</b>

<pre>
source databrickscli/bin/activate

Take alook at a json file to build out our cluster

code ./clouddrive/demo/intro/bd-cl02.json

databricks clusters create --json-file ./clouddrive/demo/intro/bd-cl02.json

databricks clusters list
</pre> 

<p> <b>Notebooks</b>: Web-based interface, combine code, visualization and text that are all organized in cells. Often production level notebooks
will be run as a job, once tweaking of code is complete. Notebooks will be the foundation for building pipelines within Azure Databricks. Supports
Python, Scala, Markdown and HTML. </p>

<p> <b>Demo: Working with Notebooks in Azure Databricks </p> </b>

<p> Import notebook by rightclicking on Workspace. Notebook has .ipynb file format (iPythonJupyterNotebook). In the left top corner we can attach a cluster. % means other code than Python (or what we opened the notebook in), %md for instance means markdown, %% bash (cell magic, will be exectued in a bash shell), try %lsmagic</p>

<p> <b>Working with Azure Databricks Tables</b>: is a collection of structured data. Tables are equivalent of Apache Spark dataframes. In Spark a dataframe is a distributed collection of data organized inte name columns. Same as dataframe in Python and R. But it comes with much richer optimizations under the hood. This means you can cache, filter and perform any operation supported by dataframes on your tables.

<a href="https://wesmckinney.com/blog/apache-arrow-pandas-internals/"> Pandas & Apache </a>

<p> <b>Demo: Working with tables </p> </b>
<p> Import the notebook, attach to cluster, create a spark table </p> 

<p> A job is a way of running a notebook on a scheduled basis. You can create and run jobs using the UI, CLI or API. Similary, you can monitor job
run results in the UI / CLI / API aswell. One thing to note is that the number of jobs in a workspace is limited to 1000. To create a job, 
simply go down to jobs, click on create jobs, you can create the job based one of the notebooks. Click edit beside schedule to schedule the job.
If we take a look at the cluster we can edit that aswell. The recommendation from Apache Spark is to use a new cluster for your production 
level jobs, or the jobs that are important to complete. You can click run now to test the job. </p>

<p> To do this with the Azure Cloud Shell </p>

<pre> 
databricks jobs list

databricks jobs get --job-id 4

code ./clouddrive/demo/intro/bd-job01.json 

databricks jobs create --json-file clouddrive/demo/intro/bd-job01.json

databricks jobs run-now --job-id 7
</pre>

<p> <b>Performing ETL (Extract, Transform, Load) Operations with Azure Databricks</b> </p>
<p> ETL (Extract Transform, Load) is a datapipeline used to collect data from various source, transform that data according to business rules
and load it into a destination data store. This makes way for your intelligente applications to access the transformed data they need, in the
format that they need it. In the ETL model, data is stored raw in different types of storage (e.g. Azure Blob Storage, Azure Data Lake Storage
, Hadoop Storage). Since you don't want to change the raw data, and it's often more data than its needed for the end consumer application, you
are going to extract it from it store, for the transform process. The process of extracting comes out of notebook calls requesting the data
that they need. This allows the process to be schedueled and interactive. And because Azure Data Bricks lives in Azure, you have easy access
to all of your storage, native and securly. Once the data is extracted, transformation can begin. Transformation in Azure Data Bricks involves
processing the raw data into predictions and insight. A transformation activity, executes in the Azure Data Bricks Apache Cluster, driven by Azure Data
Bricks notebooks and jobs. The data transformations that takes place usually involves filtering, cleaning, joining, removing duplicates etc. Once 
the data is transformed, the data is put into a database service for use by the consuming applications. Options include Azure SQL Warehouse, Cosmos DB, Azure SQL Server etc.

<p> <b>Demo</b>: Open up Data Bricks workspace. Go and create a cluster that is going to be used by the
notebook. Go into the workspace and import a couple of notebooks. Workspace, import, browse...
Bring in the audience notebook and add in the clean-audiance notebook (replace the placeholders).
Attach the notebook to the cluster. First thing is that we are going to mount a file system in
Azure Data Lake Storage Gen2 account. Now we are going to start the process of ETL and to start to
ingest data. This is going to download downloading a JSON file from github, putting it to a temporary
directory, than we are going copy that JSON file into our Azure Data Lake Storage. </p>

<pre>%sh wget -P /tmp
https://raw.githubusercontent.com/Azure/usql/master/Examples/Samples/Data/json/radiowebsite/
small_radio_json.json

shell comand
</pre>


<p> <b>Batch Scoring of Apache Spark ML Models With Azure Databricks</b> </p>

<p> Batch scroing involves a scheduled application of a ML model on a dataset to provide predictions.
This can be done using a Spark job in Azure Data Bricks. In Azure Databricks, the best way to 
implement batch scoring is by using notebooks to build a batch scoring pipeline. A batch scoring
pipeline allows you to produce and run ML Models against data in a control and scheduled manner.
Multiple notebooks are used to complete each step of the process. 

<b> Demo: Batch scoring of Spark machine learning models on Azure Databricks </b>

<pre>cd clouddrive .... 

git clone ... </pre>

<p> Demo includes building a batch scoring pipeline on Azure Data Bricks to predict machine
component faileur. This demo has 10 notebooks. Do the demo... </p>


<b> Streaming HDInsight Kafka Data into Azure Databricks </b>

<p> Apache Kafka is a distributed streaming platform. What exactly does that mean? A streaming platform has three key capabilities:

<ul> <li> Publish and subscribe to streams of records, similar to a message queue or enterprise messaging system. </li>
<li>Store streams of records in a fault-tolerant durable way. </li>
<li>Process streams of records as they occur. </li> </ul>

Kafka is generally used for two broad classes of applications:
<ul>
    <li> Building real-time streaming data pipelines that reliably get data between systems or applications </li>
     <li>Building real-time streaming applications that transform or react to the streams of data </li>
</ul>
To understand how Kafka does these things, let's dive in and explore Kafka's capabilities from the bottom up.

First a few concepts:
<ul>
    <li>Kafka is run as a cluster on one or more servers that can span multiple datacenters.</li>
 <li>The Kafka cluster stores streams of records in categories called <b>topics</b>.</li>
    <li>Each record consists of a key, a value, and a timestamp. </li></ul>   
<p> In Kafka, the communication between the clients and the servers is done with a simple, high-performance, language agnostic TCP protocol. This protocol is versioned and maintains backwards compatibility with older versions. </p>    
  <img src="https://i.ytimg.com/vi/k-7lz6Ex354/maxresdefault.jpg">
  
  
  <p>
For a long time, we have written programs that store information in databases. Databases think in
things (cards, people etc), but Kafka thinks in events (events have an description of what happend
at that time). The primary idea is that an event is an indication in time that the thing took place.
It's not easy to store events in databases, instead we use logs. A log is just a order sequence 
of the events. Apache Kafka is a system to managing these logs, using a fairly standard historical 
terms it calls them topics. A topic is just an order collection of events stored in a durable way.
Durable meanign that they are written to disc and replicated. As a result, no single hardware faileur can make
that data go away. Topics can store data from days to multiple years, topics can be relative small
or enormous. </p>

<p>
Back when databases ruled the world, there was kind of a trend to build a one gigant program that
uses one big database all by itself. These things grew to where they were difficulte to change
and difficute think about. Now the trend is to write lots and lots of small programs, each
one of which is small enough to version and change all on its own. These programs can talk to each
other thrue Kafka topics. So each one of these services can consume a message from a Kafka topic
and produce that message off to another Kafka topic that lives in another service. Now its possible 
to perform real time analysis (streaming) on these topics. In contrast to running a batch service
over night. </p>

<p>
Kafka connect is a tool that helps to connect to ifferent systems. You want to collect data from different
systems and get the data to be written into a topic. You want to transform a topic into
a different fileformat for an external legacy system. Kafta connect is also an echo system of 
connectors. There are dussins, even 100 connectors out there in the world, some of them are open source,
some of them are commercials but they are these little plugable models that you can deploy to get the
integration done. You deloy them, you configure them, you don't write code to do this reading and
wrinting from the database. Kafta connect does that integration to those external systems. </p>
  
  
 <b> HDInsight </b>
  <p>
In Azure, HDInsight is the platform for hosting Kafka. 
 You can use many open source frameworks such as Hadoop, Apache Spark and Apache Kafka and more
with HDInsight. The general setup from streaming with Kafka is quit simple. Producers send 
records (events) to clusters were they are stored as topics. A topic is just a write-ahead log where
the producers append records. Within the clusters, topics are assigned to the partitions that can
be replicated for fault tollerance across the clusters. In the case of Azure, Kafka topics reside in 
HDInsight cluster. These records, based on a key-value pairs, are available for consumers to use. 
Consumers are going to subscripe to the topics they need and receive changes in real time as event
producers send more data into Kafka. All communication between producers and consumers happens
by Kafka brokers running in the cluster.  </p>


<p> <b>Demo: Streaming Data Scenario</b> </p>
<p> Store data in Kafka topic and consuming a subset of the data into Azure Databricks. These involves
a number of steps. We are going to install the required components for HDInsight. We are going to build
and configure HDInsight with Kafka. We are going to build an Azure Databricks workspace and cluster.
We are going to implement virtual network pearing between the two clustersand than we kick off event
production and consumption stream using Databricks notebook. </p>


<p> <b>Virtual Network peering</b> </p>

<p> Often times, resources in Azure are deployed to different virtual networks based on the needs
of the services. These networks are isolated by design. For those occations when you need to
virtual networks to be connected, and the resources need to communication, Azure Virtual Netwoork
Peering is here to help. With peering, services in different Virtual Networks (or vNets) communicate
with each other via highbandwith, low latency, Azure fiber backbones. In our streaming scenario, 
setting up Virtual Netwowrk Peering between Kafka HDInsight and Azure Databricks is going to eastblish
this private communication network and allow streaming to happend. This is done by configuring each
side of the peer network. While Azure allows Network Peering across network (known as global vnet 
peering) we are using same region for our demo. Do the demo. </p>

<p> Once connected to Kafka on HDInsight via peered Vnet, Azure Databricks using connectors built into
the Spark platform makes the connection needed to establish the streaming process. The best place
to do this in Azure is to use Azure Notebooks. For basic streaming, a notebook for producing events
will be created. This establishes the flow of data from outside sources into Kafka and placed into
topics for consumption. Another notebook will be created to consum the topic desired from Kafka brokers
within the cluster and bring the data into Azure Databricks. From there, data scienties can do whatever
they need with the data. Do the demo!! </p>

---

<h1> Notes </h1>

<p> Terminal vs Bash vs Command line (CLI) vs Prompt. </p>

<p> The terminal (short for terminal emulator) is the program that is floating on your screen. Bash is the language that run
in most terminal emulators. If you want to know what language you are running, you can type in echo $0. CLI is a emulator for a
specific language? </p>
