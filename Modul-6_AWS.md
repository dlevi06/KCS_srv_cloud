Here is the completely rewritten and formatted English version of your notes in Markdown format. I have corrected typos, structured the text for better readability, and converted implied visual information into descriptive text as requested.

```markdown
# AWS Module 6 - Compute

**Original Author:** lemasyma
**Topic:** AWS Compute Services, EC2, Containers, Lambda, Elastic Beanstalk

---

## Section 1: Compute Services Overview

### AWS Compute Services List
* **Amazon EC2:** Resizable virtual machines in the cloud.
* **Amazon EC2 Auto Scaling:** Automatically launch or terminate EC2 instances based on defined conditions.
* **Amazon ECR (Elastic Container Registry):** Store and retrieve Docker images.
* **Amazon ECS (Elastic Container Service):** Container orchestration service that supports Docker.
* **VMWare Cloud on AWS:** Hybrid cloud solution without needing custom hardware.
* **AWS Elastic Beanstalk:** Platform to run and manage web applications (PaaS).
* **AWS Lambda:** Serverless compute solution (run code without provisioning servers).
* **Amazon EKS (Elastic Kubernetes Service):** Run managed Kubernetes on AWS.
* **Amazon LightSail:** Easy-to-use platform for building applications or websites (VPS).
* **AWS Batch:** Run batch jobs at any scale.
* **AWS Fargate:** Serverless compute engine for containers.
* **AWS Outposts:** Run AWS services in your on-premises data center.
* **AWS Serverless Application Repository:** Discover, deploy, and publish serverless applications.

### Categorizing and Choosing the Optimal Compute Service
The service you choose depends entirely on your specific use case.

**Aspects to consider:**
1.  **Application Design:** How is the app architected?
2.  **Usage Patterns:** Is the traffic steady or spiky?
3.  **Configuration Management:** Which settings do you want to manage yourself vs. having AWS manage?

*Note:* Selecting the wrong compute solution can lead to lower performance efficiency. A good starting place is to understand all available compute options.

---

## Section 2: Amazon EC2 (Elastic Compute Cloud)

### Overview
* Provides **virtual machines** (EC2 instances) in the cloud.
* Gives you **full control** over the guest operating system (Windows or Linux).
* You can launch instances of any size in any Availability Zone worldwide.
* Instances are launched from **Amazon Machine Images (AMIs)**.
* Speed: Launch with a few clicks or lines of code; ready in minutes.
* Security: You control network traffic to and from instances.

### Example Use Cases
* Application server
* Web server
* Database server
* Game server
* Mail server
* Media server
* Catalog server
* File server
* Computing server
* Proxy server

### Launching an Amazon EC2 Instance: Key Decisions
When creating an instance, you generally make 9 key decisions.

#### 1. Select an AMI (Amazon Machine Image)
An AMI is a template used to create the instance. It contains the OS (Windows/Linux) and often pre-installed software.
* **Quick Start:** Standard Linux and Windows AMIs provided by AWS.
* **My AMIs:** AMIs you have created previously.
* **AWS Marketplace:** Pre-configured templates from third-party vendors.
* **Community AMIs:** Shared by others (use at your own risk).

#### 2. Select an Instance Type
The instance type determines the hardware capabilities.
* **Factors:** Memory (RAM), Processing Power (CPU), Disk Space/Type (Storage), Network Performance.
* **Categories:**
    * General Purpose
    * Compute Optimized
    * Memory Optimized
    * Storage Optimized
    * Accelerated Computing
* **Naming Convention:** Types are defined by Family, Generation, and Size (e.g., `t3.micro`).

#### Networking Features
* Bandwidth (Gbps) varies by instance type.
* **Cluster Placement Group:** Use this for interdependent instances to maximize low-latency network performance.
* **Enhanced Networking:** Supported on most types (uses Elastic Network Adapter - ENA up to 100 Gbps, or Intel 82599 VF up to 10 Gbps).

---

## Section 3: Amazon EC2 (Part 2) - Network & Storage

#### 3. Specify Network Settings
* **Placement:** Identify the VPC (Virtual Private Cloud) and the Subnet.
* **Public IP:** Decide if a public IP should be automatically assigned (required for internet accessibility).

#### 4. Attach IAM Role (Optional)
* If the software on the EC2 instance needs to interact with other AWS services (e.g., S3, DynamoDB), attach an IAM Role.
* This role is kept in an **instance profile**.
* *Note:* You can attach or replace roles on instances that are already running.

#### 5. User Data Script (Optional)
* Scripts used to customize the runtime environment.
* **Execution:** Runs only the **first time** the instance starts.
* **Benefit:** Reduces the need to build and maintain many custom AMIs by automating configuration at boot.

#### 6. Specify Storage
You must configure the **Root Volume** (where the OS is installed) and can attach additional volumes.
* **Specifications per volume:** Size (GB), Volume Type (SSD vs HDD), Encryption, and "Delete on Termination" setting.

**Storage Options:**
1.  **Amazon EBS (Elastic Block Store):**
    * Durable, block-level storage.
    * Separated from the host computer.
    * **Persistence:** If you stop the instance, the data on EBS persists.
2.  **Instance Store (Ephemeral Storage):**
    * Storage disks physically attached to the host computer.
    * **Volatility:** If the instance stops (user error or system failure), **all data is deleted/lost**.

**Scenario Comparison (Data Persistence):**
* **Instance 1 (EBS Root Volume):** If stopped and started, the OS and data remain intact.
* **Instance 2 (Instance Store Root Volume):** If stopped, all data (including the OS) is lost.

*Other Storage:* You can also mount Amazon EFS (file system) or connect to S3.

---

## Section 4: Amazon EC2 (Part 3) - Final Config & Lifecycle

#### 7. Add Tags
* **Definition:** Key-value pair labels assigned to resources.
* **Purpose:** Attach metadata for filtering, automation, cost allocation, and access control.

#### 8. Security Group Settings
* **Definition:** A virtual firewall controlling traffic to the instance.
* **Operation:** Exists *outside* the guest OS.
* **Rules:** You specify the Port, Protocol (TCP/UDP/ICMP), and Source IP/Group allowed to connect.

#### 9. Identify the Key Pair
* Required for secure login.
* **Components:** Public Key (stored by AWS) + Private Key (stored by you).
* **Usage:**
    * *Windows:* Use private key to decrypt the Administrator password.
    * *Linux:* Use private key with SSH to connect.

### Programmatic Launch (CLI Example)
You can launch instances via the Command Line Interface (CLI) instead of the console.
```bash
aws ec2 run-instances \
    --image-id ami-1a2b3c4d \
    --count 1 \
    --instance-type c3.large \
    --key-name MyKeyPair \
    --security-groups MySecurityGroup \
    --region us-east-1

```

### EC2 Instance Lifecycle & IP Addressing

* **Rebooting:** Does **not** change IP addresses or DNS hostnames.
* **Stopping and Starting:**
* **Public IPv4 & External DNS:** Will change (dynamic).
* **Private IPv4 & Internal DNS:** Do **not** change.


* **Elastic IP:** Use this if you require a persistent static Public IP address that stays with your account until released.

### EC2 Instance Metadata

* Data *about* your instance (e.g., Instance ID, IPs, Region).
* **Access URL:** `http://169.254.169.254/latest/meta-data/` (accessible only from within the instance).
* **User Data Access:** `http://169.254.169.254/latest/user-data/`

### Monitoring (Amazon CloudWatch)

* **Tab:** Visible in the EC2 Console "Monitoring" tab.
* **Basic Monitoring:** Free, metrics sent every 5 minutes.
* **Detailed Monitoring:** Paid, metrics sent every 1 minute.

---

## Section 5: Amazon EC2 Cost Optimization

### Pricing Models

1. **On-Demand:** Pay by the hour/second. No commitment. Good for variable short-term workloads.
2. **Dedicated Hosts:** Physical server fully dedicated to you. (Compliance requirements).
3. **Dedicated Instances:** Instances running on hardware dedicated to a single customer.
4. **Reserved Instances (RI):** 1 or 3-year commitment. Significant discount.
* **Scheduled RIs:** Capacity reserved for specific recurring time windows.


5. **Spot Instances:**
* Bid on unused AWS capacity.
* **Cheapest option** (big discounts).
* **Risk:** Can be interrupted/terminated by AWS with a **2-minute warning**.
* Best for flexible, stateless, or fault-tolerant workloads.



### The 4 Pillars of Cost Optimization

**Pillar 1: Right Size**

* Match provisioned instances (CPU, RAM) to actual needs.
* Use CloudWatch metrics to find idle instances.
* *Strategy:* Right size first, then Reserve.

**Pillar 2: Increase Elasticity**

* Stop or hibernate non-production (dev/test) instances when not in use.
* Use **Auto Scaling** to handle peaks and valleys automatically.

**Pillar 3: Optimal Pricing Model**

* **Variable workloads:** Use On-Demand + Spot.
* **Predictable workloads:** Use Reserved Instances.
* Consider Serverless (Lambda) to avoid idle server costs.

**Pillar 4: Optimize Storage Choices**

* Resize EBS volumes if they are too large.
* Change volume types (e.g., from General Purpose SSD to Throughput Optimized HDD for cheaper storage).
* Delete unneeded EBS snapshots.
* Use Lifecycle policies to move data to S3.

**Recommendations:**

* Tag resources for cost allocation.
* Define metrics and targets.
* Assign responsibility to a team.

---

## Section 6: Container Services

### Container Basics

* **Definition:** A method of operating system virtualization.
* **Benefits:** Repeatable, self-contained, runs the same everywhere (Laptop -> Test -> Prod), faster startup than VMs.
* **Docker:** Platform to build, test, and deploy containers. Containers are created from **Images**.

### Amazon ECS (Elastic Container Service)

* Highly scalable container management service.
* **Function:** Orchestrates the running of Docker containers.
* Integrates with ELB, Security Groups, EBS, and IAM.

**Cluster Options (Launch Types):**

1. **EC2 Launch Type:** You manage the EC2 instances (nodes) that run the containers. More granular control.
2. **AWS Fargate Launch Type:** Serverless. You do not manage the underlying EC2 instances. Easier maintenance.

### Kubernetes & Amazon EKS

* **Kubernetes:** Open-source software for container orchestration at scale. Manages clusters of nodes.
* **Amazon EKS:** Fully managed Kubernetes service. Certified conformant.
* **Use Case:** Run Kubernetes on AWS without installing/operating the control plane.

### Amazon ECR (Elastic Container Registry)

* Fully managed Docker container registry.
* Used to store, manage, and deploy container images.
* Supports team collaboration and access control.

---

## Section 7: Introduction to AWS Lambda

### Run Code Without Servers

* **Serverless Compute:** You do not provision or manage servers.
* **Benefits:**
* Supports multiple languages (Python, Node.js, Java, etc.).
* Automated administration and patching.
* Built-in fault tolerance.
* Pay-per-use (pay only for compute time used).



### Configuration

1. **Create Function:** Name it.
2. **Runtime:** Select environment (e.g., Python, Node.js).
3. **Permissions:** Assign an Execution Role (IAM) to access other services.
4. **Trigger:** Define what event starts the function (e.g., file upload to S3, HTTP request, timer).
5. **Resources:** Specify Memory (up to 3008 MB). *Note: CPU scales with memory.*
6. **Timeouts:** Max execution time is 15 minutes.

### Examples

* **Schedule-based:** Start/Stop EC2 instances every night at 8 PM.
* **Event-based:** Create a thumbnail immediately when an image is uploaded to S3.

### Limits

* **Concurrent Executions:** 1,000 per region (Soft limit).
* **Hard Limits (Individual Function):**
* Max Memory: 3,008 MB.
* Timeout: 15 minutes.
* Deployment Package: 250 MB (unzipped).



---

## Section 8: Introduction to AWS Elastic Beanstalk

### Overview

* **Type:** Platform as a Service (PaaS).
* **Purpose:** Easy way to get web applications up and running.
* **Managed Service:** Automatically handles details like provisioning, load balancing, scaling, and monitoring.
* **Cost:** No charge for Beanstalk itself; you pay for the underlying resources (EC2, S3, etc.) it creates.

### Deployments

* **Supported Platforms:** Java, .NET, PHP, Node.js, Python, Ruby, Go, Docker.
* **Process:** You simply upload your code. Elastic Beanstalk handles the deployment to servers (Apache, NGINX, IIS, etc.).

```

```
