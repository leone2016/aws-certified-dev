## General

[Close all](https://aws.amazon.com/lambda/faqs/?da=sec&sec=prep#)

### Q: What events can trigger an AWS Lambda function?

Please see our [documentation](http://docs.aws.amazon.com/lambda/latest/dg/intro-core-components.html#intro-core-components-event-sources) for a complete list of event sources.

### Q: What languages does AWS Lambda support?

AWS Lambda natively supports Java, Go, PowerShell, Node.js, C#, Python, and Ruby code, and provides a Runtime API which allows you to use any additional programming languages to author your functions. Please read our documentation on using [Node.js](http://docs.aws.amazon.com/lambda/latest/dg/authoring-function-in-nodejs.html), [Python](http://docs.aws.amazon.com/lambda/latest/dg/python-lambda.html), [Java](http://docs.aws.amazon.com/lambda/latest/dg/java-lambda.html), [Ruby](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html), [C#](http://docs.aws.amazon.com/lambda/latest/dg/current-supported-versions.html), [Go](https://docs.aws.amazon.com/lambda/latest/dg/go-programming-model.html), and [PowerShell](https://docs.aws.amazon.com/lambda/latest/dg/powershell-programming-model.html).

### Q: How does AWS Lambda isolate my code?

Each AWS Lambda function runs in its own isolated environment, with its own resources and file system view. AWS Lambda uses the same techniques as Amazon EC2 to provide security and separation at the infrastructure and execution levels. Visit [documentation](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html) to learn more.

### Q: How does AWS Lambda protect my data and code?

AWS Lambda stores code in Amazon S3 and encrypts it at rest. AWS Lambda performs additional integrity checks while your code is in use. For sensitive information, such as database passwords, we recommend you use client-side encryption using [AWS Key Management Service](http://docs.aws.amazon.com/kms/latest/developerguide/overview.html) and store the resulting values as ciphertext in your environment variable. You will need to include logic in your AWS Lambda function code to decrypt these values. Visit [documentation](https://docs.aws.amazon.com/lambda/latest/dg/security-dataprotection.html) to learn more.

### Q: Why must AWS Lambda functions be stateless?

Keeping functions stateless enables AWS Lambda to rapidly launch as many copies of the function as needed to scale to the rate of incoming events. While AWS Lambda’s programming model is stateless, your code can access stateful data by calling other web services, such as Amazon S3 or Amazon DynamoDB.

### Q: Does AWS Lambda support environment variables?

Yes. You can easily create and modify environment variables from the AWS Lambda Console, CLI, or SDKs. To learn more about environment variables, see the [documentation](http://docs.aws.amazon.com/lambda/latest/dg/env_variables.html).

### Q: Can I store sensitive information in environment variables?

For sensitive information, such as database passwords, we recommend you use client-side encryption using [AWS Key Management Service](http://docs.aws.amazon.com/kms/latest/developerguide/overview.html) and store the resulting values as ciphertext in your environment variable. You will need to include logic in your AWS Lambda function code to decrypt these values.

### Q: Can I share code across functions?

Yes, you can package any code (frameworks, SDKs, libraries, and more) as a [Lambda Layer](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html) and manage and share them easily across multiple functions.

### Q: How do I monitor an AWS Lambda function?

AWS Lambda automatically monitors Lambda functions on your behalf, reporting real-time metrics through Amazon CloudWatch, including total requests, account-level and function-level concurrency usage, latency, error rates, and throttled requests. You can view statistics for each of your Lambda functions via the Amazon CloudWatch console or through the AWS Lambda console. You can also call third-party monitoring APIs in your Lambda function.
 

Visit [Troubleshooting CloudWatch metrics](http://docs.aws.amazon.com/lambda/latest/dg/monitoring-functions.html) to learn more. Standard charges for AWS Lambda apply to use Lambda’s built-in metrics.

### Q: How are compute resources assigned to an AWS Lambda function?

In the AWS Lambda resource model, you choose the amount of memory you want for your function, and are allocated proportional CPU power and other resources. For example, choosing 256MB of memory allocates approximately twice as much CPU power to your Lambda function as requesting 128MB of memory and half as much CPU power as choosing 512MB of memory. To learn more, see our [Function Configuration documentation](https://docs.aws.amazon.com/lambda/latest/dg/resource-model.html).

You can set your memory from 128MB to 10,240MB.

### Q: How long can an AWS Lambda function execute?

AWS Lambda functions can be configured to run up to 15 minutes per execution. You can set the timeout to any value between 1 second and 15 minutes.

### Q: How will I be charged for using AWS Lambda functions?

AWS Lambda is priced on a pay-per-use basis. Please see the [AWS Lambda pricing page](https://aws.amazon.com/lambda/pricing/) for details.

### Q: Does AWS Lambda support versioning?

Yes. By default, each AWS Lambda function has a single, current version of the code. Clients of your Lambda function can call a specific version or get the latest implementation. Please read our documentation on [versioning Lambda functions](http://docs.aws.amazon.com/lambda/latest/dg/versioning-aliases.html).

### Q: How can I deploy my Lambda functions?

AWS Lambda offers flexible deployment options: package and deploy functions as .zip file archives that you can upload directly through the console, CLI, or SDKs, or as container images. Both methods provide the same execution environment, scaling, and operational simplicity, giving you the flexibility to choose the approach that best fits your workflow.

## Using AWS Lambda to process AWS events

[Close all](https://aws.amazon.com/lambda/faqs/?da=sec&sec=prep#)

### Q: What is an event source?

An event source is an AWS service or developer-created application that produces events that trigger an AWS Lambda function to run. Some services publish these events to Lambda by invoking the cloud function directly (for example, Amazon S3). Lambda can also poll resources in other services that do not publish events to Lambda. For example, Lambda can pull records from an Amazon Kinesis stream or an Amazon SQS queue and execute a Lambda function for each fetched message.Many other services, such as AWS CloudTrail, can act as event sources simply by logging to Amazon S3 and using S3 bucket notifications to trigger AWS Lambda functions

### Q: How can my application trigger an AWS Lambda function directly?

You can invoke a Lambda function using a custom event through AWS Lambda’s invoke API. Only the function owner or another AWS account that the owner has granted permission can invoke the function. Visit the [Lambda Developers Guide](http://docs.aws.amazon.com/lambda/latest/dg/welcome.html) to learn more.

### Q: How do I invoke an AWS Lambda function over HTTPS?

You can invoke a Lambda function over HTTPS by defining a custom RESTful API using Amazon API Gateway. This gives you an endpoint for your function which can respond to REST calls like GET, PUT, and POST. Read more about using AWS Lambda with Amazon API Gateway.

## AWS Lambda Snapstart

[Close all](https://aws.amazon.com/lambda/faqs/?da=sec&sec=prep#)

### Q. What is AWS Lambda SnapStart?

AWS Lambda SnapStart can improve startup performance from several seconds to as low as sub-second for latency sensitive applications. SnapStart works by snapshotting your function's initialized memory (and disk) state and caching this snapshot for low-latency access. When your function is subsequently invoked, Lambda resumes [execution environments](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html) from this pre-initialized snapshot instead of initializing them from scratch, improving startup latency. For resiliency, Lambda maintains cached copies of your snapshot and automatically applies software updates, such as runtime upgrades and security patches to them. Visit [documentation](https://docs.aws.amazon.com/lambda/latest/dg/snapstart.html) to learn more.

### Q. How do I configure my Lambda function to use Lambda SnapStart?

Lambda SnapStart is a simple function level configuration that can be configured for new and existing functions by using Lambda API, the AWS Management Console, AWS Command Line Interface (CLI), AWS SDK, AWS Cloud Development Kit (CDK), AWS CloudFormation, and the AWS Serverless Application Model (SAM). When you configure Lambda SnapStart, every function version that is published thereafter benefits from the improved startup performance offered by Lambda SnapStart. To learn more about Lambda SnapStart, see the [documentation](https://docs.aws.amazon.com/lambda/latest/dg/snapstart.html).

### Q. How do I choose between Lambda SnapStart and Provisioned Concurrency (PC)?

Lambda SnapStart is a performance optimization that helps your functions to achieve faster start-up times by reducing the variable latency incurred during execution of one-time initialization code. While Lambda SnapStart reduces startup latency, it works as a best-effort optimization, and does not guarantee elimination of cold starts. If your application has strict latency requirements and requires double-digit millisecond startup times, we recommend you use PC.

### Q. Which runtimes does Lambda SnapStart support?

Lambda SnapStart supports multiple runtimes, including Java 11 (and newer), Python 3.12 (and newer) and .NET 8 (and newer). Future versions of runtimes will be supported after they are released. For all runtimes supported by Lambda, see the [Lambda runtimes documentation](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html).

### Q. Can I enable both Lambda SnapStart and PC on the same function?

No. Lambda SnapStart and PC cannot be enabled at the same time, on the same function.

### Q. Can I configure a Lambda SnapStart function with a virtual private cloud (VPC)?

Yes. You can configure a Lambda SnapStart function to access resources in a virtual private cloud (VPC). For more information on how to configure your function with a VPC, see the [Lambda documentation](https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc.html).

### Q. Will I be charged for Lambda SnapStart?

Yes, you will be charged for caching a snapshot over the period that your function version is active, for a minimum of 3 hours and per milli-second thereafter. The price depends on the amount of memory you allocate to your function. You are also charged each time Lambda resumes an execution environment by restoring your snapshot, with the price depending on the amount of memory you allocate to your function. To learn more about pricing for SnapStart, visit [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/#SnapStart_Pricing).

SnapStart pricing does not apply to [supported Java managed runtimes](https://docs.aws.amazon.com/lambda/latest/dg/snapstart.html#snapstart-runtimes), which can only cache a snapshot for up to 14 days.

## Provisioned Concurency

[Close all](https://aws.amazon.com/lambda/faqs/?da=sec&sec=prep#)

### Q: What is AWS Lambda Provisioned Concurrency?

[Provisioned Concurrency](https://docs.aws.amazon.com/lambda/latest/dg/provisioned-concurrency.html) gives you greater control over the performance of your serverless applications. When enabled, Provisioned Concurrency keeps functions initialized and hyper-ready to respond in double-digit milliseconds.

### Q: How do I set up and manage Provisioned Concurrency?

You can configure concurrency on your function through the AWS Management Console, the Lambda API, the AWS CLI, and AWS CloudFormation. The simplest way to benefit from Provisioned Concurrency is by using AWS Auto Scaling. You can use Application Auto Scaling to configure schedules, or have Auto Scaling automatically adjust the level of Provisioned Concurrency in real time as demand changes. To learn more about Provisioned Concurrency, [see the documentation](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html).

### Q: How will I be charged for Provisioned Concurrency?

Provisioned Concurrency adds a pricing dimension, of ‘Provisioned Concurrency’, for keeping functions initialized. When enabled, you pay for the amount of concurrency that you configure and for the period of time that you configure it. When your function executes while Provisioned Concurrency is configured on it, you also pay for Requests and execution Duration. To learn more about the pricing of Provisioned Concurrency, see [AWS Lambda Pricing](https://aws.amazon.com/lambda/pricing/).

### Q: When should I use Provisioned Concurrency?

Provisioned Concurrency is ideal for building latency-sensitive applications, such as web or mobile backends, synchronously invoked APIs, and interactive microservices. You can easily configure the appropriate amount of concurrency based on your application's unique demand. You can increase the amount of concurrency during times of high demand and lower it, or turn it off completely, when demand decreases.

## Lambda@Edge

[Close all](https://aws.amazon.com/lambda/faqs/?da=sec&sec=prep#)

### Q: What is Lambda@Edge?

[Lambda@Edge](https://aws.amazon.com/lambda/edge/) allows you to run code across AWS locations globally without provisioning or managing servers, responding to end-users at the lowest network latency. You just upload your Node.js or Python code to AWS Lambda and configure your function to be triggered in response to [Amazon CloudFront](https://aws.amazon.com/cloudfront/) requests (i.e., when a viewer request lands, when a request is forwarded to or received back from the origin, and right before responding back to the end-user). The code is then ready to execute across AWS locations globally when a request for content is received, and scales with the volume of CloudFront requests globally. Learn more in our [documentation](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-at-the-edge.html).

### Q: How do I use Lambda@Edge?

To use Lambda@Edge, you just upload your code to AWS Lambda and associate a function version to be triggered in response to Amazon CloudFront requests. Your code must satisfy the Lambda@Edge service limits. Lambda@Edge supports Node.js and Python for global invocation by CloudFront events at this time. Learn more in our [documentation](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-at-the-edge.html).

### Q: When should I use Lambda@Edge?

Lambda@Edge is optimized for latency-sensitive use cases where your end viewers are distributed globally. All the information you need to make a decision should be available at the CloudFront edge, within the function and the request. This means that use cases where you are looking to make decisions on how to serve content based on user characteristics (e.g., location, client device, etc.) can now be executed and served close to your users without having to be routed back to a centralized server.

### Q: Can I deploy my existing Lambda functions for global invocation?

You can associate existing Lambda functions with CloudFront events for global invocation if the function satisfies the Lambda@Edge service requirements and limits. Read more [here](http://docs.aws.amazon.com/lambda/latest/dg/API_UpdateFunctionConfiguration.html) on how to update your function properties.

## Scalability and availability

[Close all](https://aws.amazon.com/lambda/faqs/?da=sec&sec=prep#)

### Q: How available are AWS Lambda functions?

AWS Lambda is designed to use replication and redundancy to provide high availability for both the service itself and for the Lambda functions it operates. There are no maintenance windows or scheduled downtimes for either.

### Q: Do my AWS Lambda functions remain available when I change my code or its configuration?

Yes. When you update a Lambda function, there will be a brief window of time, typically less than a minute, when requests could be served by either the old or the new version of your function.

### Q: Is there a limit to the number of AWS Lambda functions I can execute at once?

No. AWS Lambda is designed to run many instances of your functions in parallel. However, AWS Lambda has a default safety throttle, for the number of concurrent executions per account per region (visit [here](http://docs.aws.amazon.com/lambda/latest/dg/concurrent-executions.html#concurrent-execution-safety-limit) for info on default safety throttle limits). You can also control the maximum concurrent executions for individual AWS Lambda functions, which you can use to reserve a subset of your account concurrency limit for critical functions, or cap traffic rates to downstream resources.

If you wish to submit a request to increase the concurrent execution limit, you can use [Service Quotas](https://docs.aws.amazon.com/servicequotas/latest/userguide/request-quota-increase.html) to request a limit increase request.

### Q: What happens if my account exceeds the default throttle limit on concurrent executions?

On exceeding the maximum concurrent executions limit, AWS Lambda functions being invoked synchronously will return a throttling error (429 error code). Lambda functions being invoked asynchronously can absorb reasonable bursts of traffic for approximately 15-30 minutes, after which incoming events will be rejected as throttled. In case the Lambda function is being invoked in response to Amazon S3 events, events rejected by AWS Lambda may be retained and retried by S3 for 24 hours. Events from Amazon Kinesis streams and Amazon DynamoDB streams are retried until the Lambda function succeeds or the data expires. Amazon Kinesis and Amazon DynamoDB Streams retain data for 24 hours.

### Q: Are default maximum concurrent execution limits applied on a per function level?

The default maximum concurrent execution limit is applied at the account level. However, you can also set limits on individually functions as well (visit [here](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html) for info on Reserved Concurrency).

### Q. How quickly do my AWS Lambda functions scale?

Each synchronously invoked Lambda function can scale at a rate of up to 1000 concurrent executions every 10 seconds. While Lambda's scaling rate is suitable for most use cases, it is particularly ideal for those with predictable or unpredictable bursts of traffic. For example, SLA-bound data processing would require predictable yet rapid scaling to meet processing demand. Similarly, serving breaking news articles, or flash sales could drive unpredictable levels of traffic in a short period of time. Lambda's scaling rate can facilitate such use cases without additional configurations or tooling. Additionally, the concurrency scaling limit is a function-level limit, which means each function in your account scales independently of other functions.

### Q: What happens if my Lambda function fails while processing an event?

On failure, Lambda functions being invoked synchronously will respond with an exception. Lambda functions being invoked asynchronously are retried at least 3 times. Events from Amazon Kinesis streams and Amazon DynamoDB streams are retried until the Lambda function succeeds or the data expires. Kinesis and DynamoDB Streams retain data for a minimum of 24 hours.

### Q: What happens if my Lambda function invocations exhaust the available policy?

On exceeding the retry policy for asynchronous invocations, you can configure a “dead letter queue” (DLQ) into which the event will be placed; in the absence of a configured DLQ the event may be rejected. On exceeding the retry policy for stream-based invocations, the data would have already expired and therefore rejected.

### Q: What resources can I configure as a dead letter queue for a Lambda function?

You can configure an Amazon SQS queue or an Amazon SNS topic as your dead letter queue.

## Security and access control

[Close all](https://aws.amazon.com/lambda/faqs/?da=sec&sec=prep#)

### Q: How do I allow my AWS Lambda function access to other AWS resources?

You grant permissions to your Lambda function to access other resources using an IAM role. AWS Lambda assumes the role while executing your Lambda function, so you always retain full, secure control of exactly which AWS resources it can use. Visit [Setting up AWS Lambda](http://docs.aws.amazon.com/lambda/latest/dg/setting-up.html) to learn more about roles.

### Q: How do I control which Amazon S3 buckets can call which AWS Lambda functions?

When you configure an Amazon S3 bucket to send messages to an AWS Lambda function, a resource policy rule will be created that grants access. Visit the [Lambda Developer Guide](http://docs.aws.amazon.com/lambda/latest/dg/welcome.html) to learn more about resource policies and access controls for Lambda functions.

### Q: How do I control which Amazon DynamoDB table or Amazon Kinesis stream an AWS Lambda function can poll?

Access controls are managed through the Lambda function role. The role you assign to your Lambda function also determines which resource(s) AWS Lambda can poll on its behalf. Visit the [Lambda Developer Guide](http://docs.aws.amazon.com/lambda/latest/dg/welcome.html) to learn more.

### Q: How do I control which Amazon SQS queue an AWS Lambda function can poll?

Access controls can be managed by the Lambda function role or a resource policy setting on the queue itself. If both policies are present, the more restrictive of the two permissions will be applied.

### Q: How do I access resources in Amazon VPC from my AWS Lambda function?

You can enable Lambda functions to access resources in your VPC by specifying the subnet and security group as part of your function configuration. Lambda functions configured to access resources in a particular VPC will not have access to the internet as a default configuration. To grant internet to these functions, use [internet gateways](https://docs.aws.amazon.com/vpc/latest/userguide/extend-intro.html). By default, Lambda functions communicate with resources in a dual-stack VPC over IPv4. You can configure your functions to access resources in a dual-stack VPC over IPv6. For more details on Lambda functions configured with VPC, see [Lambda Private Networking with VPC](https://docs.aws.amazon.com/lambda/latest/dg/foundation-networking.html).

### Q: What is Code Signing for AWS Lambda?

Code Signing for AWS Lambda offers trust and integrity controls that enable you to verify that only unaltered code from approved developers is deployed in your Lambda functions. You can use [AWS Signer](https://docs.aws.amazon.com/signer/latest/developerguide/Welcome.html), a fully-managed code signing service, to digitally sign code artifacts and configure your Lambda functions to verify the signatures at deployment. Code Signing for AWS Lambda is currently only available for functions packaged as ZIP archives.

### Q: How do I create digitally signed code artifacts?

You can create digitally signed code artifacts using a [Signing Profile](https://docs.aws.amazon.com/signer/latest/api/API_SigningProfile.html) through the AWS Signer console, the Signer API, SAM CLI or AWS CLI. To learn more, please see the [documentation for AWS Signer](https://docs.aws.amazon.com/signer/latest/api/Welcome.html).

### Q: How do I configure my Lambda functions to enable code signing?

You can enable code signing by creating a Code Signing Configuration through the AWS Management Console, the Lambda API, the AWS CLI, AWS CloudFormation, and AWS SAM. Code Signing Configuration helps you specify the approved signing profiles and configure whether to warn or reject deployments if signature checks fail. Code Signing Configurations can be attached to individual Lambda functions to enable the code signing feature. Such functions now start verifying signatures at deployment.

### Q: What signature checks does AWS Lambda perform on deployment?

AWS Lambda can perform the following signature checks at deployment:

• Corrupt signature - This occurs if the code artifact has been altered since signing.
• Mismatched signature - This occurs if the code artifact is signed by a signing profile that is not approved.
• Expired signature - This occurs if the signature is past the configured expiry date.
• Revoked signature - This occurs if the signing profile owner revokes the signing jobs.

To learn more, please see the [AWS Lambda documentation](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html).

### Q: Can I enable code signing for existing functions?

Yes, you can enable code signing for existing functions by attaching a code signing configuration to the function. You can do this using the AWS Lambda console, the Lambda API, the AWS CLI, AWS CloudFormation, and AWS SAM.

### Q: Is there any additional cost for using Code Signing for AWS Lambda?

There is no additional cost when using Code Signing for AWS Lambda. You pay the standard price for AWS Lambda. To learn more, please see [Pricing](https://aws.amazon.com/lambda/pricing/).

## Advanced monitoring capabilities

[Close all](https://aws.amazon.com/lambda/faqs/?da=sec&sec=prep#)

### Q: What advanced logging controls are supported on Lambda?

To provide you a simplified and enhanced logging experience by default, AWS Lambda offers advanced logging controls such as the ability to natively capture Lambda function logs in JSON structured format, control the log level filtering of Lambda function logs without making any code changes, and customize the Amazon CloudWatch log group Lambda sends logs to.

### Q: What can I use advanced logging controls for?

You can capture Lambda function logs in JSON structured format without having to use your own logging libraries. JSON structured logs make it easier to search, filter, and analyze large volumes of log entries. You can control the log level filtering of Lambda function logs without making any code changes, which enables you to choose the required logging granularity level for Lambda functions without sifting through large volumes of logs when debugging and troubleshooting errors. You can also set which [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) log group Lambda sends logs to, making it easier to aggregate logs from multiple functions within an application in one place. You can then apply security, governance, and retention policies to logs at the application level rather than individually to every function.

### Q. How do I use advanced logging controls?

You can specify advanced logging controls for your Lambda functions using AWS Lambda API, AWS Lambda console, AWS CLI, AWS Serverless Application Model (SAM), and AWS CloudFormation. To learn more, visit the [launch blog post](https://aws.amazon.com/blogs/compute/introducing-advanced-logging-controls-for-aws-lambda-functions/) for advanced logging controls or the [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/monitoring-cloudwatchlogs.html#monitoring-cloudwatchlogs-advanced).

### Q. Can I use my own logging libraries to generate JSON structured logs for my Lambda function?

Yes, you can use your own logging libraries to generate Lambda logs in JSON structured format. To ensure your logging libraries work seamlessly with Lambda’s native JSON structured logging capability, Lambda will not double-encode any logs generated by your function that are already JSON encoded. You can also use [Powertools for AWS Lambda](https://github.com/aws-powertools/) library to capture Lambda logs in JSON structured format.

### Q. How will I be charged for using the advanced logging controls?

There is no additional charge for using advanced logging controls on Lambda. You will continue to be charged for ingestion and storage of your Lambda logs by Amazon CloudWatch Logs. See [CloudWatch pricing page](https://aws.amazon.com/cloudwatch/pricing/) for log pricing details.

### Q: What is CloudWatch Application Signals and how does it work with Lambda?

CloudWatch Application Signals is an application performance monitoring (APM) solution which enables developers and operators to easily monitor the health and performance of serverless applications built with Lambda. Application Signals provides pre-built, standardized dashboards for critical application metrics, correlated traces, and interactions between Lambda functions and their dependencies — all without requiring manual instrumentation or code changes from developers.

### Q: What is CloudWatch Live Tail and how does it work with Lambda?

CloudWatch Logs Live Tail is an interactive log streaming and analytics capability which provides real-time visibility into logs, making it easier to develop and troubleshoot Lambda functions. This allows developers to quickly test and validate code or configuration changes in real time, accelerating the author-test-deploy cycle (also known as the “inner dev loop”) when building applications with Lambda. The Live Tail experience also enables operators and DevOps teams to detect and debug failures and critical errors in Lambda function code more efficiently, reducing the mean time to recovery (MTTR) when troubleshooting Lambda function errors.