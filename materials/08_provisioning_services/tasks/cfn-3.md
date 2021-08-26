# Domain: Automation and Optimization 

## Topic: Cloudformation. Advanced tasks

Useful links for the tasks implementation:
1) [What is VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
2) [Security groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)
3) [S3 buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#BasicsBucket)
4) [EC2 instance profiles](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html)
5) [EIP](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-eips.html)
6) [EBS Volume types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)
7) [User data](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html)
8) [Autoscaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)
9) [Launch templates](https://docs.aws.amazon.com/autoscaling/ec2/userguide/LaunchTemplates.html)
10) [Application load balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)
11) [Target group](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html)

Cloudformation template reference to above [resources](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html)  
Cloudformation [changesets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-changesets.html)


### Task: Create the infrastructure stack that imitates highly available web site, with additional security items, using Cloudformation

It is recommended to create the stack step by step, adding new items using Cloudformation Changesets, starting from step 2

##### Step 1: Create VPC
Stack items to create:
- VPC with 10.20.0.0/16 mask
- Internet Gateway attached to the VPC
- S3 bucket
Note: after the creation upload a simple file into bucket manually

##### Step 2: Extend VPC with subnets
Stack items to add:
- Two public subnets in different availability zones
- Two private subnets in different availability zones
- Security group with ports 80 and 22 opened for your personal extenal IP only. The SG has to be attached to your VPC

##### Step 3: Add NAT gateway and routing
Stack items to add:
- Elastic IP (EIP)
- NAT Gateway attached to any of public subnets and associated with EIP
- Route table for public subnets with traffic being sent to Internet gateway
- Route table for private subnets with traffic being sent to NAT gateway

##### Step 4: Create ELB
Stack items to add:
- Application load balancer with 80 port listener and associated with 2 public subnets
- Target group attached to the Application load balancer
- EC2 instance profile with access to S3 bucket
- Launch template with Ubuntu image and httpd installed
- Launch template should have EC2 instance profile attached to it
- Autoscaling group with Launch template attached. Minimum running instances - 2

##### Step 5: Create output from stack. Tagging
Stack items to add:
- Export ELB address in Output section
- Tag each possible item with tags: 
   1) "Name" (like "lab08-3-...")
   2) "Project" and value "Cloudformation"
   3) "Role" and values like ("Security", "AppTier", "LB" etc)

##### Step 6: Check if everything works
- Open site by address from Output section
- SSH to any instance and try to obtain file from S3


### Task: Disassemble the stack
- Remove the file from S3 bucket
- Delete the Cloudformation stack. Check if any resources weren't deleted and delete them manually if needed