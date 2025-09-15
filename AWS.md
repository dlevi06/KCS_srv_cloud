# Module 1: Cloud Concepts Overview

## Section 1: Introduction to Cloud Computing

### Definition
- On-demand delivery of:
  - Compute power  
  - Database  
  - Storage  
  - Applications  
  - Other IT resources  
- Delivered **via the internet** with **pay-as-you-go pricing**.  
- Shifts infrastructure from **hardware** to **software usage**.  

---

### Traditional Computing Model
- **Infrastructure = Hardware**
- Characteristics of hardware solutions:  
  - Require physical space, staff, and security  
  - Long procurement cycles  
  - High upfront capital expenditure (CapEx)  
  - Capacity planning based on theoretical peak usage (often inaccurate)  

---

### Cloud Computing Model
- **Infrastructure = Software**
- Characteristics of software solutions:  
  - Flexible and scalable  
  - Faster, easier, more cost-effective changes  
  - Eliminate undifferentiated heavy-lifting tasks  

---

### Cloud Service Models
- **IaaS** – Infrastructure as a Service (highest control)  
- **PaaS** – Platform as a Service (less control)  
- **SaaS** – Software as a Service (least control)  

---

### Deployment Models
- **Cloud (Public Cloud)**  
- **Hybrid Cloud**  
- **On-premises (Private Cloud)**  

---

### Key Components
- **Security**: Security Groups, Network ACLs, IAM (authentication & authorization)  
- **Networking**: Elastic Load Balancing, Amazon VPC  
- **Compute**: AMI (Amazon Machine Images), EC2 Instances  
- **Storage & Databases**: EBS, EFS, S3, RDS  

---

## Section 2: Advantages of Cloud Computing

1. **Trade capital expense for variable expense**  
   - No upfront data center investment  
   - Pay only for what you use  

2. **Massive economies of scale**  
   - AWS aggregates demand across customers  
   - Lower costs passed on to users  

3. **Stop guessing capacity**  
   - No over-provisioning (wasted cost)  
   - No under-provisioning (performance issues)  
   - Scale on demand  

4. **Increase speed and agility**  
   - Traditional: Weeks/months to provision resources  
   - Cloud: Minutes to get resources  

5. **Stop spending money on running and maintaining data centers**  

6. **Go global in minutes**  
   - Deploy workloads across multiple regions instantly  

---

## Section 3 - Introduction to AWS

---

## 1️ What Are Web Services?

* **Definition:**
  A web service is any piece of software that makes itself available over the internet and communicates using standardized formats such as **XML (Extensible Markup Language)** or **JSON (JavaScript Object Notation)** for the request and response in an **API (Application Programming Interface)** interaction.
* **Basic flow:**

  * **Client** sends a **request message** through the **Internet**
  * **Web service** processes the request
  * Sends back a **response message**

Web services enable different applications to talk to each other, regardless of platform or programming language.

---

## 2️ What Is AWS (Amazon Web Services)?

* **Definition:**
  AWS is a **secure cloud platform** that offers a wide range of global, cloud-based products and services.
* **Key points:**

  * Provides on-demand access to **compute, storage, networking, databases**, and other IT resources.
  * Offers flexibility and scalability.
  * **Pay-as-you-go pricing**: You pay only for what you use.
  * Services integrate like **building blocks**, allowing you to design custom solutions.

---

## 3️ Categories of AWS Services

AWS groups its offerings into many service categories, including:

* **Analytics**
* **Application Integration**
* **AR & VR (Augmented / Virtual Reality)**
* **Blockchain**
* **Business Applications**
* **Compute**
* **Cost Management**
* **Customer Engagement**
* **Database**
* **Developer Tools**
* **End User Computing**
* **Game Tech**
* **Internet of Things (IoT)**
* **Machine Learning**
* **Management & Governance**
* **Media Services**
* **Migration & Transfer**
* **Mobile**
* **Networking & Content Delivery**
* **Robotics**
* **Satellite**
* **Security, Identity & Compliance**
* **Storage**

---

## 4️ Choosing an AWS Service

* The right service depends on your **business goals** and **technical requirements**.
* Examples of compute & deployment options:

  * **VMware Cloud on AWS**
  * **Amazon EC2** – Virtual servers in the cloud
  * **AWS Lambda** – Serverless compute (run code without provisioning servers)
  * **Amazon ECS / EKS** – Container orchestration
  * **AWS Elastic Beanstalk** – Managed application platform
  * **AWS Fargate** – Serverless containers
  * **AWS Outposts** – AWS infrastructure on-premises
  * **Amazon Lightsail** – Simple virtual private servers
  * **AWS Batch** – Batch computing at scale

---

## 5️ AWS Services Covered in This Course

### Compute

* Amazon EC2
* AWS Lambda
* AWS Elastic Beanstalk
* Amazon EC2 Auto Scaling
* Amazon ECS (Elastic Container Service)
* Amazon EKS (Elastic Kubernetes Service)
* Amazon ECR (Elastic Container Registry)
* AWS Fargate

### Security, Identity & Compliance

* AWS IAM (Identity and Access Management)
* Amazon Cognito
* AWS Shield
* AWS Artifact
* AWS KMS (Key Management Service)

### Storage

* Amazon S3 (Simple Storage Service)
* Amazon S3 Glacier (archival storage)
* Amazon EFS (Elastic File System)
* Amazon EBS (Elastic Block Store)

### Database

* Amazon RDS (Relational Database Service)
* Amazon DynamoDB (NoSQL database)
* Amazon Redshift (data warehouse)
* Amazon Aurora (MySQL/PostgreSQL-compatible DB)

### Networking & Content Delivery

* Amazon VPC (Virtual Private Cloud)
* Amazon Route 53 (DNS & domain routing)
* Amazon CloudFront (Content Delivery Network)
* Elastic Load Balancing

### Management & Governance

* AWS Trusted Advisor
* Amazon CloudWatch (monitoring)
* AWS CloudTrail (logging API calls)
* AWS Well-Architected Tool
* AWS Auto Scaling
* AWS CLI (Command Line Interface)
* AWS Config
* AWS Management Console
* AWS Organizations

### Cost Management

* AWS Cost & Usage Report
* AWS Budgets
* AWS Cost Explorer

---

## 6️ Three Ways to Interact with AWS

| Method                                   | Description                                                                     |
| ---------------------------------------- | ------------------------------------------------------------------------------- |
| **AWS Management Console**               | Web-based, graphical interface; beginner-friendly                               |
| **AWS CLI (Command Line Interface)**     | Use commands or scripts to manage services                                      |
| **AWS SDKs (Software Development Kits)** | Integrate AWS services directly into your code (Java, Python, JavaScript, etc.) |

---

## Section 4 Video - Moving to the AWS Cloud

---

## 1. Overview

The **AWS Cloud Adoption Framework (CAF)** provides guidance and best practices to help organizations create a comprehensive approach to cloud computing across the entire organization and throughout the IT lifecycle.
Its goal is to accelerate successful cloud adoption.

* AWS CAF is organized into **six perspectives**.
* Each perspective is a set of **capabilities** that help you plan and manage cloud adoption.

---

## 2. AWS CAF Perspectives

| Group                  | Perspective    | Focus                                                  |
| ---------------------- | -------------- | ------------------------------------------------------ |
| Business Capabilities  | **Business**   | Aligning IT with business goals                        |
|                        | **People**     | Managing human resources and organizational change     |
|                        | **Governance** | Aligning IT strategy and processes with business goals |
| Technical Capabilities | **Platform**   | Designing and provisioning IT systems                  |
|                        | **Security**   | Protecting data, systems, and access                   |
|                        | **Operations** | Monitoring, managing, and supporting services          |

---

## 3. Perspectives and Capabilities

### 3.1 Business Perspective

**Purpose:** Ensure IT is aligned with business needs, and IT investments deliver measurable results.
**Key Capabilities:**

* IT finance
* IT strategy
* Benefits realization
* Business risk management

**Typical stakeholders:** Business managers, finance managers, budget owners, strategy stakeholders.

---

### 3.2 People Perspective

**Purpose:** Build an agile organization through training, staffing, and organizational change.
**Key Capabilities:**

* Resource management
* Incentive management
* Career management
* Training management
* Organizational change management

**Typical stakeholders:** HR, staffing teams, people managers.

---

### 3.3 Governance Perspective

**Purpose:** Align IT strategy and goals with business strategy and goals, maximizing IT’s business value and minimizing risk.
**Key Capabilities:**

* Portfolio management
* Program and project management
* Business performance measurement
* License management

**Typical stakeholders:** CIO, program managers, enterprise architects, business analysts, portfolio managers.

---

### 3.4 Platform Perspective

**Purpose:** Understand and describe IT systems, their relationships, and the target-state architecture.
**Key Capabilities:**

* Compute provisioning
* Network provisioning
* Storage provisioning
* Database provisioning
* Systems and solution architecture
* Application development

**Typical stakeholders:** CTO, IT managers, solutions architects.

---

### 3.5 Security Perspective

**Purpose:** Ensure the organization meets its security objectives.
**Key Capabilities:**

* Identity and access management
* Detective controls
* Infrastructure security
* Data protection
* Incident response

**Typical stakeholders:** CISO, IT security managers, IT security analysts.

---

### 3.6 Operations Perspective

**Purpose:** Align with and support business operations, defining how daily and long-term activities are conducted.
**Key Capabilities:**

* Service monitoring
* Application performance monitoring
* Resource inventory management
* Release/change management
* Reporting and analytics
* Business continuity / disaster recovery
* IT service catalog

**Typical stakeholders:** IT operations managers, IT support managers.

---


