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
 
   <b> Steps to Create a SQL Data Warehouse </b>
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
  <li> Always review settings </li>
  <li> If you have ever built and installed SQL servers from scratch you can appriciate how little effort it takes with Azure </li>
  <li> Pause the compute node so you dont get charged (If you were running a query, not a good idea to pause).</li>
  <li> We will still be charged for the storage? </li> 
 </ul>
 
   <b> Setting a Firewall Rule and Connecting to an SQL Data Warehouse </b>
   <p> We are going to resume the compute node, create firewall rule, connect with Microsoft SQL Server Management Studio. </p>
<ul>
  <li> Click resume </li>
  <li> Create firewall rule</li>
  <p> The SQL data warehouse creates a firewall at the service level. This prevents external application and tools to connect to the server or any database within the server. In order to connec to our SQL server that host our data warehouse we need to add a firewall rule. And this rule is going to enable connectivity for one specific ip address or a range of ip addresses. SQL Data warehouse communicates over port 1.4.3.3. You might have a situation were that port is closed in your firewall. And you are going to open up that port. </p>
  <li> To add firewall rule start with copying and clicking on servername. Needed to connect to database. </li>
  <li> Click on firewall and virtual networks </li>
  <li> Add client IP, add's it automatically under rule name. Than press save</li>
  <p> Now we have added a firewall rule, we have an admin with the password and we can connect to this datbase. </p>
  <li> Download and open Microsoft SQL Server Management Studio </li>
  <li> In object explorer, connect, Database enginge, Server name (copied from before) </li>
  <li> Authentication: SQL Server Authentication, login details </li>
  <li> Expand database, We have TestDataWareHouse and master database. 
 </ul>
 
 
  <b> Preparing an SQL Pool in Azure Synapse Analyitcs to Load Data </b>
   <p> We are going to create a login and a user to load data into our warehouse. We are going to link into NYC Taxi Source Data. We are than going to create tables to hold data inside our data warehouse. </p>
   <p> The admin account is not very good for loading massive amount of data. That data takes alot of processing power, it has to compile and compress. It's a good idea to create a login and a user account specificly for loading data. Login is going to be associated with a resource class that is going to allow us a higher maximum amount of memory being used </p>
<ul>
  <li> Rightclick master database and select new query. </li>
  <li> <pre> LOGIN marcuslarsson1 WITH PASSWORD = 'Britney123';
CREATE USER marcuslarsson1 FOR LOGIN marcuslarsson1; </pre> </li>
  <li> Rightclick TestDataWarehous
    </li>
<pre> CREATE USER marcuslarsson1 FOR LOGIN marcuslarsson1; 
GRANT CONTROL ON DATABASE::[TestDataWareHouse] to marcuslarsson1;
EXEC sp_addrolemember 'staticrc20', 'marcuslarsson1' </pre> 
  <li> Login to datebase as new user. Object explorer => Connect => Database enginge =>  </li>
  <li> Create master key for database. Now we are ready to connect to external datasource.
    </li>
 <pre> CREATE MASTER_KEY; </pre>	
  <p> This is one of the more poorly named objects in the SQL Server platform. Or perhaps the “master” database is the one that is not named well. In any case, the DMK has nothing to do with the master database. Instead, the DMK is the base encryption key inside of a database. This is the key that secures all other keys.  </p>
<pre> CREATE MASTER KEY;
CREATE EXTERNAL DATA SOURCE NYTPublic
WITH
(
	TYPE = Hadoop,
	LOCATION = 'wasbs://2013@nytaxiblob.blob.core.windows.net/'
);  </pre> 
  <li> <p>
  Now we need to create an external file store statement. And this is going to specify the formatinng charactaristics and the options for our external data file. In order for us to load the data into our data warehouse. This statement specifies that the external data is
stored as text. We use a pipe variable in order to separate the values. This file is compressed with gzip.     
 </p>
  
  <pre>
  CREATE EXTERNAL FILE FORMAT uncompressedcsv
WITH (
	FORMAT_TYPE = DELIMITEDTEXT,
	FORMAT_OPTIONS (
		FIELD_TERMINATOR =',',
		STRING_DELIMITER = '',
		DATE_FORMAT = '',
		USE_TYPE_DEFAULT = False
	)
);
CREATE EXTERNAL FILE FORMAT compressedcsv
WITH (
	FORMAT_TYPE = DELIMITEDTEXT,
	FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
		STRING_DELIMITER = '',
	DATE_FORMAT = '',
		USE_TYPE_DEFAULT = FALSE
	),
	DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
	);
  </pre>
  <p> Now our external file format is set and we are ready to create the schema. </p>
  <pre> CREATE SCHEMA ext; </pre>
  </li>
  
  <li>  </li>
  <p> Now we will create several external tables, and these tables will point to the azure blob that we defined previously. </p>
  <li>  <pre> CREATE EXTERNAL TABLE [ext].[Date] 
(
    [DateID] int NOT NULL,
    [Date] datetime NULL,
    [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [FirstDayOfMonth] date NULL,
    [LastDayOfMonth] date NULL,
    [FirstDayOfQuarter] date NULL,
    [LastDayOfQuarter] date NULL,
    [FirstDayOfYear] date NULL,
    [LastDayOfYear] date NULL,
    [IsHolidayUSA] bit NULL,
    [IsWeekday] bit NULL,
    [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
)
WITH
(
    LOCATION = 'Date',
    DATA_SOURCE = NYTPublic,
    FILE_FORMAT = uncompressedcsv,
    REJECT_TYPE = value,
    REJECT_VALUE = 0
); 
CREATE EXTERNAL TABLE [ext].[Geography]
(
    [GeographyID] int NOT NULL,
    [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
    [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
)
WITH
(
    LOCATION = 'Geography',
    DATA_SOURCE = NYTPublic,
    FILE_FORMAT = uncompressedcsv,
    REJECT_TYPE = value,
    REJECT_VALUE = 0 
);      
CREATE EXTERNAL TABLE [ext].[HackneyLicense]
(
    [HackneyLicenseID] int NOT NULL,
    [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
    [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
)
WITH
(
    LOCATION = 'HackneyLicense',
    DATA_SOURCE = NYTPublic,
    FILE_FORMAT = uncompressedcsv,
    REJECT_TYPE = value,
    REJECT_VALUE = 0
);
CREATE EXTERNAL TABLE [ext].[Medallion]
(
    [MedallionID] int NOT NULL,
    [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
    [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
)
WITH
(
    LOCATION = 'Medallion',
    DATA_SOURCE = NYTPublic,
    FILE_FORMAT = uncompressedcsv,
    REJECT_TYPE = value,
    REJECT_VALUE = 0
)
;  
CREATE EXTERNAL TABLE [ext].[Time]
(
    [TimeID] int NOT NULL,
    [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
    [HourNumber] tinyint NOT NULL,
    [MinuteNumber] tinyint NOT NULL,
    [SecondNumber] tinyint NOT NULL,
    [TimeInSecond] int NOT NULL,
    [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
    [DayTimeBucketGroupKey] int NOT NULL,
    [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
)
WITH
(
    LOCATION = 'Time',
    DATA_SOURCE = NYTPublic,
    FILE_FORMAT = uncompressedcsv,
    REJECT_TYPE = value,
    REJECT_VALUE = 0
);
CREATE EXTERNAL TABLE [ext].[Trip]
(
    [DateID] int NOT NULL,
    [MedallionID] int NOT NULL,
    [HackneyLicenseID] int NOT NULL,
    [PickupTimeID] int NOT NULL,
    [DropoffTimeID] int NOT NULL,
    [PickupGeographyID] int NULL,
    [DropoffGeographyID] int NULL,
    [PickupLatitude] float NULL,
    [PickupLongitude] float NULL,
    [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [DropoffLatitude] float NULL,
    [DropoffLongitude] float NULL,
    [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [PassengerCount] int NULL,
    [TripDurationSeconds] int NULL,
    [TripDistanceMiles] float NULL,
    [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
    [FareAmount] money NULL,
    [SurchargeAmount] money NULL,
    [TaxAmount] money NULL,
    [TipAmount] money NULL,
    [TollsAmount] money NULL,
    [TotalAmount] money NULL
)
WITH
(
    LOCATION = 'Trip2013',
    DATA_SOURCE = NYTPublic,
    FILE_FORMAT = compressedcsv,
    REJECT_TYPE = value,
    REJECT_VALUE = 0
);
CREATE EXTERNAL TABLE [ext].[Weather]
(
    [DateID] int NOT NULL,
    [GeographyID] int NOT NULL,
    [PrecipitationInches] float NOT NULL,
    [AvgTemperatureFahrenheit] float NOT NULL
)
WITH
(
    LOCATION = 'Weather',
    DATA_SOURCE = NYTPublic,
    FILE_FORMAT = uncompressedcsv,
    REJECT_TYPE = value,
    REJECT_VALUE = 0
)
;</pre></li>
  
  
 </ul>
 
 
 
 
 <b> Resource Group </b>
 <p> Resource groups (RG) in Azure is a new approach to group a collection of assets in logical groups for automatic provisioning, monitoring, and access control, and for more effective management of their costs. One benefit of using RGs in Azure is grouping related resources that belong to an application together, as they share a unified lifecycle from creation to usage and finally, de-provisioning. he underlying technology that powers resource groups is the Azure Resource Manager (ARM). ARM was built by Microsoft in response to the shortcomings of the old Azure Service Manager (ASM) technology that powered the old Azure management portal. </p> 
 
  ---
<h3> Notes </h3>

<b> Database vs Data warehouse </b>
<p> Database is a structured place to store data. Data warehouse is a form of database. Rather than to soak in data, a data warehouse is designed to produce data for analysis. That is, database is designed to record while a data warehouse is designed to analyize. A data warehouse is usually normalized etc. </p>

<b> Computing  </b>
<p> Computing is any activity that uses computers to manage, process and communicate information </p>

<b> Processing</b>
<p> Processing is the actual execution of instructions or the instance. </p>

<b> Cache </b>
<p> Browser Cache: A way to make website faster for you when your browsing the internet. When you visit the website, it basically downloads a copy of the website and stores it on your harddrive. Next time you load website it goes really fast. 

<a href="https://www.youtube.com/watch?v=yi0FhRqDJfo"> Video Explanation </a>

CPU Cache: A computer have two different types of memory. Dynamic RAM, SRAM (used in CPU Cache). SRAM does not have to be constantly refreshed. Much faster than DRAM but more expensive. The CPU Cache is the CPU internal memory. It's job is to store copy of data from RAM which is wainting to be used by the CPU. Basically what the CPU Cache does, is that it holds common data that it thinks the CPU will access. CPU always check cache memory first. </p>


<b> Ports & IP Addressing </b>

<a href ="https://www.youtube.com/watch?v=AXrFCbD4-fU"> Video Explanation </a>

<p> You can think of ports as exact house or appartment number. IP Address represents the city or street number. And port number represents the exact house number. When a computer is trying to connect and talk with another computer, it needs both IP address and port. How do you find port numbers on a computer. If you are using windows open command and type netstat -a -b -n with admin privelage. 

Common port numbers: HTTP 80, FTP (File transfer) 20 </p>

<b> TCP traffic </b>

<p> Together IP and port number is called the socket. IP adress are used to identify what computer we are sending to or from and the port represents what application or service we are sending to and from. </p> 

<b> Firewall </b>
<p> System that is designed to prevent unauthorized access to enter a private network by filtering information that comes in from the internet. A firewall blocks unwanted traffic and permits wanted traffic. Firewall => Router => Computer. A firewall works by filtering the incomming network data and determines by its rules if its allowed to enter a network. These rules are customizable and determined by the network administrator. Generally firewalls allow data to go out.  </p>

<b> SQL Server Management Studio(SSMS)</b>
<p> Integrated environment for managing any SQL infrastructure, from SQL Server to Azure SQL Database </p>


<b> Syste databases in SQL Server </b>
<ul>
  <li> <b> master </b> keeps and manages all system level information. Such as system configuration, logins, linked servers, credentials etc. Take master data backup because if it becomes corrupted/deleted you won't be able to start sql server. </li>
  <li> <b> model </b> The model database acts as a template for all the data bases. Used in the creation of any new user database created in this instance (store procedures, database configurations) </li>
  <li> <b> msdb </b> SQL Server agent information is managed by msdb. Will hold backup, log_shipping. li>
  <li> <b> tempdb </b> holds temporary data, tables like locally temporary tables.</li>
  <li> <b> resource </b> not accessable by the user </li>
  <li> <b> distribution </b> not accessable by the user </li>
</ul>

