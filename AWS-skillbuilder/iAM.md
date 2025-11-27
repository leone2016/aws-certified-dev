## General

[Close all](https://aws.amazon.com/iam/faqs/?da=sec&sec=prep#)

### What is AWS Identity and Access Management (IAM)?

IAM provides fine-grained access control across all of AWS. With IAM, you can control access to services and resources under specific conditions. Use IAM policies to manage permissions for your workforce and systems to ensure [least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege). IAM is offered at no additional charge. For more information, see [What is IAM?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)

### How does IAM work and what can I do with it?

IAM provides authentication and authorization for AWS services, which evaluate if an AWS request is allowed or denied. Access is denied by default and is allowed only when a policy explicitly grants access. You can attach policies to roles and resources to control access across AWS. For more information, see [How IAM works](https://docs.aws.amazon.com/IAM/latest/UserGuide/intro-structure.html).

### What are least-privilege permissions?

When you set permissions with IAM policies, grant only the permissions required to perform a task. This practice is known as [granting least privilege.](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege) You can apply least-privilege permissions in IAM by defining the actions that can be taken on specific resources under specific conditions. For more information, see [Access management for AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html).

### How do I get started with IAM?

To get started using IAM to manage permissions for AWS services and resources, create an IAM role and grant it permissions. For [workforce users](https://aws.amazon.com/iam/identity-center), create a role that can be assumed by your identity provider. For systems, create a role that can be assumed by the service you are using, such as [Amazon EC2](https://aws.amazon.com/ec2/) or [AWS Lambda](https://aws.amazon.com/lambda/). After you create a role, you can attach a policy to the role to grant permissions that meet your needs. When you are just starting out, you might not know the specific permissions you need, so you can start with broader permissions. [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies) provide permissions to help you get started and are available in all AWS accounts. Then, reduce permissions further by defining [customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies) specific to your use cases. You can create and manage policies and roles in the IAM console, or via AWS APIs or the AWS CLI. For more information, see [Getting started with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started.html).

## IAM resources

[Close all](https://aws.amazon.com/iam/faqs/?da=sec&sec=prep#)

### What are IAM roles and how do they work?

AWS Identity and Access Management (IAM) roles provide a way to access AWS by relying on [temporary security credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp.html). Each role has a set of [permissions](https://aws.amazon.com/iam/details/manage-permissions/) for making AWS service requests, and a role is not associated with a specific user or group. Instead, trusted entities such as [identity providers](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers.html) or AWS services assume roles. For more information, see [IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html).

### Why should I use IAM roles?

Use IAM roles to grant access to your AWS accounts by relying on short-term credentials, a security best practice. Authorized identities, which can be AWS services or users from your identity provider, can assume roles to make AWS requests. To grant permissions to a role, attach an IAM policy to it. For more information, see [Common scenarios for IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_common-scenarios.html).

### What are IAM users and should I still be using them?

IAM users are identities with long-term credentials. You might be using IAM users for [workforce users](https://aws.amazon.com/single-sign-on/faqs/#General). In this case, AWS recommends using an identity provider and federating into AWS by assuming roles. You can also use roles to grant cross-account access to services and features such as Lambda functions. In some scenarios, you might require IAM users with [access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) that have long-term credentials with access to your AWS account. For these scenarios, we recommend using IAM [access last used information](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_finding-unused.html) to rotate credentials often and remove credentials that are not being used. For more information, see [Overview of AWS identity management: Users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html).

### What are IAM policies?

IAM [policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) define permissions for the entities you attach them to. For example, to grant access to an IAM role, attach a policy to the role. The permissions defined in the policy determine whether requests are allowed or denied. You also can attach policies to some resources, such as Amazon S3 buckets, to grant direct, cross-account access. You can also attach policies to an AWS organization or organizational unit to restrict access across multiple accounts. AWS evaluates these policies when an IAM role makes a request. For more information, see [Identity-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html#policies_id-based).

## Granting access

[Close all](https://aws.amazon.com/iam/faqs/?da=sec&sec=prep#)

### How do I grant access to services and resources by using IAM?

To grant access to services and resources by using AWS Identity and Access Management (IAM), attach IAM policies to roles or resources. You can start by attaching [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies), which are owned and updated by AWS and are available in all AWS accounts. If you know the specific permissions required for your use cases, you can create [customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies) and attach them to roles. Some AWS resources provide a way to grant access by defining a policy attached to resources, such as Amazon S3 buckets. These [resource-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html) allow you to grant direct, cross-account access to the resources to which they are attached. For more information, see [Access management for AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html).

### How do I create IAM policies?

To assign permissions to a role or resource, create a policy, which is a [JavaScript Object Notation (JSON)](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_grammar.html) document that defines permissions. This document includes permissions statements that grant or deny access to specific service actions, resources, and conditions. After you create a policy, you can attach it to one or more AWS roles to grant permissions to your AWS account. To grant direct, cross-account access to resources, such as Amazon S3 buckets, use resource-based policies. Create your policies in the IAM console or via AWS APIs or the AWS CLI. For more information, see [Define custom IAM permissions with customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_create.html).

### What are AWS managed policies and when should I use them?

AWS managed policies are created and administered by AWS and cover common use cases. As you get started, you can grant broader permissions by using the AWS managed policies that are available in your AWS account and common across all AWS accounts. As you refine your requirements, you can reduce permissions by defining customer managed policies specific to your use cases with the goal of achieving least-privilege permissions. For more information, see [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies).

### What are customer managed policies and when should I use them?

To grant only the permissions required to perform tasks, you can create customer managed policies that are specific to your use cases and resources. Use customer managed policies to continue refining permissions for your specific requirements. For more information, see [Customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies).

### What are inline policies and when should I use them?

Inline policies are embedded in and inherent to specific IAM roles. Use inline policies if you want to maintain a strict one-to-one relationship between a policy and the identity to which it is applied. For example, you can grant administrative permissions to ensure they are not attached to other roles. For more information, see [Inline policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#inline-policies).

### What are resource-based policies and when should I use them?

Resource-based policies are permissions policies that are attached to resources. With resource-based policies, you can define who has access to a resource and which actions they can perform with it. For example, you can attach resource-based policies to Amazon S3 buckets, [Amazon SQS](https://aws.amazon.com/sqs/) queues, VPC endpoints, and [AWS Key Management Service](https://aws.amazon.com/kms/) (AWS KMS) encryption keys. Use resource-based policies to grant direct, cross-account access. For a list of services that support resource-based policies, see [AWS services that work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html). For more information, see [Identity-based policies and resource-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html).

### What is role-based access control (RBAC)?

RBAC provides a way for you to assign permissions based on a person’s job function, known outside of AWS as a role. IAM provides RBAC by defining IAM roles with permissions that align with job functions. You can then grant individuals access to assume these roles to perform specific job functions. With RBAC, you can audit access by looking at each IAM role and its attached permissions. For more information, see [Comparison of ABAC to the traditional RBAC model](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_attribute-based-access-control.html#introduction_attribute-based-access-control_compare-rbac).

### How do I grant access with RBAC?

As a best practice, grant access only to the specific service actions and resources required to perform each task. This is known as [granting least privilege](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege). When employees add new resources, you must update policies to allow access to those resources.

### What is attribute-based access control (ABAC)?

ABAC is an authorization strategy that defines permissions based on attributes. In AWS, these attributes are called [tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_tags.html), and you can define them on AWS resources, IAM roles, and in role sessions. With ABAC, you define a set of permissions based on the value of a tag. You can grant fine-grained permissions to specific resources by requiring the tags on the role or session to match the tags on the resource. For example, you can author a policy that grants developers access to resources tagged with the job title “developers.” ABAC is helpful in environments that are growing rapidly by granting permissions to resources as they are created with specific tags. For more information, see [Attribute-Based Access Control (ABAC) for AWS](https://aws.amazon.com/identity/attribute-based-access-control/).

### How do I grant access by using ABAC?

To grant access by using ABAC, first define the tag keys and values you want to use for access control. Then, ensure your IAM role has the appropriate tag keys and values. If multiple identities use this role, you also can define session tag keys and values. Next, ensure that your resources have the appropriate tag keys and values. You can also require users to create resources with appropriate tags and restrict access to modify them. After your tags are in place, define a policy that grants access to specific actions and resource types, but only if the role or session tags match the resource tags. For a detailed tutorial that demonstrates how to use ABAC in AWS, see [IAM tutorial: Define permissions to access AWS resources based on tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_attribute-based-access-control.html).

### What is IAM temporary delegation?

IAM temporary delegation is a feature that enables Amazon and AWS Partners to request temporary, limited access to your AWS account to perform specific tasks on your behalf. You review and approve each request before granting access, which automatically expires after a specified duration. This feature accelerates product onboarding and simplifies ongoing management by allowing product providers to automate deployment and configuration tasks instead of requiring you to manually configure multiple AWS services. For one-time or occasional tasks like initial setup, maintenance, or feature upgrades, product providers receive temporary credentials. For ongoing operations that require persistent access, product providers can use temporary delegation to create an IAM role with a permission boundary that defines the role's maximum permissions. For more information see the [AWS IAM user guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies-temporary-delegation.html)

## Restricting access

[Close all](https://aws.amazon.com/iam/faqs/?da=sec&sec=prep#)

### How do I restrict access by using IAM?

With AWS Identity and Access Management (IAM), all access is denied by default and requires a policy that grants access. As you manage permissions at scale, you might want to implement [permissions guardrails](https://docs.aws.amazon.com/prescriptive-guidance/latest/security-reference-architecture/organizations.html) and restrict access across your accounts. To restrict access, specify a Deny statement in any policy. If a Deny statement applies to an access request, it always prevails over an Allow statement. For example, if you allow access to all actions in AWS but deny access to IAM, any request to IAM is denied. You can include a Deny statement in any type of policy, including identity-based, resource-based, and service control policies with AWS Organizations. For more information, see [Controlling CloudFormation access with AWS Identity and Access Management](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-iam-template.html).

### What are AWS Organizations service control policies (SCPs) and when should I use them?

[SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html) are similar to IAM policies and use almost the same syntax. However, SCPs don’t grant permissions. Instead, SCPs allow or deny access to AWS services for individual AWS accounts with Organizations member accounts, or for groups of accounts within an organizational unit. The specified actions from an SCP affect all IAM users and roles, including the root user of the member account. For more information, see [Policy evaluation logic](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html).

## Analyzing access

[Close all](https://aws.amazon.com/iam/faqs/?da=sec&sec=prep#)

### How do I work toward least-privilege permissions?

When you get started granting permissions, you can start with broader permissions as you explore and experiment. As your use cases mature, AWS recommends that you refine permissions to grant only the permissions required with the goal of achieving [least-privilege permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#grant-least-privilege). AWS provides tools to help you refine your permissions. You can start with [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#aws-managed-policies), which are created and administered by AWS and include permissions for common use cases. As you refine your permissions, define specific permissions in [customer managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html#customer-managed-policies). To help you determine the specific permissions you require, see [AWS Identity and Access Management Access Analyzer](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html), review AWS CloudTrail logs, and inspect last accessed information. You also can use the [IAM policy simulator](https://policysim.aws.amazon.com/) to test and troubleshoot policies.

### What is IAM Access Analyzer?

Achieving least privilege is a continuous cycle to grant the right fine-grained permissions as your requirements evolve. IAM Access Analyzer helps you streamline permissions management in each step of this cycle. [Policy generation](https://aws.amazon.com/blogs/security/iam-access-analyzer-makes-it-easier-to-implement-least-privilege-permissions-by-generating-iam-policies-based-on-access-activity/) with IAM Access Analyzer generates a fine-grained policy based on the access activity captured in your logs. This means that after you build and run an application, you can generate policies that grant only the required permissions to operate the application. [Policy validation](https://aws.amazon.com/blogs/aws/iam-access-analyzer-update-policy-validation/) with IAM Access Analyzer uses more than 100 policy checks to guide you to author and validate secure and functional policies. You can use these checks while creating new policies or to validate existing policies. Custom policy checks are a paid feature to validate that developer-authored policies adhere to your specified security standards ahead of deployments. Custom policy checks use the power of automated reasoning—provable security assurance backed by mathematical proof— so that security teams can proactively detect nonconformant updates to policies.

[Public and cross-account findings](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html#what-is-access-analyzer-resource-identification) with IAM Access Analyzer help you verify and refine access allowed by your resource policies from outside your AWS organization or account. Internal findings within IAM Access Analyzer identify who within your AWS organization has access to your critical AWS resources. For more information, see [Using IAM Access Analyzer](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html). IAM Access Analyzer also continuously analyzes your accounts to identify unused access. The findings highlight unused roles, unused access keys for IAM users, and unused passwords for IAM users. For active IAM roles and users, the findings provide visibility into unused services and actions. The results from the analysis of external, internal, and unused access are displayed on a unified dashboard that allows central visibility for quick remediation.

### How do I remove unused permissions?

You might have IAM users, roles, and permissions that you no longer require in your AWS account. We recommend that you remove them with the goal of achieving least-privilege access. For IAM users, you can review password and access key last used information. For roles, you can review role last used information. This information is available through the IAM console, APIs, and SDKs. Last used information helps you identify users and roles that are no longer in use and safe to remove. You can also refine permissions by reviewing service and last accessed information to identify unused permissions. For more information, see [Refine permissions in AWS using last accessed information](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_access-advisor.html).

If you enable an unused access analyzer as a paid feature, IAM Access Analyzer continuously analyzes your accounts to identify unused access and creates a centralized dashboard with findings. Security teams can use the dashboard to review findings and prioritize which accounts to review based on the volume of findings, which highlight unused roles, unused access keys for IAM users, and unused passwords for IAM users. For active IAM roles and users, the findings provide visibility into unused services and actions, simplifying the inspection of unused access to guide you toward least privilege. With this feature, you pay per IAM role or IAM user analyzed per month.

### What is the IAM policy simulator and when should I use it?

The [IAM policy simulator](https://policysim.aws.amazon.com/) evaluates policies you choose and determines the effective permissions for each of the actions you specify. Use the policy simulator to test and troubleshoot [identity-based and resource-based policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html), [IAM permissions boundaries](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_boundaries.html), and [SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html). For more information, see [IAM policy testing with the IAM policy simulator](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_testing-policies.html).

### What are IAM Access Analyzer custom policy checks?

IAM Access Analyzer custom policy checks validate before deployments that your IAM policies adhere to your security standards. Custom policy checks use the power of [automated reasoning](https://www.amazon.science/blog/a-gentle-introduction-to-automated-reasoning)—provable security assurance backed by mathematical proof—so that security teams can proactively detect nonconformant updates to policies. For example, IAM policy changes that are more permissive than their previous version would be flagged for additional review. Security teams can use these checks to streamline their reviews, automatically approving policies that conform with their security standards and inspecting more deeply when they don't. This kind of validation provides higher security assurance in the cloud. Security and development teams can automate policy reviews at scale by integrating these custom policy checks into the tools and environments where developers author their policies, such as their CI/CD pipelines.

### What is IAM Access Analyzer unused access?

IAM Access Analyzer simplifies inspecting unused access to guide you toward least privilege. Security teams can use IAM Access Analyzer to gain visibility into unused access across their AWS organization and automate how they rightsize permissions. When an unused access analyzer is enabled, IAM Access Analyzer continuously analyzes your accounts to identify unused access and creates a centralized dashboard with findings. Security teams can use the dashboard to review findings centrally and prioritize which accounts to review based on the volume of findings. The findings highlight unused roles, unused access keys for IAM users, and unused passwords for IAM users. For active IAM roles and users, the findings provide visibility into unused services and actions.