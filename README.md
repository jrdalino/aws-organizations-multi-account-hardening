# AWS Organizations & Multi-Account Hardening

## Prerequisites
- New Email aliases

## Step 1: AWS Organizations and Multi-Account Hardening

### Step 1.1: Create AWS Organization
```
$ aws organizations create-organization
```

### Step 1.2: Create Core OU
```
$ aws organizations create-organizational-unit \
--parent-id r-examplerootid111 \
--name CoreOU
```

### Step 1.3: Create Core Accounts
- AWS Organizations AWS Account
- Shared Services AWS Account
- Log Archive AWS Account
- Security AWS Account
- Identity & Access AWS Account (Replace with AWS SSO + Directory Connector)
- (Optional) Network AWS Account for Direct Connect

### Step 1.4: Add SCP Policies
- Prevent Users from Disabling AWS CloudTrail
- Prevent Users from Disabling Amazon CloudWatch or Altering Its Configuration
- Prevent Users from Deleting Amazon VPC Flow Logs
- Prevent Users from Disabling AWS Config or Changing Its Rules
- Denies Access to AWS Based on the Requested Region
- Require Encryption on Amazon S3 Buckets
- Denies the modification of the account contacts & settings via the Billing Portal and My Account Page
- Denies the account from leaving the organization

Reference
- https://github.com/jrdalino/aws-organizations
- https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_example-scps.html
- https://github.com/jchrisfarris/aws-service-control-policies

### Step 1.5: Per new Developer Create a Sandbox and per Project a set of Development, Staging and Production Accounts
- Developer Sandbox AWS Account
- Development AWS Account
- Staging AWS Account
- Production AWS Account

### Step 1.6: In organizations account activate MFA and Secure Root User

### Step 1.7: In identity & acess account create Groups, Users and Roles

### Step 1.8: In all accounts apply IAM Password Policy

### Step 1.9: In Log Archive Account Create the following S3 Buckets
- CloudTrail Logs
- Config Logs
- ELB Logs
- Cloudfront Logs
- VPC Flow Logs

### Step 1.10: In all accounts enable SNS topics for alerting and notifications

### Step 1.11: In all accounts enable AWS CloudTrail and send logs to Log Archive Account
- https://s3-ap-southeast-1.amazonaws.com/cloudformation-stackset-sample-templates-ap-southeast-1/EnableAWSCloudtrail.yml

### Step 1.12: In all accounts enable Config for AWS resource config tracking
- https://s3-ap-southeast-1.amazonaws.com/cloudformation-stackset-sample-templates-ap-southeast-1/EnableAWSConfig.yml

### Step 1.13 In all accounts enable Config Rules
Config Rule to determine whether the root user has MFA enabled
- https://s3-ap-southeast-1.amazonaws.com/cloudformation-stackset-sample-templates-ap-southeast-1/ConfigRuleRootAccountMFAEnabled.yml

Config Rule to determine whether CloudTrail is enabled
- https://s3-ap-southeast-1.amazonaws.com/cloudformation-stackset-sample-templates-ap-southeast-1/ConfigRuleCloudtrailEnabled.yml

Config Rule to determine whether all EIP's are attached
- https://s3-ap-southeast-1.amazonaws.com/cloudformation-stackset-sample-templates-ap-southeast-1/ConfigRuleEipAttached.yml

Config Rule to determine all EBS Volumes are encyrpted
- https://s3-ap-southeast-1.amazonaws.com/cloudformation-stackset-sample-templates-ap-southeast-1/ConfigRuleEncryptedVolumes.yml

Reference:
- https://github.com/awslabs/aws-config-rules
- https://github.com/awslabs/aws-config-engine-for-compliance-as-code

### Step 1.14: In all accounts Delete Default VPC's in all Regions
- https://github.com/jrdalino/aws-delete-default-vpc

### Step 1.15: In all accounts Enable Guard Duty for Intelligent threat detection
- https://s3-ap-southeast-1.amazonaws.com/cloudformation-stackset-sample-templates-ap-southeast-1/EnableAWSGuardDuty.yml

Reference:
- https://github.com/jrdalino/aws-guardduty

### Step 1.16: In all accounts enable Security Hub for Compliance Scanning
- 

### Step 1.17: In organizations account enable Cost Usage Report
- https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-reports-gettingstarted-turnonreports.html

### Step 1.18: Create Tags
- https://aws.amazon.com/answers/account-management/aws-tagging-strategies/

### Step 1.19: Create AWS Budgets
- https://github.com/jrdalino/aws-budgets
- https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/budgets-create.html

### Step 1.20: Review usage using Cost Explorer
- https://github.com/jrdalino/aws-cost-explorer
- https://console.aws.amazon.com/billing/home?region=ap-southeast-1#/costexplorer

### Step 1.21: Review Trusted Advisor
- https://github.com/jrdalino/aws-trusted-advisor

### Step 1.22: Review AWS Health / Personal Health Dashboard
- https://github.com/jrdalino/aws-health
- https://phd.aws.amazon.com/phd/home#/dashboard/open-issues

### Step 1.23: Perform a Well Architected Review
- https://github.com/jrdalino/aws-well-architected-questions
- https://us-east-1.console.aws.amazon.com/wellarchitected/home?region=us-east-1

### Step 1.24: Perform Infrastructure Event Management before product launch
- https://github.com/jrdalino/aws-infrastructure-event-management
- https://d1.awsstatic.com/whitepapers/aws-infrastructure-event-readiness.pdf

## (Clean Up)

## Others
- Check Out https://aws.amazon.com/controltower/
