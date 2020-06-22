<p> Learn how to use Azure Devops to create and manage modern data warehouses </p>

<ul>
 <li> Creating ARM (Azure resource manager) templates to provision SQL Database and SQL Warehouses. </li>
 <li> Creating Azure DevOps CI/CD pipelines </li>
 <li> Creating Azure Data Factory data migrations </li>
 </ul>
 

 | SQL Database      | SQL Data Warehouse       |
| ------------- |:-------------:|
| Current operational data  | Historical operational data |
| Normalized relational data    | Denormalized relational data     |
| Max capacity 4TB | Max capacity near unlimited       |
| Desgined for always on  | Desgined to be paused post analysis        |
| Optimzed for CRUD operations   | Optimized for query performance      |
| Concurrent query limit 6,400 |Concurrent query limit 32|  
 
 
<h3> Demo: Creating an Azure SQL Database </h3>
<ul>
 <li> Create a new Azure SQL Database </li>
 <li> Export Azure SQL Database ARM template </li>
 </ul>
 
 <h3> Demo: Creating an Azure SQL data Warehouse </h3>
 <ul>
 <li> Create a new Azure SQL Data Warehouse </li>
 <li> Export Azure SQL Data Warehouse ARM Template </li>
 </ul>
 
 <h3> Demo: Creating an Azure Data Factory </h3>
 <ul>
 <li> Create a new Azure Data Factory </li>
 <li> Export Azure Data Factory ARM Template </li>
 </ul>
 
 
 <h3> Demo: Loading Data into Azure SQL Database </h3>
 <ul> 
 <li> Create a new Storage Account  </li>
 <li> Configure Azure Data Factory </li>
 <li> Copying data from Storage to Database </li>
 </ul>
 
 <h3> Demo: Creating an Azure Devops organization </h3>
 <ul>
 <li> Create a new account </li>
 <li> Create a new organization </li>
 </ul>
 
 <h3> Demo: Creating an Azure DevOps repository </h3>
 <ul>
 <li> Create a new Git repository </li>
 <li> Learn repository navigation UI </li>
 <li> Learn repository navigation UI </li>
 </ul>
 
 <p> Branch strategies</p>
 
 <p> Branch policies </p>
 
 <h3> Continuous integration and deployment (CI/CD) </h3>
 <b> What is DevOps? </b>
 
 <img src="https://miro.medium.com/max/3964/1*AwvDJDfErlD34ox2QpwGoA.png" width="800">
 
 
 <p> DevOps is the combination of development and operations. The marriage of software development and IT operations. The lines of being a software developer and an IT operations engineer are getting very fuzzy. Now infrastructure is becomming codeable. Even when using ARM templates, an entire enterprise can be provisioned from templated scripts, sitting in a repository. Deployment like this, usually comes in the end of the process, the process being continously updating and coninously deploying </p>     </p>
 <ul> 
 <li> Development: Involves designing, creating, testing, and implementing software applications </li>
 <li> Operations: Involves operational processes, policies, system performance, monitoring and technical infrastructure </li>
 </ul>
 
 <img src="https://cloudandmobileblogcom.files.wordpress.com/2018/07/devops.jpg?w=833" width="1200">
 
 <h3> Azure DevOps </h3>
 
  <a href="https://azure.microsoft.com/en-us/services/devops/"> azure.microsoft.com/en-us/services/devops/ </a>

 
 <img src="https://azurecomcdn.azureedge.net/cvt-fdde87d637c93aaa8d44f0dccd6bc94b93ea7d42a2bc4f5a987d991913ae6ad1/images/page/services/devops/boards/screenshot.jpg">
 
 <ul>
 <li> Repos: Here your project/code will live</li>
 <li> Boards: Agile scrum cards </li>
 <li> Pipeline: You have a build system, and you can release your software into different environments. Everytime I make a commit, it builds my code and make sure it works and it runs a number of tasks (including unit tests). It makes sure my unit test pass, before it builds.  </li>
 <li> Test Plans: If you have systems inplace for formalized testing. </li>
 <li> Artifacts: You can create your own NuGet / NPM feed (package manager system). </li>
 </ul>
 
 <h3> Demo: Creating ARM and Database Templates </h3>
 <ul>
 <li> Review .Net Azure Resource Projects </li>
 <li> Review .Net Sql Database Projects </li>
 </ul>

 <h3> Demo: Creating an Azure DevOps Pipeline </h3>
 <ul>
 <li> Connect to existing Repository </li>
 <li> Start a new build and publish </li>
 </ul>


<h3> Demo: Creating an Azure DevOps Release </h3>
<ul>
 <li> Connect to build artifact </li>
 <li> Deploy new Azure SQL Server </li>
 <li> Deploy new Azure SQL Database </li>
 </ul>
 
 <h3> Demo: Creating an Azure Devops PR Release </h3>
 <ul>
 <li> Locate release pipelines</li>
 <li> Manage release triggers</li>
 </ul>
 
 <h3> Demo: Exploring Azure Database Migration Guidance Website  </h3>
<p> <a href="https://datamigration.microsoft.com/"> datamigration.microsoft.com/ </a> </p>
<ul> 
 <li> pre-migration </li>
 <p> Assesing environemnt and resources that are currently used on-premises. What are the capabilities and capacity of Azure service we are migrating to. Don't lose performance from choosing wronge tier. </p> 
 <li> Migration </li>
 <li> Post-migration </li>
 <p> Now its time to tuning the resources </p>
</ul>

<h3> Demo: Creating an Azure Migrate Project </h3>
<ul>
 <li> Create a Database migration project </li>
 <li> Download the Azure Data Migration Assistant </li>
 </ul>
 
 <p> To create an Azure migrate project, go into the Azure portal and search for Azure Migrate. </p>
 
 <h3> Demo: Creating an Azure Migrate Project </h3>
<ul>
 <li> Demo: Using the Data Migration Assistant </li>
 <li> Create an on-premises assessment </li>
  <li> Migrate on-premises SQL Server database to Azure SQL Server </li>
 </ul>
 
 <p><a href="https://www.microsoft.com/en-us/download/details.aspx?id=53595"> Download Data Migration Assistant </a> </p>
 <p> Create project type Assesment. As part of assesement, check for database compatibility and check feature parity.</p>
 <p> Create project type Migration. For migration scope, choose schema and data. 
 
 <h3> Demo: Setting up Azure SQL Data Sync </h3>
 <ul>
 <li> Create new Data Sync group </li>
 <li> Connect Azure SQL Server Hub </li>
 <li> Connect on-premises SQL Server </li>
 </ul>

<p> Click on SQL Databases, Sync to other databases, create new sync group. The sync group is what is used to keep an Azure SQL Database in sync with other Azure SQL Databases or on-premis databases. Easiest to create new database to save sync data </p>
