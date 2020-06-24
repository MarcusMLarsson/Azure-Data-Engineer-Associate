
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

<p> Running SQL Server on Linux: Doing this on docker container for windows, its going to be virtualized. I can't run a Linux container on windows so virtualisation can be used to create that Linux environment. To get started, I need an Image which is going to be used by the container. See powershell code below</p>

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
  <li> The operations can easily deploy with cchange control without the need for xomplex runbooks that are often incomplete.</li>
  <li> Very fast deployment as existing container hosts are leveraged instead of requiring new VMs enabling faster response oto scale requirements </li>
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
  <p> Make that a container host, manually or something that can create the BMS for me. </p>
  <li> Use Azure Container Instances </li>
  <p> You can think of this as container as a service. All I say is, Hey I want a container. here is my image, here is some configurations go create it for me. I'm not thinking about container host. </p>
  <li> Many PaaS services utilize containers </li>
  <p> For example if I want to run Linux on an app service plans, it uses containers under the scene </p>
  </ul>
  
  <h3> Orchestration </h3>
 <p> Individually managing 1 or 2 containers on a node is possbile but does not scale. When dealing with a large scale environments orchestration is required around. There are a number of different aspecs you have to think about </p>
 <ul>
  <li> Deployment/planning </li>
  <p> Deployment of the node (the container host), planning etc
  <li> Scaling </li>
    <p> If my worker nodes are filling up, I need to add more. 
  <li> Management</li>
  <p> If I do have a large scale environment, I may have to update the container host. how do I roll out a new version of the image?</p>
</ul>

<h3> Kubernetes 101 </h3>
<img src="https://miro.medium.com/max/2920/1*UnrkdMdY3XBHOUSx9H-sJw.png">
<p> While there are a number of container orchestration solutions, Kubernetes has become the standard. This was a Google project, which is now open source. Kubernetes is not replacing Docker. Docker is still my container runtime on Linux. It is still my tool face. Kubernetes sits on top of Docker to provide the Orchestration. I'm going to run Kubernetes to orchestrate the containers I run on Docker. </p>

<p> Kubernetes enables developers to automate the process of deploying, scaling and managing containerized applications. The fundamental premise behind Kubernetes is that we can enforce what is called "Desired state management". What that means is that im going to feed the cluster services a specific configuration. And it will be up to the cluster service to run that configuration in my infrastructure.   </p>

<p> Kubernets cluster consisft of two types of node. </p>
<ul>
  <li> The Kubernetes master runs a number of components that acts as the brain. </li>
  <li> The Worker nodes run the actual pods (which have 1 or more containers) which are grouped into pools that share the same configuration </li>
  <li> The workers run a kublet that helps with the scheduling and health checking of pods </li>
 </ul>
 
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

<h3> Azure Kubernetes Service </h3>
<p> Kubernetes has master and worker nodes. In the demo above, Docker Desktop deployed this for me. If I deployed it manually, its quite a lot to it. There is configuration around networking, storage, etc. Azure Kubernetes Service provides a managed Kubernetes service. I'm not deploying Kubernetes, I'm not patching Kubernetes, I'm not scaling the master infrastructure etc. With Azure Kubernetes Services, I get a dedicated master created for my, but I never see it. </p>
