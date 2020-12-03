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
Azure AD is Microsoft's cloud-based identity and authentication service. A security principal is an object in Azure AD
  
 <h3> Type of security principals  </h3> 
<ul>
  <li>User </li>
  <li>Groups (contains users and might also contain other things)</li>
  <li>Service principal (typically used by an application. The service principal is created when an application is registered with Azure AD)</li>
  <li>Managed identity (Similar to service principal, used for services running in azure that is going to access other services in aure)</li>
</ul>
</p>
  
  
 <h3> Shared access signatures </h3>
 
 
 
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
  
  <h3> Types Shared Access Signature </h3>
  <ul>
  <li> Service SAS: Provides access to a specific resource, in one of the storage services. For example, a container, a blob or a file</li>
  <li> Account SAS: Provides access to one or more services. Specific operations can be granted for that serivce and the right for the service content</li>
  </ul>
  
 <p> A SAS token for access to a container, directory, or blob may be secured by using either Azure AD credentials or an account key. A SAS secured with Azure AD credentials is called a user delegation SAS </p>
 
 <p> To create a user delegation SAS, you must first request a user delegation key, which is then used to sign the SAS. </p>
