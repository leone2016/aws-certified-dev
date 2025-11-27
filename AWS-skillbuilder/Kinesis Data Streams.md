## General

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### What is Amazon Kinesis Data Streams?

With Kinesis Data Streams, you can build custom applications that process or analyze streaming data for specialized needs. You can add various types of data such as clickstreams, application logs, and social media to a Kinesis data stream from hundreds of thousands of sources. Within seconds, the data will be available for your applications to read and process from the stream.

### What does Kinesis Data Streams manage on my behalf?

Kinesis Data Streams manages the infrastructure, storage, networking, and configuration needed to stream your data at the level of your data throughput. You don't have to worry about provisioning, deployment, or ongoing maintenance of hardware, software, or other services for your data streams. In addition, Kinesis Data Streams synchronously replicates data across three Availability Zones, providing high availability and data durability. By default, Kinesis Data Streams scales capacity automatically, freeing you from provisioning and managing capacity. You can choose provisioned mode if you want to provision and manage throughput on your own.

### What can I do with Kinesis Data Streams?

Kinesis Data Streams is useful for rapidly moving data off data producers and then continuously processing the data, whether that means transforming it before emitting to a data store, running real-time metrics and analytics, or deriving more complex data streams for further processing.

The following are typical scenarios for using Kinesis Data Streams:

- **Accelerated log and data feed intake:** Instead of waiting to batch the data, you can have your data producers push data to a Kinesis data stream as soon as the data is produced, preventing data loss in case of producer failure. For example, system and application logs can be continuously added to a data stream and be available for processing within seconds.
- **Real-time metrics and reporting:** You can extract metrics and generate reports from Kinesis data stream data in real time. For example, your Amazon Kinesis application can work on metrics and reporting for system and application logs as the data is streaming in, rather than waiting to receive data batches.
- **Real-time data analytics:** With Kinesis Data Streams, you can run real-time streaming data analytics. For example, you can add clickstreams to your Kinesis data stream and have your Kinesis application run analytics in real time, allowing you to gain insights from your data in minutes instead of hours or days.
- **Log and event data collection:** Collect log and event data from sources such as servers, desktops, and mobile devices. You can then build applications using Amazon Lambda or Amazon Managed Service for Apache Flink to continuously process the data, generate metrics, power live dashboards, and emit aggregated data into stores such as Amazon Simple Storage Service (Amazon S3).
- **Power event-driven applications:** Quickly pair with AWS Lambda to respond or adjust to immediate occurrences within the event-driven applications in your environment, at any scale.

### How do I use Kinesis Data Streams?

After you sign up for AWS, you can start using Kinesis Data Streams by creating a Kinesis data stream through either the AWS Management Console or the CreateStream operation. Then configure your data producers to continuously add data to your data stream. You can optionally send data from existing resources in AWS services such as [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/kds.html), [Amazon Aurora,](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/DBActivityStreams.html) [Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Subscriptions.html), and [AWS IoT Core](https://docs.aws.amazon.com/iot/latest/developerguide/kinesis-rule-action.html). You can then use AWS Lambda, Amazon Managed Service for Apache Flink, or AWS Glue Streaming to quickly process data stored in Kinesis Data Streams. You can also build custom applications that run on Amazon Elastic Compute Cloud (Amazon EC2), Amazon Elastic Container Service (Amazon ECS), and Amazon Elastic Kubernetes Service (Amazon EKS) using either Amazon Kinesis API or Amazon Kinesis Client Library (KCL).

## Key concepts

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### What is a shard, producer, and consumer in Kinesis Data Streams?

A shard has a sequence of data records in a stream. It serves as a base throughput unit of a Kinesis data stream. A shard supports 1 MB/second and 1,000 records per second for writes and 2 MB/second for reads. The shard limits ensure predictable performance, making it easy to design and operate a highly reliable data streaming workflow. A producer puts data records into shards and a consumer gets data records from shards. Consumers use shards for parallel data processing and for consuming data in the exact order in which they are stored. If writes and reads exceed the shard limits, the producer and consumer applications will receive throttles, which can be handled through retries.

### What is a record?

A record is the unit of data stored in an Amazon Kinesis data stream. A record is composed of a sequence number, partition key, and data blob. Data blob is the data of interest your data producer adds to a data stream. The maximum size of a data blob (the data payload before Base64-encoding) is 10 mebibyte (MiB).

### What is a partition key?

A partition key is used to isolate and route records to different shards of a data stream. A partition key is specified by your data producer while adding data to a Kinesis data stream. For example, let’s say you have a data stream with two shards (shard 1 and shard 2). You can configure your data producer to use two partition keys (key A and key B) so that all records with key A are added to shard 1 and all records with key B are added to shard 2.

### What is a sequence number?

A sequence number is a unique identifier for each record. Sequence number is assigned by Amazon Kinesis when a data producer calls PutRecord or PutRecords operation to add data to a Amazon Kinesis data stream. Sequence numbers for the same partition key generally increase over time; the longer the time period between [PutRecord](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_PutRecord.html) or [PutRecords](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_PutRecords.html) requests, the larger the sequence numbers become.

### What are On-demand Standard and On-demand Advantage modes?

On-demand Standard mode is the default mode that comes with automatic capacity management and a throughput-based pricing model. On-demand Advantage mode provides new capabilities and a simpler pricing model to on-demand streams in exchange for committing an account to a minimum throughput usage. The minimum commitment duration is only 24 hours.

### How do I choose between On-demand Standard and On-demand Advantage mode?

On-demand Standard is best suited for workloads with unpredictable and highly variable traffic patterns. You should use this mode if you prefer AWS to manage capacity on your behalf or you do not know the expected data throughput. On-demand Advantage is best suited for workloads with at least 25MB/s of data ingest and 25MB/s of data retrieval. In addition to having AWS manage capacity on your behalf, you can also proactively scale streams’ capacity by configuring warm throughput to handle expected data traffic increases. On-demand Advantage is also suitable if you want to fan-out streaming data to many consuming applications or if you want to retain data beyond 24 hours, as its simple pricing does not charge a premium for using enhanced fan-out consumers or extended retention. All Kinesis Data Streams write and read APIs, along with optional features such as Extended Retention and Enhanced Fan-Out, are supported in both modes.

### Can I switch between On-demand Standard and On-demand Advantage mode?

Yes. You can switch between On-demand Standard and On-demand Advantage mode. Switch from On-demand Standard to On-demand Advantage by enabling an account-level setting that changes the billing for all On-demand streams and provides access to additional capabilities. After enabling On-demand Advantage mode, you must wait at least 24 hours before you can switch back to On-demand Standard mode.

## Adding data to Kinesis Data Streams

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### How do I add data to my Amazon Kinesis data stream?

You can add data to a Kinesis data stream through PutRecord and PutRecords operations, KPL, or Amazon Kinesis Agent.

### What is the difference between PutRecord and PutRecords?

PutRecord operation allows a single data record within an API call, and PutRecords operation allows multiple data records within an API call. For more information, see [PutRecord](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_PutRecord.html) and [PutRecords](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_PutRecords.html).

### What is Amazon Kinesis Producer Library (KPL)?

KPL is an easy-to-use and highly configurable library that helps you put data into an Amazon Kinesis data stream. KPL presents a simple, asynchronous, and reliable interface that helps you quickly achieve high producer throughput with minimal client resources.

### What is Amazon Kinesis Agent?

Amazon Kinesis Agent is a prebuilt Java application that offers an easy way to collect and send data to your Amazon Kinesis data stream. You can install the agent on Linux-based server environments such as web servers, log servers, and database servers. The agent monitors certain files and continuously sends data to your data stream. For more information, see [Writing with Agents](https://docs.aws.amazon.com/kinesis/latest/dev/writing-with-agents.html#setting-up-agent).

### What data is counted against the data throughput of an Amazon Kinesis data stream during a PutRecord or PutRecords call?

Your data blob, partition key, and data stream name are required parameters of a [PutRecord](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_PutRecord.html) or [PutRecords](https://docs.aws.amazon.com/kinesis/latest/APIReference/API_PutRecords.html) call. The size of your data blob (before Base64 encoding) and partition key will be counted against the data throughput of your Amazon Kinesis data stream, which is determined by the number of shards within the data stream.

## Reading and processing data from Kinesis Data Streams

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### What is a consumer, and what are different consumer types offered by Kinesis Data Streams?

A consumer is an application that processes all data from a Kinesis data stream. You can choose between shared fan-out and enhanced fan-out consumer types to read data from a Kinesis data stream. The shared fan-out consumers all share a shard’s 2 MB/second of read throughput and five transactions per second limits and require the use of the GetRecords API. An enhanced fan-out consumer gets its own 2 MB/second allotment of read throughput, allowing multiple consumers to read data from the same stream in parallel, without contending for read throughput with other consumers. You need to use the SubscribeToShard API with the enhanced fan-out consumers. We recommend using enhanced fan-out consumers if you want to add more than one consumer to your data stream.

### How I can process data captured and stored in Kinesis Data Streams?

You can use managed services such as AWS Lambda, Amazon Managed Service for Apache Flink, and AWS Glue to process data stored in Kinesis Data Streams. These managed services take care of provisioning and managing the underlying infrastructure so you can focus on writing your business logic. You can also deliver data stored in Kinesis Data Streams to Amazon S3, [Amazon OpenSearch Service](https://aws.amazon.com/opensearch-service/), Amazon Redshift, and custom HTTP endpoints using its prebuilt integration with Kinesis Data Firehose. You can also build custom applications using Amazon Kinesis Client Library, a prebuilt library, or the Amazon Kinesis Data Streams API.

### What is Amazon Kinesis Client Library (KCL)?

KCL for Java, Python, Ruby, Node.js, and .NET is a prebuilt library that helps you easily build Amazon Kinesis applications for reading and processing data from an Amazon Kinesis data stream.

KCL handles complex issues such as adapting to changes in data stream volume, load-balancing streaming data, coordinating distributed services, and processing data with fault tolerance. KCL enables you to focus on business logic while building applications. Refer to Kinesis Data Streams documentation [here](https://docs.aws.amazon.com/streams/latest/dev/shared-throughput-kcl-consumers.html) for more details on KCL.

### What is the SubscribeToShard API?

The SubscribeToShard API is a high-performance streaming API that pushes data from shards to consumers over a persistent connection without a request cycle from the client. The SubscribeToShard API uses the HTTP/2 protocol to deliver data to registered consumers whenever new data arrives on the shard, typically within 70 milliseconds, offering approximately 65% faster delivery compared to the GetRecords API. The consumers will enjoy fast delivery even when multiple registered consumers are reading from the same shard.

### What is enhanced fan-out?

Enhanced fan-out is an optional feature for Kinesis Data Streams consumers that provides logical 2 MB/second throughput pipes between consumers and shards. This allows you to scale the number of consumers reading from a data stream in parallel, while maintaining high performance.

### When should I use enhanced fan-out?

You should use enhanced fan-out if you have, or expect to have, multiple consumers retrieving data from a stream in parallel, or if you have at least one consumer that requires the use of the SubscribeToShard API to provide sub-200 millisecond data delivery speeds between producers and consumers.

### How is enhanced fan-out used by a consumer?

Consumers use enhanced fan-out by retrieving data with the SubscribeToShard API. The name of the registered consumer is used within the SubscribeToShard API, which leads to utilization of the enhanced fan-out benefit provided to the registered consumer.

### Can I have some consumers using enhanced fan-out, and other not?

Yes. You can have multiple consumers using enhanced fan-out and others not using enhanced fan-out at the same time. The use of enhanced fan-out does not impact the limits of shards for traditional GetRecords usage.

### Do I need to use enhanced fan-out if I want to use SubscribeToShard?

Yes. To use SubscribeToShard, you need to register your consumers, which activates enhanced fan-out. By default, your consumer will use enhanced fan-out automatically when data is retrieved through SubscribeToShard.

## On-demand mode

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### What are the default throughput quotas to write data into data stream using on-demand mode?

A new data stream created in on-demand mode has a quota of 4 MB/second and 4,000 records per second for writes. By default, these streams automatically scale up to 200 MB/second and 200,000 records per second for writes.

### How do data streams scale in on-demand mode to handle increase in write throughput?

A data stream in on-demand mode accommodates up to double its previous peak write throughput observed in the last 30 days. As your data stream’s write throughput hits a new peak, Kinesis Data Streams scales the stream’s capacity automatically. For example, if your data stream has a write throughput that varies between 10 MB/second and 40 MB/second, Kinesis Data Streams will ensure that you can easily burst to double the peak throughput of 80 MB/second. Subsequently, if the same data stream sustains a new peak throughput of 50 MB/second, Data Streams will ensure that there is enough capacity to ingest 100 MB/second of write throughput. However, you will see “ProvisionedThroughputExceeded” exceptions if your traffic grows more than double the previous peak within a 15-minute duration. You need to retry these throttled requests.

### What are the throughput limits for reading data from streams in on-demand mode?

On-demand mode’s aggregate read capacity increases proportionally to write throughput to ensure that consuming applications always have adequate read throughput to process incoming data in real time. You get at least twice the write throughput to read data using the GetRecords API. We recommend using one consumer with the GetRecord API so it has enough room to catch up when the application needs to recover from downtime. To add more than one consuming application, you need to use enhanced fan-out, which supports adding up to 20 consumers to a data stream using the SubscribeToShard API, with each having dedicated throughput.

## Provisioned mode

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### What is provisioned mode?

In provisioned mode, you specify the number of shards for the data stream. The total capacity of a data stream is the sum of the capacities of its shards. You can increase or decrease the number of shards in a data stream as needed, and you pay for the number of shards at an hourly rate. You should consider using provisioned mode if you want fine-grained control over how data is distributed across shards.

### What are the limits of Kinesis Data Streams in provisioned mode?

The throughput of a Kinesis data stream in provisioned mode is designed to scale without limits by increasing the number of shards within a data stream.

### How do I scale capacity of Kinesis Data Streams in provisioned mode?

You can scale up a Kinesis data stream capacity in provisioned mode by splitting existing shards using the SplitShard API. You can scale down capacity by merging two shards using the MergeShard API. Alternatively, you can use UpdateShardCount API to scale up (or down) a stream capacity to a specific shard count.

### How do I decide the throughput of my Amazon Kinesis data stream in provisioned mode?

The throughput of a Kinesis data stream is determined by the number of shards within the data stream. Follow the steps below to estimate the initial number of shards your data stream needs in provisioned mode. Note that you can dynamically adjust the number of shards within your data stream through resharding.

Estimate the average size of the record written to the data stream in kilobytes (KB), rounded up to the nearest 1 KB. (average_data_size_in_KB)

Estimate the number of records written to the data stream per second. (number_of_records_per_second)

Decide the number of Amazon Kinesis Applications consuming data concurrently and independently from the data stream. (number_of_consumers)

Calculate the incoming write bandwidth in KB (incoming_write_bandwidth_in_KB), which is equal to the average_data_size_in_KB multiplied by the number_of_records_per_second.

Calculate the outgoing read bandwidth in KB (outgoing_read_bandwidth_in_KB), which is equal to the incoming_write_bandwidth_in_KB multiplied by the number_of_consumers.

You can then calculate the initial number of shards (number_of_shards) your data stream needs using the following formula: number_of_shards = max (incoming_write_bandwidth_in_KB/1000, outgoing_read_bandwidth_in_KB/2000)

### What is the maximum throughput I can request for my Amazon Kinesis data stream in provisioned mode?

The throughput of a Kinesis data stream is designed to scale without limits. The default shard quota is 20,000 shards per stream for the following AWS Regions: US East (N. Virginia), US West (Oregon), and Europe (Ireland). For all other Regions, the default shard quota is 1,000 or 6,000 shards per stream. You can view your shard quota and request an increase via the AWS Service Quotas console.

### What happens if the capacity limits of an Amazon Kinesis data stream are exceeded while the data producer adds data to the data stream in provisioned mode?

In provisioned mode, the capacity limits of a Kinesis data stream are defined by the number of shards within the data stream. The limits can be exceeded either by data throughput or by the number of PUT records. While the capacity limits are exceeded, the put data call will be rejected with a ProvisionedThroughputExceeded exception. If this is due to a temporary rise of the data stream’s input data rate, retry by the data producer will eventually lead to completion of the requests. If it’s due to a sustained rise of the data stream’s input data rate, you should increase the number of shards within your data stream to provide enough capacity for the put data calls to consistently succeed. In both cases, Amazon CloudWatch metrics allow you to learn about the change of the data stream’s input data rate and the occurrence of ProvisionedThroughputExceeded exceptions.

### What happens if the capacity limits of an Amazon Kinesis data stream are exceeded while the Amazon Kinesis application reads data from the data stream in provisioned mode?

In provisioned mode, the capacity limits of a Kinesis data stream are defined by the number of shards within the data stream. The limits can be exceeded either by data throughput or by the number of read data calls. While the capacity limits are exceeded, the read data call will be rejected with a ProvisionedThroughputExceeded exception. If this is due to a temporary rise of the data stream’s output data rate, retry by the Amazon Kinesis application will eventually lead to completion of the requests. If it’s due to a sustained rise of the data stream’s output data rate, you should increase the number of shards within your data stream to provide enough capacity for the read data calls to consistently succeed. In both cases, Amazon CloudWatch metrics allow you to learn about the change of the data stream’s output data rate and the occurrence of ProvisionedThroughputExceeded exceptions.

## Extended and long-term data retention

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### What is the retention period supported by Kinesis Data Streams?

The default retention period of 24 hours covers scenarios where intermittent lags in processing require catch-up with the real-time data. A seven-day retention lets you reprocess data for up to seven days to resolve potential downstream data losses. Long-term data retention greater than seven days and up to 365 days lets you reprocess old data for use cases such as algorithm back testing, data store backfills, and auditing.

### Can I use the existing Kinesis Data Streams APIs to read data older than seven days?

Yes. You can use the same getShardIterator, GetRecords, and SubscribeToShard APIs to read data retained for more than seven days. The consumers can move the iterator to the desired location in the stream, retrieve the shard map (including both open and closed), and read the records.

### Are there any new APIs to further assist in reading old data?

Yes. There are API enhancements to ListShards, GetRecords, and SubscribeToShard APIs. You can use the new filtering option with the TimeStamp parameter available in the ListShards API to efficiently retrieve the shard map and improve the performance of reading old data. The TimeStamp filter lets applications discover and enumerate shards from the point in time you wish to reprocess data and eliminate the need to start at the trim horizon. GetRecords and SubscribeToShards have a new field, ChildShards, which allows you to quickly discover the children shards when an application finishes reading data from a closed shard, instead of having to traverse the shard map again. The fast discovery of shards makes efficient use of the consuming application’s compute resources for any sized stream, irrespective of the data retention period.

### When do I use the API enhancements?

You should consider the API enhancements if you plan to retain data longer and scale your stream’s capacity regularly. Stream scaling operations close existing shards and open new child shards. The data in all the open and closed shards is retained until the end of the retention period. So the total number of shards increase linearly with a longer retention period and multiple scaling operations. This increase in the shard map requires you to use ListShards with the TimeStamp filter and ChildShards field in GetRecords, and SubscribeToShard API for efficient discovery of shards for data retrieval. You will need to upgrade your KCL to the latest version (1.x for standard consumers and 2.x for enhanced fan-out consumers) for these features.

### Does Kinesis Data Streams support schema registration?

Yes. Clients of Kinesis Data Streams can use the AWS Glue Schema Registry, a serverless feature of AWS Glue, either through the KPL and KCL or through AWS Glue Schema Registry APIs in the AWS Java SDK. The Schema Registry is available at no additional charge. 

Visit the Schema Registry [user documentation](https://docs.aws.amazon.com/glue/latest/dg/schema-registry.html) to get started and to learn more.

## Managing Kinesis Data Streams

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### How do I change the throughput of my Amazon Kinesis data stream in provisioned mode?

There are two ways to change the throughput of your data stream. You can use the UpdateShardCount API or the AWS Management Console to scale the number of shards in a data stream, or you can change the throughput of an Amazon Kinesis data stream by adjusting the number of shards within the data stream (resharding).

### How long does it take to change the throughput of my Amazon Kinesis data stream running in provisioned mode using UpdateShardCount or the AWS Management Console?

Typical scaling requests should take a few minutes to complete. Larger scaling requests will take longer than smaller ones.

### Does Kinesis Data Streams remain available when I change the throughput of my Kinesis data stream in provisioned mode or when the scaling happens automatically in on-demand mode?

Yes. You can continue adding data to and reading data from your Kinesis data stream while you use UpdateShardCount or reshard to change the throughput of the data stream or when Kinesis Data Streams does it automatically in on-demand mode.

### How do I monitor the operations and performance of my Amazon Kinesis data stream?

The Amazon Kinesis Data Streams Management Console displays key operational and performance metrics such as throughput of data input and output of your Kinesis data streams. Kinesis Data Streams also integrates with Amazon CloudWatch so you can collect, view, and analyze CloudWatch metrics for your data streams and shards within those data streams. For more information about Kinesis Data Streams metrics, see [Monitoring Amazon Kinesis Data Streams with Amazon CloudWatch](https://docs.aws.amazon.com/kinesis/latest/dev/monitoring_with_cloudwatch.html).

Note that all stream-level metrics are free of charge. All enabled shard-level metrics are charged at Amazon CloudWatch pricing.

### How do I manage and control access to my Amazon Kinesis data stream?

Kinesis Data Streams integrates with AWS Identity and Access Management (IAM), a service that helps you securely control access to your AWS services and resources for your users. For example, you can create a policy that allows only a specific user or group to add data to your data stream. You can also attach a resource-based policy to your data stream or registered consumer to control access at the resource level. For more information about access management and control of your data stream, see [Controlling Access to Amazon Kinesis Data Streams Resources using IAM](https://docs.aws.amazon.com/kinesis/latest/dev/kinesis-using-iam.html).

### How do I share access to my data stream with another account?

You can use IAM assume role or resource-based policy to share access with another account. To share access with a cross-account AWS Lambda function, attach a resource-based policy to your data stream or consumer to grant access to the the Lambda function's execution role. See more at more at [Using AWS Lambda with Amazon Kinesis](https://docs.aws.amazon.com/lambda/latest/dg/with-kinesis.html).

### How do I log API calls made to my Amazon Kinesis data stream for security analysis and operational troubleshooting?

Kinesis Data Streams integrates with Amazon CloudTrail, a service that records AWS API calls for your account and delivers log files to you. For more information about API call logging and a list of supported Amazon Kinesis API operations, see [Logging Amazon Kinesis API calls Using Amazon CloudTrail](https://docs.aws.amazon.com/kinesis/latest/dev/logging_using_cloudtrail.html).

### How do I effectively manage my Amazon Kinesis Data Streams resources and the costs associated with them?

Kinesis Data Streams allows you to tag your Kinesis data streams and enhanced fan-out (EFO) consumers for easier resource and cost management. A tag is a user-defined label expressed as a key-value pair that helps organize AWS resources. For example, you can tag your Amazon Kinesis data streams or EFO consumers by cost centers so that you can categorize and track your Amazon Kinesis Data Streams costs based on cost centers. For more information about, see [Tag your Amazon Kinesis Data Streams resources](https://docs.aws.amazon.com/streams/latest/dev/tagging.html).

### How do I warm the throughput of my Amazon Kinesis data stream in On-demand Advantage mode?

You can use change the write throughput of an on-demand stream during creation and afterwards by configuring warm throughput. You can use the UpdateStreamWarmThroughput API or the AWS Management Console to set warm throughput for an existing data stream.

## Security

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### When I use Kinesis Data Streams, how secure is my data?

Amazon Kinesis is secure by default. Only the account and data stream owners have access to the Kinesis resources they create. Kinesis supports user authentication to control access to data. You can use IAM policies to selectively grant permissions to users and groups of users. You can securely put and get your data from Kinesis through SSL endpoints using the HTTPS protocol. If you need extra security, you can use server-side encryption with AWS Key Management Service (AWS KMS) keys to encrypt data stored in your data stream. AWS KMS allows you to use AWS-generated KMS keys for encryption, or if you prefer, you can bring your own KMS key into AWS KMS. Lastly, you can use your own encryption libraries to encrypt data on the client side before putting the data into Kinesis.

### Can I privately access Kinesis Data Streams APIs from my Amazon Virtual Private Cloud (Amazon VPC) without using public IPs?

Yes. You can privately access Kinesis Data Streams APIs from your Amazon VPC by creating VPC Endpoints. With VPC Endpoints, the routing between the VPC and Kinesis Data Streams is handled by the AWS network without the need for an internet gateway, NAT gateway, or VPN connection. The latest generation of VPC Endpoints used by Kinesis Data Streams are powered by AWS PrivateLink, a technology that enables private connectivity between AWS services using Elastic Network Interfaces (ENI) with private IPs in your VPCs. To learn more about PrivateLink, visit the [PrivateLink documentation](https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Introduction.html#what-is-privatelink).

## Encryption

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### Can I encrypt the data I put into a Kinesis data stream?

Yes, and there are two options for doing so. You can use server-side encryption, which is a fully managed feature that automatically encrypts and decrypts data as you put and get it from a data stream. You can also write encrypted data to a data stream by encrypting and decrypting on the client side.

### Why should I use server-side encryption instead of client-side encryption?

You might choose server-side encryption over client-side encryption for any of the following reason:

- It is hard to enforce client-side encryption.
- They want a second layer of security on top of client-side encryption.
- It is hard to implement client-side key management schemes.

### What is server-side encryption?

Server-side encryption for Kinesis Data Streams automatically encrypts data using a user specified AWS KMS key before it is written to the data stream storage layer, and decrypts the data after it is retrieved from storage. Encryption makes writes impossible and the payload and the partition key unreadable unless the user writing or reading from the data stream has the permission to use the key selected for encryption on the data stream. As a result, server-side encryption can make it easier to meet internal security and compliance requirements governing your data.

With server-side encryption your client-side applications (producers and consumers) do not need to be aware of encryption, they do not need to manage KMS keys or cryptographic operations, and your data is encrypted when it is at rest and in motion within the Kinesis Data Streams service. All KMS keys used by the server-side encryption feature are provided by the AWS KMS. AWS KMS makes it easy to use an AWS-managed KMS key for Kinesis (a “one-click” encryption method), your own AWS KMS customer-managed key, or a KMS key that you imported for encryption.

### Is there a server-side encryption getting started guide?

Yes, there is a getting started guide in the user [documentation](https://docs.aws.amazon.com/streams/latest/dev/server-side-encryption.html).

### Does server-side encryption interfere with how my applications interact with Kinesis Data Streams?

Possibly. It depends on the key you use for encryption and the permissions governing access to the key.

- If you use the AWS-managed KMS key for Kinesis (key alias = aws/kinesis) your applications will not be impacted by enabling or disabling encryption with this key.
- If you use a different KMS key, like a custom AWS KMS key or one you imported into the AWS KMS service, and if your producers and consumers of a data stream do not have permission to use the KMS key used for encryption, then your PUT and GET requests will fail. Before you can use server-side encryption you must configure AWS KMS key policies to allow encryption and decryption of messages. For examples and more information about AWS KMS permissions, see AWS KMS API Permissions: Actions and Resources Reference in the AWS Key Management Service Developer Guide or the permissions guidelines in the Kinesis Data Streams [server-side encryption user documentation](https://docs.aws.amazon.com/streams/latest/dev/server-side-encryption.html).

### Is there an additional cost associated with the use of server-side encryption?

Yes, however if you are using the AWS-managed KMS key for Kinesis and are not exceeding the AWS Free Tier KMS API usage costs, your use of server-side encryption is free. The following describes the costs by resource:

**Keys:**

The AWS-managed KMS key for Kinesis (alias = “aws/kinesis”) is free.
Customer managed KMS keys are subject to KMS key costs. [Learn more](https://aws.amazon.com/kms/pricing/).

**KMS API Usage:**

API usage costs apply for every KMS key, including custom ones. Kinesis Data Streams calls KMS approximately every five minutes when it’s rotating the data key. In a 30-day month, the total cost of KMS API calls initiated by a Kinesis data stream should be less than a few dollars. Note that this cost scales with the number of user credentials you use on your data producers and consumers because each user credential requires a unique API call to AWS KMS. When you use IAM role for authentication, each assume role-call will result in unique user credentials, and you might want to cache user credentials returned by the assume-role-call to save KMS costs.

### Which AWS regions offer server-side encryption for Kinesis Data Streams?

Kinesis Data Streams server-side encryption is available in the AWS GovCloud Region and all public Regions except the China (Beijing) Region.

### How do I start, update, or remove server-side encryption from a data stream?

All of these operations can be completed using the AWS Management Console or the AWS SDK. To learn more, see the [Kinesis Data Streams server-side encryption getting started guide](https://docs.aws.amazon.com/streams/latest/dev/server-side-encryption.html).

### What encryption algorithm is used for server-side encryption?

Kinesis Data Streams uses an [AES-GCM 256 algorithm](https://docs.aws.amazon.com/kms/latest/developerguide/crypto-intro.html) for encryption.

### If I encrypt a data stream that already has data written to it, either in plain text or ciphertext, will all of the data in the data stream be encrypted or decrypted if I update encryption?

No. Only new data written into the data stream will be encrypted (or left decrypted) by the new application of encryption.

### What does server-side encryption for Kinesis Data Streams encrypt?

Server-side encryption encrypts the payload of the message along with the partition key, which is specified by the data stream producer applications.

### Is server-side encryption a shard specific feature or a stream specific feature?

Server-side encryption is a stream specific feature.

### Can I change the KMS key that is used to encrypt a specific data stream?

Yes, using the AWS Management Console or the AWS SDK, you can choose a new KMS key to apply to a specific data stream.

### Is Kinesis Data Streams available in the AWS Free Tier?

No. Kinesis Data Streams is not currently available in the AWS Free Tier. AWS Free Tier is a program that offers free trial for a group of AWS services. For more details about AWS Free Tier, see AWS Free Tier.

## Service Level Agreement

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### What does the Kinesis Data Streams SLA guarantee?

Our Kinesis Data Streams SLA guarantees a Monthly Uptime Percentage of at least 99.9% for Kinesis Data Streams.

### How do I know if I qualify for a SLA Service Credit?

You are eligible for a SLA credit for Kinesis Data Streams under the Kinesis Data Streams SLA if more than one Availability Zone in which you are running a task, within the same Region has a Monthly Uptime Percentage of less than 99.9% during any monthly billing cycle.

For full details on all of the terms and conditions of the SLA, as well as details on how to submit a claim, please see [Amazon Kinesis Data Streams SLA](https://aws.amazon.com/kinesis/data-streams/sla/).

## Pricing and billing

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### How does Kinesis Data Streams pricing work?

Kinesis Data Streams uses simple pay-as-you-go pricing. The pricing and minimum charges are different based on the mode used. Kinesis Data Streams has three modes—On-demand Standard, On-demand Advantage, and Provisioned—and all come with specific billing options

### How does Kinesis Data Streams pricing work in On-demand Standard mode?

With on-demand mode, you don’t need to specify how much read and write throughput you expect your application to perform. In this mode, pricing is based on the volume of data ingested and retrieved along with a per-hour charge for each data stream in your account. There are additional charges for optional features: Extended data retention (beyond the first 24 hours and within the first seven days), Long-Term data retention (beyond seven days and up to one year), and Enhanced Fan-Out. For more information about Kinesis Data Streams costs, see [Amazon Kinesis Data Streams Pricing](https://aws.amazon.com/kinesis/data-streams/pricing/).

### How does Kinesis Data Streams pricing work in On-demand Advantage mode?

In this mode, pricing is based on the volume of data ingested and retrieved across all on-demand streams in the account. This mode charges for a minimum of 25MB/s of data ingest and 25MB/s of data retrieval at On-demand Advantage rates across all on-demand streams in the region, but there is no per-stream fixed charge. There is only an additional charges for using the optional feature Extended Retention (beyond the first 24 hours and up to one years). There is no additional charge for using Enhanced Fan-Out. For more information about Kinesis Data Streams costs, see [Amazon Kinesis Data Streams Pricing](https://aws.amazon.com/kinesis/data-streams/pricing/).

### How does Kinesis Data Streams pricing work in provisioned mode?

With provisioned mode, you specify the number of shards necessary for your application based on its write and read request rate. A shard is a unit of capacity that provides 1 MB/second of write and 2 MB/second of read throughout. You’re charged for each shard at an hourly rate. You also pay for records written into your Kinesis data stream. You incur additional charges when you use optional features such as Extended retention and Enhanced Fan-Out.

Following are two core dimensions and three optional dimensions in Kinesis Data Streams provisioned mode:

- Hourly Shard cost determined by the number of shards within your Amazon Kinesis data stream.
- PUT Payload Unit cost determined by the number of 25 KB payload units that your data producers add to your data stream.

Optional:

- Extended data retention is an optional cost determined by the number of shard hours incurred by your data stream. When extended data retention is enabled, you pay the extended retention rate for each shard in your stream.
- Long-term data retention is an optional cost with two cost dimensions: long-term data storage and long-term data retrieval. Long-term data storage reflects the numbers of GB-months data is stored for the period greater than seven days and up to 365 days. Long-term data retrieval reflects the number of GBs of data retrieved that has been stored for more than seven days.
- Enhanced fan-out is an optional cost with two cost dimensions: consumer-shard hours and data retrievals. Consumer-shard hours reflect the number of shards in a stream multiplied by the number of consumers using enhanced fan-out. Data retrievals are determined by the number of GBs delivered to consumers using enhanced fan-out.

For more information about Kinesis Data Streams costs, see [Amazon Kinesis Data Streams Pricing](https://aws.amazon.com/kinesis/data-streams/pricing/).

### How is a consumer-shard hour calculated for Enhanced Fan-Out usage in provisioned mode?

A consumer-shard hour is calculated by multiplying the number of registered stream consumers with the number of shards in the stream. You will also pay only for the prorated portion of the hour the consumer was registered to use enhanced fan-out. For example, if a consumer-shard hour costs $0.015, for a 10-shard data stream, this consumer using enhanced fan-out would be able to read from 10 shards, and thus incur a consumer-shard hour charge of $0.15 per hour (1 consumer * 10 shards * $0.015 per consumers-shard hour). If there were two consumers registered for enhanced fan-out simultaneously, the total consumer-shard hour charge would be $0.30 per hour (2 consumers * 10 shards * $0.015).

## Comparison with other AWS services

[Close all](https://aws.amazon.com/kinesis/data-streams/faqs/?da=sec&sec=prep#)

### When should I use Kinesis Data Streams and when should I use Amazon Managed Streaming for Apache Kafka (Amazon MSK)?

Kinesis Data Streams and Amazon MSK are both popular data streaming platforms that help you build your own streaming workloads that process data for specialized needs. Both services are scalable, secure, and highly available. They can both be deployed to run streaming use cases such as real-time web and log analytics, personalizing customer experiences, event-driven architectures, IoT analytics, and real-time fraud detection. When choosing between the two, it is important to consider your specific use case and requirements. Here are some factors to consider:

**Familiarity**

-  If you are new to streaming technologies, use Kinesis Data Streams.
- If you have existing applications that are running on Apache Kafka, use MSK. MSK has an existing Kafka migration program (KMP) and a migration guide to make the migration experience easy.

**Preference for open-source**

- If you have a preference for using open-source technologies, our recommendation is to use MSK. Both MSK and MSK Connect are fully compatible with open-source Apache Kafka and Kafka Connect, respectively.

### How does Kinesis Data Streams differ from Amazon SQS?

Kinesis Data Streams enables real-time processing of streaming big data. It provides ordering of records, as well as the ability to read and/or replay records in the same order to multiple Amazon Kinesis Applications. The Amazon Kinesis Client Library (KCL) delivers all records for a given partition key to the same record processor, making it easier to build multiple applications reading from the same Kinesis data stream (for example, to perform counting, aggregation, and filtering). Amazon Simple Queue Service (Amazon SQS) offers a reliable, highly scalable hosted queue for storing messages as they travel between computers. Amazon SQS lets you easily move data between distributed application components and helps you build applications in which messages are processed independently (with message-level ack/fail semantics), such as automated workflows.

### When should I use Kinesis Data Streams, and when should I use Amazon SQS?

We recommend Kinesis Data Streams for use cases with requirements that are similar to the following:

- **Routing related records to the same record processor (as in streaming MapReduce).** For example, counting and aggregation are simpler when all records for a given key are routed to the same record processor.
- **Ordering of records.** For example, you want to transfer log data from the application host to the processing/archival host while maintaining the order of log statements.
- **Ability for multiple applications to consume the same stream concurrently.** For example, you have one application that updates a real-time dashboard and another that archives data to Amazon Redshift. You want both applications to consume data from the same stream concurrently and independently.
- **Ability to consume records in the same order a few hours later.** For example, you have a billing application and an audit application that runs a few hours behind the billing application. Because Kinesis Data Streams stores data for up to 365 days, you can run the audit application up to 365 days behind the billing application.

We recommend Amazon SQS for use cases with requirements that are similar to the following:

- **Messaging semantics (such as message-level ack/fail) and visibility timeout.** For example, you have a queue of work items and want to track the successful completion of each item independently. Amazon SQS tracks the ack/fail so the application doesn’t have to maintain a persistent checkpoint/cursor. Amazon SQS will delete acked messages and redeliver failed messages after a configured visibility timeout.
- **Individual message delay.** For example, you have a job queue and need to schedule individual jobs with a delay. With Amazon SQS, you can configure individual messages to have a delay of up to 15 minutes.
- **Dynamically increasing concurrency/throughput at read time.** For example, you have a work queue and want to add more readers until the backlog is cleared. With Kinesis Data Streams, you can scale up to a sufficient number of shards (note, however, that you’ll need to provision enough shards ahead of time).
- **Using the ability of Amazon SQS to scale transparently.** For example, you buffer requests and the load changes as a result of occasional load spikes or the natural growth of your business. Because each buffered request can be processed independently, Amazon SQS can scale transparently to handle the load without any provisioning instructions from you.