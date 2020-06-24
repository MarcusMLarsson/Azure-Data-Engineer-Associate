
<h3> Deploying SQL Server Containers in Azure </h3>

<h3> SQL Server Fundamentals </h3>
<p> SQL Server is a relational database management system (RDBMS) from Microsoft (released 1987). SQL Server utilizes a table with a defined schema that is comprised of columns and rows. T-SQL is primarily used to interact with the database. There are a number of versions of SQL server available. SQL Server is one of the leading relational databases in the market. SQL Server 2017 and above are available on both Windows and Linux. </p>

<p> The point about Linux is very important when we start talking about containers because containers historically has been Linux based. Even today, when we are starting to see Windows based containers, it's still Linux that is the primary platform for containers. When we are thinking about SQL Server in a container, its going to be SQL Server running on Linux in a container. </p>

<h3> Database Services in Azure </h3>
<p> Azure has a large number of database services. </p>
<ul>
  <li> IaaS: Database software can be deployed to types of compute services like VMs where the customer maintains all management and maintenance responsibility. Those VMs can run Windows or a number of Linux distributions. I can create a VM and than install a database product into that VM. In that IaaS model, I as a customer is responsible for the installation, management, maintenance, backup etc. </li>
  <li> Paas: Large number of PaaS offerings that are databases provided as managed services. The responsibility shifts to Azure. I'm not worrying about patching operating systems or runtimes etc. </li>
  </ul>
  
  <p> Go to the portal, go to compute, under compute you will find SQL Server, templates and images available that has SQL Server and other database offerings, preconfigured and ready to go to run in a VM. </p>
  
<h3> Critical SQL Server Requirements </h3>
<p> These most haves conflict in how we think about containers </p>
<ul>
  <li> Durable state, the state is critical, I can not lose my data. </li>
  <li> Needs consistent network access (DNS/IP). Application cant change name and IP etc. </li>
  <li> High availability, if an accident happend, I need to heal it quickly. </li>
  </ul>
  
 <h3> Containers 101 </h3>
 
 <img src="https://miro.medium.com/max/1248/1*ql_47xetzYIEbkx4jeYZug.png">
