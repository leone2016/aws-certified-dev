## Overview

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### What are the benefits of Amazon SQS over homegrown or packaged message queuing systems?

Amazon SQS provides several advantages over building your own software for managing message queues or using commercial or open-source message queuing systems that require significant upfront time for development and configuration. 

These alternatives require ongoing hardware maintenance and system administration resources. The complexity of configuring and managing these systems is compounded by the need for redundant storage of messages that ensures messages are not lost if hardware fails.

In contrast, Amazon SQS requires no administrative overhead and little configuration. Amazon SQS works on a massive scale, processing billions of messages per day. You can scale the amount of traffic you send to Amazon SQS up or down without any configuration. Amazon SQS also provides extremely high message durability, giving you and your stakeholders added confidence.

### How is Amazon SQS different from Amazon Simple Notification Service (SNS)?

Amazon SNS allows applications to send time-critical messages to multiple subscribers through a “push” mechanism, eliminating the need to periodically check or “poll” for updates. Amazon SQS is a message queue service used by distributed applications to exchange messages through a polling model, and can be used to decouple sending and receiving components. 

### How is Amazon SQS different from Amazon MQ?

If you're using messaging with existing applications, and want to move your messaging to the cloud quickly and easily, we recommend you consider [Amazon MQ](https://aws.amazon.com/amazon-mq/) . It supports industry-standard APIs and protocols so you can switch from any standards-based message broker to Amazon MQ without rewriting the messaging code in your applications. If you are building brand new applications in the cloud, we recommend you consider Amazon SQS and Amazon SNS. Amazon SQS and SNS are lightweight, fully managed message queue and topic services that scale almost infinitely and provide simple, easy-to-use APIs. 

### Does Amazon SQS provide message ordering?

Yes. FIFO (first-in-first-out) queues preserve the exact order in which messages are sent and received. If you use a FIFO queue, you don't have to place sequencing information in your messages. For more information, see [FIFO Queue Logic](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html) in the Amazon SQS Developer Guide.

Standard queues provide a loose-FIFO capability that attempts to preserve the order of messages. However, because standard queues are designed to be massively scalable using a highly distributed architecture, receiving messages in the exact order they are sent is not guaranteed.

### Does Amazon SQS guarantee delivery of messages?

Standard queues provide at-least-once delivery, which means that each message is delivered at least once.

FIFO queues provide [exactly-once processing](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html) , which means that each message is delivered once and remains available until a consumer processes it and deletes it. Duplicates are not introduced into the queue.

### How is Amazon SQS different from Amazon Kinesis Streams?

Amazon SQS offers a reliable, highly-scalable hosted queue for storing messages as they travel between applications or microservices. It moves data between distributed application components and helps you decouple these components. Amazon SQS provides common middleware constructs such as dead-letter queues and poison-pill management. It also provides a generic web services API and can be accessed by any programming language that the AWS SDK supports. Amazon SQS supports both standard and FIFO queues.

Amazon Kinesis Streams allows real-time processing of streaming big data and the ability to read and replay records to multiple Amazon Kinesis Applications. The Amazon Kinesis Client Library (KCL) delivers all records for a given partition key to the same record processor, making it easier to build multiple applications that read from the same Amazon Kinesis stream (for example, to perform counting, aggregation, and filtering).

For more information, see the [Amazon Kinesis Documentation](https://aws.amazon.com/documentation/kinesis/).

### Does Amazon use Amazon SQS for its own applications?

Yes. Developers at Amazon use Amazon SQS for a variety of applications that process large numbers of messages every day. Key business processes in both Amazon.com and AWS use Amazon SQS.

## Billing

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### How much does Amazon SQS cost?

You pay only for what you use, and there is no minimum fee.

The cost of Amazon SQS is calculated per request, plus data transfer charges for data transferred out of Amazon SQS (unless data is transferred to Amazon Elastic Compute Cloud (EC2) instances or to AWS Lambda functions within the same region). For detailed pricing breakdowns per queue type and region, see [Amazon SQS Pricing](https://aws.amazon.com/sqs/pricing/).

### What can I do with the Amazon SQS Free Tier?

The Amazon SQS Free Tier provides you with 1 million requests per month at no charge.

Many small-scale applications are able to operate entirely within the limits of the Free Tier. However, data transfer charges might still apply. For more information, see [Amazon SQS Pricing](https://aws.amazon.com/sqs/pricing/) .

The Free Tier is a monthly offer. Free usage does not accumulate across months.

### Will I be charged for all Amazon SQS requests?

Yes, for any requests beyond the free tier. All Amazon SQS requests are chargeable, and they are billed at the same rate.

### Do Amazon SQS batch operations cost more than other requests?

No. Batch operations ([SendMessageBatch](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/APIReference/API_SendMessageBatch.html), [DeleteMessageBatch](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/APIReference/API_DeleteMessageBatch.html), and [ChangeMessageVisibilityBatch](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/APIReference/API_ChangeMessageVisibilityBatch.html)) all cost the same as other Amazon SQS requests. By grouping messages into batches, you can reduce your Amazon SQS costs.

### How will I be charged and billed for my use of Amazon SQS?

There are no initial fees to begin using Amazon SQS. At the end of the month, your credit card will be automatically charged for the month’s usage.

You can view your charges for the current billing period at any time on the AWS website:

1. Log into your AWS account.
2. Under **Your Web Services Account**, select **Account Activity**.

### How can I track and manage the costs associated with my Amazon SQS queues?

You can tag and track your queues for resource and cost management using cost allocation tags. A tag is a metadata label comprised of a key-value pair. For example, you can tag your queues by cost center and then categorize and track your costs based on these cost centers.

For more information, see [Tagging Your Amazon SQS Queues in the Amazon SQS Developer Guide](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-queue-tags.html). For more information on cost allocation tagging of AWS resources, see [Using Cost Allocation Tags](http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/cost-alloc-tags.html) in the AWS Billing and Cost Management User Guide.

### Do your prices include taxes?

Except as noted otherwise, our prices don't include any applicable taxes and duties such as VAT or applicable sales tax.

For customers with a Japanese billing address, the use of AWS in any region is subject to Japanese Consumption Tax. For more information, see the [Amazon Web Services Consumption Tax FAQ](https://aws.amazon.com/c-tax-faqs/).

## Features, functionality, and interfaces

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### Can I use Amazon SQS with other AWS services?

Yes. You can make your applications more flexible and scalable by using Amazon SQS with compute services such as Amazon EC2, Amazon Elastic Container Service (ECS), and AWS Lambda, as well as with storage and database services such as Amazon Simple Storage Service (Amazon S3) and Amazon DynamoDB.

### How can I interact with Amazon SQS?

You can access Amazon SQS using the [AWS Management Console](https://aws.amazon.com/console/), which helps you create Amazon SQS queues and send messages easily.

Amazon SQS also provides a web services API. It is also integrated with the [AWS SDKs](https://aws.amazon.com/tools/), allowing you to work in the programming language of your choice.

### What API actions are available for Amazon SQS?

For information on message queue operations, see the [Amazon SQS API Reference.](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/APIReference/Welcome.html)

### Who can perform operations on a message queue?

Only an AWS account owner (or an AWS account that the account owner has delegated rights to) can perform operations on an Amazon SQS message queue.

### Can I use Java Message Service (JMS) with Amazon SQS?

Yes. You can take advantage of the scale, low cost, and high availability of Amazon SQS without the worry and high overhead of running your own JMS cluster. 

Amazon provides the [Amazon SQS Java Messaging Library](https://github.com/awslabs/amazon-sqs-java-messaging-lib) that implements the JMS 1.1 specification and uses Amazon SQS as the JMS provider. For more information, see [Using JMS with Amazon SQS](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/jmsclient.html) in the Amazon SQS Developer Guide.

[Java Message Service (JMS)](https://en.wikipedia.org/wiki/Java_Message_Service)

### How does Amazon SQS identify messages?

All messages have a global unique ID that Amazon SQS returns when the message is delivered to the message queue. The ID isn’t required to perform any further actions on the message, but it is useful for tracking the receipt of a particular message in the message queue.

When you receive a message from the message queue, the response includes a receipt handle that you must provide when deleting the message.

For more information, see [Queue and Message Identifiers](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-queue-message-identifiers.html) in the Amazon SQS Developer Guide.

### How does Amazon SQS handle messages that can't be processed?

In Amazon SQS, you can use the API or the console to configure dead letter queues, which receive messages from other source queues. When configuring a dead letter queue, you are required to set appropriate permissions for the dead letter queue redrive using RedriveAllowPolicy.

RedriveAllowPolicy includes the parameters for the dead-letter queue redrive permission. It defines which source queues can specify dead-letter queues as a JSON object.

Once you make a dead letter queue, it receives messages after a maximum number of processing attempts cannot be completed. You can use dead letter queues to isolate messages that can't be processed for later analysis.

For more information, see [Using Amazon SQS Dead Letter Queues](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html) in the Amazon SQS Developer Guide.

### What is a visibility timeout?

The visibility timeout is a period of time during which Amazon SQS prevents other consuming components from receiving and processing a message. For more information, see [Visibility Timeout](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/AboutVT.html) in the Amazon SQS Developer Guide.

### Does Amazon SQS support message metadata?

Yes. An Amazon SQS message can contain up to 10 metadata attributes. You can use message attributes to separate the body of a message from the metadata that describes it. This helps process and store information with greater speed and efficiency because your applications don't have to inspect an entire message before understanding how to process it.

Amazon SQS message attributes take the form of name-type-value triples. The supported types include string, binary, and number (including integer, floating-point, and double). For more information, see [Using Amazon SQS Message Attributes](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/SQSMessageAttributes.html) in the Amazon SQS Developer Guide.

### How can I determine the time-in-queue value?

To determine the time-in-queue value, you can request the SentTimestamp attribute when receiving a message. Subtracting that value from the current time results in the time-in-queue value.

### What is the typical latency for Amazon SQS?

Typical latencies for SendMessage, ReceiveMessage, and DeleteMessage API requests are in the tens or low hundreds of milliseconds.

### For anonymous access, what is the value of the SenderId attribute for a message?

When the AWS account ID is not available (for example, when an anonymous user sends a message), Amazon SQS provides the IP address.

### What is Amazon SQS long polling?

Amazon SQS long polling is a way to retrieve messages from your Amazon SQS queues. While the regular short polling returns immediately, even if the message queue being polled is empty, long polling doesn’t return a response until a message arrives in the message queue, or the long poll times out.

Long polling makes it inexpensive to retrieve messages from your Amazon SQS queue as soon as the messages are available. Using long polling might reduce the cost of using SQS, because you can reduce the number of empty receives. For more information, see [Amazon SQS Long Polling](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-long-polling.html) in the Amazon SQS Developer Guide.

### Is there an additional charge for using Amazon SQS long polling?

No. Long-polling ReceiveMessage calls are billed exactly the same as short-polling ReceiveMessage calls.

### When should I use Amazon SQS long polling, and when should I use Amazon SQS short polling?

In almost all cases, Amazon SQS long polling is preferable to short polling. Long-polling requests let your queue consumers receive messages as soon as they arrive in your queue while reducing the number of empty ReceiveMessageResponse instances returned.

Amazon SQS long polling results in higher performance at reduced cost in the majority of use cases. However, if your application expects an immediate response from a ReceiveMessage call, you might not be able to take advantage of long polling without some modifications to your application.

For example, if your application uses a single thread to poll multiple queues, switching from short polling to long polling will probably not work, because the single thread will wait for the long-poll timeout on any empty queues, delaying the processing of any queues that might contain messages.

In such an application, it is a good practice to use a single thread to process only one queue, allowing the application to take advantage of the benefits that Amazon SQS long polling provides.

### What value should I use for my long-poll timeout?

In general, you should use a maximum of 20 seconds for a long-poll timeout. Because higher long-poll timeout values reduce the number of empty ReceiveMessageResponse instances returned, try to set your long-poll timeout as high as possible.

If the 20-second maximum doesn't work for your application (see the example in the previous question), set a shorter long-poll timeout, as low as 1 second.

All AWS SDKs work with 20-second long polls by default. If you don't use an AWS SDK to access Amazon SQS, or if you configured your AWS SDK to specifically have a shorter timeout, you might need to modify your Amazon SQS client to allow longer requests or to use a shorter long-poll timeout.

### What is the AmazonSQSBufferedAsyncClient for Java?

The AmazonSQSBufferedAsyncClient for Java provides an implementation of the AmazonSQSAsyncClient interface and adds several important features:

- Automatic batching of multiple SendMessage, DeleteMessage, or ChangeMessageVisibility requests without any required changes to the application
- Prefetching of messages into a local buffer that allows your application to immediately process messages from Amazon SQS without waiting for the messages to be retrieved

Working together, automatic batching and prefetching increase the throughput and reduce the latency of your application while reducing your costs by making fewer Amazon SQS requests. For more information, see [Client-Side Buffering and Request Batching](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/buffering.html) in the *Amazon SQS Developer Guide*.

### Where can I download the AmazonSQSBufferedAsyncClient for Java?

You can download the AmazonSQSBufferedAsyncClient as part of the [AWS SDK for Java](https://aws.amazon.com/sdkforjava/).

### Do I have to rewrite my application to use the AmazonSQSBufferedAsyncClient for Java?

No. The AmazonSQSBufferedAsyncClient for Java is implemented as a drop-in replacement for the existing AmazonSQSAsyncClient.

If you update your application to use the latest AWS SDK and change your client to use the AmazonSQSBufferedAsyncClient for Java instead of the AmazonSQSAsyncClient, your application will receive the added benefits of automatic batching and prefetching.

### How can I subscribe Amazon SQS message queues to receive notifications from Amazon SNS topics?

1. In the Amazon SQS console, select an Amazon SQS standard queue.
2. Under Queue Actions, select Subscribe Queue to SNS Topic from the drop-down list.
3. In the dialog box, select the topic from the Choose a Topic drop-down list, and click Subscribe.

For more information, see [Subscribing a Queue to an Amazon SNS Topic](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqssubscribe.html) in the *Amazon SQS Developer Guide*.

### Can I delete all messages in a message queue without deleting the message queue itself?

Yes. You can delete all messages in an Amazon SQS message queue using the PurgeQueue action.

When you purge a message queue, all the messages previously sent to the message queue are deleted. Because your message queue and its attributes remain, there is no need to reconfigure the message queue; you can continue using it.

To delete only specific messages, use the DeleteMessage or DeleteMessageBatch actions.

For more information, see this Tutorial: [Purging Messages from an Amazon SQS Queue](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-using-purge-queue.html).

## FIFO queues

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### What regions are FIFO queues available in?

FIFO queues are available in all AWS regions where Amazon SQS is available. See [here](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services) for details on Amazon SQS region availability.

### How many copies of a message will I receive?

FIFO queues are designed to never introduce duplicate messages. However, your message producer might introduce duplicates in certain scenarios: for example, if the producer sends a message, does not receive a response, and then resends the same message. Amazon SQS APIs provide deduplication functionality that prevents your message producer from sending duplicates. Any duplicates introduced by the message producer are removed within a 5-minute deduplication interval.

For standard queues, you might occasionally receive a duplicate copy of a message (at-least-once delivery). If you use a standard queue, you must design your applications to be idempotent (that is, they must not be affected adversely when processing the same message more than once).

For more information, see [Exactly-Once Processing](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html) in the Amazon SQS Developer Guide.

### Are the Amazon SQS queues I used previously changing to FIFO queues?

No. Amazon SQS standard queues (the new name for existing queues) remain unchanged, and you can still create standard queues. These queues continue to provide the highest scalability and throughput; however, you will not get ordering guarantees and duplicates might occur.

Standard queues are appropriate for many scenarios, such as work distribution with multiple idempotent consumers.

### Can I convert my existing standard queue to a FIFO queue?

No. You must choose the queue type when you create it. However, it is possible to move to a FIFO queue. For more information, see [Moving From a Standard Queue to a FIFO Queue](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues-moving.html) in the Amazon SQS Developer Guide.

### Are Amazon SQS FIFO queues backwards-compatible?

To take advantage of FIFO queue functionality, you must use the latest AWS SDK.

FIFO queues use the same API actions as standard queues, and the mechanics for receiving and deleting messages and changing the visibility timeout are the same. However, when sending messages, you must specify a message group ID. For more information, see [FIFO Queue Logic](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html) in the Amazon SQS Developer Guide.

### With which AWS or external services are Amazon SQS FIFO queues compatible?

Some AWS or external services that send notifications to Amazon SQS might not be compatible with FIFO queues, despite allowing you to set a FIFO queue as a target.

The following features of AWS services aren't currently compatible with FIFO queues:

- [Auto Scaling Lifecycle Hooks](https://docs.aws.amazon.com/autoscaling/latest/userguide/lifecycle-hooks.html)
- [AWS IoT Rule Actions](http://docs.aws.amazon.com/iot/latest/developerguide/iot-rule-actions.html)
- [AWS Lambda Dead Letter Queues](http://docs.aws.amazon.com/lambda/latest/dg/dlq.html)

For information about compatibility of other services with FIFO queues, see your service documentation.

### Are Amazon SQS FIFO queues compatible with the Amazon SQS Buffered Asynchronous Client, the Amazon SQS Extended Client Library for Java, or the Amazon SQS Java Message Service (JMS) Client?

FIFO queues aren't currently compatible with the Amazon SQS Buffered Asynchronous Client.

FIFO queues are compatible with the Amazon SQS Extended Client Library for Java and the Amazon SQS Java Message Service (JMS) client.

### Which AWS CloudWatch metrics do Amazon SQS FIFO queues support?

FIFO queues support all metrics that standard queues support. For FIFO queues, all approximate metrics return accurate counts. For example, the following AWS CloudWatch metrics are supported:

- ApproximateNumberOfMessagesDelayed - The number of messages in the queue that are delayed and not available for reading immediately.
- ApproximateNumberOfMessagesVisible - The number of messages available for retrieval from the queue.
- ApproximateNumberOfMessagesNotVisible - The number of messages that are in flight (sent to a client but have not yet been deleted or have not yet reached the end of their visibility window).

### What are message groups?

Messages are grouped into distinct, ordered "bundles" within a FIFO queue. For each message group ID, all messages are sent and received in strict order. However, messages with different message group ID values might be sent and received out of order. You must associate a message group ID with a message. If you don't provide a message group ID, the action fails.

If multiple hosts (or different threads on the same host) send messages with the same message group ID are sent to a FIFO queue, Amazon SQS delivers the messages in the order in which they arrive for processing. To ensure that Amazon SQS preserves the order in which messages are sent and received, ensure that multiple senders send each message with a unique message group ID.

For more information, see [FIFO Queue Logic](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html) in the Amazon SQS Developer Guide.

### Do Amazon SQS FIFO queues support multiple producers?

Yes. One or more producers can send messages to a FIFO queue. Messages are stored in the order that they were successfully received by Amazon SQS.

If multiple producers send messages in parallel, without waiting for the success response from SendMessage or SendMessageBatch actions, the order between producers might not be preserved. The response of SendMessage or SendMessageBatch actions contains the final ordering sequence that FIFO queues use to place messages in the queue, so your multiple-parallel-producer code can determine the final order of messages in the queue.

### Do Amazon SQS FIFO queues support multiple consumers?

By design, Amazon SQS FIFO queues don't serve messages from the same message group to more than one consumer at a time. However, if your FIFO queue has multiple message groups, you can take advantage of parallel consumers, allowing Amazon SQS to serve messages from different message groups to different consumers.

### What is the throughput quota for an Amazon SQS FIFO queue?

By default, FIFO queues support up to 3,000 messages per second with batching or up to 300 messages per second (300 send, receive, or delete operations per second) without batching. If you require higher throughput, you can enable high throughput mode for FIFO on the Amazon SQS console, which will support up to 70,000 messages per second without batching and even higher with batching. For a detailed breakdown of FIFO high throughput mode quotas per region, please see [AWS Documentation](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/quotas-messages.html).

### Are there any limits specific to FIFO queue attributes?

The name of a FIFO queue must end with the .fifo suffix. The suffix counts towards the 80-character queue name limits. To determine whether a queue is FIFO, you can check whether the queue name ends with the suffix.

## Fair Queues

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### What are Amazon SQS fair queues?

Fair queues are an extension to Amazon SQS standard queues that mitigate noisy neighbor impact in multi-tenant systems. They maintain consistent time between sending and receiving messages across all tenants. When one tenant sends a disproportionately large volume of messages or has messages that require longer processing time, fair queues ensure other tenants' messages maintain low dwell time. This preserves quality of service for all tenants while maintaining the scalability and throughput of standard queues.

### When should I use fair queues?

You should use fair queues when you have a multi-tenant queue where consistent, low message dwell time is critical for all tenants. Common scenarios include queues that contain messages from multiple customers, client applications, or request types, especially when some tenants occasionally generate large message backlogs or require varying processing times that could impact others. Fair queues are particularly valuable when you need to ensure quality of service without implementing complex custom solutions or over-provisioning your consumer fleet.

### How do I get started with fair queues?

To enable fair queues, include a message group ID when sending messages to your Amazon SQS standard queues. No changes to message consumers are required, allowing you to adopt fair queues in live systems with no interruption or migration.

### What is a tenant in fair queues?

A tenant can be any entity that shares a queue with others, such as your customer, a client application, or a request type. You define what constitutes a tenant in your system by assigning message group IDs to your messages within a given queue.

### How are fair queues different from FIFO queues in mitigating noisy neighbor events?

FIFO queues maintain strict ordering by limiting the number of in-flight messages from each tenant. While this prevents noisy neighbors, it limits throughput for each tenant. Fair queues are designed for multi-tenant scenarios where high throughput, low dwell time, and fair resource allocation are priorities. Fair queues allow multiple consumers to process messages from the same tenant concurrently while helping all tenants maintain consistent dwell times.

### Do fair queues affect my queue's throughput?

No. Fair queues maintain the same high throughput capabilities of standard queues. The feature only reorders messages to help maintain consistent dwell time across tenants, without imposing throughput limitations.

### How do fair queues work?

Fair queues help maintain consistent dwell time across tenants by reordering messages when a single tenant causes the queue to build a backlog. The queue prioritizes delivering messages from other tenants. Messages from the tenant causing the backlog continue to be delivered to consumers, but their dwell time increases based on available consumer capacity.

### Do fair queues limit the per-tenant consumption rate?

Fair queues do not limit per-tenant consumption rate. They prioritize messages from tenants that are not causing backlogs, while still returning messages from noisy neighbors.

### How can I monitor fair queues?

Fair queues have all standard queues’ CloudWatch metrics. Additionally, several metrics specific to fair queues are available through Amazon CloudWatch. These include the number of noisy neighbors detected (tenants causing queue backlogs), message count for quiet tenants (those not causing backlogs), and dwell time statistics. These metrics help you monitor how effectively the queue maintains consistent message dwell times across your tenants.

### How can I stop using fair queues?

You can stop using fair queues by omitting the message group ID when sending messages. New messages will then follow standard queue behavior with no additional charges.

### Do I need to add message group IDs to all messages?

No. You can selectively apply message group IDs. Messages without a message group ID are treated as belonging to unique tenants. This allows you to mitigate noisy neighbor impact where needed while optimizing costs.

### What regions are fair queues available in?

Fair queues are available in all AWS Regions where Amazon SQS is available. See [here](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) for details on Amazon SQS region availability.

## Security and reliability

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### How reliable is the storage of my data in Amazon SQS?

Amazon SQS stores all message queues and messages within a single, highly-available AWS region with multiple redundant Availability Zones (AZs), so that no single computer, network, or AZ failure can make messages inaccessible. For more information, see [Regions and Availability Zones](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html) in the Amazon Relational Database Service User Guide.

### How can I secure the messages in my message queues?

Authentication mechanisms ensure that messages stored in Amazon SQS message queues are secured against unauthorized access. You can control who can send messages to a message queue and who can receive messages from a message queue. For additional security, you can build your application to encrypt messages before they are placed in a message queue.

Amazon SQS has its own resource-based permissions system that uses policies written in the same language as [AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) policies: for example, you can use variables, just like in IAM policies. For more information, see [Amazon SQS Policy Examples](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/SQSExamples.html) in the Amazon SQS Developer Guide.

Amazon SQS supports the HTTP over SSL (HTTPS) and Transport Layer Security (TLS) protocols. Most clients can automatically negotiate to use newer versions of TLS without any code or configuration change. Amazon SQS supports versions 1.0, 1.1, and 1.2 of the Transport Layer Security (TLS) protocol in all regions.

### Why are there separate ReceiveMessage and DeleteMessage operations?

When Amazon SQS returns a message to you, the message stays in the message queue whether or not you actually receive the message. You're responsible for deleting the message and the deletion request acknowledges that you’re done processing the message.

If you don’t delete the message, Amazon SQS will deliver it again when it receives another receive request. For more information, see [Visibility Timeout](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/AboutVT.html) in the Amazon SQS Developer Guide.

### Can a deleted message be received again?

No. FIFO queues never introduce duplicate messages.

For standard queues, under rare circumstances, you might receive a previously-deleted message a second time. 

### What happens if I issue a DeleteMessage request on a previously-deleted message?

When you issue a DeleteMessage request on a previously-deleted message, Amazon SQS returns a success response.

## Server-Side encryption (SSE)

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### What are the benefits of SSE for Amazon SQS?

SSE lets you transmit sensitive data in encrypted queues. SSE protects the contents of messages in Amazon SQS queues using keys managed in the [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms/). SSE encrypts messages as soon as Amazon SQS receives them. The messages are stored in encrypted form and Amazon SQS decrypts messages only when they are sent to an authorized consumer.

For more information, see [Protecting Data Using Server-Side Encryption (SSE) and AWS KMS](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html) in the Amazon SQS Developer Guide.

### Can I use SNS, Cloud Watch Events and S3 Events with encrypted queues?

Yes. To do this you need to enable compatibility between AWS services (eg. Amazon CloudWatch Events, Amazon S3, and Amazon SNS), and Queues with SSE. For detailed instructions see the [Compatibility section of the SQS Developer Guide](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html).  

### What regions are queues with SSE available in?

Server-side encryption (SSE) for Amazon SQS is available in all AWS regions where Amazon SQS is available. See [here](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/) for details on Amazon SQS region availability.

### How do I enable SSE for a new or existing Amazon SQS queue?

To enable SSE for a new or existing queue using the Amazon SQS API, specify the customer master key (CMK) ID: the alias, alias ARN, key ID, or key ARN of an AWS-managed CMK or a custom CMK by setting the KmsMasterKeyId attribute of the CreateQueue or SetQueueAttributes action.

For detailed instructions, see [Creating an Amazon SQS Queue with Server-Side Encryption](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-create-queue-sse.html) and [Configuring Server-Side Encryption (SSE) for an Existing Amazon SQS Queue](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-configure-sse-existing-queue.html) in the Amazon SQS Developer Guide.

### What Amazon SQS queue types can use SSE?

Both standard and FIFO queues support SSE.

### What permissions do I need to use SSE with Amazon SQS?

Before you can use SSE, you must configure AWS KMS key policies to allow encryption of queues and encryption and decryption of messages.

To enable SSE for a queue, you can use the AWS-managed customer master key (CMK) for Amazon SQS or a custom CMK. For more information, see [Customer Master Keys](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html) in the AWS KMS Developer Guide.

To send messages to an encrypted queue, the producer must have the kms:GenerateDataKey and kms:Decrypt permissions for the CMK.

To receive messages from an encrypted queue, the consumer must have the kms:Decrypt permission for any CMK that is used to encrypt the messages in the specified queue. If the queue acts as a [dead letter queue](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html) , the consumer must also have the kms:Decrypt permission for any CMK that is used to encrypt the messages in the source queue.

For more information, see [What Permissions Do I Need to Use SSE?](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html) in the Amazon SQS Developer Guide.

### Are there any charges for using SSE with Amazon SQS?

There are no additional Amazon SQS charges. However, there are charges for calls from Amazon SQS to AWS KMS. For more information, see [AWS Key Management Service Pricing](https://aws.amazon.com/kms/pricing/).

The charges for using AWS KMS depend on the data key reuse period configured for your queues. For more information, see [How Do I Estimate My AWS KMS Usage Costs?](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html) in the Amazon SQS Developer Guide.

### What does SSE for Amazon SQS encrypt and how is it encrypted?

SSE encrypts the body of a message in an Amazon SQS queue.

SSE doesn't encrypt the following components:

- Queue metadata (queue name and attributes)
- Message metadata (message ID, timestamp, and attributes)
- Per-queue metrics

Amazon SQS generates [data keys](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#data-keys) based on the AWS-managed customer master key (CMK) for Amazon SQS or a custom CMK to provide [envelope encryption](http://docs.aws.amazon.com/kms/latest/developerguide/workflow.html#envelope_encryption) and decryption of messages for a configurable time period (from 1 minute to 24 hours).

For more information, see [What Does SSE for Amazon SQS Encrypt?](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html#sqs-encryption-what-does-sse-encrypt) in the *Amazon SQS Developer Guide.*

### What algorithm does SSE for Amazon SQS use to encrypt messages?

SSE uses the [AES-GCM 256 algorithm](https://docs.aws.amazon.com/kms/latest/developerguide/crypto-intro.html).

### Does SSE limit the transactions per second (TPS) or number of queues that can be created with Amazon SQS?

SSE doesn't limit the throughput (TPS) of Amazon SQS. The number of SSE queues that you can create is limited by the following:

- The [data key reuse period](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html#sqs-sse-key-terms) (1 minute to 24 hours).
- The AWS KMS per-account quota (100 TPS by default).
- The number of IAM users or accounts that access queues.
- The existence of a large backlog (a larger backlog requires more AWS KMS calls).

For example, let's assume the following:

- You set your data key reuse period to 5 minutes (300 seconds).
- Your KMS account has a default AWS KMS TPS quota of 100 TPS.
- You use an Amazon SQS queue without a backlog and with 1 IAM user for SendMessage or ReceiveMessage actions to all queues.

In this case, you can calculate the theoretical maximum of Amazon SQS queues with SSE as follows:

**300 seconds × 100 TPS / 1 IAM user = 30,000 queues**

### How can I estimate my AWS KMS usage costs?

To predict costs and better understand your AWS bill, you might want to know how often Amazon SQS uses your CMK.

**Note**: Although the following formula can give you a very good idea of expected costs, actual costs might be higher because of the distributed nature of Amazon SQS.

To calculate the number of API requests per queue (R), use the following formula:

**R = B / D \* (2 \* P + C)**

**B** is the billing period (in seconds)

**D** is the [data key reuse period](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html#sqs-sse-key-terms) (in seconds)

**P** is the number of producing [principals](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#Principal) that send to the Amazon SQS queue.

**C** is the number of consuming principals that receive from the Amazon SQS queue.

**Important**: In general, producing principals incur double the cost of consuming principals. For more information, see [How Does the Data Key Reuse Period Work?](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html#sqs-how-does-the-data-key-reuse-period-work) in the *Amazon SQS Developer Guide*.

If the producer and consumer have different IAM users, the cost increases.

For more information, see [How Do I Estimate My AWS KMS Usage Costs?](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html#sqs-estimate-kms-usage-costs) in the *Amazon SQS Developer Guide*

## Compliance

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### Is Amazon SQS PCI DSS certified?

Yes. Amazon SQS is PCI DSS Level 1 certified. For more information, see [PCI Compliance](https://aws.amazon.com/compliance/pci-dss-level-1-faqs/).

### Is Amazon SQS HIPAA-eligible?

Yes, AWS has expanded its HIPAA compliance program to include Amazon SQS as a HIPAA Eligible Service. If you have an executed Business Associate Agreement (BAA) with AWS, you can use Amazon SQS to build your HIPAA-compliant applications, store messages in transit, and transmit messages—including messages containing protected health information (PHI).

If you already have an executed BAA with AWS, you can start using Amazon SQS right away. If you don't have a BAA or have other questions about using AWS for your HIPAA-compliant applications, contact us for more information.

**Note**: If you prefer not to transfer PHI through Amazon SQS (or if you have messages larger than 1 MiB), you can alternatively [send Amazon SQS message payloads through Amazon S3](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-s3-messages.html) using the Amazon SQS Extended Client Library for Java (Amazon S3 is a HIPAA Eligible Service, excluding the use of Amazon S3 Transfer Acceleration). For more information, see [Using the Amazon SQS Extended Client Library for Java](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-s3-messages.html#s3-messages-examples) in the *Amazon SQS Developer Guide*.

## Limits and restrictions

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### How long can I keep my messages in Amazon SQS message queues?

Longer message retention provides greater flexibility to allow for longer intervals between message production and consumption.

You can configure the Amazon SQS message retention period to a value from 1 minute to 14 days. The default is 4 days. Once the message retention quota is reached, your messages are automatically deleted.

### How do I configure Amazon SQS to support longer message retention?

To configure the message retention period, set the MessageRetentionPeriod attribute using the console or using the Distributiveness method. Use this attribute to specify the number of seconds a message will be retained in Amazon SQS.

You can use the MessageRetentionPeriod attribute to set the message retention period from 60 seconds (1 minute) to 1,209,600 seconds (14 days). For more information on working with this message attribute, see the [Amazon SQS API Reference](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/APIReference/Welcome.html) .

### How do I configure the maximum message size for Amazon SQS?

To configure the maximum message size, use the console or the SetQueueAttributes method to set the MaximumMessageSize attribute. This attribute specifies the number of bytes that an Amazon SQS message can contain. Set this attribute to a value between 1,024 bytes (1 KiB), and 1,048,576 bytes (1 MiB). For more information, see [Using Amazon SQS Message Attributes](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/SQSMessageAttributes.html) in the Amazon SQS Developer Guide.

To send messages larger than 1 MiB, use the [Amazon SQS Extended Client Library for Java](https://github.com/awslabs/amazon-sqs-java-extended-client-lib) or Python. This library lets you send an Amazon SQS message that contains a reference to a message payload in Amazon S3 that can be as large as 2 GiB.

### What kind of data can I include in a message?

Amazon SQS messages can contain up to 1 MiB of text data, including XML, JSON and unformatted text. The following Unicode characters are accepted:

\#x9 | #xA | #xD | [#x20 to #xD7FF] | [#xE000 to #xFFFD] | [#x10000 to #x10FFFF]

For more information, see the [XML 1.0 Specification](https://www.w3.org/TR/REC-xml/) .

### How large can Amazon SQS message queues be?

A single Amazon SQS message queue can contain an unlimited number of messages. However, there is a quota of 120,000 for the number of inflight messages for a standard queue and 120,000 for a FIFO queue. Messages are inflight after they have been received from the queue by a consuming component, but have not yet been deleted from the queue.

### How many message queues can I create?

You can create any number of message queues.

### Is there a size limit on the name of Amazon SQS message queues?

Queue names are limited to 80 characters.

### Are there restrictions on the names of Amazon SQS message queues?

You can use alphanumeric characters, hyphens (-), and underscores (_).

### Can I reuse a message queue name?

A message queue's name must be unique within an AWS account and region. You can reuse a message queue's name after you delete the message queue.

## Queue sharing

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### How do I share a message queue?

You can associate an access policy statement (and specify the permissions granted) with the message queue to be shared. Amazon SQS provides APIs for creating and managing access policy statements:

- AddPermission
- RemovePermission
- SetQueueAttributes
- GetQueueAttributes

For more information, see the *[Amazon SQS API Reference](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/APIReference/Welcome.html)*.

### Who pays for shared queue access?

The message queue owner pays for shared message queue access.

### How do I identify another AWS user I want to share a message queue with?

The Amazon SQS API uses the AWS account number to identify AWS users.

### What do I need to provide to an AWS user I want to share a message queue with?

To share a message queue with an AWS user, provide the full URL from the message queue you want to share. The CreateQueue and ListQueues operations return this URL in their responses.

### Does Amazon SQS support anonymous access?

Yes. You can configure an access policy that allows anonymous users to access a message queue.

### When should I use the permissions API?

The permissions API provides an interface for sharing access to a message queue to developers. However, this API cannot allow conditional access or more advanced use cases.

### When should I use the SetQueueAttributes operation with JSON objects?

The SetQueueAttributes operation supports the full access policy language. For example, you can use the policy language to restrict access to a message queue by IP address and time of day. For more information, see [Amazon SQS Policy Examples](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/SQSExamples.html) in the Amazon SQS Developer Guide.

## Service access and regions

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### What regions is Amazon SQS available in?

For service region availability, see the [AWS Global Infrastructure Region Table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/).

### Can I share messages between queues in different regions?

No. Each Amazon SQS message queue is independent within each region.

### Is there a pricing difference between regions?

Amazon SQS pricing is the same for all regions, except China (Beijing). For more information, see [Amazon SQS Pricing](https://aws.amazon.com/sqs/pricing/).

### What is the pricing structure between various regions?

You can transfer data between Amazon SQS and Amazon EC2 or AWS Lambda free of charge within a single region.

When you transfer data between Amazon SQS and Amazon EC2 or AWS Lambda in different regions, you will be charged the normal data transfer rate. For more information, see [Amazon SQS Pricing](https://aws.amazon.com/sqs/pricing/).

## Dead-letter queues

[Close all](https://aws.amazon.com/sqs/faqs/?da=sec&sec=prep#)

### What are dead-letter queues?

A dead-letter queue is an Amazon SQS queue to which a source queue can send messages if the source queue’s consumer application is unable to consume the messages successfully. Dead-letter queues make it easier for you to handle message consumption failures and manage the life cycle of unconsumed messages. You can configure an alarm for any messages delivered to a dead-letter queue, examine logs for exceptions that might have caused them to be delivered to the queue, and analyze message contents to diagnose consumer application issues. Once you recover your consumer application, you can redrive the messages from your dead-letter queue to the source queue.

### How do dead-letter queues work?

When you create your source queue, Amazon SQS allows you to specify a dead-letter queue (DLQ) and the condition under which SQS should move messages to the DLQ. The condition is the number of times a consumer can receive a message from the queue, defined as maxReceiveCount. This configuration of a dead-letter queue with a source queue and the maxReceiveCount is known as the redrive policy. When the ReceiveCount for a message exceeds the maxReceiveCount for a queue, Amazon SQS is designed to move the message to a dead-letter queue (with its original message ID). For example, if the source queue has a redrive policy with maxReceiveCount set to five, and the consumer of the source queue receives a message six times without successfully consuming it, SQS moves the message to the dead-letter queue.

The redrive policy manages the first half of the life cycle of unconsumed messages by moving them from a source queue to a dead-letter queue. Now the dead-letter queue redrive to source queue efficiently completes the cycle by moving those messages back to their source queue, as shown below.

![AWS Local Zones how it works](https://d1.awsstatic.com/legal/AmazonMessaging_SQS_SNS/product-page-diagram_Amazon-SQS.e817373cca6780f567a26cf630526f72b0b2baec.png)

### How does the dead-letter queue redrive to source queue work?

First, it allows you to investigate a sample of messages available in the dead-letter queue by showing message attributes and related metadata. Then, once you have investigated the messages, you can move them back to their source queue(s). You can also select the redrive velocity to configure the rate at which Amazon SQS will move the messages from the dead-letter queue to the source queue.

### Can I use a dead letter queue with FIFO queues?

Yes. However, you must use a FIFO dead letter queue with a FIFO queue. (Similarly, you can use only a standard dead letter queue with a standard queue.)