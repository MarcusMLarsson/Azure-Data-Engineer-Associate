<h1> Azure Disks </h1>

<p> By default when deploying VM you get a operating system disk. In addition to our operating system disk, you can also add a data disk 
(ofted required in production environment). When you create the disks, you have two options; unmanaged disks and managed disks. </p> 

<h3> Unmanaged vs Managed disks</h3>
<p> In unmanaged disks, you have to create storage accounts to hold the disks (VHD files) for your Azure VMs. 
With Managed Disks, you are no longer limited by the storage account limits. You can have one storage account per Azure region. </p>


<h3> Azure Managed disks </h3>
<p>
Azure Managed Disks are like physical disks but are virtual and managed by Azure. Azure offers a few types of managed disks </p>
<ul>
<li> Ultra Disk</li>
<li> Premium SSD Managed Disks</li>
<li> Standard SSD Managed Disks</li>
<li> Standard HDD Managed Disks </li>
</ul>


<h3> Solid state drive (SSD) vs Hard drive (HDD) </h3>
<p> HDD are good for storing data at rest (playing back downloaded music, looking at photos etc). SSD are good for little data transactions and raw speed 
(running operating system or running programs like photoshop) </p>
