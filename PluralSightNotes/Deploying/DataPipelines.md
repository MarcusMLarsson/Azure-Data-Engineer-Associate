<p> Continous integration </p>
<p> CI is a development methodology that invovles integrating code changes into a shared repository on a frequent basis. There are many advantages to using CI, such as:</p>
<ul>
  <li> Smaller code changes </li>
  <li> Early bug detection </li>
  <li> Faster release rates </li>
  </ul>
  
<p> CI/CD Process </p>
<ul> 
  <li> Work on a new feature on isolated feature branch (fork) </li>
  <li> Test and make sure the change works </li>
  <li> Integrate changes in collaboration branch </li>
    <li> Push changes to the testing environment </li>
    <li> Test and make sure the change works </li>
  <li> Push changes to the production environment </li>
  </ul>
  
  <p> We can achive CI and CD in Azure in two ways </p>
  <ul>
  <li> The UI based method: Use data factory visual tools integration with ARM templates </li>
  <li> The automated method: Use ADF to import/export ARM templates. Integraet with a version control system </li>
  </ul>
  
  <h3> Demo: Azure Resource Groups </h3>
  <p> One RG for Development environment, one for Staging and one for Production </pl>
  
  <h3> Demo: Creating one storage account per Resource Group </h3>
  <p> The storage account which is related to the development should be grouped in the resource group for development environment etc </p>
  
  <h3> Azure Key Vaults </h3>
  <p> With Azure Key Vault we can securely store and contol access to tokens, passwords, certificates, API keys, and other secrets. Normally, within web applciations when you connect to a database you are storing connecting strings using appsettings. What you can do, using key vault is move those connections string into the key vault and not visible in the portal. Once the conenction strings are secured in a key vault, you can references them frrom the webapplciation using somethjing called keyvault references.  </p> 
  
  <p> Another secnario is when we are centrilizing secrets. If you have multiple services, that need to use the same connection strings, you can use Azure key vault to centerlize the settings </p>
  
  <h3> Demo: Azure Key Vaults </h3>
  <p> Create key vault for every environment </p>
  
  <h3> Demo: Configure Azure Data Factory and Azure Key Vault</h3>
  <p> Copy connection string from Azure Blob Storage. Store it in Azure Key Vault. Its possible to add the connection string directly into ADF. This is bad practice however; we want to secure the connection string first, which is possible with Azure Key Vault. To do this, go inte Azure Key Vault. Go to Secrets, and press generate/import. Select the manual opload option. Paste the Blob storage connection string in the name field. The next step is to give our Data Factory access to this key vault. We can do this by using Azure Service Principles and Managed Service Identity. Go to Access policies and click add access policy.</p>
  
  <h3> Integrating Azure Data Factory Pipelines with source control using Azure DevOps </h3>
  <p> Do not confuse Azure Pipelines with ADF data pipelines. </p>
