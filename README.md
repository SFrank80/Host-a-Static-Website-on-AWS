![Alt-text](/Host_a_Static_Website_on_AWS.png)

 ---
 This README provides a concise yet detailed guide for deploying a static website on AWS, perfect for collaborators or users interested in replicating or contributing to your project.

# Hosting a Static Website on AWS

## Overview

This DevOps project demonstrates the process of hosting a static HTML web application on Amazon Web Services (AWS), utilizing a variety of resources to ensure the application is secure, highly available, and scalable. The application infrastructure spans across multiple availability zones within a Virtual Private Cloud (VPC), employing an Application Load Balancer (ALB) and Auto Scaling to efficiently manage web traffic and maintain performance.

## Architecture

1. **Virtual Private Cloud (VPC):** Configured with public and private subnets across two different availability zones for enhanced fault tolerance and reliability.
2. **Internet Gateway (IGW):** Facilitates connectivity between VPC instances and the internet.
3. **Security Groups:** Acts as a virtual firewall to control inbound and outbound traffic to instances.
4. **Public and Private Subnets:** Hosts infrastructure components like the NAT Gateway and Application Load Balancer, with web servers positioned within private subnets for security.
5. **EC2 Instances:** Serve the static website content, accessible securely via EC2 Instance Connect.
6. **Application Load Balancer (ALB):** Distributes incoming web traffic across EC2 instances in multiple availability zones.
7. **Auto Scaling Group:** Ensures the application can scale automatically, maintaining availability and performance.
8. **Certificate Manager:** Secures application communications.
9. **Simple Notification Service (SNS):** Alerts on activities within the Auto Scaling Group.
10. **Route 53:** Manages domain name services, including DNS records pointing to the ALB.

## Deployment Steps

### Prerequisites

- An active AWS account.
- Basic understanding of AWS services (VPC, EC2, ALB, Route 53).
- A registered domain name, either through AWS or another domain registrar.

### Deploying the Website

The deployment involves setting up the AWS infrastructure as described above and then deploying the static content to EC2 instances. The provided bash script automates the deployment of the static web content on EC2 instances.

### Automated Deployment Script

Below is the script to set up your EC2 instances with the static website content. Ensure you have the necessary permissions to execute these commands and replace the GitHub repository URL with your project's repository URL.

```bash
#!/bin/bash

# This script is designed to be run on an Amazon Linux 2 EC2 instance with root privileges.
# It will install Apache, clone your static website from GitHub, and configure Apache to serve the website.

#!/bin/bash

# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install -y git

# Clone the project GitHub repository to the current directory
git clone https://github.com/SFrank80/Host-a-Static-Website-on-AWS.git

# Enable Apache HTTP Server on boot
systemctl enable httpd

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R Host-a-Static-Website-on-AWS/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf Host-a-Static-Website-on-AWS

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd 

# Start the Apache HTTP Server to serve web content
systemctl start httpd

echo "Website deployment successful."
```

## Conclusion

This setup ensures a scalable, secure, and fault-tolerant environment for hosting a static web application, leveraging AWS's robust infrastructure.

Replace ` https://github.com/SFrank80/Host-a-Static-Website-on-AWS.git` with the actual URL to your GitHub repository where the static website's files are stored.
