# Databricks Deployment Roles

Databricks documentation goes over how to [Create a cross-account IAM role](https://docs.databricks.com/administration-guide/account-api/iam-role.html#language-Your%C2%A0VPC,%C2%A0custom) for deployment of e2 account. There are many different configurations depending on security and deployment requirements for each customer and use case. We want to organize the IAM policy here for as many of those use cases as possible. There is already a corresponding repo for restricting DBFS write called [databricks-aws-bucket-policies](https://github.com/databricks/databricks-aws-bucket-policies) that might be frequently used in conjunction.

### Deployment	Policy

| Deployment | Policy |
| ----------- | ----------- |
| Customer-managed VPC with default policy restrictions: Launch Databricks workspaces in your own VPC. | [Your VPC, default](e2-your-vpc-policy) |
| Customer-managed VPC with custom policy restrictions: Launch Databricks workspaces in your own VPC with policy restrictions by account ID, VPC ID, region, and security group. | [Your VPC, custom](e2-custom-vpc-policy) |
| Databricks-managed VPC: Launch Databricks workspaces in a Databricks-managed VPC.| 	[Databricks VPC](e2-databricks-vpc-policy) |

### Customer-managed VPC with secure cluster connectivity (no public IP / NPIP) with custom restrictions for account ID, VPC ID, region, and security group.

Replace the following values in the [policy](e2-custom-vpc-policy) with your own configuration values:

- `ACCOUNTID` : Your AWS account ID, which is a number.

- `VPCID` : ID of your AWS VPC in which you want to launch workspaces.

- `REGION` : AWS region name for your VPC deployment, for example us-west-2.

- `SECURITYGROUPID-A` : ID of your AWS security group. When you add a security group restriction, you cannot reuse the cross-account IAM role or reference credentials ID (credentials_id) for any other workspaces. For those other workspaces, you must create separate roles, policies, and credentials objects.

- `SECURITYGROUPID-B` : ID of your AWS security group. When you add a security group restriction, you cannot reuse the cross-account IAM role or reference credentials ID (credentials_id) for any other workspaces. For those other workspaces, you must create separate roles, policies, and credentials objects.
