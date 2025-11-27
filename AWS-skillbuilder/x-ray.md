## Simple setup

[Close all](https://aws.amazon.com/xray/features/#)

### Overview

AWS X-Ray can be used with applications running on [Amazon Elastic Compute Cloud](https://aws.amazon.com/ec2/) (EC2), [Amazon EC2 Container Service](https://aws.amazon.com/ecs/) (Amazon ECS), [AWS Lambda](https://aws.amazon.com/lambda/), [AWS Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/). It’s easy to get started with X-Ray. You just integrate the X-Ray SDK with your application and install the X-Ray agent. With AWS Elastic Beanstalk, you only have to integrate the X-Ray SDK with your application since the X-Ray agent is pre-installed on Elastic Beanstalk.

## End-to-end tracing

[Close all](https://aws.amazon.com/xray/features/#)

### Overview

AWS X-Ray provides an end-to-end, cross-service view of requests made to your application. It gives you an application-centric view of requests flowing through your application by aggregating the data gathered from individual services in your application into a single unit called a trace. You can use this trace to follow the path of an individual request as it passes through each service or tier in your application so that you can pinpoint where issues are occurring.

### AWS Service and Database Integrations

AWS X-Ray supports applications running on Amazon Elastic Compute Cloud (Amazon EC2), Amazon EC2 Container Service (Amazon ECS), AWS Lambda, and AWS Elastic Beanstalk. The X-Ray SDK captures metadata for requests made to MySQL and PostgreSQL databases (self-hosted, Amazon RDS, Amazon Aurora), and Amazon DynamoDB. It also captures metadata for requests made to Amazon Simple Queue Service and Amazon Simple Notification Service.

### Request sampling

You can set the trace sampling rate that is best suited for your production applications or applications in development. X-Ray continually traces requests made to your application and stores a sampling of the requests for your analysis. This provides you with the appropriate amount of data to make your analysis meaningful, while avoiding the overhead of storing and managing excessive data volume.

### Support for multiple languages

AWS X-Ray supports tracing for applications that are written in Node.js, Java, and .NET.

## Service map

[Close all](https://aws.amazon.com/xray/features/#)

### Overview

AWS X-Ray creates a map of services used by your application with trace data that you can use to drill into specific services or issues. This provides a view of connections between services in your application and aggregated data for each service, including average latency and failure rates. You can create dependency trees, perform cross-availability zone or region call detections, and more.

## Server- and Client-side latency detection

[Close all](https://aws.amazon.com/xray/features/#)

### Overview

AWS X-Ray allows you to visually detect node and edge latency distribution directly from the service map. You can quickly isolate outliers, graph pattern and trends, drill into traces and filter by built-in keys and custom annotations to better understand performance issues impacting your application and end users.

## Data annotation and filtering

[Close all](https://aws.amazon.com/xray/features/#)

### Overview

AWS X-Ray lets you add annotations to data emitted from specific components or services in your application. You can use this to append business-specific metadata that help you better diagnose issues. You can also view and filter data for traces by properties such as annotation value, average latencies, HTTP response status, timestamp, database table used, and more.

## Console and programmatic access

[Close all](https://aws.amazon.com/xray/features/#)

### Overview

You can use AWS X-Ray with the AWS Management Console, AWS CLI, and AWS SDKs. The X-Ray API lets you programmatically access the service so you can easily export trace data or ingest the data into your own tools and custom analytics dashboards.

## Security

[Close all](https://aws.amazon.com/xray/features/#)

### Overview

AWS X-Ray is integrated with [AWS Identity and Access Management](https://aws.amazon.com/iam/) (IAM) so that you can control which users and resources have permission to access your traces and how.