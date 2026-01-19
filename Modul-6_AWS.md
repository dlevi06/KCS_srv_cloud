---

# Module 5 - Networking and Content Delivery

## Objectives / Topics

- Recognize the basics of networking
- Describe virtual networking in the cloud with Amazon VPC
- Label a network diagram
- Design a basic VPC architecture
- Indicate the steps to build a VPC
- Identify security groups
- Create your own VPC and add additional components to it to produce a customized network
- Identify the fundamentals of Amazon Route 53
- Recognize the benefits of Amazon CloudFront

<br/>

## Section 1: Networking Basics

**Network:** Two or more machines that are connected together in order to communicate. A network can be divided into subnets and networking requires a networking device such as a router or a switch.

**IP Address:** A unique numerical label assigned to each device connected to a computer network. IPv4 defines an IP address as a 32-bit number, but because of the growth of the Internet IPv6 was created, using 128 bits for the IP address.

**Classless Inter-Domain Routing (CIDR):** A method for allocating IP addresses and IP routing. CIDR notation is a compact representation of an IP address and its associated routing prefix. The notation is constructed from an IP address, a slash ('/') character, and an integer. The integer is the count of leading 1 bits in the subnet mask. Larger values here indicate smaller networks. The maximum size of the network is given by the number of addresses that are possible with the remaining, least-significant bits below the prefix.

- Example: The IPv4 block 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.

**Open Systems Interconnection (OSI) Model:** A conceptual model that characterises and standardises the communication functions of a computing system without regard to its underlying internal structure and technology. Its goal is the interoperability of diverse communication systems with standard communication protocols. The model partitions a communication system into abstraction layers.

| Layer        | Number | Function                                                             | Protocol/Address         |
|--------------|--------|----------------------------------------------------------------------|--------------------------|
| Application  | 7      | Means for an application to access a computer network                | HTTP(S), FTP, DHCP, LDAP |
| Presentation | 6      | - Ensures that the application layer can read the data <br/>- Encryption  | ASCI, ICA                |
| Session      | 5      | Enables orderly exchange of data                                     | NetBIOS, RPC             |
| Transport    | 4      | Provides protocols to support host-to-host communication             | TCP, UDP                 |
| Network      | 3      | Routing and packet forwarding (routers)                              | IP                       |
| Data Link    | 2      | Transfer data in the same LAN network (hubs and switches)            | MAC                      |
| Physical     | 1      | Transmission and reception of raw bit streams over a physical medium | Signals (1s and 0s)      |

<br/>

## Section 2: Amazon VPC

- Enables you to provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define
- Gives you control over your virtual networking resources, including: Selection of IP address range, creation of subnets, and configuration of route tables and network gateways
- Closely resembles a traditional network that you would operate in your own data center, with the benefits of using the scalable infrastructure of AWS
- Enables you to customize the network configurationfor your VPC
- Enables you to use multiple layers of security
- You can create a VPC that spans multiple Availability Zones

### **VPCs**

- Logically isolated from other VPCs
- Dedicated to your AWS account
- Belong to a single AWS Region and can span multiple Availability Zones
- When you create a VPC, you assign it to an IPv4 or IPv6 CIDR block. You cannot change the address range after creation.

### **Subnets**

- Range of IP addresses that divide a VPC
- Belong to a single Availability Zone
- Classified as public (has route to the internet) or private (no internet)
- CIDR blocks of subnets cannot overlap
- Each CIDR block has 5 reserved addresses for: network address, internal communication, DNS resolution, future use, and network broadcast address

### **Elastic Network Interface**

- An Elastic IP address is a static IPv4 address, associated with your AWS account, designed for dynamic cloud computing. You can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.
- A virtual network interface that you can attach to an instance.You can detach from the instance, and attach to another instance to redirect network traffic.
- Its attributes follow when it is reattached to a new instance.
- Each instance in your VPC has a default network interface that is assigned a private IPv4 address from the IPv4 address range of your VPC

### **Routes and Route Tables**

- The route table controls routing for the subnet
- A route table contains a set of rules (or routes) that you can configure to direct network traffic from your subnet
- Each route specifies a destination and a target
- By default, every route table contains a local route for communication within the VPC
- Each subnet must be associated with a single route table

<br/>

## Section 3: VPC Networking

### **Internet Gateway**

A scalable, redundant, and highly available VPC component that allows communication between instances in your VPC and the public internet. An internet gateway serves two purposes:

1. Provide a target in your VPC route tables for internet traffic
2. Perform network address translation for instances that were assigned public IPv4 addresses.

To make a subnet public, you attach an internet gateway to your VPC and add a route entry to the route table associated with the subnet.

### **Network Address Translation (NAT) Gateway**

Enables instances in a private subnet to connect to the internet or other AWS services, but it prevents the public internet from initiating a connection with those instances. To create a NAT Gateway you must:

1. Specify the public subnet in which the gateway should live.
2. Specify an elastic IP address to associate with the NAT Gateway when you create it.

After you create a NAT Gateway, you must update the route table that is associated with one or more of your private subnets to point internet-bound traffic to the NAT gateway. This allows instances in your private subnets to communicate with the internet.

### **VPC Sharing**

Enables customers to share subnets with other AWS accounts in the same organization. VPC Sharing enables multiple AWS accounts to create their application resources in a shared, centrally managed VPC.

The account that owns the VPC shares one or more subnets with other accounts, called participants, that belong to the same organization. After a subnet is shared, participants can view, create, modify, and delete their application resources in the subnets that are shared with them.

### **VPC Peering**

Enables you to privately route traffic between two VPCs. Instances in either VPC can communicate with each other as if they were on the same network. You can create VPC peering connection between your own VPCs with a VPC in another AWS accounts, or between regions.

When you set up the VPC peering connection, you create rules in your route table to allow the VPCs to communicate with each other. VPC peering has some restrictions:

- IP Spaces cannot overlap
- Transitive peering (chaining VPC peering) is not supported
- You can only have one peering resource between the same two VPCs

### **AWS Direct Connect**

Enables your to establish a dedicated private connection between your network and one of the direct connect locations. The private connection can increase bandwidth, throughput, and provide a more consistent network experience than internet-based or VPN connections.

### **VPC Endpoints**

A virtual device that enables you to privately connect a VPC to supported AWS services. There are two types of endpoints:

1. Gateway endpoints that you specify as a target for a route in your route table to either S3 or DynamoDB
2. Interface endpoints are powered by AWS PrivateLink. PrivateLink provides private connectivity between VPCs, AWS services, and on-premises applications.

### **AWS Transit Gateway**

A network transit hub that is used to interconnect virtual private clouds, on-premises networks, VPCs, Direct Connect gateways, and VPN connections to a transit gateway.

The topology of a Transit Gateway is a hub and spoke which reduces the number of connections required, and the complexity to implement and maintain it.

<br/>

## Section 4: VPC Security

### **Security Groups**

- Act at the instance level
- Security groups have rules that control inbound and outbound instance traffic.
- Default security groups deny all inbound traffic and allow all outbound traffic.
- Security groups are stateful - return traffic is automatically allowed, regardless of rules
- You can specify allow rules, but not deny rules.
- All rules are evaluated before the decision to allow traffic.

### **Network Access Control Lists (ACLs)**

- Act at the subnet level
- A network ACL has separate inbound and outbound rules, and each rule can either allow or deny traffic.
- Default network ACLs allow all inbound and outbound IPv4 traffic.
- Network ACLs are stateless - return traffic must be explicitly allowed by rules
- Customn network ACLs deny all inbound and outbound traffic until you add rules.
- You can specify both allow and deny rules.
- Rules are evaluated in number order, starting with the lowest number

<br/>

## Section 5: Amazon Route 53

- A highly available and scalable Domain Name System (DNS) web service
- Used to route end users to internet applications by translating names into numeric IP addresses (like 192.0.2.1) that computers use to connect to each other
- Fully compliant with IPv4 and IPv6
- Connects user requests to infrastructure running in AWS and also outside of AWS
- Is used to check the health of your resources
- Features traffic flow
- Enables you to register domain names

### **Supported Routing**

- Simple routing – Use in single-server environments
- Weighted round robin routing – Assign weights to resource record sets to specify the frequency
- Latency routing – Help improve your global applications
- Geolocation routing – Route traffic based on location of your users
- Geoproximity routing – Route traffic based on location of your resources
- Failover routing – Fail over to a backup site if your primary site becomes unreachable. Improve the availability of your applications that run on AWS by:
  - Configuring backup and failover scenarios for your own applications
  - Enabling highly available multi-region architectures on AWS
  - Creating health checks
- Multivalue answer routing – Respond to DNS queries with up to eight healthy records selected at random

<br/>

## Section 6: Amazon CloudFront

- Fast, global, and secure CDN service
- Global network of edge locations and Regional edge caches
- Self-service model
- Pay-as-you-go pricing

### **CloudFront Infrastructure**

Edge locations – A network of data centers that CloudFront uses to serve popular content quickly to customers.

Regional edge cache – CloudFront location that caches content that is not popular enough to stay at an edge location. It is located between the origin server and the global edge location.

### **Content Delivery Network**

- A globally distributed system of caching servers
- Caches copies of commonly requested files (static content)
- Delivers a local copy of the requested content from a nearby cache edge or Point of Presence
- Accelerates delivery of dynamic content
- Improves application performance and scaling

### **CloudFront Pricing**

- Charged for the volume of data transferred out from Amazon CloudFront edge location to the internet or to your origin.
- Charged for number of HTTP(S) requests.
- No additional charge for the first 1,000 paths that are requested for invalidation each month. Thereafter, $0.005 per path that is requested for invalidation.
- $600 per month for each custom SSL certificate that is associated with one or more CloudFront distributions that use the Dedicated IP version of custom SSL certificate support.
<br/>

---

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
