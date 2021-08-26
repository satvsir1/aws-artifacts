# AWS Container Services

## Table of Content
- ECR
- ECS
- EKS

## Elastic Container Registry (ECR)

**Amazon Elastic Container Registry (Amazon ECR)** is an AWS managed container image registry service. Amazon ECR supports private container image repositories with resource-based permissions using AWS IAM. This is so that specified users or Amazon EC2 instances can access your container repositories and images. You can use your preferred CLI to push, pull, and manage **Docker images**, Open Container Initiative (**OCI**) images, and **OCI compatible artifacts**. 

**Amazon Elastic Container Registry Public** is a managed AWS container image registry service that is secure, scalable, and reliable. Amazon ECR supports public image repositories with resource-based permissions using AWS IAM so that specific users can access your public repositories to push images. Developers can use their preferred CLI to push and manage Docker images, Open Container Initiative (OCI) images, and OCI compatible artifacts. Your images are publicly available to pull, either anonymously or using an Amazon ECR Public authentication token. 

Amazon ECR provides the following features: 

- **Lifecycle policies** help with managing the lifecycle of the images in your repositories. You define rules that result in the cleaning up of unused images. You can test rules before applying them to your repository. For more information, see [Lifecycle policies](https://docs.aws.amazon.com/AmazonECR/latest/userguide/LifecyclePolicies.html)

- Image scanning helps in identifying software vulnerabilities in your container images. Each repository can be configured to scan on push. This ensures that each new image pushed to the repository is scanned. You can then retrieve the results of the image scan. For more information, see [Image scanning](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html)

- Cross-Region and cross-account replication makes it easier for you to have your images where you need them. This is configured as a registry setting and is on a per-Region basis. For more information, see [Private registry settings](https://docs.aws.amazon.com/AmazonECR/latest/userguide/registry-settings.html)


**Amazon ECR** is often used as source point for **ECS** and **EKS** workflows. It can perfectly suit as a backup solution for your on-premise docker registry. 

![](images/scanning-concept-1024x733.png)


### Pricing considerations 

- [Amazon Elastic Container Registry pricing ](https://aws.amazon.com/ecr/pricing/)

## Elastic Container Service (ECS)

![](images/ecs-console.jpg)

Amazon Elastic Container Service (Amazon ECS) is the Amazon Web Service you use to run Docker applications on a scalable cluster. In this tutorial, you will learn how to run a Docker-enabled sample application on an Amazon ECS cluster behind a load balancer, test the sample application, and delete your resources to avoid charges.

An Amazon ECS cluster is a logical grouping of **tasks** (a logical group of containers running on an instance) or **services** (a scheduling logic that decides when and where containers should run in your cluster)

![](images/alpine-aws-arch.png)

**AWS Fargate Support**

AWS Fargate technology is available with Amazon ECS. With AWS Fargate, you no longer have to select Amazon EC2 instance types, provision and scale clusters, or patch and update each server. You do not have to worry about task placement strategies, such as binpacking or host spread and tasks are automatically balanced across availability zones. Fargate manages the availability of containers for you. You just define your application’s requirements, select Fargate as your launch type in the console or CLI, and Fargate takes care of all the scaling and infrastructure management required to run your containers.
<!-- 
You can run them by choosing on of the following launch types:

- Using the Fargate launch type
- Using the EC2 launch type

Please get [more details here](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/application_architecture.html). 
-->

### Getting started Videos:

- [Amazon ECS: Core Concepts](https://youtu.be/eq4wL2MiNqo)
- [Writing Task Definitions for Amazon ECS](https://youtu.be/o_qSS4S1g34)
- [Task Placement with Amazon ECS](https://youtu.be/8XwNPX4AV2M)
- [Amazon ECS: Load Balancing for Containers](https://youtu.be/hu7SyJHWJZ0)
- [Amazon ECS: Autoscaling for Containers](https://youtu.be/YEvU6uIckDc)


## Amazon Elastic Kubernetes Service (EKS)

**EKS** stands for **Elastic Kubernetes Service**, which is an Amazon offering that helps in running the Kubernetes on AWS without requiring the user to maintain their own Kubernetes control plane. It is a fully managed service by Amazon.

Amazon EKS helps run Kubernetes control plane instances over multiple Availability Zones which makes sure that they are highlyavailable. Amazon EKS automatically detects and replaces control plane instances that are unhealthy, as well as provisioning automated version upgrades and patching for the unhealthy control planes.  

Amazon EKS can be integrated with other Amazon service in order to provide scalability and security for user applications, and some of the services have been listed below: 

- Authentication is served by IAM. 
- Isolation is served by Amazon VPC.  
- Amazon ECR for container images.  
- Elastic Load Balancing service to distribute the load. 

Amazon EKS helps run up-to-date version of the open-source Kubernetes software, thereby allowing the user to use all the existing plugins and tooling which is availability in the Kubernetes community. Applications that run on Amazon EKS are completely compatible with applications which run on other standard Kubernetes environment, be it running in on premise data centres or in public clouds. This indicates that the user can migrate to other standard Kubernetes application very easily without modifying any code. 

### Amazon EKS Control Plane Architecture
Amazon EKS runs along with a single tenant Kubernetes control plane for every cluster. This control pane infrastructure can’t be shared with other clusters or AWS accounts. The control plane consists of a minimum of two API server nodes and three ‘etcd’ nodes which run across three Availability Zones which is present in a Region. 

![](images/eks_3_az_3.png)

EKS runs the Kubernetes control plane across multiple AWS Availability Zones, automatically detects and replaces unhealthy control plane nodes, and provides on-demand, zero downtime upgrades and patching. EKS offers a 99.95% uptime SLA. At the same time, the EKS console provides observability of your Kubernetes clusters so you can identify and resolve issues faster.

EKS automatically applies the latest security patches to your cluster’s control plane. AWS works closely with the community to address critical security issues and help ensure that every EKS cluster is secure.

**Serverless Compute**

EKS supports AWS Fargate to run your Kubernetes applications using serverless compute. Fargate removes the need to provision and manage servers, lets you specify and pay for resources per application, and improves security through application isolation by design.
### Pricing considerations 

With AWS EKS, you have to pay for: 
- EC2/Fargate instances deployed 
- Volumes attached to them 
- EKS cluster itself  

More info can be found on [AWS EKS pricing page](https://aws.amazon.com/eks/pricing/)


### More details 

- https://www.youtube.com/watch?v=7vxDWDD2YnM  
