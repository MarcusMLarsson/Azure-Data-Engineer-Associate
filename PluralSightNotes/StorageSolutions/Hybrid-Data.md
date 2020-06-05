<h1> Implementing Hybrid Data Solutions in Microsoft Azure </h1>

---

<p> <b> Understanding Hybrid Data Systems </b></p>

<p> Hybrid is an architecture that invloves components on-premises and components in the cloud. When switching to 
hybrid solution (seperating aspect of computing data) its critical to understand attributes and requirements (things
like latency). How does my application access the data? </p>


<p>Connectivity: For a hybrid solution there needs to be a communcation between on-premises and the cloud service.
By default most services are accessed via a internet facing endpoint (via encrypted data). </p>

<p><b> Implementing Hybrid Data Systems </p></b>

<p> All resources in Azure are deployed into a subscription. With PaaS services are also deployed to a region. I typically collect things together in a resource group that has an common lifecycle (run together, de-provisioned together etc).In production, you should not be creating resources in the portal. You want to be using a JSON template (might be
created as part of DevOps pipeline, ARM). Before you click create when using the portal you can download a template for automation (basis or hints for creating ARM?). There are few locations between on-premises to services on Azure: 
Internet, S2S VPN, ExpressRoute Private/Microsoft peering. Most hybrid solutions will leverage ExpressRoute and if not
VNet-based Microsoft peering will be required. This is because of the quality of the connection, because of the
end-to-end service level agreement, consistent latency. </p>

<p> If using a SAN (Storage Area Network) solution there is not a native replication to Azure (you can't store your
machine inside of Azure center). However, some vendors have partnership to enable replication to Microsoft network edge sites that can be accessed with low latency from VNets. </p>

<p> ACL: Access control list works as a package filter. That is, to allow or deny traffic. Package filters provide
security into the network. Perhaps we only want to allow https traffic to a server. We can use ACL for this, to allow
some traffic and deny other.   





---

<h3> Notes </h3>

<b> Virtual Network </b>

<p>A virtual network is a representation of a network in the cloud. Generally, we have our own network, and on that 
network we are going to have different resources, different machines. On Azure, instead of physical machines, we will
have virtual machines </p>

<p> ExpressRoute </p>
<p> I have different VMs running in the cloud services, running in Windows Azure that's sitting inside an affinity
group (which is a region) within my cloud subscription. But also I have on-premis infrastructure and within there
I have VMs, I have physical servers and I want connectivity between them. 


<p> VPN: A virtual private network ensures your data is private, encrypted, and anonymous. When you visit a site,
you make an HTTP request and sends your data (IP address etc, and alot of other informaiton). If you use a VPN,
your data is protected. When you send your information online, a VPN creates a tunnel that encrypts your information.
A VPN also adds in en extra server. When you make the HTTP request the data is first sent to the VPN. That's how
a VPN can change your location. </p>

<p> NAS vs SAN: Network Attached Storage vs Storage Area Network </p>
<p> If you want to store data on a centaralized location, where it can be accessed from all of your devices on
one network, you can do this by using a NAS. A NAS is a storage device that is used for storing data (and
it does not do anything else). Typically a NAS is a box that has multiple harddrives in a raid confiugration for
redundancy. In engineering, redundancy is the duplication of critical components of a system with the intention
to increase reliability of the system, usually in the form of a backup or fail-safe. The box has a network interface
card that is directly attached to a swich or a router network so that the data can be accessed over the network. A 
network interface card is a hardware component without which a computer cannot be connected over a network.
It is a circuit board installed in a computer that provides a dedicated network connection to the computer. 
It is also called a network adpter or LAN adapter. One of hte main disadvantaged with a NAS is that it has a
single point of faileur. If a component fail (e.g. power supply on the NAS) nobody can access data. SAN is a 
special, high speed network that stores and provides access to large amounts of data. The network consists of 
multiple disk arays, switches and server. A SAN is fault tolerant because it has more than one of these divces. </p>
