<pre> You have five databases hosted in a single Azure SQL lgoical server. How do you run jobs on four of them?</pre>
<ul>
	<li> <b> Add the logical server into the target group and exclude one database. </b></li>
	<li> It is not possible. The job will enumerate through all databases on a server.</li>
	<li> Create four separate target groups. </li>
	<li> Add each individual database seperately into the target group. </li>
</ul>


<pre> Which notification types does Azure SQL Database managed instance supports for Agent jobs?</pre>
<ul>
	<li> Emails and Net Send</li>
	<li> Pager, Net Send and emails</li>
	<li> Emails and pagers </li>
	<li> <b>Emails only </b></li>
</ul>


<pre> Which technology should be used for data migration?</pre>
<ul>
	<li> <b>Azure Database Migration Service</b></li>
	<li> Azure SQL Data Sync</li>
	<li> Read-only replicas </li>
	<li> Azure Data Factory</li>
</ul>


<pre> Which technology synchronizes data between multiple databases in the cloud?</pre>
<ul>
	<li> <b>SQL Data Sync</b></li>
	<li> Azuer Data Factory</li>
	<li> Read-only replicas </li>
	<li> Azure Data Lake</li>
</ul>


<pre> What is the main difference between general purpose and business critical pricing tiers?</pre>
<ul>
	<li> Auditing</li>
	<li> <b>Storage latency </b></li>
	<li> Security features </li>
	<li> Backup availability</li>
</ul>


<pre> You are migarting an on-premises databse to Azure SQL Database. Which purchasing model is the easiest to calculate the resources you need?</pre>
<ul>
	<li> Both vCore and Database Throughput Unit (DTU)</li>
	<li> Use infrastructure-as-a-service (IaaS) SQL virtual machines (VMs)</li>
	<li> Database Throughput Unit (DTU) based</li>
	<li> <b>vCore-based</b></li>
</ul>



<pre> You must make sure database administrators can not see employees personal inforamtion. Which technology will you use?</pre>
<ul>
	<li> Transparetn Data Encryption (TDE)</li>
	<li> Secure Sockets Layer (SSL)/Transport Layer Security (TLS) for data in transit</li>
	<li> <b> Always Encrypted </b> </li>
	<li> Managed Identities (MSI) </li>
</ul>



<pre> You have provisioned an Azure SQL Database instance. However, you can not connect to the database from your local SQL Server Management Studio (SSMS). What is the first think you check?</pre>
<ul>
	<li> Make sure the Azure Active Directory account is set properly</li>
	<li> Double check your server administrators credentials</li>
	<li> <b> Login to Azure portal and white list your IP in the database firewall </b> </li>
	<li> Make sure Always Encrypted is turned off. </li>
</ul>



<pre> For managed instance, which authentication option can you use instead of Windows authentication?</pre>
<ul>
	<li> <b> c (AAD) authentication </></li>
	<li> Transport Layer Security</li>
	<li> Managed Identities (MSI) </li>
	<li> Database logins </li>
</ul>


<pre> What kind of backups are kept for the long-term-retention (LTR) backups?</pre>
<ul>
	<li> All backup types are kept</li>
	<li> <b>Full weekly backups only </b></li>
	<li> Transaction log backups </li>
	<li> Full and differential backups </li>
</ul>


<pre> You must keep long term backups for your Azure SQL Database managed instance. What is the solution?</pre>
<ul>
	<li> <b>Take copy-only backups and store them in the blob storage </b></li>
	<li> Use the business critical service tier.</li>
	<li>  Managed instance automatically creates long term backups</li>
	<li> Configure long-term backup retention (LTR) backups for your instnace </li>
</ul>


<pre> Which scheduling technologies are availabile to Azure SQL Database single database and elastic pools?</pre>
<ul>
	<li> SQL Agent Jobs</li>
	<li> Elastic Database Jobs and SQL Agent Jobs</li>
	<li> Azure Automation runbooks for manually scheduling jobs</li>
	<li> Elastic Database jobs </li>
</ul>

<pre> You must make sure only the members' data updates from the Hub and the Hub is intact. Which sync direction would you choose?</pre>
<ul>
	<li> Not supported</li>
	<li> To Hub</li>
	<li> <b>From Hub </b></li>
	<li> Bi-directional </li>
</ul>


<pre> How can you run SQL Server Integration Services (SSIS) packages in a manged instance?</pre>
<ul>
	<li> Azure does not support SSIS packages.</li>
	<li>  Use Azure Data Lake</li>
	<li> <b>Use Azure Data Factory </b></li>
	<li> Convert your package to Logic App flows. </li>
</ul>
