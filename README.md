<h1>AWS DevOps vProfile Deployment Project</h1>



## Description

This project is a hands-on DevOps deployment of the **vProfile** application, inspired by a Udemy course. It simulates a real-world production deployment of a **multi-tier web application** using AWS services, shell scripts, and manual DevOps practices.

### Application Overview
The application follows a **microservices-based architecture**, consisting of:
- **Frontend:** Apache Tomcat  
- **Backend Services:** MySQL, RabbitMQ, Memcached  

### Repository Contents
This repository includes essential files for deployment and automation:
- **pom.xml** – Maven build configuration  
- **Jenkinsfile** – CI/CD pipeline for automated deployments  
- **Ansible Playbooks** – Infrastructure automation and configuration management  
- **application.properties** – Application configuration settings  
- **dbsetup** – Database initialization scripts  

### Deployment Features
- **EC2 Instance Provisioning** – Automated setup for application servers  
- **Security Groups & Key Pair Setup** – Defined inbound/outbound rules and secure access  
- **ELB + Auto Scaling Configuration** – Load balancing and dynamic scaling implementation  
- **Domain Management with Route 53 + GoDaddy** – DNS setup and mapping configurations  
- **SSL with AWS Certificate Manager** – Securing application traffic with HTTPS  
- **App Deployment Pipeline** – Build automation and artifact management  

### Screenshots
Screenshots of all deployment steps are available in the **`screenshots`** folder.

## Technologies Used

- **Cloud Services:** AWS EC2, S3, Route 53, IAM, ACM, Auto Scaling, ALB  
- **Application Server:** Apache Tomcat 10  
- **Databases & Messaging:** MySQL, RabbitMQ, Memcached  
- **Development & Automation:** Maven, Bash, Git  
- **Domain Management:** GoDaddy for Domain Mapping  

## Key Features

### End-to-End DevOps Deployment
Full-stack deployment of a Java web application using AWS services and automated provisioning.

### Infrastructure as Code (IaC)
EC2 instances provisioned and configured using bash scripts with user-data.

### Secure and Scalable Architecture
- Custom Security Groups for frontend and backend services.
- IAM Role & User setup to manage access control securely.

### S3 Artifact Management
Built and stored the application artifact in S3, then deployed it to the frontend server.

### Application Build Automation
Used Maven to compile the application and generate a deployable `.war` file.

### Dynamic DNS Setup
Integrated Route 53 and GoDaddy domain to route traffic to the correct endpoint.

### HTTPS with ACM
Secured the website with an SSL certificate via AWS Certificate Manager and linked to the Load Balancer.

### Auto Scaling Group
Achieved high availability and fault tolerance with an Auto Scaling Group and Launch Template built from an AMI.

### Load Balancer Integration
Configured Application Load Balancer (ALB) with health checks and target groups to distribute traffic.

### Production-Ready Workflow
Verified the deployment process from build to launch using best DevOps practices and rollback-ready AMIs.


# Deployment Steps

This project demonstrates how I deployed the vProfile application using core DevOps practices on AWS, including provisioning, configuration, load balancing, and auto scaling.

## Step 1: IAM & S3 Setup

- **Created a new IAM User**  
  Granted programmatic access and AmazonS3FullAccess permission.  

- **Created an IAM Role for Tomcat**  
  Attached AmazonS3FullAccess and linked it to the EC2 instance.  

- **Created an S3 Bucket**  
  Used for storing the application artifact (.war file).  

---

## Step 2: Key Pairs & EC2 Provisioning

- **Generated SSH Key Pairs**  
  Ensured secure access to EC2 instances.  

- **Launched EC2 Instances**  
  Provisioned instances for:
  - Tomcat (Frontend)  
  - MySQL DB  
  - RabbitMQ  
  - Memcached  

- **Used User-Data Scripts**  
  Automated installation and configuration.  

---

## Step 3: Security Group Configuration
- **Created Security Group for Load Balancer**  
  - Allowed inbound access from the internet on ports **80 (HTTP) and 443 (HTTPS)**.  
  - Ensured only public traffic reaches the Load Balancer.  

- **Created Security Group for Tomcat Instance**  
  - Allowed inbound traffic **only from the Load Balancer** on port **8080**.  
  - Restricted direct internet access for security.  

- **Configured Custom Security Groups**  
  - **Database & Backend Services:** Allowed only internal communication ports.  
  - Followed least privilege principle for secure access 

---

## Step 4: Application Build & Configuration

- **Cloned vProfile Repository**  
  Retrieved source code for deployment.  

- **Edited application.properties File**  
  Updated database hostname, ports, and credentials for EC2 setup.  

- **Built the Application**  
  Ran `mvn install` to generate `target/vprofile.war`.  

---

## Step 5: S3 Upload & Deployment to Tomcat

- **Uploaded `.war` Artifact to S3**  
  Ensured accessibility for deployment.  

- **Connected to Tomcat Instance**  
  Removed default ROOT webapp in Tomcat 10.  

- **Downloaded & Deployed `.war` from S3**  
  Moved it to the ROOT directory for automatic application startup.  

---

## Step 6: DNS Configuration (Route 53 + GoDaddy)

- **Created a Hosted Zone in Route 53**  
  Managed domain DNS records efficiently.  

- **Mapped Subdomains**  
  Linked `app.example.com` to EC2 or ALB DNS names.  

- **Updated GoDaddy DNS**  
  Configured nameservers to point to Route 53 hosted zone.  

---

## Step 7: Load Balancer & HTTPS (ACM)

- **Configured Application Load Balancer (ALB)**  
  Distributed traffic efficiently.  

- **Created Target Groups**  
  Assigned instances for handling requests.  

- **Issued SSL Certificate via AWS Certificate Manager (ACM)**  
  Secured the application with HTTPS encryption.  

- **Enabled HTTPS on ALB**  
  Verified domain access using SSL.  

---

## Step 8: Creating AMI & Launch Template

- **Created an Amazon Machine Image (AMI)**  
  Captured pre-configured Tomcat instance snapshot.  

- **Built a Launch Template**  
  Integrated AMI, IAM Role, and security settings for autoscaling.  

---

## Step 9: Auto Scaling Group

- **Configured Auto Scaling**  
  - Set minimum, maximum, and desired instance counts.  
  - Defined health checks and instance refresh mechanisms.  

- **Linked ALB Target Group**  
  Balanced incoming requests dynamically.  

- **Verified Scaling Behavior**  
  Simulated load and checked automatic scaling responses.  

---

## Step 10: Final Verification & Testing

- **Accessed Application via HTTPS**  
  Ensured domain resolution and security.  

- **Validated Frontend & Backend Communication**  
  Checked requests between services and database.  

- **Confirmed Load Balancer Distribution**  
  Ensured traffic was evenly spread across instances.  

- **Checked Auto Scaling Behavior**  
  Verified dynamic scaling up/down.  

---


</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
