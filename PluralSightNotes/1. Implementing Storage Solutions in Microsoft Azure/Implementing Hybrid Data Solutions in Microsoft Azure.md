<h3> Understanding Azure Synapse Analytics </h3>

<p> Synapse Analytics is a combination of Azure Data Lake Storage, Azure SQL Data Warehouse and Azure Analytics </p>

<p> Clouse base enterprise data warehouse (EDW) that uses massiveley parallel processing (MPP) </p>

<p> SQL Data Warehouse is most appropriate when you need to keep historical data seperate from transaction </p>

<p> The data is not necessary there for transactional purposes. You have a warehouse of all your data. And it's sitting there for waiting for analyitcs to happen to it. </p>

<h3> Understanding massively parallel processing (MMP) </h3>

<p> Have processing acting in parallel with different nodes that you have of your storage. At the bottom is the Azure storage that we keep our data. It is seperate from the compute power that will cost the most money </p>

<p> <b> Control Node </b> The front end that interacts with all applications and connections. The MPP enginge runs on the control node to optimize and coordinate parallel queries.  </p>

<p> <b> Compute Node </b> Provide the computational power for analytics. Separated from storage nodes. These are scaled using data warehouse units (DWU)  </p>

<p> <b> Storage Node </b> Separate from Compute in order to keep data at rest. This is cheaper than data that is being analyzed.  </p>

<p> <b> Data Warehouse unit </b> A collection of analytic resources that are provisioned. This is a combination of CPU, memory and IO (Input/output). These can be scaled to up or down to meet needs. </p>

<p> <b> Data Movement Service </b> Data transport technology that coordinates data movement between compute nodes. When SQL Data Warehouse runs a query, the work is divided into 60 smaller queries that run in parallel.  </p>

<img src="Images/parallel.JPG" width="700">


<b> Implementing Data Distribution for an SQL Data Warehouse </p> 
<p> A distribution is the basic unit of storage and processing for parallel queries. Rows are stored across 60 distributions which are run in parallel. Each Compute node manages one or more of the 60 distributions.</p>

<p> Three types of distribution. Replicated Table

---

<h3> </h3>

<p> Computing is any activity that uses computers to manage, process and communicate information </p>


<p> Browser Cache: A way to make website faster for you when your browsing the internet. When you visit the website, it basically downloads a copy of the website and stores it on your harddrive. Next time you load website it goes really fast. 

<a href="https://www.youtube.com/watch?v=yi0FhRqDJfo"> Video Explanation </a>

CPU Cache: A computer have two different types of memory. Dynamic RAM, SRAM (used in CPU Cache). SRAM does not have to be constantly refreshed. Much faster than DRAM but more expensive. The CPU Cache is the CPU internal memory. It's job is to store copy of data from RAM which is wainting to be used by the CPU. Basically what the CPU Cache does, is that it holds common data that it thinks the CPU will access. CPU always check cache memory first. </p>
