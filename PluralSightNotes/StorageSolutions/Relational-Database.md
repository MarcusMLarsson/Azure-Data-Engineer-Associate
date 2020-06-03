
<h1> Implementing a Relational Database in Microsoft Azure SQL Database </h1>

---
<h3> Azure SQL Database (DBaas) vs SQL Server on Azure VM (Iaas) </h3>

<p> Imagen you have a server which talks to a SQL server database in the back end. In the old days, before the cloud, you would get the server either on-premises or in your data center and install SQL Server on that box. You were responsible to configre the networking, the security, operating system patching, and the performance and scaling of your SQL server. Azure gives you two options to run SQL server-based workloads. The first option, which is the main focus of this course, is Azure SQL Database (DBaas). The other option is to provision a SQL Server installation on an Azure virtual machine. This is a SQL Server inside a fully managed virtual machine in Azure. You still don't need to worry about the physical machine. However, it's still a virtual machine so you need to manage the instance of SQL Server manually. How do you choose between the two? Do you want to manually manage your database engine, apply patches, take backups, or delegate these operations to Azure?  </p>

<p><b>SQL Server on Azure VMs</b>: is an Infrastructure-as-a-Service (IaaS) offering and allows you to run SQL Server inside a fully-managed VM in Azure. This is a good option for migrating on-premises SQL Server databases and applications without any database change. The SQL Server installed on the VM is identical to the SQL Server you have installed on-premises. Also, the IaaS option gives you full control over the database engine. You could control the timing of maintenance and patching of your database engine. You could also pause or stop the virtual machine whenever you don't need the SQL database (to save some costs).  </p>

<p><b>Azure SQL Database</b>: A relational database-as-a-service (DBaaS) hosted in Azure, this is a platform-as-a-service (PaaS) offering. The database has additional features that are not availaible in SQL Server, such as built-in high availability, intelligence, and management. Pay-as-you-go with options to scale up or out for greater power (with no interruption). Has multiple deployment options and service tiers. </p>

<b> Benefits </b>

| SQL Server on VM        | Azure SQL Database       |
| ------------- |:-------------:|
| Up to 99.95% availaiblity     | 99.99% availability guaranteed  |
| Full control over the SQL Server enginge     | The most commonly used SQL Server features are available      |
| Full parity with the matching version of on-premises SQL Server | Built-in backups, patching, recovery      |
| Easy migration from SQL Server on-premises | Ability to assign necessary resources (CPU/storage) to individual databases      |
| Private IP address within Azure VNet | Built-in advanced intelligence and security      |
|  | Online change of resources (CPU/storage) with no downtime     |







<b> Limitations  </b>

| SQL Server on VM        | Azure SQL Database       |
| ------------- |:-------------:|
| Need to manually manage your backups and patches     | Migration from SQL Server might be hard  |
| You need to implement your own high-availability solution     | Some SQL Server features are not available      |
| There is a downtime while changing the resources (CPU/storage) | No guaranteed exact maintenance time (but nearly transparent)       |
| Need to implement additional mechanisms to ensure availability of your databases | Private IP address cannot be assigned (with exception)       |


<h3> Azure SQL Database </h3>

<ul>
  <p> There are 3 Azure SQL Database deployment options</p>
  <li> Single database: Isolated database that is perfect for applications that need a single data source</li>
  <li> Elastic pool: Collection of Single databases with a shared set of resources such as CPU or memory</li>
  <li> Managed instance: A set of databases that can be used together, easy migration of on-premis databases</li>
</ul>

<b> Understanding Elastic pool</b> 
 <p> Elastic pools are a simple, cost-effective solution for managing and scaling multiple databases that have varying and unpredictable usage demands. The databases in an elastic pool are on a single Azure SQL Database server and share a set number of resrouces as a set price. Elastic pools enables developers to optimize the price performance fo a group of databases within a prediscribed budget. Prevents over-provisioning or under-provisioning of resources. Elastic pool is not for every scenario however. The pools are well suited for multiple databases with specific utilization patterns. This pattern is low average utilization with infrequent utilization spikes. </p> 

<p>
Imagen we only have Azure SQL Database Single Database option available to us and we have 4 databases. We do know that each of these databases needs 20 DTUs (20,20,20,20 => 80 DTUs). Another scenario is when we have 4 other databases (10,40,40,20 => 110 DTUs) and two of these databases needs 40 DTUs for a short time at the peak of its usage. However, you don't know the exact time when the usage will peak. Having only Azure Database Single Instance we need to provision 110 DTUs for all these 4 databases, to accomidate database #2 & #3. We are overprovisioning since the databases only needs 40 DTUs for a short time. So now let's see how Azure SQL Database Elastic Pools can help in this scenario. The first thing you will do, is to create a elastic pool. You will than put all the 4 databases into this pool. You will assign a set amount of resources to the elastic pool (let's say 80 eDTUs). All these databases are going to share the resources.  </p>
  

<b> Understanding Azure SQL Database Managed Instance</b>
<p> The third deployment option, which is Managed Instance. Managed instances are a set of databases that can be used together, allows easy migration of on-premises databases. Managed instace is a deployment option of Azure SQL Database, providing near 100% compatibility with the latest SQL Server on-premises.This allows the existing SQL Server customer to lift and shift their on-premises applications with minimal changes. This deployment option provides a native virtual network implementation. Managed instance presvers all PaaS capabilities that reduces management overhead. The managed instance deployment option targets user scenarios with mass database migration from on-premises or IaaS database. Differences between SQL Server On-premises and Managed Instance (near 100% compatibility): High-availability is built in and pre-configured. For example, provisioning multiple database servers and put them in an availability set or behind load balancer (this is not the case for the managed instances, high availability is built in and pre-configured). Using SQL server, you can specify full physical paths to back up files or other entities, which is not supported Azure SQL Database (because the underlying SQL Server hosting the database is abstraced out from the user). In Microsoft SQL Server you can use Windows authentication which is not the case for managed instance, isntead you can use Azure Active Directory identification. Also, the XTP filegroups and in-memory OLTP (online transaction processing) objects are automatically managed. Finally you can't use SSIS (SQL Server Integration Service) with Azure SQL Database. Instead you should use Azure Data Factory (ADF) which can run SSIS packages. </p>

<p> You have two options to migrate your on premises database to manage instance. Back up and restor, which creates backup files and places them in Azure Blob Storage. Than these backups can be stored into a manged instace using T-SQL RESTORE command. The other option is to use Azure Data Migration Service (ADMS). This is a fully managed service enabling easy migrations from SQL Server databases to Azure Data platforms, including Azure SQL database. Managed Instance also offers different service tiers.</p>

   <p><b>Why move to Azure SQL Database</b>: Reduces the amount of time needed for admin. For many businesses, moving to a cloud service is about offloading complexity of administration. You can continue to administer your database, but no need to manage the DB Enginge, OS, or hardware. You can manage logins, index, and query tuning, auditing security and high availability. </p>
   
   <p> <b>How are resources assigned to various deployment options to Azure database?</b> In a single database, each database gets its own guaranteed compute, memory and storage. In the elastic pool, there is a fixed amount of resources that will be shared by all databases in the pool. In managed instance each instance has its guaranteed resources. </p>
   
   <p> <b>Resource purchasing models</b>: 
<ul>	<li> <b>DTU-based</b> (guarantess a certain level of compute, storage and I/O resources). You assign a bundle of resources to the Azure SQL database, you can not adjust individual resources such as compute and memory. </li>
	<li>	The other purchasing model is the <b>vCore-based</b> purchasing model. This purchasing model gives you the option to choose between generations of hardware, number of cores, memory and storage size. </li></ul></p>
   
  <p> <i>DTU: A database transaction unit represents a blend of measure of CPU, memory, reads, and writes. </i> </p>
  
  | vCore-based        | DTU-based       |
| ------------- |:-------------:|
| For single database, elastic pool and managed instance     | Only for single database and elastic pool  |
| Best for customers who need flexibility, control and transparency     | Best for customers who want simple, preconfigured resource options      |
| Strightforward way to translate on-premises workload to the cloud | Might need to calculate the needed DTUs before migration       |
| Microsoft recommends vCore-based model | If the DTU-based purchasing model meets your performance and business reqirements, you should continue using it       |
    
  <p> If your single database or elastic pool consumes more than 300 DTUs, converting to the vCore-based model might reduce your costs. You can convert to vCore-based model by using your API of choice or by using the Azure portal, with no downtime. Azure SQL Database managed instance only supports vCore-based purchasing model. </p>
  
  <b> Options for Azure SQL Database </b>
  <ul>
	<p> <li>First you choose deployment options (single database, elastic pool, managed instance) </li>
	<li>Then you choose purchasing models (DTU-based, vCore-based) </li>
	<li>Then you choose Service tiers (general purpose/standard, business critical/premium, hyperscale). </li> </p>
</ul>
<ul>
<b>Different Service tiers</b>
<p>
	<li>General purpose / standard: is designed for most generic workloads, 99,99% SLA, 5-10 ms storage latency. </li>
	<li>Business Critical / Premium: For applications requiring low-latency, 99,99% SLA, 1.2 ms storage latency.  </li>
	<li>Hyperscale: Is primarly intended for customers who have large databases, up to 100 TB (vCore only). </li> </p>
</ul> 
    
<p> <b>Securing Azure SQL Database </b></p>
<ul>
	<li> Network security </li>
 <p> Your Azure SQL Database instance is managed by logical Azure SQL Server. You can defined firewall rules on these server. This way you can grant access to databases based on the originating IP address of each request. Also, Azure SQL Database firewall enables you to only accept requests originated from subnets inside the virtual network. </p> 
  <li> Access management</li>
  <p> Azure SQL Database supports SQL authentication. You can define DB username and password (like normal) and use them in your client application to connect to the database. Azure SQL Database also supports Azure active directory authentication, so you can use Azure active identity to connect to the database. Azure SQL Database supports row level security aswell. That is, you can control access to rows in a table based on the role of the user.</p>
  <li> Threat protection</li>
  <p> SQL auditing in Azure Monitor logs and Event Hubs tracks database activites and helps maintaining compliance with security standards. You can also utilize Advanced Threat Protection to analyze your SQL Server logs to detect unusual behaviour and potentially harmful attempts. </p>
  <li> Information protection and encryption </li>
  <p> First of all, the data in transit is always encrypted using Transport Layer Security (TLS). Also transparent data encryption is available, which encrypts the raw files, such as database files and backup files on Azure servers, this way your data is protected from offline access, incase the database files are compromised. Dynamic data masking protects sensitive data (credit card numbers, sallaries) by masking it for non-priviledged users. Any non-priviledged user trying to query this data will see the masked version of the data. Always Encrypted protects data from high privileged, unauthorized users such as database admins. Finally, all the encryptions keys are stored in Azure Key Vault and are protected from unauthorized access. </p>
 </ul>
 
 <hr>
 
 <h3> Demo: Provisioning an Azure SQL Database single database </h3>
 
 <p> We managed to connect to this Azure SQL Database using the administrator user. Using the database administrator user with a full set of permissions might not be a good idea. Because this user have administrator access over the database, so it's not wise to give this username and password to any client. The right approach would be to create a few database users and provide my client applications with those users. Click on Security => Logins => let's go ahead and create a new login. RIght click, new login =>
<pre> CREATE LOGIN appuser
          WITH PASSWORD ='12345xwqsxws'
      GO </pre> </p>
 <p> Now let's create a user which uses this login. Click on Security, right click on user and click on new user. 
<pre> CREATE USER user01
          FOR LOGIN appuser
      GO </pre></p>
<p> This user will have no permission. Let's add user to the dbowner role (See options, Roles => Database Roles) for the single one database. </p>     
<pre> EXEC sp_addrolemember N'db_owner', N'user01'
      GO
</pre>
<p> Now connect with new user  </p>

<p> Demo: Provisioning Azure SQL Elastic Pools </p>
<p> Create multiple Azure SQL Database Single Databases and than add them to a new elastic pool. We only need one server. Create a resource => SQL Elastic database pool => Create. Place Elastic pool inside same resource group. Which logical server do I want to put my elastic pool in? When you have created the resource you are ready to add the databases to the pool. Let's click on configure. Here you can change the amoungt of resources you assigne to the elastic pool. Let's click on databases, here you have the option to create databases which will be added to the pool. Let's choose the databases and click apply. Now it should say Elastic General Purpose for the pricing tier. </p>

<p> Scaling: Could be single database or elastic pool. Click on database => Pricing tier </p>
  
<p> Provisioning an Azure SQL Database managed. Already prepared an Azure SQL Database Managed Instance since the provisioning can take hours. </p>

<p> The first step is to create a virtual machinea and the next step is to connect to the virtual machine using RDP (Remote Desktop Protocol). Third step is to run SQL Server Management Studio from within the virtual machine and connect to the managed instance.</p>

<b> Configuring Data Backup </b>

<p> Azure SQL Database takes automatic back-up and stores them. If you previously worked with Microsoft SQL Server you probably know that we have three kind of back-ups: Full, differential, and transaction log backups. </p>

<p> Azure SQL Database automatically creates the database backups that are kept between 7-35 days. Full backup: Azure backs up the entire database. Differential back up: which captures only the data that has changed since the last full backup. Transaction log back up: Records of all the committed and uncommitted transactions. Full backup: Taken every week, Differential backup: Taken every 12 hours, Transaction log backup: Taken every 5-10 minutes. These backups are stored in Azure read-access geo-redundant (RA-GRS) standard blob storage by default. This means your backup are stored in two seperate regions (?), which the second region is a read only region. All backups are automatically encrypted at rest using Transparent Data Encryption (TDE), blob torage is also protected.  </p>

<p> In turn of retention period, there are two types of backups. Point in time (7-35 days), you can use this backup to retore your database to an exact point in time. This is because all three type of backups, full backup, differential and transaction logs are keept. You might need to keep your backup for more than 3 days for compliance reasons. In that case, you can use long-term retention (up to 10 years). You can't disable point in time backups, you can only configure the retention period which is between 7-35 days. All Azure SQL databases (single, pooled, managed instance) have a default backup retention period of 7 days). If you delete a database, Azure SQL Database will keep the bakcups in the same way it would for an online database. LTR is not yet available for databases in Managed Instances. Instead you can use SQL Agent jobs to schedule copy-only database backups as an alternative to LTR (beyond 35 days). </p>

<p> Usage of backups. You can restore an existing database to a point-in-time in the past. You can restore a deleted datbase to the time it was delete. You can restore a database to another geographical region. Note, if you delete an Azure SQL server, all elastic pools and databases that belong to that server are also deleted and cannot be restored. If you delete the parent logical server there is no way to restore. Restore time is impacted by size of the database, amount of activity that needs to be replayed, what service tier, network bandwidth, number of transaction etc. Might take several hours. </p>

<b> Demo: restoring an Azure SQL instance </b>
<p> Configure backup period: SQL database => click on server name => click on manage backups (under settings) => configure retention. Restore Database: => Sql databases => Restore => The restore will create a new database (you can't overwrite). Restore deleted databases: Under settings click on deleted databases </p>

<p> LTR backups: Database => Configure retention => How long would I like to keep the weekly backup... </p>

<p> Configure Elastic Database jobs </p>

<p> Scheduling technologies in Azure SQL Database: Elastic Database Jobs, SQL Agent Jobs. Database Scheduled jobs can be periodically executed against one or many databases to run T-SQL quereis and perform maintenance tasks. A few use cases are for management task to run after hours (for example you can deploy schema changes or credentials management, you can also use them to update or load data from Azure Blob storage, collect query results from a set of databases in an on-going basis, rebuild indexes to imrpove query performance) collect data for reporting (aggregate data from a collection of Azure SQL databases into a single destination, execute long-running data pro data processing queries across a large set of databases), data movements (replicate changes made in your databases to other databases, load data from or to your databases using SQL Server Integration Services (SSIS) </p>

<p> Scheduling technologies in Azure: Azure Automation (runbooks), Azure Functions (using timer trigger), Azure Logic Apps, Azure Scheduler, Elastic Database jobs and SQL Agent Jobs. </p>

<p> Elastic Database Job is a native Azure SQL Database service that executes custom jobs on one or many Azure SQL Databases, in an interval. This concept is very similar to SQL server jobs.  </p>

<ul> 
  <p> SQL agent : Elastic job</p>
  <li> Any individual database in the same SQL Server instance as the SQL agent : Targets can be in different SQL Database servers, subscriptions, and/or regions</li>
  <li> T-SQL, SQL Server Management Studio (SSMS) : Single databases, data warehouses, pool, SQL Server, or shardmap</li>
  <li> : Portal, Azure Resource Manager, PowerShell, T-SQL </li>
</ul>

<p> Elastic jobs are available for single and pooled instances. Agent jobs can be used for Managed Instance. In other words, elastic jobs are not available for managed instance at the time. Elastic database jobs provide the ability to run one or more T-SQL scripts in parallel, across many databases, on a schedule or on demand. Elastic database can target single and pooled databases, also SQL Server and shardmap are supported. Let's take a look at elastic job components. The first component is the elastic job agent. This is the process responsible to execute the job against the target database. To be able to create a job agent you should have an clean,empty and existing database. Which will be configured as a job database. The job defenitions and execution history will be saved inside the job database. After you have defined the job, the agent will execute the job on the targets. In the target group you can have individual databases, SQL Server, Elastic Pool, Data Warehouse as part of your target group. The status and job execution will be saved inside the job database (a unique database to the job agent?). If your job has an output, you can configure an output database and the job agent is going to write the job output into the output database. </p>

<ul>
  <p> Elastic Job Components </p>
  <li> Job Agent </li>
  <p> Is the Azure resource for creating, running and managing jobs. Requires an existing clean SQL database (job Database). The Elastic job agent is free, but you will pay for the resources used as part of the execution</p>
  <li> Job Database</li>
  <p> The Job database is used for defining jobs and tracking the status and history of job executions. The job database is also used to store agent metadata, logs, results, job definitions, and contains many useful stored procedures. </p>
  <li> Target Group </li>
  <p> You can have Azure SQL Database logical server </p>
  <li> Job </li>
  <p> </p>
</ul>

<b> Demo: Creating and running an Elastic Database Job </b>

<p> Create two databases, the first one is the job database and the second one is the target database which we will run a job against. Click on SQL Databases, Click on add, the database should be clean and empty (database has to be S0,
standard) Next step is to create a target database (put them in the same resource group). Create a new logical server for the target database, point the job to the logical server that is hosting the target database (?). The target database can both be empty and populated, and it can be any user database. Login to Microsoft SQL Server Management Studio; and login to the job datbase (requried to whitelist your ip address). Now let's go ahead and create and elastic job agen,
 choose an empty database as our job database. Let's connect to our job database again and see if anything has changed. We now have a bunch of stored procedures created. All these database objects are needed by elastic job agents, so it can run jobs against the target database.

<b> Demo: Creating and running an Elastic Database Job </b>
<p> In our scenario we are going to run job against a single database. This will be done with the help of t-SQL. In this case we need to configure 3 databases, the job db, the master db, the target server and the target db. However, if you
 are running your job against multiple database you need to follow this step on every target database. To get started, open SSMS. The first step is to create a few credentials in the job database. The elastic job agent is going to use
credentials to run commands against the target database. Click jobdb01 and new query. In the first step we need to create a master create and to specifiy a password. And then we need to create two identities. The first identity will be
used to execute the job on the target database. The second credential will be used to connect to the target master db. 

<pre> 
REATE MASTER KEY ENCRYPTION BY PASSWORD='Britney123';

CREATE DATABASE SCOPED CREDENTIAL myjobcred WITH IDENTITY = 'jobcred',
	SECRET = 'Britney123';
GO

CREATE DATABASE SCOPED CREDENTIAL mymastercred WITH IDENTITY = 'mastercred',
	SECRET = 'Britney123';
GO

------------------

EXEC jobs.sp_add_target_group 'ServerGroup1'

EXEC jobs.sp_add_target_group_member
'ServerGroup1',
@target_type = 'SqlServer',
@refresh_credential_name='mymastercred',
@server_name='mlatargetserver.database.windows.net'


--------------

EXEC jobs.sp_add_job @job_name='CreateTableTest', @description='Crete Table Test' 

EXEC jobs.sp_add_jobstep @job_name='CreateTableTest',
@command=N'IF NOT EXISTS (SELECT * FROM sys.tables
			WHERE object_id = object_id(''Test''))
CREATE TABLE [dbo].[Test]([TestId] [int] NOT NULL);',
@credential_name='myjobcred',
@target_group_name='ServerGroup1'

EXEC jobs.sp_start_job 'CreateTableTest'

SELECT * FROM jobs.job_executions
WHERE is_active = 1 AND job_name = 'CreateTableTest'
ORDER BY start_time DESC
GO

EXEC jobs.sp_stop_job ''
</pre>

<p> configure master database on server </p>

<pre> CREATE LOGIN mastercred WITH PASSWORD ='Britney123'
CREATE USER mastercred FROM LOGIN mastercred

CREATE LOGIN jobcred WITH PASSWORD ='Britney123' </pre>

<p> In the last step, we need to go ahead and configure all the target databases. In our case, only one database. </p>

<pre> CREATE USER jobcred FROM LOGIN jobcred

GRANT ALTER ON SCHEMA::dbo TO jobcred
GRANT CREATE TABLE TO jobcred </pre>

REATE MASTER KEY ENCRYPTION BY PASSWORD='Britney123';

CREATE DATABASE SCOPED CREDENTIAL myjobcred WITH IDENTITY = 'jobcred',
	SECRET = 'Britney123';
GO

CREATE DATABASE SCOPED CREDENTIAL mymastercred WITH IDENTITY = 'mastercred',
	SECRET = 'Britney123';
GO

------------------

EXEC jobs.sp_add_target_group 'ServerGroup1'

EXEC jobs.sp_add_target_group_member
'ServerGroup1',
@target_type = 'SqlServer',
@refresh_credential_name='mymastercred',
@server_name='mlatargetserver.database.windows.net'


--------------

EXEC jobs.sp_add_job @job_name='CreateTableTest', @description='Crete Table Test' 

EXEC jobs.sp_add_jobstep @job_name='CreateTableTest',
@command=N'IF NOT EXISTS (SELECT * FROM sys.tables
			WHERE object_id = object_id(''Test''))
CREATE TABLE [dbo].[Test]([TestId] [int] NOT NULL);',
@credential_name='myjobcred',
@target_group_name='ServerGroup1'

EXEC jobs.sp_start_job 'CreateTableTest'

SELECT * FROM jobs.job_executions
WHERE is_active = 1 AND job_name = 'CreateTableTest'
ORDER BY start_time DESC
GO

EXEC jobs.sp_stop_job ''
</pre>

<p> configure master database on server </p>

<pre> CREATE LOGIN mastercred WITH PASSWORD ='Britney123'
CREATE USER mastercred FROM LOGIN mastercred

CREATE LOGIN jobcred WITH PASSWORD ='Britney123' </pre>

<p> In the last step, we need to go ahead and configure all the target databases. In our case, only one database. </p>

<pre> CREATE USER jobcred FROM LOGIN jobcred

GRANT ALTER ON SCHEMA::dbo TO jobcred
GRANT CREATE TABLE TO jobcred </pre>

<p> Configure SQL Agent Jobs </p>

<p> Introducing SQL Agent jobs for managed instaces (you can use Elastic Database Jobs). SQL Agent Jobs are series of T-SQL scripts to run against your database. SQL Agent jobs can be used to run administrative tasks, one or more
times, these jobs can be monitored for success or failure. A job can run on one local server or on multiple remote servers. A job is an internal database engine component that is executed within the managed instance service. SQL Agent jobs are not available for single and pooled instances, use Elastic jobs for those instances. The are three job components to SQL Agent Jobs. Job step, a job is a set of one or many steps that should be executed. Schedule, when the job should be executed. Notification, define rules that will be used to notify operators via emails once the job completes. A job step is a sequences of actions that SQL Agent should execute. For each job step, you can define retry strategy and action when the step succeeds or fails. There are several job step types you can choose from. For example, T-SQL OS command, PowerShell, SSIS. You can also use replication steps to publish changes to other databases. The schedule specifies when
a job runs, it could be very day or every other day etc. Multiple jobs can run on the same schedule, multiple scheduels can apply to the same jobs. You can also schedule a job to execute whenever the managed instance is restarted.
A job can run on time or under recurring schedule. SQL Agent jobs enable you to get notifications when the job finishes successfully or fail. You can receive notifcation via email. SQL Agent settings are read only, procedure
sp_set_agent_properties is not supported. Disabling Agent is currently not supported in Managed Instance, SQL Agent is always running. Pager, NetSend and alters are not supported (only emails). </p>

<b> Create a SQL Agent job in a managed instance </b>

<p> Create an Azure SQL Database Managed Instance and a VM (use as a Jumpbox). We are going to use the JumpBox virtual machine to connect to our Managed Instance and create an SQL agent job. Connect => Download the RDP (Remote Dekstop). Inside the VM open SSMS and connect to the instance. Scroll down, and expandSQL Server Agent, click on jobs. Right click, click new job. Click on general and add description. Click on Steps, New, Step Name, Target Database (Database)....
In schedueles you can add scheduels.. Fill in everything. To run manually right click on job, and pick start job. Now let's go a head and configure email registration for our job (each thime job runs, email trigger). Before we do this we
need to configre the database mail: Click on Management folder,  rightclik on database mail and choose Configure Database Mail. Next => Configure a mail account (go with the first option), Create a new e-mail profile and specify its
SMTP accounts (Send email from printer, scanner, or app. If you are using SSL (Secure Sockets Layer) firewall needs to open port 587. Go to Network Security group. Click on outbound security rules and make sure the outgoing port 587 is
 allowed. Name your profile AzureManagedInstance_dbmail_profile. You can right-click on the Database Mail and send a test email. Now let's configure our agent to send notificaitons. Before doing that, I need to define an operator. An operator could be a database administrator who needs to be notified on agent jobs. Right click on Operators and click new operator. Now letäs dubbelclick on Jobs, click on notifcaiton and click on e-mail, and choose other operator from the
dropdown. </p>

---

<p> Managing Data Synchronization between Azure and SQL Server On-premises</p>

<p> Do you need to sync data between multiple databases? SQL Data Sync is an Azure SQL Database service that lets you syncrhonize the data bi-directionally across multiple SQL databases and SQL Server instances. Data sync is useful
when data needs to be kept up-to-date across several Azure SQL databases or SQL Server databases. Why would you like to have multiple databases with the same schema etc? One of the scenarios is a hybrid data syncrhonization (sync you
on-premises and Azure SQL databases). Also distributed applications can benefit from this scenario (you can have separate different workloads across multiple identical databases. This scenario also works good for globally distributed 
applications. You can easily sync databases in regions around the world. Do <b> not </b> use Data sync for disaster recovery (use Azure geo-redundant backups). Also if you need multiple versions of the same database and you will only
write to one of these databases you should not go with SQL Data Sync, you can use read-only replicas instead. SQL Data Sync is not that good for ETL, use Azure Data Factory or SSIS instead. Its also not a migration tool (use Azure Database Migration Service instead. 

Let's take alook at the Data Sync building blocks. A Sync Group is a group of databases that you want to synchronize. You define one of the databases in the sync group as the Hub Database. The rest of the databases are member databases.
The Sync occures only between the Hub and individual members. The Sync Schema describes which data is being synchronized. The Sync Direction can be bi-directional or can flow in only one direction (if I go with bi-directional any update I
do in Hub effect the members and vice versa) in directon (only from hub to members). The Sync Interval describes how often synchronization occurs. And finally, each time you merge data between databases you need to think about
the Conflic Resolution Policy. The Conflic Resolution Policy in a Data Sync, specifies what should be done incase an conflict happends between the hub database and member databases. You can make the Hub Data overwrite Member database or
versa. The Hub database needs to be an Azure SQL Database (you can not have SQL Server on premise as a Hub). A Sync database is created automatically by Azure, and keeps the meta data for your Sync job. To recap: Both the Hub and
the Sync database must be an Azure SQL Database. Both Hub and Sync databases should be in the same region. The member databases can be either SQL Databases, on-premises SQL Server databases, or SQL Server instances
on Azure VMs. If you're using an on-premiseds database as a member database, you must install and configure a local sync agent. Since Data Sync is triggerr-based, transactional consistency is not guaranteed. Microsoft
guarantees that all changes are made eventually, and that Data Sync does not cause data loss. Data Sync uses insert, update, and delete triggers to track changes. It creates side tables in the user database for change tracking.
These change tracking activities have an impact on your database workload. It's important to asses your service tier and upgrade if needed. </p>

<p> There are a few requirements for Data Sync. Each table must have a primary key. Don't change the value of the primary key in any row. Snapshot isolation must be enabled. A table cannot have an identity column that is not the primary
key. Tables with same name but different schema are not supported. Columns with User Defined Data Types are not supported. Currently, Azure SQL DAta Sync does not support Azure SQL Database Managed Instance. </p>

<b> Setting up SQL Data Sync between two Azure SQL Database single instance </b>

<p> Start with creating an Hub database (use standard db, and sample data). Let's also create a member database (let's use same RG, configure with DTU model, use sample database so schema is same?). Now click on the hub database
and make sure client ip is added to the server firewall. Do the same thing for the member database. Now let's start SSMS and connect to our hub database. Let's update a row in the customer table, after that we will run Data Sync
(which checks for change tracking, update, insert, etc) and make sure this update is reflected in the member database.

<pre> UPDATE SalesLT.Customer SET FirstName = 'Reza', LastName = 'Salehi' WHERE CustomerID = 1 </pre>

<p> Now let's go back tu Azure portal and setup Data Sync. Make sure you are in the hub database, scroll down, click
on sync to other databases, click on new sync group, crete a new database for the sync metadata database, while 
configuring make sure we pick the same logical server as the hub database (not a requirement, the only requirement is for the databases to be in same region). You have the option to setup automatic sync, so right after your data sync
is created it is going to start synchronizing based on the schedule you provide. Conflic resolution (Hub win / member win) what happends when a conflict happends. After deployment of the Sync Group is finished, I need to put the
user credentials of my hub database. In the next step I need to configure the member database (choose same logical
server). In the last step of our wizard, we need to choose which tables we want to be synced. We also need to allow 
Azure services and resources to access this server for all databases (same place as firewall settings)


 

---
  
  <h3> Notes </h3>
  
 <p> Remote Desktop Protocol is a proprietary protocol (a communications protocol owned by a single organization or individual) developed by Microsoft, which provides a user with a graphical interface to connect to another computer over a network connection. </p>
  
 <p> A communication protocal is a system of rule that allow two or more entities of a communications system to transmit information via any kind of variation of a physical quantity. Protocal are to communcations wat programming languages are to computations. 
  
  <p> 
Virtual Networking: is primary used for cloud. A virtual network is software based. It is part of a LAN or WAN that has been sectioned off. Virtual networks can have their own security, encryption, login credentials etc.

The physical underlay is the physical infrastructure, physical computers, physical routers, physical switches. Using this physical infrastructure with some specific software enables the virtual network (also called the overlay). </p>
  
  <p> vCPUs (virtual CPUs), Physical CPUs, Cores </p>
  
  <p> It's from the server we receive compute power. Your primary compute power is from the processor (we also have RAM and cache). A quad processing server, within this server there are 4 physical CPUs. In more modern times, we also have a cores within that physical CPU. Let's say we have 4 cores within the CPU chip. Within those cores, typically in a cloud environment, we put vCPUs. x Cores = x vCPU.</p>
  
<p> Let's say you want to buy an intel core i7 8 core CPU. In this case, that CPU would have 4 physical cores and 4 more virtual cores (total 8 logical cores). The 4 physical cores has hyper threading, each core can accepts two threads (this is how you get extra cores).    </p>
  
<p> Transparent Data Encryption </p>
<p> TDE is used to protect data at rest. Master Key is stored in an external storage (outside the database called keystore)</p>

<p> SQL Server and Database Encryption Keys </p>

<p> SQL Server uses encryption keys to help secure data, credentials and connection information that is stored in a server database. SQL Server has two kinds of keys, symmetric and asymmetric. Symmetric keys use the same password
to encrypt and decrypt data. Asymmetric keys use one password to encrypt data (called the public key) and another to decrypt data (called the private key).

SQL Server has two primary applications for keys: a service master key (SMK) generated on and for a SQL Server instance, and a database master key (DMK) used for a database.

The Service Master Key is the root of the SQL Server encryption hierarchy. The SMK is automatically generated the first time the SQL Server instance is started and is used to encrypt a linked server password, credentials, and the
database master key. The SMK is encrypted by using the local machine key using the Windows Data Protection API (DPAIP). TThe service master key can only be decrypted by the service account under which it was created or by
principal that has access to the machine's credentials.

The database master key is a symmetric key that is used to protect the private keys of certificates and asymmetric keys that are present in the database. It can also be used to encrypt data, but it has length limitations that make
it less practical for data than using a symmetric key. To enable the automatic decryption of the database master key, a copy of the key is encrypted by using the SMK. It is stored in both the database where it is used and in the master
system database. 


<p> SQL Server Change Tracking (CT) </p>
<p> SSQL Server Change Tracking, also known as CT, is a lightweight tracking mechanism, introduced the first time in SQL Server 2008, that can be used to track the DML (Data Manipulation Language, insert, update, delete) changes peformed in SQL Server database tables. SQL Change Tracking can be configured in all SQL Server editions, including the free Express edition. 
