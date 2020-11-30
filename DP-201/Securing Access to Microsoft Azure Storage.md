
<h3> Type of security principals  </h3> 
<p> A security principal is an object in Azure AD </p>
<ul>
  <li>User </li>
  <li>Groups (contains users and might also contain other things)</li>
  <li>Service principal (typically used by an application. The service principal is created when register an application with Azure AD)</li>
  <li>Managed identity (Similar to Service principal, used for services running in azure that is going to access other services in aure)</li>
</ul>

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
