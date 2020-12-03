<h1> Securing Access to Microsoft Azure Storage </h1>

<p> This document will discuss how to access Azure storage services in a secure way. </p>

<h3> Secure access options </h3>

<p>  In order to securly access Azure Storage, some kind of authentication and authorization process has to be applied. Different options for secure access includes
 <ul>
   <li> Azure Active Directory (Azure AD)</li>
   <li> Shared access signatures </li>
   <li> Azure Storage Access Keys </li>
   </ul>
 </p>
  

<h3> Azure Active Directory </h3>
  <p>  
Azure AD is Microsoft's cloud-based identity and authentication service which can be used when accessing Azure storage. A security principal is an object in Azure AD. A security principal can further be divided into four different types
<ul>
  <li>User </li>
  <li>Groups (contains users and might also contain other things)</li>
  <li>Service principal (typically used by an application. The service principal is created when an application is registered with Azure AD)</li>
  <li>Managed identity (Similar to service principal, used for services running in azure that is going to access other services in aure)</li>
</ul>
</p>
  
  
 <h3> Shared access signatures </h3>
 <p> A shared access signature can be used for secure access. The signature represents a key that is added to the Azure service endpoint. With a SAS, you have granular control over how a client can access your data. For example

<ul>
 <li> What resources the client may access. </li>
 <li> What permissions they have to those resources. </li>
 <li> How long the SAS is valid. </li>
 <li> Protocal that is allowed: HTTP / HTTPS </li>
 <li> IP that is allowed</li>
</ul>

 <p> Azure Storage supports three types of shared access signatures: </p>
  <ul>
  <li> Service SAS: A service SAS is secured with the storage account key. A service SAS delegates access to a resource in only one of the Azure Storage services: Blob storage, Queue storage, Table storage, or Azure Files.</li>
  <li> Account SAS: An account SAS is secured with the storage account key. An account SAS delegates access to resources in one or more of the storage services.</li>
 <li> User delegation SAS: A user delegation SAS is secured with Azure Active Directory (Azure AD) credentials and also by the permissions specified for the SAS. A user delegation SAS applies to Blob storage only. To create a user delegation SAS, you must first request a user delegation key, which is then used to sign the SAS. </li>
  </ul>
 

</p>
 
 
 <h3> Azure Storage Access Keys </h3>


<h3> Azure Data Lake Storage Gen 2 </h3>
<p> 
  The Azure Data Lake Storage Gen2 connector supports the following authentication types. 
<ul>
  <li> Account key authentication</li>
  <li> Service principal authentication</li>
  <li> Managed identities for Azure resources authentication</li>
</ul>
  </p>







<h3> RBAC</h3>
<p> Can be applied to Subscription, Resource group or at Resource level. If I apply at the Subscription level it will be inherited down </p>
<p> Blobs and Queues supports RBAC within the resource </p>

<h3> ACL </h3>
<ul>
  <p> Types of permissions </p>
  <li>4: Read</li>
  <li>2: Write</li>
  <li>1: Execute</li>
  </ul>
  
  <h3> Storage Account keyes</h3>
  <p> Two different keys. Provide super access </p>
  
