---
title: AWS organization notes
draft: false
tags:
  - aws
---
 ## What is an IAM User

An IAM user is a permanent identity representing a person or application.

### Use Cases for IAM Users

- Individual developers needing AWS console access
- Service accounts for applications (though roles are better)
- Third-party tools that require long-term credentials

**Federated Access** refers to a secure, seamless method that allows users to access multiple systems, applications, or websites using a single set of credentials, typically issued by their home organization (like a university or company)

It works by establishing a **trust relationship** between an **identity provider (IdP)**, which authenticates the user, and **service providers (SPs)**, which grant access to resources.

Instead of managing separate usernames and passwords for each service, users log in once to their IdP, and the SPs trust the IdP’s authentication.

### Purpose of IAM Groups

Groups are collections of IAM users that share the same permissions. Instead of attaching policies to each user individually, you attach them to a group. It’s like creating a “Developers” team and giving the whole team the same access.

### Group vs User Policies

- **Group policies:** Apply to all members of the group
- **User policies:** Apply to specific users only
- A user can be in multiple groups and inherits all their policies

### When (and When Not) to Use Groups

**Use groups when:**

- Multiple users need the same permissions
- You want simplified permission management
- Team-based access makes sense

**Don’t use groups when:**

- You only have one user with unique permissions
- You’re working across multiple accounts (groups don’t work cross-account)
- You’re implementing federated access (use Identity Center instead)

### 2.3 IAM Roles

### What is an IAM Role

A role is an identity you can assume temporarily to get short-term credentials. Unlike users, roles don’t have permanent credentials. Think of it as borrowing someone else’s badge for a specific task, then returning it.

![[Pasted image 20260124115038.png]]
## Difference Between User and Role

- **User:** Permanent identity with long-term credentials
- **Role:** Temporary identity that can be assumed by trusted entities
- **Key benefit:** Roles provide temporary security credentials that automatically expire

### Difference Between User and Role

- **User:** Permanent identity with long-term credentials
- **Role:** Temporary identity that can be assumed by trusted entities
- **Key benefit:** Roles provide temporary security credentials that automatically expire

### Trust Policy vs Permission Policy

Every role has two types of policies:

- **Trust policy (who can assume):** Defines which principals are allowed to assume the role
- **Permission policy (what they can do):** Defines what actions the role can perform once assumed

### Common Role Types

**AWS Service Roles:**

- Roles assumed by AWS services (EC2, Lambda, etc.)
- Example: Lambda execution role to access S3

**Cross-Account Roles:**

- Allow users from one AWS account to access another
- Example: Dev account users accessing production resources

**Federated Roles:**

- Allow external identity providers (Google, Active Directory) to grant AWS access
- Example: Employees logging in with corporate credentials

### AWS Managed vs Customer Managed

- **AWS managed:** Pre-built policies by AWS (e.g., ReadOnlyAccess)
- **Customer managed:** Custom policies you create and control

### 3.2 Policy Structure

Every IAM policy is a JSON document with this structure:

![[Pasted image 20260124115120.png]]
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket/*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "203.0.113.0/24"
        }
      }
    }
  ]
}
```

**Key components:**

- **Version:** Always use “2012-10-17” (the current policy language version)
- **Statement:** An array of permission statements
- **Effect:** Either “Allow” or “Deny”
- **Action:** What API operations are allowed/denied (e.g., s3:GetObject)
- **Resource:** Which AWS resources this applies to (using ARNs)
- **Principal:** Who this applies to (used in resource-based policies)
- **Condition:** Optional conditions that must be met

### 3.3 Policy Properties (Advanced)

### Wildcards and ARN Patterns

Use wildcards (*) to match multiple resources:

- `s3:*` = All S3 actions
- `arn:aws:s3:::my-bucket/*` = All objects in the bucket
- `arn:aws:ec2:us-east-1:123456789012:instance/*` = All instances in the region

## AWS Organizations

![[Pasted image 20260124115149.png]] 
## What is AWS Organizations

AWS Organizations is a free service that lets you manage multiple AWS accounts from a central location. Think of it as corporate headquarters managing branch offices.

### Accounts vs Organizational Units (OU)

- **Account:** Individual AWS account with its own resources
- **OU:** A container for organizing accounts (like folders)
- **Structure:** Root → OUs → Accounts (you can nest OUs)

Example structure:

> Root ├
>  ── Production OU 
>  ── Prod-App Account 
>       └── Prod-Data Account 
>       └── Development OU 
>    ── Dev-App Account 
>      └── Dev-Test Account

### Consolidated Billing Overview

All accounts roll up to one bill in the management account. Benefits:

- Single payer for all accounts
    
- Volume discounts apply across all accounts
    
- Easier cost tracking and allocation
    
- Reserved Instance sharing
    

## Reserved Instance Sharing

**The problem without Organizations:** Reserved Instances (RIs) and Savings Plans provide significant discounts (up to 72%) but are purchased for specific instance types. If you buy an RI in Account A but don't fully utilize it there, you can't apply the unused discount to Account B's instances.

**How Organizations solves this:** When accounts are part of an Organization, AWS **automatically shares RI and Savings Plan discounts** across all accounts:

1. **Purchase flexibility**: Your central team can purchase RIs in the management account or any member account
2. **Automatic application**: If the purchasing account doesn't use 100% of the RI, the discount automatically applies to matching instances in other accounts
3. **No manual configuration**: This happens automatically with consolidated billing - you don't need to set up sharing rules
4. **Maximizes utilization**: Instead of RIs sitting unused in one account while another account pays on-demand prices, the discount "floats" to where it's needed

**Example:**

- Finance team purchases 10 Reserved Instances for m5.large in US-East-1
    
- Finance only uses 6 at any given time
    
- The remaining 4 RI discounts automatically apply to m5.large instances running in Engineering and Marketing accounts
    
- Result: Organization-wide savings instead of wasted RI capacity
    
- **RI = billing discount**, not a physical server reservation
    
- **"Utilized" = discount is being applied** to a running instance that matches the RI specs
    
- **"Unused" = you have the RI** but no matching instances running, so the discount sits idle
    
- **Organizations = automatic sharing** - unused RIs in one account instantly apply to matching instances in other accounts
    
- **No configuration needed** - AWS does this automatically every hour based on which instances are running
    

## SCPs (Service Control Policies)

### What are SCPs

SCPs are guardrails that limit what users and roles can do in member accounts, even if their IAM policies allow it. They’re like corporate policies that override individual permissions.

### SCP vs IAM Policy

- **IAM policy:** Grants permissions (allows access)
- **SCP:** Sets maximum permissions (denies access)
- **Key difference:** SCPs don’t grant access, they only restrict it

An SCP that denies EC2 termination means NO ONE in that account can terminate EC2 instances, regardless of their IAM permissions.

## Identity Provider (IdP) Integration

### 9.1 Single AWS Account with SAML Federation

### How SAML Federation Works

SAML lets you use your existing corporate identity provider (like Okta, Azure AD) to access AWS:

1. User authenticates with IdP (e.g., enters corporate username/password)
2. IdP sends SAML assertion to AWS
3. AWS STS converts SAML assertion to temporary AWS credentials
4. User accesses AWS with temporary credentials

### IAM Role + IdP Flow

Your IdP must be configured as a SAML provider in IAM, and you create roles that trust this provider. Users authenticate with IdP, then assume the appropriate AWS role.

### Limitations in Single-Account Setups

- Must create separate IAM roles for each type of user
- Managing many roles becomes complex
- No central view of who has access to what
- Role sprawl across teams

### What is IAM Identity Center

IAM Identity Center (formerly AWS SSO) is a centralized service for managing access across all your AWS accounts. It’s like having a single security desk for your entire building instead of one at each door.

### How It Solves Multi-Account Access

Instead of creating roles in each account:

1. Define permission sets once in Identity Center
2. Assign users/groups to accounts with those permission sets
3. Identity Center automatically provisions roles in each account
4. Users get a single sign-on portal to access all accounts

### Supported Identity Sources

- **Identity Center directory:** Built-in user directory
- **Active Directory:** Connect to on-premises or AWS Managed AD
- **External IdP:** SAML 2.0 providers (Okta, Azure AD, Google, etc.)

### What is a Permission Set

A permission set is a template that defines permissions. It’s like a job description that gets turned into an IAM role in each account where you assign it.

### Permission Sets vs IAM Roles

- **Permission set:** Template in Identity Center (lives centrally)
- **IAM role:** Actual role in each account (auto-created by Identity Center)

When you create a permission set called “Developers” and assign it to 10 accounts, Identity Center creates 10 identical IAM roles automatically.

### Managed Policies and Inline Policies

Permission sets can include:

- AWS managed policies (e.g., ReadOnlyAccess)
- Customer managed policies (your own reusable policies)
- Inline policies (custom JSON directly in the permission set)

### Session Duration and Relay State

- **Session duration:** How long credentials last (1-12 hours)
- **Relay state:** Optional URL to redirect users after login (e.g., specific console page)

### What is an Instance Profile

An instance profile is a container that passes an IAM role to an EC2 instance. It’s like giving your EC2 instance an employee badge so it can access other AWS services.

### Instance Profile vs IAM Role

- **IAM role:** Defines what permissions are available
- **Instance profile:** Delivers the role to the EC2 instance

