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
4. Choose the **Standard Create** option and select **MySQL** as the database engine.
   
<img width="490" alt="Screenshot 2025-01-26 134244" src="https://github.com/user-attachments/assets/f3c4f8ca-53f0-4902-900e-be0e39d05856" />
   
5. Configure the following settings:
   - **DB Instance Identifier**: e.g., `wordpress-db`
   - **Master Username and Password**: Set strong credentials.
   - **Instance Type**: Choose an appropriate size (e.g., `db.t2.micro` for testing).
6. Ensure **Public Access** is enabled (only for testing; disable for production).
7. Add a **VPC security group** to control database access.
9. Click **Create Database** to complete the setup.

<img width="476" alt="Screenshot 2025-01-26 135220" src="https://github.com/user-attachments/assets/6893e4cf-3e96-4abd-8955-bd6476624d32" />

### Step 2: Set Up Elastic Beanstalk
1. Navigate to **AWS Elastic Beanstalk** in the AWS Console.
2. Click **Create Application**.
3. Provide the following details:
   - **Application Name**: e.g., `wordpress-app`.
   - **Platform**: Select **PHP**.

<img width="626" alt="Screenshot 2025-01-26 135422" src="https://github.com/user-attachments/assets/aa5b24ae-a3af-4239-bc77-5d8b27ede637" />

4. In service role click create and use new service role and select aws-elasticbeanstalk-service-role from it
5. choose your ec2 keypair and your ec2 instance profile to ec2accessdemoapp

   <img width="530" alt="Screenshot 2025-01-26 140153" src="https://github.com/user-attachments/assets/bbba591f-0165-4c79-9f45-44bca9e69157" />

6. In VPC choose default vpc and then select your instance subnet and database subnets

click next
7. select the default security group from the options and click next

<img width="470" alt="Screenshot 2025-01-26 140321" src="https://github.com/user-attachments/assets/4352a873-9005-4e84-b8c4-be7f25884317" />

8. in health reporting choose basic and untick the manged updates options

<img width="634" alt="Screenshot 2025-01-26 140419" src="https://github.com/user-attachments/assets/aa18d1c6-4cd9-40d3-927b-5885072e8add" />


9. Now connect your database by adding environment properties

1. RDS_HOSTNAME

The hostname of the DB instance.

where to find →On the Connectivity & security tab on the Amazon RDS console: Endpoint.

2. RDS_PORT

The port where the DB instance accepts connections. The default value varies among DB engines.

where to find →On the Connectivity & security tab on the Amazon RDS console: Port.

3. RDS_DB_NAME

The database name, ebdb.

where to find →On the Configuration tab on the Amazon RDS console: DB Name.

4.RDS_USERNAME

The username that you configured for your database.

where to find →On the Configuration tab on the Amazon RDS console: Master username.

RDS_PASSWORD

The password that you configured for your database.

Not available for reference in the Amazon RDS console.

<img width="545" alt="Screenshot 2025-01-26 140724" src="https://github.com/user-attachments/assets/d721d6cb-76a1-49a9-aa2c-ab3631706190" />

review your configuration and click on sumbit

It takes around 5 min to create your application

click on url provided by elastic beanstalk you will find a page like this

<img width="519" alt="Screenshot 2025-01-26 140844" src="https://github.com/user-attachments/assets/bad67d46-511d-4f10-b42e-4c5a45787170" />

## Download Wordpress 

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

