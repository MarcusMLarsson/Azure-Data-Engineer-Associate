<h1> Azure Disks </h1>

<p>  A disk is a hard or floppy round, flat, and magnetic platter capable of having information read from and written to it. The most commonly found disks with a computer are the hard disks and floppy disks.
  
  
  
  By default when deploying a VM in Azure you get a operating system disk (for a comptuer, the OS is stored on the Hard Disk, but on boot, the BIOS will start the OS, which is loaded into RAM, and from that point on, the OS is accessed while it is located in your RAM.). In addition to our operating system disk, you can also add a data disk 
(ofted required in production environment). When you create the disks, you have two options; unmanaged disks and managed disks. </p> 

<h3> Unmanaged vs Managed disks</h3>
<p> In unmanaged disks, you have to create storage accounts to hold the disks (VHD files) for your Azure VMs. 
With Managed Disks, you are no longer limited by the storage account limits. You can have one storage account per Azure region. </p>


<h3> Azure Managed disks </h3>
<p>
Azure Managed Disks are like physical disks but are virtual and managed by Azure. Azure offers a few types of managed disks </p>
<ul>
<li> Ultra Disk: 160,000 IOPS, 2,000 MB/s throughput </li>
<li> Premium SSD Managed Disks: 20,000 IOPS, 900 MB/s throughput </li>
<li> Standard SSD Managed Disks: 6,000 IOPS, 750 MB/s throughput </li>
<li> Standard HDD Managed Disks: 2,000 IOPS, 500 MB/s throughput  </li>
</ul>


<h3> Solid state drive (SSD) vs Hard drive (HDD) </h3>
<p> HDD are good for storing data at rest (playing back downloaded music, looking at photos etc). SSD are good for little data transactions and raw speed 
(running operating system or running programs like photoshop) </p>
