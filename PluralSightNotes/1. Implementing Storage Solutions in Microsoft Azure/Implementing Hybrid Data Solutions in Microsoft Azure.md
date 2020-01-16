<h1> Implementing a Cloud Data Warehouse in Microsoft Azure Synapse Analytics </h1>

---

<h3> Understanding Azure Synapse Analytics </h3>

<p> Synapse Analytics is a combination of: </p>
<ul>
  <li>Azure Data Lake Storage </li> 
  <li>Azure SQL Data Warehouse</li>
  <li>Azure Analytics</li>
</ul>

<p> However, Azure SQL Data Warehouse and Azure Synapse Analytics uses interchangeable. Azure SQL Data Warehouse is a cloud based enterprise data warehouse (EDW) that uses <b> massiveley parallel processing (MPP)</b>. SQL Data Warehouse is appropriate when you need to keep historical data seperate from transaction. That is, when the data is not necessary there for transactional purposes. It's reasonable to use Azure SQL Data Warehouse when you have a warehouse of all your data. And it's sitting there and waiting for analyitcs to happen to it. </p>

<b> Understanding massively parallel processing (MPP) </b>

<p> Multiple processing nodes (computers) which are interconnected to each other and kept in the same chassi. Each computer has its own memory, disk-space, operating system and IO.  </p>

<p> <b> Control Node </b> The front end that interacts with all applications and connections. The MPP enginge runs on the control node to optimize and coordinate parallel queries.  </p>

<p> <b> Compute Node </b> Provides the computational power for analytics. The compute nodes are separated from storage nodes and scaled using the data warehouse units (DWU)  </p>

<p> <b> Storage Node </b> The storage nodes are separateed from the compute nodes in order to keep data at rest. Storage is cheaper than data that is being analyzed.  </p>

<p> <b> Data Warehouse unit </b> A collection of analytic resources that are provisioned. This is a combination of CPU, memory and IO (Input/output). These can be scaled to up or down to meet needs. </p>

<p> <b> Data Movement Service </b> Data transport technology that coordinates data movement between compute nodes. When SQL Data Warehouse runs a query, the work is divided into 60 smaller queries that run in parallel.  </p>

<img src="Images/parallel.JPG" width="700">

  <p> At the bottom of the picture is the Azure storage where we keep our data. It is seperate from the compute power that will cost the most money </p>

<b> Implementing Data Distribution for a SQL Data Warehouse </b> </p> 
<p> When SQL Analytics runs a query, the work is divided into 60 smaller queries that run in parallel. Each of the 60 smaller queries runs on one of the data distributions. Each Compute node manages one or more of the 60 distributions. A SQL pool with maximum compute resources has one distribution per Compute node. A SQL pool with minimum compute resources has all the distributions on one compute node.
  </p>

<p> Three types of distributions.</p>
<ul>
  <li> Replicated Table</li>
  <p>  A replicated table provides the fastest query performance for small tables. Replicating a table removes the need to transfer data among compute nodes before a join or aggregation. Replicated tables are best utilized with small tables. Extra storage is required and there is additional overhead that is incurred when writing data which make large tables impractical. </p>
  <li> Round Robin</li>
  <p> Round Robin distributes data evenly across the table without additional optimization. Loading data into Round Robin is quick but query performance is better for Hash. </p> 
  <li> Hash Table </li>
  <p> A hash distributed table can deliver the highest query performance for joins and aggregations on large tables.
To shard data into a hash-distributed table, SQL Analytics uses a hash function to deterministically assign each row to one distribution.</p>
</ul>
  
<img src="Images/table.JPG" width="700">

<b> Implemening Partitions for a SQL Data Warehouse </b>

<p> Table partitions enable you to divide your data into smaller groups of data. In most cases, table partitions are created on a date column. Partitioning can benefit data maintenance and query performance. Improve the efficiency and performance of loading data by use of partition deletion, switching and merging </p>


<p> There are three types of table partitions </p>
<ul>
  <li> Clustered columnstore </li>
  <p> Updateable primary storage method. Great for read-only </p> 
  <li> Clustured index</li>
  <p> An index that is physically stored in the same order as the data being indexed. </p>
  <li> Heap </li>
  <p> Data is not in any particular order. Use when data has no natural order. </p>
  
</ul>
</p>

<p> Creating a table with to many partitions can hurt performance under some circumstances. Usually you talk around 10 to few hundreds. For clustered columnstore tables, it is important to consider how many rows belong to each partions. Before paritions are created SQL Data Warehouse already divides each table into 60 distributed databases. 
  
  ---
 <h3> Deploying a Data Warehouse in Microsoft Azure Synapse Analytics </h3>
  
  <p> We are going to deploy a data warehouse in Microsoft Azure Synapse Analytics (Formerly SQL Data Warehouse). </p>
<ul>
  <li> Connect to data warehouse</li>
  <li> Prepare the data warehouse to load data</li>
  <li> Load data into the data warehouse</li>
  <li> Examine configuration settings and tasks in the portal </li>
 </ul>
 </p>
 
   <p> Steps to Create a SQL Data Warehouse </p>
<ul>
  <li> Create a resource </li>
  <li> Click Databases </li>
  <li> Click Azure Synapse Analytics (formerly SQL DW)</li>
  <li> Select subscription and resource group </li>
  <li> Give the Data Warehouse a name </li>
  <li> Create a Azure SQL server </li>
  <li> Performance level, välj lägsta</li>
  <li> Additioanl settings: Collation</li>
  <p> It's important to pick the right collation when you install SQL server. When you store something in a database, you use characters (abc$*). A character set is a group of these (American Standard vs European etc). UTF8 allows for like a million characters. What a collation does, it tells how to organize these variables (ABCabc123). An example of collasions UTF8_unicode_ci (case insensitive). ASCII (American Standard Code for Interchange, American standard). </p>
 </ul>
 </p>
 
 
 <b> Resource Group </b>
 <p> Resource groups (RG) in Azure is a new approach to group a collection of assets in logical groups for automatic provisioning, monitoring, and access control, and for more effective management of their costs. One benefit of using RGs in Azure is grouping related resources that belong to an application together, as they share a unified lifecycle from creation to usage and finally, de-provisioning. he underlying technology that powers resource groups is the Azure Resource Manager (ARM). ARM was built by Microsoft in response to the shortcomings of the old Azure Service Manager (ASM) technology that powered the old Azure management portal. </p> 
 
 
 
 
 
 
 
  
  ---
<h3> Notes </h3>

<b>Database vs Data warehouse </b>
<p> Database is a structured place to store data. Data warehouse is a form of database. Rather than to soak in data, a data warehouse is designed to produce data for analysis. That is, database is designed to record while a data warehouse is designed to analyize. A data warehouse is usually normalized etc. </p>

<b> Computing  </b>
<p> Computing is any activity that uses computers to manage, process and communicate information </p>

<b> Processing</b>
<p> Processing is the actual execution of instructions or the instance. </p>

<b>Cache </b>
<p> Browser Cache: A way to make website faster for you when your browsing the internet. When you visit the website, it basically downloads a copy of the website and stores it on your harddrive. Next time you load website it goes really fast. 

<a href="https://www.youtube.com/watch?v=yi0FhRqDJfo"> Video Explanation </a>

CPU Cache: A computer have two different types of memory. Dynamic RAM, SRAM (used in CPU Cache). SRAM does not have to be constantly refreshed. Much faster than DRAM but more expensive. The CPU Cache is the CPU internal memory. It's job is to store copy of data from RAM which is wainting to be used by the CPU. Basically what the CPU Cache does, is that it holds common data that it thinks the CPU will access. CPU always check cache memory first. </p>
