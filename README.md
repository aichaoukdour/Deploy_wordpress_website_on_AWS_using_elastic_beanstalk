# Deploying a WordPress Website on AWS Using Elastic Beanstalk

## Introduction
This guide explains how to deploy a WordPress website on Amazon Web Services (AWS) using Elastic Beanstalk. It covers integrating services like Amazon RDS for database management and Amazon S3 for image storage. By leveraging AWS, you can build a scalable, reliable, and efficient environment for hosting your WordPress site.

---

## What is AWS Elastic Beanstalk?
AWS Elastic Beanstalk is a fully managed service that simplifies the deployment and management of web applications. It automates tasks like provisioning servers, configuring load balancers, and scaling resources. Elastic Beanstalk supports multiple programming languages such as PHP, Python, Java, and Node.js.

### Key Features:
- **Cost-effective**: You only pay for the AWS resources you use (e.g., EC2 instances, RDS databases).
- **Monitoring**: Integrated with AWS CloudWatch for performance insights.
- **Customization**: Retain full control over the underlying resources.
- **Use Cases**: Ideal for hosting web applications, deploying APIs, and scaling workloads efficiently.

---

## Deployment Steps

### Step 1: Launch an RDS Database
1. Log in to the **AWS Management Console**.
2. Navigate to the **RDS** service from the AWS Services menu.
   
<img width="949" alt="search1" src="https://github.com/user-attachments/assets/75f91dd8-6fb3-47ba-a022-362370c64787" />
3. Click **Create Database**.
5. Choose the **Standard Create** option and select **MySQL** as the database engine.
6. Configure the following settings:
   - **DB Instance Identifier**: e.g., `wordpress-db`
   - **Master Username and Password**: Set strong credentials.
   - **Instance Type**: Choose an appropriate size (e.g., `db.t2.micro` for testing).
7. Ensure **Public Access** is enabled (only for testing; disable for production).
8. Add a **VPC security group** to control database access.
9. Click **Create Database** to complete the setup.

### Step 2: Set Up Elastic Beanstalk
1. Navigate to **AWS Elastic Beanstalk** in the AWS Console.
2. Click **Create Application**.
3. Provide the following details:
   - **Application Name**: e.g., `wordpress-app`.
   - **Platform**: Select **PHP**.
   - **Platform Version**: Choose the latest PHP version.
4. Upload your WordPress application code as a `.zip` file.

### Step 3: Connect WordPress to RDS
1. Update the `wp-config.php` file in your WordPress application with the following:
   ```php
   define('DB_NAME', 'your-database-name');
   define('DB_USER', 'your-database-username');
   define('DB_PASSWORD', 'your-database-password');
   define('DB_HOST', 'your-rds-endpoint');
   define('DB_CHARSET', 'utf8mb4');
   define('DB_COLLATE', '');
   ```
2. Redeploy your WordPress application using Elastic Beanstalk.

### Step 4: Test Your Deployment
1. Access your WordPress site via the **Elastic Beanstalk URL** (e.g., `http://your-app-name.elasticbeanstalk.com`).
2. Complete the WordPress setup wizard by entering your site details, admin credentials, and database connection information.
3. Verify that your WordPress site functions correctly, including plugins, themes, and media uploads.

---

## Additional Configurations

### Amazon S3 Integration
- Configure S3 for storing media files by installing a plugin like **WP Offload Media**.

### Security Best Practices
- Use **IAM Roles** for secure resource access.
- Disable public access to the database for production environments.
- Enable HTTPS using **AWS Certificate Manager (ACM)**.

---

## Conclusion
By following this guide, you can deploy a fully functional WordPress website using AWS Elastic Beanstalk. This approach leverages AWS’s scalable infrastructure and simplifies application deployment, making it an ideal solution for hosting WordPress sites efficiently.

