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
