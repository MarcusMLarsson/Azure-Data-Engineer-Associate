
<h1> Deploying SQL Server Containers in Azure </h1>

<h3> SQL Server Fundamentals </h3>
<ul>
  <li> SQL Server is a relational database management system (RDBMS) from <b>Microsoft</b> (the entire database architecture and not a language). SQL Server utilizes a table with a defined schema that is comprised of columns and rows. </li>
<li> T-SQL is the proprietary form of SQL used by Microsoft SQL Server (the language). It includes special functions like cast, convert, date(), etc. that are not part of the ANSI standard. </li>
<li> There are a number of versions of SQL server available.  SQL Server 2017 and above are available on both Windows and Linux. </li>
  </ul>

<p> The point about Linux is very important when we start talking about containers because containers historically has been Linux based. Even today, when we are starting to see Windows based containers, it's still Linux that is the primary platform for containers. When we are thinking about SQL Server in a container, its going to be SQL Server running on Linux in a container. </p>


<h3> Database Services in Azure </h3>
<p> Azure has a large number of database services. </p>
<ul>
  <li> IaaS: Database software can be deployed to types of compute services like VMs where the customer maintains all management and maintenance responsibility. Those VMs can run Windows or a number of Linux distributions. I can create a VM and than install a database product into that VM. In that IaaS model, I as a customer is responsible for the installation, management, maintenance, backup etc. </li>
  <li> PaaS: There are a large number of PaaS offerings that are databases provided as managed services. The responsibility of management, patching, runtimes etc shifts to Azure.  </li>
  </ul>
 
  <p> To find IaaS for databases, go to the portal, go to compute, under compute you will find SQL Server, templates and images are available that has SQL Server and other database offerings, preconfigured and ready to run in a VM. </p>
  
<h3> Critical SQL Server Requirements </h3>

<ul>
  <li> Durable state, the state is critical, I can't lose my data. </li>
  <li> Needs consistent network access (DNS/IP). Application cant change name and IP etc. </li>
  <li> High availability, if an accident happend, I need to heal it quickly. </li></ul>

<p> Most of these critical SQL Server requirements are in direct conflict in how we think about containers. </p>


<h3> What is a virtual machine </h3>
<p> A virtual machine is a software that allows us to run an operating system within another operating system. It runs in a window, much like any other program, giving the end user the same experience on a virtual machine as they would have on the host operating system itself. This produces an ideal environment for testing other operating systems including beta releases, accessing virus-infected data, creating operating system backups, and running software or applications on operating systems they weren’t originally intended for. Examples of virtual machine managers are VirtualBox and VMWARE. The virtual machine is sandboxed from the rest of the system, meaning that the software inside a virtual machine can’t escape or tamper with the computer itself. 

Multiple virtual machines can run simultaneously on the same physical computer. For servers, the multiple operating systems run side-by-side with a piece of software called a hypervisor to manage them, while desktop computers typical employ one operating system to run the other operating systems within its program windows. A hypervisors only has one goal. To help you carve up or divide your servers resources into multiple sources. Each virtual machine provides its own virtual hardware, including CPUs, memory, hard drives, network interfaces, and other devices. The virtual hardware is then mapped to the real hardware on the physical machine which saves costs by reducing the need for physical hardware systems along with the associated maintenance costs that go with it, plus reduces power and cooling demand. 
</p>

<h3> What is an image </h3>
<p> An image is a virtual hard disk (.vhd) file that is used as a template for creating a virtual machine. An image is a template because it doesn’t have the specific settings that a configured virtual machine has, such as the computer name and user account settings. If you want to create multiple virtual machines that are set up the same way, you can capture an image of a configured virtual machine and use that image as a template. </p>

<h3> What is a container?</h3>
<p align="center">
<img src="https://miro.medium.com/max/1248/1*ql_47xetzYIEbkx4jeYZug.png">
</p>

<p> A container takes us back before virtualization. Now, we are going to install one operating system on the entire server. One operating system gets access to everything our server has to offer. If we think of traditional virtualization as virtualising the hardware, containers is about virtualising the operating system.  This gives us a much thinner environment (not as heavy) as it not running a complete OS for every container. Another way of saying this, is that a container is a sandbox for a process (an operating system has multiple processes). Containers can run different operating systems, has its own CPU, memeroy, network and are lightweight. </p>


<h3> Docker </h3>
<p align="center">
<img src="https://www.aldakur.net/wp-content/uploads/2017/03/docker-logo-1024x914.png" width=500> 
 </p>
<p> Docker is the standard for container implementation for <b>Linux</b>. Note that docker is a container runtime for Linux, Windows has its own one. Docker takes your operating system, and splits it into many self contained areas, where applications can run in. It is very similar to a VM where people would take a single operating system and divide it into many small operating system, each one thinking they are running on its own system. The problem with VMs is that they are very heavy weight and that they take up a lot of resources. You dont really want to run multiple VMs on a single system, it just overloads the system. Docker brings this abstraction up one level. All it really is, is a command line tool. You can choose an application and it will run it in its own space in isolation. So that is what Docker is, its a self contained space for applications to run. </p>

<p> What is a kernel? </p>
<p> Every multitasking computer system uses a kernel. The kernel is the thing that manages the CPU resources, the memory resources and the processors. It really is the lowest layer, above the CPU. For example, when you start an app, it is in fact the kernel that starts that app and enables the app to be loaded from the flash to the memory. </p>

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/8f/Kernel_Layout.svg/1200px-Kernel_Layout.svg.png" width=500> 
 </p>
 
 <p> Docker containers share the underlying kernel. Let's say we have a system with Ubunto OS and Docker installed on it. Docker can run any flavor of OS ontop of it as long as they share the same Linux kernel. if the underlying system is Ubuntu, Docker can run a container based on another Linux like Debian. You wont be able to run a windows based container on a docker host with Linux OS on it. For that, you would require Docker on a Windows server. Unlike VM, docker is not meant to run different OS on the same hardware. The main purpose of docker is to containarise application, to ship them and run them. </p>

<p> Why should you use docker </p> 
<ul>
  <li>Portability </li
<p> Irrespective of your operating system, you can ship your docker containers to other people and they can easily run it without falling into any dependencies problems. When you normally create a webapplication, you install a bunch of random dependencies on the server. After a while, you will lose track of what you installed on there. If you wanted to sell this webapplication to somebody else someday, alot of problems would arise. In worst case. you might have to sell the server and a lease on the server aswell. The application might be entierly tied to the sever it is on. With docker, you can take this webapplication and contain it to an image and that is essentially the whole application. Than you can redeploy this image on any other server, and duplicate the website functionall.  </p>
<li> Promotes the usage of microservices </li>
<p> Imagen setting up an end-to-end stack for a webserver using node express, a database using mongoDB, a messaging system using Redis and an orchestreation tool like Ansible. Alot of issues will appear using all these different components like compatibility with the version of operating system or components requiring differnt versions of dependencies etc. The architecture of the application might change over time. Everytime something change you might have to go to the same process of checking compatibility. This compatibility matrix issue is usally refered to as the matrix from hell.</(p>
</ul>

<h3> Docker Dekstop </h3>
<p align="center">
<img src="https://i1.wp.com/www.docker.com/blog/wp-content/uploads/2019/05/2b432538-f368-4850-a384-01992a9ef0fd.jpg?ssl=1" width=800> 
  </p>

<p> Docker Desktop is Docker designed to run on Windows 10 or Mac. It also gives access Kubernetes (a orchestrator). I can't run a Linux container on Windows or Mac so virtualisation is needed to create that Linux environment. To get started, I need an Docker Image which is going to be used by the container. See powershell code below </p>

<a href="https://hub.docker.com/editions/community/docker-ce-desktop-windows"> Download Docker Dekstop for Windows </a>

<pre>

#Pull down certain image
docker pull ubuntu:latest

#list all the images
#we are going to have alot of images as we are running kubernetes
docker images

#Create a container
#the container has a job, in this case the container will echo "hello world"
docker run ubunto echo "hello world"

#See running containers
docker ps

#See all containers
#the container has a job, they are commonly used with microservices, if I want it to continue to run forever, then the job that I give it has to be instructing it to keep going (like a webserver). It's not like a VM, when you create it and it just keep running. For a container, when the job is finsihed it will exit. 
docker ps -a

#Run interactively (could also -d for it to be detached)
#I can now peak inside the container
docker run -it ubuntu bash

#Have a name
docker run -name UbuntuContinaer -it ubuntu bash

#Remove containers
docker rm 3692e8685c77 (container ID)

#Remove all not running on Linux
docker rm $(docker ps -a -q -f status=exited)

#Remove all on PowerShell
docker rm @(docker ps -a -q -f status=exited)

#Start existing 
docker ps -a 
$ContainerId = xxxxxx
docker start $ContainerID
docker exec $ContainerID echo "hello john"
docker exec -it $ContainerID bash
docker stop $ContinaerID

</pre>

<h3> Benefits of Containers </h3>

<ul>
  <li> Enable the application to be the prime focus </li>
  <li> The developer can specify what the application needs to run successfully and provides immutability for the execution </li>
  <li> The operations can easily deploy with change control without the need for complex runbooks that are often incomplete.</li>
  <li> Very fast deployment as existing container hosts are leveraged instead of requiring new VMs enabling faster response to scale requirements </li>
  <li> Simpler upgrade patterns </li>
  <li> Portability </li>
  <li> Very thin instances on a shared kernel </li>
  <li> State separation between applications </li>
  <li> Enables multiple versions of applications to be maintained </li>
  <li> Greate imaging system that leverages a repository that can be cloud shared, cloud private or on-premises private </li>
  </ul>
  
  <h3> Containers in Azure </h3>
  <p> There are a number of ways to run containers in Azure </p>
  <ul>
  <li> Deploy inside an Azure IaaS VM </li>
  <p> Make Azure VM the container host. </p>
  <li> Use Azure Container Instances </li>
  <p> You can think of this as container as a service. All I say is, Hey I want a container. Here is my image, here is some configurations, go create a container for me. </p>
  <li> Many PaaS services utilize containers </li>
  <p> For example if I want to run Linux on an app service plans, it uses containers under the scene. </p>
  </ul>


<h3> Kubernetes (also known as K8s)</h3>
<p align="center">
<img src="https://miro.medium.com/max/2920/1*UnrkdMdY3XBHOUSx9H-sJw.png" width="700">
 </p>
<p> Individually managing 1 or 2 containers on a node is possbile. But what if the docker host crashes? and what about if you have a large application with 10,000 containers? When dealing with a large scale environment, orchestration is required. While there are a number of container orchestration solutions, Kubernetes has become the standard. Kubernetes was a Google project, which is now open source. Kubernetes is not replacing Docker. Docker is still the container runtime on Linux. It is still the tool face. Kubernetes sits on top of Docker to provide the Orchestration. You run Kubernetes to orchestrate the containers that are created with Docker. </p>

<p> With Kubernetes, using the Kubernetes CLI (known as kubctl), you can run a 1,000 instances of the same application (kubectl run --replicas=1000 my-web-server) with a single command. Kubernetes can scale it up to 2,000 using a single command. Kubernetes can scale automatically on user load. Kubernetes can upgrade the instances with a single command. Kubernets uses docker host to host to host applications in the form of docker containers. It however does not need to be Docker.  </p>

<p> Kubernetes cluster consist of a set of nodes. A node is a machine, physical or virtual, on which a Kubernetes software tools are installed. A node is a worker machine and that is where containers will be launched by Kubernetes. We have a cluster, but who is responsible for managing this cluster?  Where is the information about the members of the cluster? How are the nodes monitored, when a node fails how do you move the workload to another worker node? That is where the Master comes in. The master is a node with the Kubernetes control plane components installed. The master watches over the nodes in the cluster and is responbile for the actual orchestration of containers on the worker nodes. 
  
  <ul>
  <li> API Server: Acts like the front end for Kubernetes. All services talk to the API server to interact with the Kubernetes cluster</li>
  <li> etcd: is a distributed reliable key value stored used by Kubernetes to store all data used to manage the cluster.</li>
  <li> Scheduler: is responsible for distributing work or containers across multiple nodes. It looks for newley created containers and assigns them to nodes.</li>
  <li> The controllers: are the brain behind the orchestration. They are responsible for noticing and responding when node containers or endpoints goes down. </li>
  <li> The container runtime is the underlying software that is used to run containers (in our case Docker).</li>
    <li> Kublet: is the agent that runs on each node in the cluster. The agent is responsible for making sure that the containers are running on the nodes as expected.</li>
  </ul>

<p align="center">
<img src="https://miro.medium.com/max/981/1*HXbT0c4Q5XaiCIp6y3VMvw.png" width="700">
 </p>

 <h3> Using Kubernets with Docker desktop </h3>
<pre> kubectl get services
kubectl get nodes

kubectl create namespace k8s-demo
kubectl apply -f pod.yaml --namespace-k8s-demo

kubectl get pod --namespace-k8s-demo
kubectl describe pod <pod>
docker ps -a
kubectl get pod container1 --output-yaml --namespace-k8s-demo
docker stop fd510b9df468
docker rm fd510b9df468
kubectl get pod --namespace-k8s-demo # its still there
docker ps -a #Note the age
docker exec ab4821831 uname -a 
docker exec -it ab4821831 bash
kubectl delete pod container1 --namespace-k8s-demo
#stays gone since it just an object. if node died would also just be gone
  
#Whole deployment
kubectl apply -f deployment.yaml --namespace=k8s-demo
kubectl get pod --namespace=k8s-demo
kubectl get all --namespace=k8s-demo -o wide
kubectl get all --all-namespace -o wide

#We don't want to focus on pods and instead abstract with a service
kubectl apply -f service.yaml --namespace=k8s-demo
kubectl get svc --namespace=k8s-demo

#Test the resiliency 
kubectl delete god webapp1-deployment-48123481283 --namespace=k8s-demo
kubectl get pod --namespace=k8s-demo #deployment gets it running again!
docker ps -a 

#cleanup
kubectl delete service webapp1-service --namespace=k8s-demo 
</pre>
</pre>

<h3> Introduction to YAML (Yet another markup language) </h3>
<p> A YAML file is used to represent data.  </p>

<pre> 
<b>Key Value Pair</b>
name: Server1
owner: John
created: 12321312
status: running
</pre>

<pre> 
<b>Array/list</b>
Fruits:
- Orange
- Apple
- Banana
</pre>

<h3> Azure Kubernetes Service </h3>
<p> Kubernetes has master and worker nodes. In the demo above, Docker Desktop deployed this for me. If I deployed it manually, its quite a lot to it. There is configuration around networking, storage, etc. Azure Kubernetes Service provides a managed Kubernetes service. I'm not deploying Kubernetes, I'm not patching Kubernetes, I'm not scaling the master infrastructure etc. With Azure Kubernetes Services, I get a dedicated master created for my, but I never see it. </p>

<h3> Why SQL Server in Containers? </h3>
<ul>
  <li> Ease of use, development testing. It is very easy to grab an image and create a container from it. With a SQL image, you don't need to install SQL, it's already there. </li>
  <li> Standardization </li>
  <li> Portability</li>
  <li> Migration</li>
  <li> DevOps integration </li>
</ul>
  
  
