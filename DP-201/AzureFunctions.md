<h1> Azure Functions </h1>
<p> Azure Functions is a serverless compute service that lets you run event-triggered code without having to explicitly provision or manage infrastructure.
In other words, <b>Azure Functions is a solution for easily running small pieces of code, or "functions," in the cloud </b>. 
You can write just the code you need for the problem, without having to worry about a whole application or the infrastructure to run it. 
These Azure Functions can make development even more productive, and you can use your development language of choice, 
such as C#, Java, JavaScript, PowerShell, and Python. You need to pay only for the time your code runs and trust Azure to scale as needed. 
</p>

<h3> Hosting plan </h3>
<p> When you create a function app in Azure, you need to choose a hosting plan for your app. There are three available hosting plans </p>
<ul>
<li> Consumption: compute instances are dynamically added or removed based on incomming requests. Pay only when your function is used (consumed)</li>
<li> Premium: You specify a number of pre-warmed instances that are always online and ready to respond. When the function is run, Azure scales out automatically if needed. 
You pay for pre-warmed instances and additional use as Azure scale out</li>
<li> App Service Plan: Run your functions, just like a webb app</li>
</ul>
