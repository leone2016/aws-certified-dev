Below is your **practice assignment written in the same structured format as the previous AWS practice (S3 + SNS + Lambda)**.
 It keeps the same **professor / lab format, acceptance criteria, tasks, and submission requirements**.

------

# AWS Assignment – ALB, NLB and Auto Scaling Groups

**Total Score:** 10 out of 10

Start: **2025-12-15 10:00:00 America/Chicago**
 Stop: **2025-12-16 10:00:00 America/Chicago**

------

# AWS Load Balancing and Auto Scaling Lab

## 3 Deliverable(s)

zip

------

# Lab Exercise: High Availability and Auto Scaling with ALB, NLB, and EC2

## Objective

This assignment demonstrates how modern cloud applications achieve **high availability, scalability, and reliability** using AWS infrastructure.

You will learn how to:

- Deploy web servers in **multiple Availability Zones**
- Distribute traffic using **Application Load Balancer (ALB)** and **Network Load Balancer (NLB)**
- Automatically scale infrastructure using **Auto Scaling Groups (ASG)**
- Monitor health checks and scaling activities

These concepts are fundamental in **production cloud architectures and microservices deployments**.

------

# Acceptance Criteria

Include the following screenshots in your submission PDF:

• Screenshot showing **healthy instances in both Target Groups of ALB and NLB**

• Screenshot of the **Activity tab in the Auto Scaling Group**

------

# Task 1 — Run Web Servers Behind an Application Load Balancer (ALB)

## Goal

Deploy two EC2 web servers in different Availability Zones and distribute traffic through an **Application Load Balancer (Layer 7)**.

------

## Step 1 — Create EC2 Instance #1

Region: **us-east-1**

Availability Zone: **us-east-1a**

Install a simple web application.

User data example:

```
#!/bin/bash
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>I am server one</h1>" > /var/www/html/index.html
```

------

## Step 2 — Create EC2 Instance #2

Availability Zone: **us-east-1b**

User data:

```
#!/bin/bash
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>I am server two</h1>" > /var/www/html/index.html
```

------

## Step 3 — Create Target Group

# How to Create a Target Group (TG) for ALB

### 1. Open the AWS Console

Go to:

```
EC2 → Load Balancing → Target Groups
```

Then click:

```
Create target group
```

------

# 2. Configure the Target Group

### Target type

Select:

```
Instances
```

Because we are routing traffic to EC2 instances.

------

### Target Group name

Example:

```
web-alb-tg
```

------

### Protocol and port

For **ALB (Layer 7)** use:

```
Protocol: HTTP
Port: 80
```

------

### VPC

Select the **same VPC where your EC2 instances are running**.

------

### Health check settings

Use the default values:

```
Protocol: HTTP
Path: /
Port: traffic port
```

Why `/`?

Because Apache serves the default page at `/`.

### Register Targets (Add EC2 instances)

You will see your EC2 instances listed.

Select both:

```
server-one
server-two
```

Then click:

```
Include as pending below
```

Then click:

```
Create target group
```

------

## Step 4 — Create Application Load Balancer

Configuration:

Type: **Application Load Balancer**

Scheme: **Internet-facing**

Availability Zones:

```
us-east-1a
us-east-1b
```

Listener:

```
HTTP : 80
```

Forward to the Target Group created earlier.

------

## Step 5 — Test the Load Balancer

Open the ALB DNS name in your browser:

```
http://ALB-DNS-name
```

Refresh multiple times.

Expected behavior:

```
I am server one
I am server two
```

Traffic should alternate between instances.

------

## Important Note (Debugging)

The load balancer can **only route traffic to instances located in the same Availability Zones where the load balancer nodes exist**.

If instances appear **unused or unhealthy**, verify:

- Web server is running
- Port **80 is open**
- Health check path works

For easier debugging, open port 80 to:

```
0.0.0.0/0
```

------

# Task 2 — Run Web Servers Behind a Network Load Balancer (NLB)

## Goal

Repeat the same architecture but using **Network Load Balancer (Layer 4)** instead of ALB.

------

## Key Difference

| Load Balancer | OSI Layer | Protocol     |
| ------------- | --------- | ------------ |
| ALB           | Layer 7   | HTTP / HTTPS |
| NLB           | Layer 4   | TCP          |

------

## Steps

Create a new Target Group with:

Protocol:

```
TCP
```

Port:

```
80
```

Register the same EC2 instances.

Create an **NLB** and attach the target group.

------

## Test

Open the NLB DNS endpoint.

Verify traffic is distributed between both servers.

------

# Task 3 — Run Web Servers Using Auto Scaling Group (ASG)

## Goal

Instead of manually managing EC2 instances, automatically scale servers based on demand.

------

## Step 1 — Create Launch Template

Use **Launch Template** (recommended instead of Launch Configuration).

Configuration:

Name:

```
web-launch-template
```

AMI:

```
Amazon Linux
```

Instance type:

```
t2.micro
```

------

## User Data Script

This script installs and starts Apache automatically when the instance launches.

```
#!/bin/bash
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello YourName from $(hostname -f)</h1>" > /var/www/html/index.html
```

------

## Step 2 — Create Auto Scaling Group

Configuration:

Launch Template:

```
web-launch-template
```

Subnets:

```
us-east-1a
us-east-1b
```

Attach to existing load balancer:

```
Select ALB target group
```

Health check type:

```
ELB
```

------

## Step 3 — Configure Scaling Policy

Capacity configuration example:

```
Desired capacity: 2
Minimum capacity: 2
Maximum capacity: 4
```

Scaling policy:

```
Target tracking policy
Metric: Average CPU Utilization
Target value: 50%
```

------

## Step 4 — Simulate Load

You can simulate high CPU load using the **stress** tool.

SSH into an EC2 instance:

```
sudo yum install stress -y
stress --cpu 4 --timeout 300
```

The Auto Scaling Group should launch additional instances.

Verify scaling activity in:

```
Auto Scaling Group → Activity tab
```

------

# Task 4 — Clean Up Resources

⚠️ AWS resources generate costs.

Delete the following after completing the assignment:

- Auto Scaling Group
- Launch Template
- ALB
- NLB
- Target Groups
- EC2 instances

------

# Submission Instructions

Submit a **ZIP file** containing:

1️⃣ **PDF Report**

Include screenshots of:

- Healthy instances in **ALB Target Group**
- Healthy instances in **NLB Target Group**
- **Auto Scaling Group Activity tab**

2️⃣ **README.md**

Explain briefly:

- Difference between ALB and NLB
- How Auto Scaling improves reliability
- How health checks work

------

# Grading Criteria (10 points)

| Criteria                                       | Points |
| ---------------------------------------------- | ------ |
| ALB setup with two healthy instances           | 2      |
| NLB setup with healthy instances               | 2      |
| Auto Scaling Group with launch template        | 2      |
| Scaling policy configuration                   | 1      |
| Successful scaling event shown in Activity tab | 1      |
| Correct multi-AZ architecture                  | 1      |
| Documentation and screenshots                  | 1      |

------

# Instructor’s Note

> Modern cloud applications must be **highly available and scalable**.
>  Load balancers distribute traffic across servers, while Auto Scaling Groups automatically add or remove servers depending on demand.
>  These technologies are widely used in **microservices architectures and large-scale cloud platforms**.

------

If you want, I can also help you create **Assignment 5** in the same format for something like:

- **API Gateway + Lambda + DynamoDB**
- **Microservices with ECS**
- **Kubernetes (EKS) deployment**
- **CI/CD pipeline with CodePipeline**

These are typically the **next AWS topics after ALB + ASG**.