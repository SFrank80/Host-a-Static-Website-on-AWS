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

# Ensure running as root
if [ "$(id -u)" != "0" ]; then
   echo "This script must be run as root" 1>&2
   exit 1
fi

# Update all installed packages
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Install Git
yum install -y git

# Navigate to the Apache document root
cd /var/www/html

# Clone the project repository (Replace the URL with your repository URL)
git clone https://github.com/YourUsername/YourRepositoryName.git .

# Enable Apache HTTP Server on boot
systemctl enable httpd

# Start Apache HTTP Server
systemctl start httpd

echo "Website deployment successful."
```

Make sure to adjust the `git clone https://github.com/YourUsername/YourRepositoryName.git .` line to point to your project's repository.

## Conclusion

This setup ensures a scalable, secure, and fault-tolerant environment for hosting a static web application, leveraging AWS's robust infrastrusture.

Replace `https://github.com/YourUsername/YourRepositoryName.git` with the actual URL to your GitHub repository where the static website's files are stored.
