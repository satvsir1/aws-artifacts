# Task: Creating and using of IAM roles/policies.

## Problem to Be Solved
Study how to create IAM roles/policies and use them for different AWS services, e.g. assume role. 

## Implementation Details

Pre-requisites:
- Already created S3 bucket
- Installed jq - https://stedolan.github.io/jq/download/ 
- Installed AWS cli v1 - https://docs.aws.amazon.com/cli/latest/userguide/install-cliv1.html
- https://awspolicygen.s3.amazonaws.com/policygen.html or https://aws.amazon.com/blogs/security/use-the-new-visual-editor-to-create-and-modify-your-aws-iam-policies/ 

Create the following roles with:

- AWS managed policy S3 full access
- Inline policy `ssm:ReadOnly`
- Customer managed policy `kms:Decrypt`

Hint: Use policy generator  
Assign this policy to new user, add permission for programmatic api access

Add one more role with ability of assuming by user from previous step
S3 read-only

Verification:
1. credentials retrieval from cli for user
2. write file to existing s3 bucket to test full access
3. perform role assuming using cli
4. make a try to write file from step 2
5. copy file from s3 using cli


## Solution levels (could be done in a sequence):
- Basic - create IAM roles and user using AWS Console and policy generator, proceed with verification from cli
- Medium - create everything using AWS cli (hint: use policies in json forma from Basic level) and proceed with verification
- Pro - create everything using IaC approach with CloudFormation/Terraform, proceed with verification from cli


## Benefits / Outcomes / Pros and Cons / Summary
1.	Almost everything in AWS is tied with IAM.
2.	Usage of AWS managed and custom managed policies.
3.	Understanding of IAM roles precedence.
4.	Understanding of service-managed roles.
5.	Assuming roles practice and key points.
6.	Instance-profile
7.	Resource-based policies

## Tearing down
Delete all resources and delete IAM roles/policies, since you cannot delete policy or role that is in use.
