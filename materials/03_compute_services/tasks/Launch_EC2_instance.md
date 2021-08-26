**Domain: Compute Services**

**Topic: EC2**

**Task: Launch EC2 instance**

**Problem to Be Solved**

_Learn how to launch EC2 instances with required parameters_

## Explanation of the Solution

- [Setup pre-requirements](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/get-set-up-for-amazon-ec2.html)
- [Instance launch](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
- [Terminate instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/terminating-instances.html)

## Implementation Details

_Prerequisites:_

- _Create ssh-key_
- _Create security group to allow access to port 22 from your ip address (see the explanation above)_

_Launch instance:_

1. _From the console dashboard, choose **Launch Instance**._
2. _Choose an **Amazon Machine Image**(AMI) with the following name "Amazon Linux 2 AMI"_
3. _Choose an **Instance Type** and select t2.nano_
4. _On the Review Instance Launch page, choose **Launch**._
5. _When prompted for a key pair, select **Choose an existing key pair**, then select your key pair_
6. _Locate your instance in **Instances** navigation pane._
7. _Select your instance, and then choose **Actions,Security,Change security group.**_
8. _Select required security group from the list and choose **Add security group**._

_Connect to the instance_

1. _From bash console type_ `ssh -i your_ssh_key ec2-user@ec2_instance_public_name`.
2. _Observe instance root directory with `ls` command_
3. _Type `exit` to disconnect from the instance._

## Benefits / Outcomes / Pros and Cons / Summary

_This simple task shows you how to launch standalone EC2 instance with defined shape and image._

## Tearing down

_Terminate instance(see the explanation above), security group and ssh-key._