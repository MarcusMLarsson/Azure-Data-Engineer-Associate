
<h3> What is a computer network? </h3>
<p> A network are computres that are connected together</p>

<h3>What is a virtual network? </h3>
<p> VNet enables many types of Azure resources, such as Azure Virtual Machines (VM), to securely communicate with each other, 
the internet, and on-premises networks. It is a representation of your own network in the cloud</p>



<h3> Service endpoints </h3>
<p> Resources like VMs are stored in a Vnet. The internet is outside this virtual network but by default the resources (e.g. VMs) have a public facing endpoint (protected
by a stateful firewall).  </p>

<h3> Virtual Network Injection</h3>
<p> One approach to limit access to services, is to deploy the service into an Azure Vnet. </p>

<h3> Service endpoints</h3>
<p> Used for services that cannot integrate with a virtual network (like Azure SQL and Azure Storage account). This means that our Azure VMs
can interact with Azure SQL and Azure Storage accounts as if they’re part of the same virtual network, rather than our 
Azure virtual machines accessing them over the public endpoint – very neat </p>

<h3> Network secuirty groups </h3>
<p> You can use an Azure network secuirty groups (NGS) to filter network traffic to and from Azure resources in an Azure virtual network. 
A network security group contains security rules that allow or deny inbound network traffic to, or outbound network traffic from, several types of Azure resources.
For each rule, you can specify source and destination, port, and protocol.</p>

<h3> Azure private link </h3>
<p> Azure private link enables private endpoints to be created in Vnets. The private endpoint uses an IP address from the target Vnet. </p>

<h3> Network Virtual Appliance (NVA) </h3>
<p> VMs that perform specific network functions such as Firewall, Router, VPN, WAN optimization. </p>

<h3> Microsoft Peering </h3>
<p> ExpressRoute provides a private link between a customer network and the Microsoft WAN  </p>
