
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
<p> Docker is the standard for containers, in terms of isolating (the container implementation) for Linux. It's a container runtime for Linux, Windows has its own one. </p>

<p> Docker takes your operating system, and spltis it into many self contained areas, where applications can run in. It is very similar to a VM where people would take a single operating system and divide it into many small operating system, each one thinking they are running on its own system. The problem with VMs it is very ehavy weight and it takes a lot of resources. You dont really want to run multiple VMs on a single system, it just overloads the system. Docker brings this abstraction up one level. Docker is more on the application level. All it really is, is a command line tool. You can choose an application and it will run it in its own space. So that is what Docker is, its a self contained space for applications to run </p>.

<b> Why should you use docker </b>
<b> Portability </b>
<p> Irrespective of your operating system, you can ship your docker containers to other people and they can easily run it without falling into any dependencies trap. When you normally create a webapplication, you install a bunch of random dependencies on the server. After a while, you will lose track of what you installed on there. If you have a webbsite with a bunch of software and tools on a certain machine, if you wanted to sell this webbsite to somebody else how would you do that? You had to sell the server and a lease on the server aswell. The website or application is entierly tied to the sever it is on. With docker, you can take this website and contain it to an image and that is essentially the whole application. Than you can redeploy this image on any other server, and dupplicate the website functionall.  </p>

<b> Promotes the usage of microservices </b>


<pre> Docker run flask </pre>

<img src="https://www.aldakur.net/wp-content/uploads/2017/03/docker-logo-1024x914.png" width=500> 

<p> Using a container in Docker. imagen I'm a developer, I'm creating my application, I need a local database, I want to use containers for that, then I want it in production running in Azure. If I'm developing, I want the ability to have those containers locally. Docker Desktop gives me that ability on a Windows or Mac machine. It also gives me Kubernetes (a orchestrator).    </p>

<a href="https://hub.docker.com/editions/community/docker-ce-desktop-windows"> Download Docker Dekstop for Windows </a>

<b> Docker Dekstop </b>
