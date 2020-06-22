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
 
 <img src="https://cloudandmobileblogcom.files.wordpress.com/2018/07/devops.jpg?w=833" width="800">
