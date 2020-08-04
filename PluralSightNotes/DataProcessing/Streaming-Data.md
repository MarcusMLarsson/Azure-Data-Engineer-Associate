<h1> Building Streaming Data Pipelines in Microsoft Azure </h1>


<p> Due to the nature of live data - data ingestion, processing and output should happen in real-time. This introduces some challenges. First you have to make sure, that your live data processing is supporting
high volume data ingestion. In some situations your system needs to ingest input of MG or even GB per second. We 
also need enough processing power, so data ingestion is not interrupted. This means, in most cases, live data
processing systems can not be deployed to a commodity machine. The machine need to be scaleable and powerfull. You
also need to make sure that your output storage has high bandwidth. </p>

<p> Azure Options for Live Data Processing </p>
<ul> 
  <li> You can implement HDInsight with Spark Streaming </li>
  <li> HDInsight with storm </li>
  <li> Apache Spark in Azure Databricks </li>
  <li> Azure Functions </li>
  <li> Azure WebJobs </li>
  <li> Azure Stream Analytics (main focus). </li> 
</ul>

<p> Azure Stream Analytics is a fully managed, real-time analytics service designed to process fast moving streams
of data. First you need to provision an Azure Stream Analytics Jobs. Azure Stream Analytics jobs can accept
streaming data from three different imput times. The first on is Event Hubs. Any application can be configured
to send events to Azure Event Hubs. For example, you might have an application which monitors stock prices.
This application can be configured to send stock prices in a specific interval, e.g. every one second, sent to Event
Hubs and inturn ingested to Azure Stream Analytics. IoT Hub is another streaming input type which can be used with
Azure Stream Analytics. Azure IoT Hub is an event ingestion service, which is highly optimized for IoT scenarios.
You can have drones, or robots, send events to IoT hub which inturn will be ingested into Azure Stream Analytics.
Finally Azure Blob Store can be used as a source to ingest data into Azure Stream Analytics. This option is great
for log files. You can configure Azure Stream Analytics to write output into Azure Blobs, Data Lake Gen 2, Azure SQL
Database & DW, Event Hubs and Power BI. </p>


<p> Time Windowing: Time is the most import variable in any live streaming system. Each data event has a timestamp
which is equal to what time it was when the data was ingested. There is a need to perform an operation on events 
falling in the same time window (e.g. COUNT). An easy method is needed to find these subset of data events.
Azure Stream Analytics achieves this through windows. There are 4 different Stream Analytics windows: Tumbling
Window, Hopping Window, Sliding Window, Session Window. Tumbling Window: The size is fixed and there is no
overlapping between windows. </p>

<pre> SELECT COUNT()
FROM input
GROUP BY TumblingWindow(second,5) 
</pre>

<p> Hopping Window: Similar to a tumbling window, the size of the window is fixed. The difference is that the
windows are overlapping. 

<pre>
SELECT COUNT()
FROM Input
GROUP BY HoppingWindows(second, 10, 5)   // first argument is unit of time, second is the size of the window, the third is the hopping size (overlaps by 5 seconds)
</pre>

<p> Sliding window: Size are fixed, but I'm only getting new windows if new events are happening. 
<pre>
SELECT COUNT()
FROM Input
GROUP BY SlidingWindow(second, 10)
</pre>


<p> Session window: Are not fixed size and the windows might not overlap? Session window only created a new event is created (no window in moments of silence). </p>
<pre>
SELECT COUNT()
FROM Input
GROUP BY SessionWindow(second, 5, 10)
</pre>

<p> Demo: Provision a new Azure Stream Analytics instance. Process blob storage input. </p>

<p> Configure Azure Stream Analytics with Event Hub and Blob Storage Inputs </p>

<p> Azure Stream Analytics Input types. A data stream is an ongoing sequence of events over time. At least one data stream input is needed for a stream analytics job.
Azure Event Hubs, Azure IoT Hub, Azure Blob storage. Azure Event Hubs (you can confiugre any application to send data to Azure Even Hub). Azure IoT Hub (Highly optimized for IoT).
Azure Blob storage (bulk data such as log files). The second type of data you can use with Azure Stream Analytics is reference data input. Think of reference data input as data which does not
change or changes very slowly, such as metadata lookups. Azure Stream Analytics can accept reference data from two different input type. Azure Blob Storage and Azure SQL Database. You can store
meta data information about the object you are going to process in your reference data. Imagen you are accepting live events from a few devices. Each event comming from a device contains an device id. 
You can store meta data for all your devices in a refrence data input. This data can include device capacity, name and model. Add reference input in inputs. </p>

<p> Provisioning an Event Hubs instance, Create a .Net application to send telemetry data to Azure Event Hubs. </p>


<p> Query data using Azure Stream Analytics </p>

<p> Which data formats are supported as input data streams? CSV, JSON, Avro. Apache Avro is a data serialization framework, you can use this format to send data over the wire. Apache Avro was developed
within Apche's Hadoop project. And Hadoop have native support for apache Avro. Avro uses JSON for defining its schema (is it int, datetime, string etc). The main part of the data (data body) is
serialized into binary formats. So these two sections makes up Avro (binary formats and JSON). You can also use Other (XXML, Protobuf...) which is any custom dataformat as you like assuming you go
ahead and use c# and develop a deserializer for your custom data types. </p>

<p> The important question is, how do you take in this input (from Event Hub, IoT Hub, Blob Storage) and process them and project them to the output. The answer to this question is 
Azure Stream Analytics Query Language (90% similar to T-SQL). </p>

<p> Event time vs Arrival Time: Event time is when the event take place. Arrival time is the Event time plus the small delay that it takes for the data to be ingested via Event Hub/IoT Hub/Blob Storage. The arrival time
is used as the timestamp. Arrival time for Event Hubs and Iot Hub events is when the event was received. Arrival time for Blob storage events is the last modified time. </p> 

<p> Demo: Stream Analytics Query Language </p>

<p> Azure Stream Analytics and Power BI integration. You can use Power BI to visualse output of Azure Stream Analytics. Demo: Visualize Azure Stream Analytics in Power BI </p>




---

<h3> Notes </h3>

<p> Bandwith, throughput and speed: Bandwith refers to the maximum amount of data transfer per second. "The bandwith
for a single mode fiber can carry 10Gbps". Throughput is actual amount of data passing through media or connection.
Bandwidth is what is possible in a perfect word, Throughput should be lower (in practise)
