
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
    
  
  
  
