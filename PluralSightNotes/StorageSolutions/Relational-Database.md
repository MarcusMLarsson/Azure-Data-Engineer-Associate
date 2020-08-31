
<h1> Implementing a Relational Database in Microsoft Azure SQL Database </h1>
<p align="center"><img src="https://azurecomcdn.azureedge.net/cvt-44b6d935a36108a6094b09447175fe8029569450b1147a48cc44fbed5496ce82/images/page/services/sql-database/index/image-value-prop-1.png" width="1000"></p>
<p>  Azure gives you two options to run SQL server-based workloads. The first option, which is the main focus of this course, is Azure SQL Database (Paas). The other option is to provision a SQL Server installation on an Azure virtual machine. This is a SQL Server inside a fully managed virtual machine in Azure. You still don't need to worry about the physical machine. However, it's still a virtual machine so you need to manage the instance of SQL Server manually. H  </p>

<h3> IaaS vs PaaS vs SaaS </h3>
<p align="center"><img src="https://blogs.bmc.com/wp-content/uploads/2017/09/saas-vs-paas-vs-iaas-810x754.png"></p>
<ul>
	<li> Infrastructure as a service: IaaS delivers cloud computing infrastructure, including servers, network and storage, through virtualization technology (virtual machines). </li>
	<li> Platform as a service: PaaS allows businesses to design and create applications that are built into the PaaS with special software components. </li>
	<li> Service as a service: SaaS utilizes the internet to deliver applications, which are managed by a third-party vendor, to its users. </li>
</ul>


<h3> SQL Server on Azure VMs (IaaS) </h3>

<p>SQL Server on Azure VMs is an Infrastructure-as-a-Service (IaaS) offering and allows you to run SQL Server inside a fully-managed VM in Azure. This is a good option for migrating on-premises SQL Server databases and applications without any database change. The SQL Server installed on the VM is identical to the SQL Server you have installed on-premises. Also, the IaaS option gives you full control over the database engine. You could control the timing of maintenance and patching of your database engine. You could also pause or stop the virtual machine whenever you don't need the SQL database (to save some costs).  </p>

<p> <i> A database engine (or storage engine) is the underlying software component that a database management system (DBMS) uses to create, read, update and delete (CRUD) data from a database. </p> </i>

<h3> Azure SQL Database (PaaS)  </h3>
<p>Azure SQL Database is a relational database-as-a-service (PaaS) hosted in Azure, this is a platform-as-a-service (PaaS) offering. The database has additional features that are not availaible in SQL Server, such as built-in high availability, intelligence, and management. Pay-as-you-go with options to scale up or out for greater power (with no interruption). Has multiple deployment options and service tiers. </p>

<h3>SQL Server on Azure VMs (IaaS) vs  Azure SQL Database (PaaS) </h3>


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
  <p> There are 3 Azure SQL Database deployment options</p>
<p align="center"><img src="https://www.ebecs.com/wp-content/uploads/Azure-SQL-Database-graphic.png" width="800"></p>
<ul>
  <li> Single database: Isolated database that is perfect for applications that need a single data source</li>
  <li> Elastic pool: Collection of Single databases with a shared set of resources such as CPU or memory</li>
  <li> Managed instance: A set of databases that can be used together, easy migration of on-premis databases</li>
</ul>

<h3> Understanding Elastic pool</h3>
 <p> Elastic pools are a simple, cost-effective solution for managing and scaling multiple databases that have varying and unpredictable usage demands. The databases in an elastic pool are on a single Azure SQL Database server and share a set number of resources as a set price. Elastic pools enables developers to optimize the price performance for a group of databases within a prediscribed budget. Using Elastic pools prevents over-provisioning or under-provisioning of resources. Elastic pool is not for every scenario however. The pools are well suited for multiple databases with specific utilization patterns. This pattern is low average utilization with infrequent utilization spikes. </p> 

<p>
Imagen we only have Azure SQL Database Single Database option available to us and we have 4 databases. We do know that each of these databases needs 20 DTUs (20,20,20,20 => 80 DTUs). Another scenario is when we have 4 other databases (10,40,40,20 => 110 DTUs) and two of these databases needs 40 DTUs for a short time at the peak of its usage. However, you don't know the exact time when the usage will peak. Having only Azure Database Single Instance we need to provision 110 DTUs for all these 4 databases, to accomidate database #2 & #3. We are overprovisioning since the databases only needs 40 DTUs for a short time. So now let's see how Azure SQL Database Elastic Pools can help in this scenario. The first thing you will do, is to create an elastic pool. You will than put all the 4 databases into this pool. You will assign a set amount of resources to the elastic pool (let's say 80 eDTUs). All these databases are going to share the resources.  </p>
  

<h3> Understanding Azure SQL Database Managed Instance</h3>
<p> The third deployment option is Managed Instance. Managed instances are a set of databases that can be used together and allows easy migration of on-premises databases. Managed instance is a deployment option of Azure SQL Database, providing near 100% compatibility with the latest SQL Server on-premises. This allows the existing SQL Server customer to lift and shift their on-premises applications with minimal changes. This deployment option provides a native virtual network implementation. Managed instance preserves all PaaS capabilities that reduces management overhead. The managed instance deployment option targets user scenarios with mass database migration from on-premises or IaaS database. </p>

<b> Migrate options </b>
<p> You have two options to migrate your on premises database to manage instance. 
<ul> <li>Back up and restor, which creates backup files and places them in Azure Blob Storage. Than these backups can be stored into a manged instace using T-SQL RESTORE command. </li>
<li>The other option is to use Azure Data Migration Service (ADMS). This is a fully managed service enabling easy migrations from SQL Server databases to Azure Data platforms, including Azure SQL database. Managed Instance also offers different service tiers.</li> </ul></p>

<h3> Why move to Azure SQL Database </h3>
</p> By moving to Azure SQL Database you can reduce the amount of time needed for admin. For many businesses, moving to a cloud service is about offloading complexity of administration. You can continue to administer your database, but no need to manage the DB Enginge, OS, or hardware. You can manage logins, index, and query tuning, auditing security and high availability. </p>

<h3> How are resources assigned to various deployment options to Azure database? </h3>
<p>
<ul>
	<li> In a single database, each database gets its own guaranteed compute, memory and storage. </li>
<li>In the elastic pool, there is a fixed amount of resources that will be shared by all databases in the pool. </li> 
	<li> In managed instance each instance has its guaranteed resources. </li>
</ul>
</p>
<h3>Resource purchasing models </h3>
<p> 
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
  
<h3> Options for Azure SQL Database </h3>
  <ul>
	<p> <li>First you choose deployment options (single database, elastic pool, managed instance) </li>
	<li>Then you choose purchasing models (DTU-based, vCore-based) </li>
	<li>Then you choose Service tiers (general purpose/standard, business critical/premium, hyperscale). </li> </p>
</ul
	>
<h3>Different Service tiers</h3>
<ul>
<p>
	<li>General purpose / standard: is designed for most generic workloads, 99,99% SLA, 5-10 ms storage latency. </li>
	<li>Business Critical / Premium: For applications requiring low-latency, 99,995% SLA, 1.2 ms storage latency.  </li>
	<li>Hyperscale: Is primarly intended for customers who have large databases, up to 100 TB (vCore only). </li> </p>
</ul> 
    
<h3>Securing Azure SQL Database </h3>
<ul>
	<li> Network security </li>
 <p> Your Azure SQL Database instance is managed by logical Azure SQL Server. You can defined firewall rules on these server. This way you can grant access to databases based on the originating IP address of each request. Also, Azure SQL Database firewall enables you to only accept requests originated from subnets inside the virtual network. </p> 
  <li> Access management</li>
  <p> Azure SQL Database supports SQL authentication. You can define DB username and password (like normal) and use them in your client application to connect to the database. Azure SQL Database also supports Azure active directory authentication, so you can use Azure active identity to connect to the database. Azure SQL Database supports row level security aswell. That is, you can control access to rows in a table based on the role of the user.</p>
  <li> Threat protection</li>
  <p> SQL auditing in Azure Monitor logs and Event Hubs tracks database activites and helps maintaining compliance with security standards. You can also utilize Advanced Threat Protection to analyze your SQL Server logs to detect unusual behaviour and potentially harmful attempts. </p>
  <li> Information protection and encryption </li>
  <p> <ul>
	
<li> First of all, the data in transit is always encrypted using Transport Layer Security (TLS). TLS is a protocol for securing information between the client and the server. It is used in the HTTPS protocol, and TLS is what the S stands for in HTTPS. </li> 
<li>Transparent Data Encryption (often abbreviated to TDE) is a technology employed by Microsoft, IBM and Oracle to encrypt database files. TDE offers encryption at file level. TDE solves the problem of protecting data at rest, encrypting databases both on the hard drive and consequently on backup media. It does not protect data in transit nor data in use. </li>
<li> <p>Dynamic data masking protects sensitive data (credit card numbers, sallaries) by masking it for non-priviledged users. Any non-priviledged user trying to query this data will see the masked version of the data. SQL users excluded from masking - A set of SQL users or Azure AD identities that get unmasked data in the SQL query results. Users with administrator privileges are always excluded from masking, and see the original data without any mask. </p></li>
<li> <p>Always Encrypted is a feature designed to protect sensitive data, such as credit card numbers or national identification numbers (for example, U.S. social security numbers), stored in Azure SQL Database or SQL Server databases. Always Encrypted allows clients to encrypt sensitive data inside client applications and never reveal the encryption keys to the Database Engine (SQL Database or SQL Server). As a result, Always Encrypted provides a separation between those who own the data and can view it, and those who manage the data but should have no access. Always Encrypted provides <b>confidential computing capabilities </b> by enabling the Database Engine to process some queries on encrypted data, while preserving the confidentiality of the data and providing the above security benefits. Always Encrypted uses two types of keys: column encryption keys and column master keys. A column encryption key is used to encrypt data in an encrypted column. A column master key is a key-protecting key that encrypts one or more column encryption keys. The master key are stored in a external trusted key store, such as Azure Key Vault, Windows Certificate Store on a client machine, or a hardware security module. </p>

<p> The Database Engine never operates on plaintext data stored in encrypted columns, but it still supports some queries on encrypted data, depending on the encryption type for the column. Always Encrypted supports two types of encryption: randomized encryption and deterministic encryption. Deterministic encryption always generates the same encrypted value for any given plain text value. Using deterministic encryption allows point lookups, equality joins, grouping and indexing on encrypted columns. However, it may also allow unauthorized users to guess information about encrypted values by examining patterns in the encrypted column, especially if there's a small set of possible encrypted values, such as True/False, or North/South/East/West region. Randomized encryption uses a method that encrypts data in a less predictable manner. Randomized encryption is more secure, but prevents searching, grouping, indexing, and joining on encrypted columns.</p>

</li>
<li> Finally, all the encryptions keys are stored in Azure Key Vault and are protected from unauthorized access.  </li>
 </ul>
 </ul>
 
<h3> Configuring Data Backup </h3>

<p> Azure SQL Database takes automatic back-up and stores them. If you previously worked with Microsoft SQL Server you probably know that we have three kind of back-ups: Full, differential, and transaction log backups. </p>

<p> Azure SQL Database automatically creates the database backups that are kept between 7-35 days. 
<ul>	
	<li> Full backup (taken every week): Azure backs up the entire database. </li>
	<li> Differential back up (taken every 12 hours): which captures only the data that has changed since the last full backup. </li>
	<li> Transaction log back up (Taken every 5-10 minutes): Records of all the committed and uncommitted transactions. </li>
</ul>
</p>
<p> These backups are stored in Azure read-access geo-redundant (RA-GRS) standard blob storage by default. This means your backup are stored in two seperate regions (?), with the second region being a read only region. All backups are automatically encrypted at rest using Transparent Data Encryption (TDE), blob torage is also protected.  </p>

<p> In turn of retention period, there are two types of backups; Point in time (7-35 days) and long-term retention (up to 10 years). Point in time backup can be used to retores your database to an exact point in time. This is because all three type of backups, full backup, differential and transaction logs are keept. You might need to keep your backup for more than 35 days for compliance reasons. In that case, you can use long-term retention (up to 10 years). You can't disable point in time backups, you can only configure the retention period which is between 7-35 days. All Azure SQL databases (single, pooled, managed instance) have a default backup retention period of 7 days. If you delete a database, Azure SQL Database will keep the backups in the same way it would for an online database. LTR is not yet available for databases in Managed Instances. Instead you can use SQL Agent jobs to schedule copy-only database backups as an alternative to LTR (beyond 35 days). </p>

<p> Usage of backups. You can restore an existing database to a point-in-time in the past. You can restore a deleted datbase to the time it was delete. You can restore a database to another geographical region. Note, if you delete an Azure SQL server, all elastic pools and databases that belong to that server are also deleted and cannot be restored. If you delete the parent logical server there is no way to restore. Restore time is impacted by size of the database, amount of activity that needs to be replayed, what service tier, network bandwidth, number of transaction etc. Might take several hours. </p>


<h3> Role Based Access Control </h3>
<p> Azure role-based access control (Azure RBAC) is a system that provides fine-grained access management of Azure resources. Using Azure RBAC, you can segregate duties within your team and grant only the amount of access to users that they need to perform their jobs. Some of the most common rules are the following. </p>
<ul>
	<li>Owner: Full access to resources in Azure and can delegate access to other users.</li>
	<li>Contributor: Full Access to resources in Azure, but cannot delegate control.</li>
	<li>Reader: Can only view resources in Azure </li>
	<li>User access administrator: Granted permission to manage access to Azure resources </li>
</ul>
 
<h3> Scheduling technologies in Azure SQL Database </h3>

<p>Database Scheduled jobs can be periodically executed against one or many databases to run T-SQL quereis and perform maintenance tasks. A few use cases are for management task to run after hours. for example you can deploy schema changes or credentials management, you can also use them to update or load data from Azure Blob storage, collect query results from a set of databases in an on-going basis, rebuild indexes to improve query performance, collect data for reporting, load data from or to your databases using SQL Server Integration Services (SSIS) etc. Below the scheduling technologies for Azure are listed</p>

<ul> 
	<li> <b> Elastic Database Jobs </b></li>
	<li> <b>SQL Agent Jobs </b></li>
	<li> Azure Automation (runbooks) </li>
	<li> Azure Functions </li>
	<li> Azure Logic Apps </li>
	<li> Azure Scheduler </li>
</ul>

 <h3> SQL Elastic database job </h3>
Elastic database job executes custom jobs on one or many Azure databases in an interval. Elastic jobs are available for <b>single and pooled instances</b>. In other words, elastic jobs are not available for managed instance at the time. Elastic database jobs provide the ability to run one or more T-SQL scripts in parallel, across many databases, on a schedule or on demand. </p>


<ul>
  <p> Elastic Job Components </p>
  <li> Job Agent </li>
  <p> Is the Azure resource for creating, running and managing jobs. The Elastic job agent is free, but you will pay for the resources used as part of the execution</p>
  <li> Job Database (s0 required)</li>
  <p> The Job database is used for defining jobs and tracking the status and history of job executions. The job database is also used to store agent metadata, logs, results, job definitions, and contains many useful stored procedures. </p>
  <li> Target Group </li>
</ul>



 <h3> SQL agent job </h3>
 <p> SQL Agent jobs can be used for Managed Instance. 
 <p> While SQL elastic database jobs covers single and pooled instances, SQL agent job is designed for manage instances. </p>
 <p> SQL Agent job components </p>
 <ul>
	<li> A <b>Job step</b>: is a set of one or many stetps that should be executed</li>
	<li> <b>Schedule</b>: when the job should be executed</li>
	<li> <b>Notification</b>: Define rules that will be used to notify operators via emails once the job completes</li>
 </ul>
 
 
 
 <h3> SQL Data Sync </h3>


<p> Do you need to sync data between multiple databases? SQL Data Sync is an Azure SQL Database service that lets you syncrhonize the data bi-directionally across multiple SQL databases and SQL Server instances. Data sync is useful
when data needs to be kept up-to-date across several Azure SQL databases or SQL Server databases. Why would you like to have multiple databases with the same schema etc? One of the scenarios is a hybrid data syncrhonization (sync you
on-premises and Azure SQL databases). Also distributed applications can benefit from this scenario (you can have separate different workloads across multiple identical databases. You can easily sync databases in regions around the world. Do <b> not </b> use Data sync for disaster recovery (use Azure geo-redundant backups). Also if you need multiple versions of the same database and you will only
write to one of these databases you should not go with SQL Data Sync, you can use read-only replicas instead. SQL Data Sync is not that good for ETL, use Azure Data Factory or SSIS instead. Its also not a migration tool (use Azure Database Migration Service instead). 


<b>SQL Sync building blocks </b>
<ul>
<li> Sync group is a group of databases that you want to syncrhonize. </li>
<li> Define one of the databases in the sync group as the Hub database </li>
<li> The rest of the databases are member databases </li>
<li> The sync occurs only between the Hub and individual members </li>
</ul>

Let's take alook at the Data Sync building blocks. A Sync Group is a group of databases that you want to synchronize. You define one of the databases in the sync group as the Hub Database. The rest of the databases are member databases.
The Sync occures only between the Hub and individual members. The Sync Schema describes which data is being synchronized. The Sync Direction can be bi-directional or can flow in only one direction (if I go with bi-directional any update I
do in Hub effect the members and vice versa) in directon (only from hub to members). The Sync Interval describes how often synchronization occurs. And finally, each time you merge data between databases you need to think about the Conflic Resolution Policy. The Conflic Resolution Policy in a Data Sync, specifies what should be done incase an conflict happends between the hub database and member databases. You can make the Hub Data overwrite Member database or
versa. The Hub database needs to be an Azure SQL Database (you can not have SQL Server on premise as a Hub). A Sync database is created automatically by Azure, and keeps the meta data for your Sync job. To recap: Both the Hub and
the Sync database must be an Azure SQL Database. Both Hub and Sync databases should be in the same region. The member databases can be either SQL Databases, on-premises SQL Server databases, or SQL Server instances
on Azure VMs. If you're using an on-premiseds database as a member database, you must install and configure a local sync agent. Since Data Sync is triggered-based, transactional consistency is not guaranteed. Microsoft
guarantees that all changes are made eventually, and that Data Sync does not cause data loss. 

<p> There are a few requirements for Data Sync. Each table must have a primary key. Don't change the value of the primary key in any row. Snapshot isolation must be enabled. A table cannot have an identity column that is not the primary
key. Tables with same name but different schema are not supported. Columns with User Defined Data Types are not supported. Currently, Azure SQL DAta Sync does not support Azure SQL Database Managed Instance. </p>
 

 
 <p> Data Sync Overview </p>
<ul>
	<li> Both hub and sync databases must be Azure SQL database (not on-premise) </li>
	<li> Both hub and sync databases should be in the same region </li>
	<li> The member databases can be either SQL databases, on-premises SQL server databases, or SQL Server instances on Azure VMs </li>
	<li> If you are using an on premises database as a member database, you must install and configure a local sync agent </li>
</ul>
 
 <hr>

 
 <b> Demo: Provisioning an Azure SQL Database single database </b>
<p> <b>Demo: Provisioning Azure SQL Elastic Pools </b></p>
<b> Demo: restoring an Azure SQL instance </b>
<b> Demo: Creating and running an Elastic Database Job </b>

