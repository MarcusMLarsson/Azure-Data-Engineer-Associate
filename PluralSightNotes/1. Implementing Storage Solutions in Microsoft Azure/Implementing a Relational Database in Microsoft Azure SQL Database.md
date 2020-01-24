
<h1> Implementing a Relational Database in Microsoft Azure SQL Database </h1>

---

<ul>
  <p> Azure SQL Database deployment options</p>
  <li> Single database: Isolated database that is perfect for applciations that need a single data source</li>
  <li> Elastic pool: Collection of Single databases with a shared set of resources such as CPU or memory</li>
  <li> Managed instance: A set of databases that can be used together, easy migration of on-premises databases</li>
</ul>

<p> Imagen you have a server which talks to a SQL server database inthe back end. In the old days, before the cloud, you would get the server either on-premises or in your data center and install SQL Server on that box. You were responsible to configre the networking, the security, operating system patching, and the performance and scaling of your SQL server. Azure gives you two options to run SQL server-based workloads. The first option, which is the main focus of this course, is Azure SQL Database (DBaas).   The other option is to provision a SQL Server installation on an Azure virtual machine. This is a SQL Server inside a fully managed virtual machine in Azure. You still don't need to worry about the physical machine. However, it's still a virtual machine so you need to manage the instance of SQL Server manually. How do you choose between the two? Do you want to manually manage your database engine, apply patches, take backups, or delegate these operations to Azure?  </p>

<p> SQL Server on Azure VMs: is an Infrastructure-as-a-Service (IaaS) offering and allows you to run SQL Server inside a fully-managed VM in Azure. This is a good option for migrating on-premises SQL Server databases and applications without any database change. The SQL Server insallted on the VM is identical to the SQL Server you have installed on-premises. Also, the IaaS option gives you full control over the database engine. You could control the timing of maintenance and patching of your database engine. You could also pause or stop the virtual machine whenever you don't need the SQL database to save some costs.  </p>

<p> Azure SQL Database: A relational database-as-a-service (DBaaS) hosted in Azure, this is a platform-as-a-service (PaaS) offering. Has additional features that are not availaible in SQL Server, such as built-in high availability, intelligence, and manaagement. Pay-as-you-go with options to scale up or out for greater power (with no interruption). Has multiple deployment options and service tiers. </p>

<b> Benefits </b>
<ul>
  <p> SQL Server on VM : Azure SQL Database </p>
  <li>Up to 99.95% availaiblity : 99.99% availability guaranteed </li>
  <li>Full control over the SQL Server enginge : The most commonly used SQL Server features are available</li>
  <li>Full parity with the matching version of on-premises SQL Server : Built-in backups, patching, recovery</li>
  <li>Easy migration from SQL Server on-premises : Ability to assign necessary resources (CPU/storage) to individual databases</li>
  <li>Private IP address within Azure VNet : Built-in advanced intelligence and security</li>
  <li> : Online change of resources (CPU/storage) with no downtime</li>
  <ul>
    
   <b> Limitations </b> 
    <ul>
  <p> SQL Server on VM : Azure SQL Database </p>
  <li> Need to manually manage your backups and patches : Migration from SQL Server might be hard</li>
  <li> You need to implement your own high-availability solution : Some SQL Server features are not available</li>
  <li> There is a downtime while changing the resources (CPU/storage) : No guaranteed exact maintenance time (but nearly transparent) </li>
  <li>Need to implement additional mechanisms to ensure availability of your databases : Private IP address cannot be assigned (with exception) </li>
  <ul>
    
    
   <p> Why move to Azure SQL Database: Reduces the amount of time needed for admin. For many businesses, moving to a cloud service is about offloading complexity of administration. Continue t administer your database, but no need to manage the DB Enginge, OS, or hardware. You can manage logins, index, and query tuning, auditing security and high availability. </p>
   
   
   <p> How are resources assigned to various deployment options to Azure database? In a single database, each database gets its own guaranteed compute, memory and storage. In the elastic pool, there is a fixed amount of resources that will be shared by all databases in the pool. In managed instance each instance has its guaranteed resources. </p>
   
   <p> Resource purchasing models: DTU-based (guarantess a certain level of compute, storage and I/O resources). You assign a bundle of resources to the Azure SQL database, you can not adjust individual resources such as compute and memory. The other purchasing model is the vCore-based purchasing model. This purchasing model gives you the option to choose between generations of hardware, number of cores, memory and storage size. </p>
   
  <p> DTU: A database transaction unit represents a blend of measure of CPU, memory, reads, and writes.  </p>
  

    <ul>
  <p> vCore-based : DTU-based </p>
  <li> For single database, elastic pool and managed instance : Only for single database and elastic pool </li>
  <li> Best for customers who need flexibility, control and transparency : Best for customers who want simple, preconfigured resource options </li>
  <li> Strightforward way to translate on-premises workload to the cloud : Might need to calculate the needed DTUs before migration  </li>
  <li> Microsoft recommends vCore-based model : If the DTU-based purchasing model meets your performance and business reqirements, you should continue using it </li>
  <ul>
  
  <p> IF your single database or elastic pool consumes more than 300 DTUs, converting to the vCore-based model might reduce your costs. You can convert to vCore-based model by using your API of choice or by using the Azure portal, with no downtime. Azure SQL Database managed instance only supports vCore-based purchasing model. </p>
  
  <p> (Service tiers) General purpose / standard : is designed for most generic workloads, 99,99% SLA, 5-10 ms storage latency. Business Critical / Premium: For applications requiring low-latency, 99,99% SLA, 1.2 ms storage latency. Hyperscale: Is primarly intended for customers who have large databases, up to 100 TB (vCore only). </p>
  
  <p> First you choose deployment options (single database, elastic pool, managed instance)
  Then you choose purchasing models (DTU-based, vCore-based), than you choose Service tiers (general purpose/standard, business      critical/premium, hyperscale). </p>
  
  <b> Provisioning a SQL Server instance in a managed VM (IaaS scenario) </b>
  
  <p> Search for SQL server </p>
  
  
  <b> Provisioning a SQL Server instance in Azure SQL Database (PaaS scenario) </b>
   <p> Search for SQL Database </p>
    
    
 <p> SQL Datbase Elastic Pools </p>
 
 <p> Are a simple, cost-effective solution for managing and scaling multiple dataabases that have varying and unpredictable usage demands. Imagen we only have Azure SQL Database Single Database option available to us and we have 4 databases. We do know that each of these databases needs 20 DTUs (20,20,20,20 => 80 DTUs). Another scenario is when we have 4 other databases (10,40,40,20 => 110 DTUs) and two of these databases needs 40 DTUs for a short time at the peak of its usage. However, you don't know the exact time when the usage will peak. Having only Azure Database Single Instance we need to provision 110 DTUs for all these 4 databases, to accomidate database #2 & #3. We are overprovisioning since the databases only needs 40 DTUs for a short time. So now let's see how Azure SQL Database Elastic Pools can help in this scenario. The first thing you will do, is to create a elastic pool. You will than put all the 4 databases into this pool. You will assign a set amount of resources to the elastic pool (let's say 80 eDTUs). All these databases are going to share the resources.  </p>
  
<p> Azure SQL Database Elastic Pool is a cost-effective solution for managing and scaling multiple databases that have varying and unpredictable usage of demands. The databases in an elastic pool are on a single Azure SQL Database server and share a set number of resrouces as a set price. Enables developers to optimize the price performance fo a group of databases within a prediscribed budget. Prevents over-provisioning or under-provisioning of resources. Elastic pool is not for every scenario however. The pools are well suited for multiple databases with specific utilization patterns. This pattern is low average utilization with infrequent utilization spikes. </p>

<p> Securing Azure SQL Database </p>
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
 
 <p> Demo: Provisioning an Azure SQL Database single database </p>
 
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


<b> Understanding Azure SQL Database managed instance</b>
<p> The third deployment option, which is Managed Instance. Managed instances are a set of databases that can be used together, allows easy migration of on-premises databases. Managed instace is a deployment option of Azure SQL Database, providing near 100% compatibility with the latest SQL Server on-premises.This allows the existing SQL Server customer to lift and shift their on-premises applications with minimal changes. This deployment option provides a native virtual network implementation. Managed instance presvers all PaaS capabilities that reduces management overhead. The managed instance deployment option targets user scenarios with mass database migration from on-premises or IaaS database. Differences between SQL Server On-premises and Managed Instance (near 100% compatibility): High-availability is built in and pre-configured. For example, provisioning multiple database servers and put them in an availability set or behind load balancer (this is not the case for the managed instances, high availability is built in and pre-configured). Using SQL server, you can specify full physical paths to back up files or other entities, which is not supported Azure SQL Database (because the underlying SQL Server hosting the database is abstraced out from the user). In Microsoft SQL Server you can use Windows authentication which is not the case for managed instance, isntead you can use Azure Active Directory identification. Also, the XTP filegroups and in-memory OLTP (online transaction processing) objects are automatically managed. Finally you can't use SSIS (SQL Server Integration Service) with Azure SQL Database. Instead you should use Azure Data Factory (ADF) which can run SSIS packages. </p>

<p> You have two options to migrate your on premises database to manage instance. Back up and restor, which creates backup files and places them in Azure Blob Storage. Than these backups can be stored into a manged instace using T-SQL RESTORE command. The other option is to use Azure Data Migration Service (ADMS). This is a fully managed service enabling easy migrations from SQL Server databases to Azure Data platforms, including Azure SQL database. Managed Instance also offers different service tiers.</p>

<ul>
  <p> General purpose : Business Critical
  <li> 99.99% availability that enable you to independently select storage and compute : 99.99% availability and enable you to independently elect storage and compute</li>
  <li> Business applications with typical performance requirements : Business applications with highest performance requirements </li>
  <li> High-performance Azure BloB storage (8 TB) : Super-fast local SSD storage (up to 1 TB on Gen4 and up to 4 TB on Gen5</li>
    <li> Built in high-availability : Built-in high availability based on Always On Availability Groups</li>
    <li> : Additional read-only DB replica (for reporting or other read-only workloads) </li>
</ul>

<p> Managed Instance Management Operations: Instance creation, 90 % of clustured creations finishes in less than 4 hours. Instance update, 90 % of cluster expansions finish in less than 2.5 hours. Instance deletion, 90 % of  virtual cluster deletions finis in 1.5 hours. For the first instance in a subnet, deployment time is typically much longer than in subsequent instance. So the first time you are creating a managed instance, the deployment might take up to 6h.

<p> Managed Instance Security </p> 
<p> The managed instance deployment option combines advanced security features provided by Azure cloud and SQL Server Database Enginge. Azure SQL Database Security technologies include applies to all deployment options of Azure SQL databases, including managed instance. These security technologies are transparent data encryption (TDE), Threat detection, Row-level security, managed instance auditing, dynamic data masking, Azure AD Integration. Now let's talk about Managed Instance Advanced Security (unique for managed instance). So your managed instance is deployed into a virtual network, you can connect your on-premises environment to this virtual network; using VPN or express route. This gives your on-premises application a quick and secure way to communicate with Azure SQL Database managed instance. By default, the managed instance SQL endpoint is only exposed through a private IP address, allowing safe connectivity from private Azure or hybrid networks. Your Azure SQL Database Managed Instance is deployed to a single-tenant with dedicated underlying infrastructure (compute, storage)
  
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
