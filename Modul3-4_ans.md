# Modul 3

1.Which component of the AWS Global Infrastructure does Amazon CloudFront use to ensure 
# AWS Edge locations

2.You can run applications and workloads from a region closer to the end users to ______ latency
Decrease

3.True / False? Networking, storage, compute and databases are examples of service categories that AWS offers.
# True

4.Which of the following are geographic areas that host two or more Availability Zones?
# AWS Regions

5. _____ means the infrastructure has built-in component redundancy and _____ means that resources dynamically adjust to increases or decreases in capacity requirements.
# Fault-tolerant, elastic and scalable

6.True or False? Availability Zones within a region are connected through low-latency links.
# True

7.Which of these statements about Availability Zones is not true? (Select the best answer)
# A data center can be used for more than one availability zone

8.What is true about Regions (Choose two)
# A region is a physical location that has multiple availability zones
# Each region is located in a separate geographic area

9.AWS highly recommends provisioning your compute resources across _____ availability zones.
# Multiple

10. True or False? Edge locations are only located in the same general area as regions.
# False


# Modul 4

1. In the shared responsibility model, AWS is responsible for providing what? (Select the best answer).
# Security of the cloud.

2. In the shared responsibility model, which of the following are examples of "security in the cloud?" (Choose two).
# Security group configurations.
# Encryption of data at rest and data in transit.

3.Which of the following is the responsibility of AWS under the AWS shared responsibility model? (Select the best answer).
# Maintaining physical hardware.

4.When creating an AWS Identity and Access Management (IAM) policy, what are the two types of access that can be granted to a user? (Choose two).
# Programmatic Access.
# AWS Management Console Access.

5.True or false? AWS organizations enables you to consolidate multiple aws accounts so that you centrally manage them.
# True.

6.Which of the following are best practices to secure your account using aws identity and access management? (Choose 2).
# Manage access to AWS resources.
# Define fine-grained access rights.

7.Which of the following should be done by the AWS account root user? (Select the best answer)
# Change the AWS support plan.

8.After initial login, what does AWS recommend as the best practice for the AWS account root user?
# Delete the access keys of the AWS account root user.

9.How would a system administrator add an additional layer of login security to a user's AWS management console?
# Enable multi-factor authentication.

10.True or false? AWS key management service (AWS KMS) enables you to assess, audit, and evaluate the configurations of your AWS resources.
# False.

# notes

Networking and Content Delivery Services

    Amazon VPC - Lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define.
    Elastic Load Balancing - Automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions.
    Amazon CloudFront - A fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment.
    AWS Transit Gateway - A service that enables customers to connect their Amazon Virtual Private Clouds (VPCs) and their on-premises networks to a single gateway.
    Amazon Route 53 - A highly available and scalable cloud Domain Name System (DNS) web service.
    AWS Direct Connect - A cloud service solution that makes it easy to establish a dedicated network connection from your premises to AWS.
    AWS VPN - Lets you establish a secure and private encrypted tunnel from your network or device to the AWS global network.

AWS Storage Services

    Amazon Simple Storage Services (S3) - Object storage service that offers industry-leading scalability, data availability, security, and performance.
    Amazon Elastic Block Storage (EBS) - An easy to use, high performance block storage service designed for use with Amazon Elastic Compute Cloud (EC2) for both throughput and transaction intensive workloads at any scale.
    Amazon Elastic File System (EFS) - A simple, scalable, fully managed elastic NFS file system for use with AWS Cloud services and on-premises resources.
    Amazon Simple Storage Service Glacier - A secure, durable, and extremely low-cost Amazon S3 cloud storage classes for data archiving and long-term backup.

AWS Compute Services

    Amazon EC2 - A web service that provides secure, resizable compute capacity in the cloud.
    Amazon EC2 Auto Scaling - Helps to maintain application availability and allows you to automatically add or remove EC2 instances according to conditions you define.
    Amazon Elastic Container Services (ECS) - A fully managed container orchestration service.
    Amazon EC2 Container Registry (ECR) - A fully-managed Docker container registry that makes it easy for developers to store, manage, and deploy Docker container images.
    AWS Elastic Beanstalk - An easy-to-use service for deploying and scaling web applications and services developed with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker on familiar servers such as Apache, Nginx, Passenger, and IIS.
    AWS Lambda - Lets you run code without provisioning or managing servers.
    Amazon Elastic Kubernetes Services (EKS) - A fully managed Kubernetes service.
    AWS Fargate - A serverless compute engine for containers that works with both Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes Service (EKS).

