
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
  <li> High availability, if an accident happend, I need to heal it quickly. </li></ul>

<h3> Containers 101 </h3>
 <p> In traditional virtualization (VMs), we have a physical assets, a server, it has CPU and memory, it has a certain amount of bandwith and storage that we can access. We would install a hypervisor, a type 1 hypervisor runs in a ring -1, so we can still ahve the operating system and kernel running ring -0. It sits underneath any operating system we run. Its not running inside a parent operating system. Then we create VMs, that VM is aside a certain amount of resource, virtual CPU and memory etc. Into that VM, we install a operating system, in that operating system we have various run times, libaries and dlls and than we have an app. We have great isolation between applications but it is fairly heavy, as each VM is an entier operating system. Its heavy in terms of in terms of runnning that os. The os has its own requirement on CPU cycle and memory and disk footprint. It is heavy in terms of management, I have to patch all of those OS instances, I have to worry about security and it takes a while to provision them. </p>
 
 <p> With containers, we move up a level. If I think of traditional virtualization as virtualising the hardware, containers is about virtualising the operating system. Here, we are sharing a a desk os kernel. We create isolated name spaces that are based in images in terms of what is sees for the file system. This gives us a much thinner environment, itäs not running a complete OS for every container. </p>
 
 <p> The layering of images is a key feature of containers. Images are stored in repositiries with versions ensuring immutability and prescriptive deployment. 
 
<img src="https://miro.medium.com/max/1248/1*ql_47xetzYIEbkx4jeYZug.png">


<h3> Docker </h3>

<img src="https://www.aldakur.net/wp-content/uploads/2017/03/docker-logo-1024x914.png" width=500>
<p> 
