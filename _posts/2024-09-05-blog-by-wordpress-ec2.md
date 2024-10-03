---
layout: post
title: Deploying Blog Using WordPress on AWS with Docker
categories: [AWS]
---

- [Prerequisites](#prerequisites)
- [Step 1: Launch an EC2 Instance](#step-1--launch-an-ec2-instance)
- [Step 2: Connect to Your EC2 Instance](#step-2--connect-to-your-ec2-instance)
- [Step 3: Install Docker and Docker Compose](#step-3--install-docker-and-docker-compose)
- [Step 4: Create Docker Compose File for WordPress](#step-4--create-docker-compose-file-for-wordpress)
- [Step 5: Start the WordPress and MySQL Containers](#step-5--start-the-wordpress-and-mysql-containers)
- [Step 6: Configure WordPress](#step-6--configure-wordpress)
- [Step 7: Access Your WordPress Site](#step-7--access-your-wordpress-site)
- [Additional Configuration (Optional)](#additional-configuration--optional-)
- [Reference](#reference)

## Prerequisites
1. AWS Account
2. Basic knowledge of AWS EC2 and SSH
3. Docker and Docker Compose installed on your local machine

## Step 1: Launch an EC2 Instance

1. Log in to the AWS Management Console.
2. Navigate to the EC2 Dashboard and click “Launch Instance”.
3. Choose an Amazon Machine Image (AMI):
Select Amazon Linux 2 AMI (recommended).

4. Choose an Instance Type:
Select the instance type (t2.micro is eligible for the free tier).

5. Configure Instance Details:
Default settings are usually sufficient. Ensure the instance is in the desired VPC and subnet.

6. Add Storage: Default 8 GB is typically sufficient, but you can adjust based on your needs.

7. Add Tags:Optionally, add tags to help identify your instance.

8. Configure Security Group:
- Create a new security group or select an existing one
b. Add rules to allow HTTP (port 80), HTTPS (port 443), and SSH (port 22) access.

9. Review and Launch:
- Review your settings and click “Launch”.
- Choose an existing key pair or create a new one for SSH access. Make sure to download the key pair if you create a new one.

## Step 2: Connect to Your EC2 Instance
1. Open your terminal and navigate to the directory where your key pair (.pem file) is located.

2. Connect to your EC2 instance using SSH:

```
ssh -i "your-key-pair.pem" ec2-user@your-ec2-public-ip

```

## Step 3: Install Docker and Docker Compose

1. Update the package index:
```
sudo yum update -y
```
2. Install Docker:
```
sudo amazon-linux-extras install docker -y
sudo service docker start
sudo usermod -a -G docker ec2-user
```
3. Install Docker Compose:
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```
4. Verify installation: docker-compose --version


## Step 4: Create Docker Compose File for WordPress

1. Create a new directory for your WordPress project:
```
mkdir wordpress && cd wordpress
```
2. Create a docker-compose.yml file:
```
nano docker-compose.yml
```
3. Add the following content to the docker-compose.yml file:
```
version: '3.1'
services:
     wordpress:
       image: wordpress:latest
       restart: always
       ports:
         - 80:80
       environment:
         WORDPRESS_DB_HOST: db
         WORDPRESS_DB_USER: exampleuser
         WORDPRESS_DB_PASSWORD: examplepass
         WORDPRESS_DB_NAME: exampledb

     db:
       image: mysql:5.7
       restart: always
       environment:
         MYSQL_DATABASE: exampledb
         MYSQL_USER: exampleuser
         MYSQL_PASSWORD: examplepass
         MYSQL_ROOT_PASSWORD: rootpassword
```

## Step 5: Start the WordPress and MySQL Containers

1. Run Docker Compose to start the containers:
```
sudo docker-compose up -d
```
2. Verify that the containers are running:
```
sudo docker-compose ps
```

## Step 6: Configure WordPress

1. Open your browser and navigate to your EC2 instance’s public IP address.

2. Complete the WordPress installation:

3. Choose your language.

4. Enter your site title, username, password, and email.

5. Click “Install WordPress”.

## Step 7: Access Your WordPress Site

1. Log in to your WordPress site:
- Go to http://your-ec2-public-ip/wp-admin.
- Enter the username and password you set during the WordPress installation.
2. Customize and start blogging: You can now customize your WordPress site and start creating content.

## Additional Configuration (Optional)

1. Enable HTTPS: Consider using a reverse proxy like Nginx with Let's Encrypt to enable HTTPS for your site.

2. Backup and Monitoring: Set up regular backups and monitoring to ensure your site’s availability and security.

3. Scalability: As your site grows, consider scaling your infrastructure using AWS services like Elastic Load Balancing and RDS.

## Reference

For additional details, you can refer to this comprehensive guide: How to Build a Web on AWS for Yourself.

This guide should help you get your blog up and running using WordPress on an AWS EC2 instance with Docker. Have fun