<h1> Implementing an Azure Databricks Environment in Microsoft Azure </h1>

<p> What is Azure Databricks. It's a scalable apache spark based analytics platform that is optimized for Azure. Designed in
collaboration with the founders of Apache Spark, Azure Databricks provides streamline workflow in an ineractive workspace that
enables collaboration between your data scienties, your data engineers etc. </p>

<ul> 
<li> Ingest: Kafka, Event Hub, IoT Hub </li>
<li> Store: Blobs, Data Lake </li>
<li> Prep & Train: Databricks (Machine Learning) </li>
<li> Model & Serve: Cosmos DB, SQL DAtabase, SQL Data Warehouse </li>
<li> Intelligence: Analytical Dashboards, predictive apps </li>

<p> Apache Spark is an open-source distributed general-purpose cluster-computing framework. Spark provides an interface from
programming entire clusters with implicit data parallelism and fault tolerance. The purpose of Apache Spark is to process
large amount of data and Spark is suitable for batching and streaming processing. With MapReduce you first have to do Map
and than Reduce, while Spark has more flexibility. </p> 

<p> Azure Databricks comprises the complete set of open source Apache Spark open source technology capabilities. Spark SQL is the
Spark module for working with structured data in within Azure Databricks. A Dataframe is a distributed collection of data organized
into name columns. It's conceptionally equivalent to a table or a dataframe in Python. Than we have streaming support, which provides
real time data processing and analysis for analytic and interactive applications. Its integrate with things like HDFS, flume and 
Apache Kafka. Next, we have the MLLib (Machine Learning libary), which consist of common learning algorithims for classification,
regression etc. Next, we have the GraphX, which provides graphs and graphs computation for a broad scope of use cases. Last we have
the Spark core API (includes support for R, SQL, Python, Scala, Java). </p>

<p> Typical use cases for Azure Databricks: Dealing with streaming processing (IoT devices, sensors), machine learning etc.
When working with Azure Databricks you need to understand a few components. First are the collaborative Workspaces that
contain all of your assets. Than you have Apache Clusters, these do the heavy lifting of your analysis work. Next we have the
Notebooks which provides a collaborative space for traning and preparing your data and creating your data pipelines. We have
Tables which provide datastructures in your work spaces and last are the jobs for scheduling jobs in your work spaces. Now let's take
alook at these by their own. </p>

<ul>
<p> Workspace: A workspace is an environment for assesing all of your Azure Databricks assets. It organizes notebooks, libaries,
dashboards, and experiments into folders. By default the workspace and all it containts its available to all the user who have
access to the workspace. Each user however have their private folder which is note shared. You can create and manage workspaces
using UI, CLI or Workspace API. Folders hold everything within the workspace (like a folder on your local computre). There exist
three folders; Workspace, Shared and Users. Workspace is a special root folder for all of your assets, the Shared folder is for 
sharing objects across your organization. The user folder is for each user. </p>

<p> Demo: Creating an Azure Databricks workspace </p>

<p> Search for Databricks, Add (new workspace), pricing tier: standard allows you to secure with Azure AD, while premium allows
Role-based access control (RBAC). Create, Launch workspace, click on user profile, admin console, add user. You can also use 
groups, for example create a group for data science etc. 

Create Workspace: Workspace, Workspace, create, folder. Right click folder and modify permission. 

<b> Demo: Getting started with the Databricks CLI: We will be using Azure Cloud Shell, a webb based CLI for accessing Azure.
You can also setup the CLI locally. CLI stands for command-line interface. First, I need to generate a new token for my user to able access
my workspacing using the databricks cli. Copy the token, and go into https://shell.azure.com. Let's create an virtual environment for
my Data Bricks CLI to live in. 

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

<p> Demo: Working with Spark clusters. </p>

<p> Go down to the common task, and click new cluster or go over to the cluster icon. Click create cluster. Leave enable autoscaling,
it will automatically scale the minimum and maximum number of nodes based on loads. For worker type, you can choose a number off different
virtual machines. For the type of driver, you can pick the same as a worker. This is how you create a cluster with the UI. </p>

<p> How to create a cluster with the shell. 

<pre>
source databrickscli/bin/activate

Take alook at a json file to build out our cluster

code ./clouddrive/demo/intro/bd-cl02.json

databricks clusters create --json-file ./clouddrive/demo/intro/bd-cl02.json

databricks clusters list


</pre> 

<p> Notebooks: Web-based interface, combine code, visualization and text that are all organized in cells. Often production level notebooks
will be run as a job, once tweaking of code is complete. Notebooks will be the foundation for building pipelines within Azure Databricks. Supports
Python, Scala, Markdown and HTML. </p>

<p> Demo: Working with Notebooks in Azure Databricks </p>

<p> Import notebook by rightclicking on Workspace. Notebook has .ipynb file format (same file format of Jupyter Notebook). In the left top corner
we can attach a cluster. % means other code than Python (or what we opened the notebook in), %md for instance means markdown. </p>

<p> Working with Azure Databricks Tables: is a collection of structured data. Tables are equivalent of Apache Spark dataframes. In Spark a dataframe
is a distributed collection of data organized inte name columns. Same as dataframe in Python and R. But it comes with much richer optimizations
under the hood. This means you can cache, filter and perform any operation supported by dataframes on your tables.

<a href="https://wesmckinney.com/blog/apache-arrow-pandas-internals/"> Pandas & Apache </a>

<p> Demo: Working with tables </p>
<p> Import the notebook, attach to cluster, create a spark table </p> 

<p> A job is a way of running a notebook on a scheduled basis. You can create and run jobs using the UI, CLI or API. Similary, you can monitor job
run results in the UI / CLI / API aswell. One thing to note is that the number of jobs in a workspace is limited to 1000. To create a job, 
simply go down to jobs, click on create jobs, you can create the job based one of the notebooks. Click edit beside schedule to schedule the job.
If we take a look at the cluster we can edit that aswell. The recommendaiton from Apache Spark is to use a new cluster for your production 
level jobs, or the jobs that are important to complete. You can click run now to test the job. </p>

<p> To do this with the Azure Cloud Shell </p>

<pre> 

databricks jobs list

databricks jobs get --job-id 4

code ./clouddrive/demo/intro/bd-job01.json 

databricks jobs create --json-file clouddrive/demo/intro/bd-job01.json

databricks jobs run-now --job-id 7

</pre>

<p> Performing ETL (Extract, Transform, Load) Operations with Azure Databricks </p>
<p> ETL (Etract, Transform, Load) is a datapipeline used to collect data from various source, transform that data according to business rules
and load it into a destination data store. This makes way for your intelligente applications to access the transformed data they need, in the
format that they need it. In the ETL model, data is stored raw in different types of storage (e.g. Azure Blob Storage, Azure Data Lake Storage
,Hadoop Storage). Since you don't want to change the raw data, and it's often more data than its needed for the end consumer application, you
are going to extract it from it store, for the transform process. The process of extracting comes out of notebook calls requesting the data
that they need. This allows the process to be schedueled and interactive. And because Azure Data Bricks lives in Azure, you have easy access
to all of your storage, native and securly. Once the data is extracted, transformation can begin. Transformation in Azure Data Bricks involves
processing the raw data into predicts and insight. A transformation activity, executes in the Azure Data Bricks Apache Cluster, driven by Azure Data
Bricks notebooks and jobs. The data transformations that takes place usually involves filtering, cleaning, joining, removing duplicates etc. Once 
the database is transformed the data is put into a database service for use by the consuming applications. Options include Azure SQL Warehouse,
Cosmos DB, Azure SQL Server etc.

<p> Demo 

---

<h1> Notes </h1>

<p> Terminal vs Bash vs Command line (CLI) vs Prompt. </p>

<p> The terminal (short for terminal emulator) is the program that is floating on your screen. Bash is the language that run
in most terminal emulators. If you want to know what language you are running, you can type in echo $0. CLI is a emulator for a
specific language? </p>
