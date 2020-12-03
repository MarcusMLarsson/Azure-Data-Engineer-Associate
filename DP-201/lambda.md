<h1> Lambda Architecture </h1>


<h3> Streaming </h3>
<p> Often we want to deploy our machine learning models to make prediction on live data. Opearting on a stream of data presents some unique challanges including</p>

<ul>
<li> Rebuilding our model to reflect the changing world</li>
<li> Deploy models that can run quickly</li>
<li> Scalability and fault tolerance</li>
</ul>

<p> For instance we build a machine learning model to predict a price. As inflation expecations changes etc, our model needs to take this new information into account. </p>

<p> The most common way we address these problems are using Lambda Architecture. In other words, Lambda architecture is a generic architecture that let's us handle streams of data and deploy machine learning models to them  </p>

<img src="https://docs.microsoft.com/en-us/azure/architecture/data-guide/big-data/images/lambda.png"/>

<p> We have new data arriving to the left in the image. As this new data is comming in, we are going to split this data and assign it to a batch layer and a speed layer. The new data is deposited in the batch layer and it becomes part of our master dataset. We pool up data over and over again in this master data set until we have enough. Once we do, we build the model. Once we have our model built, we serialize it (save it offline somewhere, maybe we pickle it), test it, validate it etc. We than take the model and deploy it into the speed layer. Lastly we have the service layer, which take the decision the deployed machine learning model is making and does something with it. </p>
