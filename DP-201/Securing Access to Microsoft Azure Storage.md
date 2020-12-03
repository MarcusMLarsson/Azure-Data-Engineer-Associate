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

<p> When you create a storage account, Azure generates two 512-bit storage account access keys. These keys provide super access, including the ability to delete the storage account or its content. These keys can be used to authorize access to data in your storage account via Shared Key authorization.Microsoft recommends that you use Azure Key Vault to manage your access keys, and that you regularly rotate and regenerate your keys. Using Azure Key Vault makes it easy to rotate your keys without interruption to your applications. You can also manually rotate your keys. </p>


<h3> Secure Access to Azure Data Lake Storage Gen 2 </h3>
<p> 
  The Azure Data Lake Storage Gen2 connector supports the following authentication types. 
<ul>
  <li> Service principal authentication</li>
 
 <p> To use service principal authentication, follow these steps. </p>
 
<ol>
 <li> Register an application entity in Azure Active Directory (Azure AD) by following the steps in Register your application with an Azure AD tenant. Make note of the following values, which you use to define the linked service:, Application ID, Application key, Tenant ID. </lu>
 <li> Grant the service principal proper permission using ACL </li>
 </ol>
 <br>

  <li> Managed identities for Azure resources authentication</li>
  
 <p> A data factory can be associated with a managed identity for Azure resources, which represents this specific data factory. You can directly use this managed identity for Data Lake Storage Gen2 authentication, similar to using your own service principal. It allows this designated factory to access and copy data to or from your Data Lake Storage Gen2. To use managed identities for Azure resource authentication, follow these steps.</p>
  <ol> 
 <li> Retrieve the Data Factory managed identity information by copying the value of the managed identity object ID generated along with your factory.</li>
 <li> Grant the managed identity proper permission using ACL</li>
 
 </ol>
 <br>
   <li> Account key authentication</li>
</ul>
  </p>


<h3> RBAC</h3>
<p> Azure role-based access control (Azure RBAC) is a system that provides fine-grained access management of Azure resources. RBAC can be applied to Subscription, Resource group or at Resource level. If RBAC is applied at the Subscription level it will be inherited down. Blobs and Queues supports RBAC within the resource </p>

<h3> Access control list </h3>
<p> Azure Data Lake Storage Gen2 implements an access control model that supports both Azure role-based access control (Azure RBAC) and POSIX-like access control lists (ACLs). You can associate a security principal with an access level for files and directories. These associations are captured in an access control list (ACL). Each file and directory in your storage account has an access control list. When a security principal attempts an operation on a file or directory, An ACL check determines whether that security principal (user, group, service principal, or managed identity) has the correct permission level to perform the operation.</p>
<ul>
  <p> Types of permissions </p>
  <li>4: Read</li>
  <li>2: Write</li>
  <li>1: Execute</li>
  </ul>
  
  
