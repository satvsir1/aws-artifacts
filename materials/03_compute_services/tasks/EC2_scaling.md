# Domain: Automation and Optimization 

## Topic: EC2 Autoscaling groups 

### Task: Creating EC2 Autoscaling groups from Launch template

### Problem to Be Solved  

You are a System Engineer witch has to administrate online supermarket. Next month you are expected big sales in your company and this will generate huge traffic on the web site and overload it. So in this task you will learn how create ES2 Autoscaling group from Launch template witch will scale up and down instances (web servers) group depending on the instance CPU load. 

**NOTICE**: in the future task you will configure Application Load Balancer to load balance between the instance inside the Autoscaling group. 


### Explanation of the Solution  

Reference documentation:
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html 
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/AutoScalingGroup.html 
- https://docs.aws.amazon.com/autoscaling/ec2/userguide/GettingStartedTutorial.html 
- http://en.clouddesignpattern.org/index.php/CDP:Scale_Out_Pattern  
- https://docs.microsoft.com/en-us/azure/architecture/example-scenario/apps/hpc-saas  
 
### Implementation Details  

_We’ll need cloud formation for almost each task_
_OR we can reference VPC and SGs made in previous tasks_

**Required**: Key Pairs, VPC, Security Group 

1. Create a Launch Template:
    - Navigate to EC2 > Instances > Launch Templates. 
    - Click Create launch template, call it "MyLaunchTemplate", and mark checkbox Auto Scaling guidance . 
    - Select for "AMI" Amazon Linux 2 AMI (HVM) (64-bit x86) image.
    - Set the instance type as t2.micro. 
    - Select the key pair you created earlier or create new. 
    - Network settings set VPC and "XXXXXname" security group. 
    - Storage will be automatically set, don’t change it. 
    - Expand Advanced Details, and paste in the User data provision script to install app. For example: "sudo yum –y install httpd" 
    - Click Create Launch Template. 

2. Create a Autoscaling group 
    - Navigate to EC2  > Auto Scaling > Auto Scaling Groups. 
    - Click Create an Auto Scaling group. 
    - Name the group "MyASG"
    - Select Launch Template, and choose the template you just created "MyLaunchTemplate"
    - Select Adhere to Launch Template. 
    - Version will set by "Default (1)", don’t change it. 
    - Click "Next"
    - Set Network VPC "YYYYYname", Subnets "ZZZZname". 
    - Click "Next". 
    - Load balance optional set to "No load balancer". 
    - Health check don’t change. 
    - Additional setting don’t change. 
    - Click "Next". 
    - In Group Size enter next  
        - Desired Capacity: 1 
        - Minimum Capacity: 1 
        - Maximum Capacity: 2 
    - Scaling policies set to "Target tracking scaling policy", don’t change "Scaling policy name",  "Metric type" and "Target value". (moves to next module) 
    - Click "Next". 
    - Don’t change Notifications 
    - Click "Next". 
    - Click "Next". 
    - Click "Create Auto Scaling group". 
 
_Get rid from autoscaling and move it to another submodule_

3. Test Horizontal Scaling 
    - Connect to one of the EC2 instances via SSH. 
    - Install stress test utility, run:
        ```
        sudo amazon-linux-extras install epel -y. 
        sudo yum install -y stress 
        ```
    - Run stress test:
        ```
        stress --cpu 2 --timeout 300 
        ```
    - Wait 5-10 minutes, go to EC2 > Auto Scaling groups > MyASG click "Monitoring" then "EC2" and see "CPU Utilization" graph. Then check on the page EC2  > Instance and check the number of Runnig Instance. 

  

## Benefits / Outcomes / Pros and Cons / Summary  

(say a few words about how ASGs connected with HA) 

In this task you known how to create Auto scaling group and how to manage  the size of the Auto Scaling group by changing tracking scaling policy (CPU Utilisation). 


## Pricing  

Link to cost calculator: https://aws.amazon.com/ec2/pricing/on-demand/?nc1=h_ls 

## Tearing down  

1. Delete Auto Scaling Ggroups 
    - Navigate to EC2  > Auto Scaling > Auto Scaling Groups. 
    - Mark "MyASG" group and click "Delete". On the next page type in the field "delete" and click "Delete". 
2. Delete Launch Templates 
    - Navigate to EC2  > EC2 > Instances > Launch Templates. 
    - Mark "MyLaunchTemplate" click on "Action" and set  "Delete template". On the next page type in the field "delete" and click "Delete". 
