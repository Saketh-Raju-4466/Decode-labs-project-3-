# ☁️ Decode Labs — AWS RDS & EC2 Bastion Host Setup

![AWS](https://img.shields.io/badge/AWS-Cloud-orange)
![EC2](https://img.shields.io/badge/AWS-EC2-blue)
![RDS](https://img.shields.io/badge/AWS-RDS-red)
![MySQL](https://img.shields.io/badge/Database-MySQL-blue)
![Linux](https://img.shields.io/badge/OS-Amazon%20Linux%202023-green)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)

> A hands-on AWS infrastructure project completed as part of my **Decode Labs internship**, focused on Amazon RDS MySQL, Amazon EC2, Linux, security groups, and database connectivity.

---

## 📌 Project Overview

This project focuses on building a basic AWS cloud infrastructure environment using **Amazon RDS and Amazon EC2**.

The primary objective was to:

- Deploy a managed MySQL database using Amazon RDS.
- Create an Amazon EC2 instance to act as a bastion host.
- Access the EC2 server using EC2 Instance Connect.
- Configure an Amazon Linux 2023 environment.
- Install the MySQL-compatible command-line client.
- Identify the RDS endpoint and MySQL port.
- Test connectivity between the EC2 instance and RDS.
- Understand AWS Security Groups and network access.

This project provided practical exposure to cloud infrastructure, Linux administration, database connectivity, networking, and troubleshooting.

---

# 🏗️ Architecture

```text
                         AWS Cloud
                             │
                             ▼
                         VPC Network
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
       ┌───────────────┐             ┌───────────────┐
       │      EC2      │             │      RDS      │
       │ Bastion Host  │────────────►│     MySQL     │
       │   t3.micro    │   Port 3306 │  db.t4g.micro │
       └───────────────┘             └───────────────┘
              ▲
              │
              │ EC2 Instance Connect
              │
          Developer

Intended Flow
Developer
    │
    │ EC2 Instance Connect
    ▼
EC2 Bastion Host
    │
    │ MySQL / TCP 3306
    ▼
Amazon RDS MySQL
☁️ AWS Services Used
Service	Purpose
Amazon EC2	Bastion host / Linux server
Amazon RDS	Managed MySQL database
Amazon VPC	Network environment
Security Groups	Network traffic control
EC2 Instance Connect	Browser-based EC2 access
🖥️ EC2 Configuration

The EC2 instance was configured as a bastion host.

Configuration
Property	Value
Instance Name	decodelabs-bastion
Instance Type	t3.micro
Operating System	Amazon Linux 2023
Region	Europe (Stockholm)
Availability Zone	eu-north-1b
Username	ec2-user
Purpose	Bastion Host

The EC2 instance was successfully accessed through EC2 Instance Connect.

Example terminal:

[ec2-user@ip-172-31-44-205 ~]$
🗄️ Amazon RDS Configuration

An Amazon RDS MySQL database was deployed.

Configuration
Property	Value
Database Identifier	database-1
Engine	MySQL Community
Instance Class	db.t4g.micro
Region	Europe (Stockholm)
Availability Zone	eu-north-1c
Port	3306
Master Username	admin

The RDS endpoint is intentionally not stored in this repository as a configuration file or secret.

🔐 Security Groups

Security Groups were used to control network communication between AWS resources.

The intended architecture allows:

EC2 Bastion Host
       │
       │ TCP 3306
       ▼
RDS MySQL

The RDS security group should allow MySQL traffic on port 3306 from the appropriate EC2 security group.

Security groups are an important part of AWS networking because they control which inbound and outbound traffic is permitted.

🐧 Amazon Linux 2023

The EC2 instance uses Amazon Linux 2023.

After connecting to the instance through EC2 Instance Connect, the Linux environment was prepared for database connectivity.

🐬 MySQL Client Installation

The MySQL-compatible client was installed using:

sudo dnf install mariadb105 -y

After installation, the client was verified using:

mysql --version

The installed client returned:

mysql Ver 15.1 Distrib 10.5.29-MariaDB

This confirmed that the database command-line client was successfully installed and available on the EC2 instance.

🔗 RDS Connectivity Test

The RDS connection was tested from the EC2 bastion host using:

mysql -h <RDS-ENDPOINT> -P 3306 -u admin -p

The connection attempt returned:

ERROR 2002 (HY000): Can't connect to MySQL server
Current Status

The EC2 instance and RDS database are successfully deployed, but the EC2 → RDS connectivity test still requires security-group/network configuration troubleshooting.

This is intentionally documented as in progress rather than being presented as a successful database connection.

📊 Project Progress
Task	Status
AWS environment setup	✅ Completed
RDS MySQL deployment	✅ Completed
RDS configuration	✅ Completed
EC2 Bastion Host deployment	✅ Completed
Amazon Linux 2023 setup	✅ Completed
EC2 Instance Connect	✅ Completed
MySQL/MariaDB client installation	✅ Completed
MySQL client verification	✅ Completed
RDS endpoint identification	✅ Completed
EC2 → RDS connectivity test	⚠️ Troubleshooting
Successful RDS login	⏳ Pending
Database creation/testing	⏳ Pending
🧪 Commands Used
Install MySQL-compatible client
sudo dnf install mariadb105 -y
Verify installation
mysql --version
Test RDS connection
mysql -h <RDS-ENDPOINT> -P 3306 -u admin -p

Replace <RDS-ENDPOINT> with the RDS endpoint when using the command locally.

📸 Project Screenshots
Amazon RDS

The RDS console showing the deployed MySQL database.

RDS Connectivity & Security

RDS networking and security configuration.

EC2 Bastion Host

EC2 instance configured as the bastion host.

EC2 Terminal

Amazon Linux 2023 terminal accessed through EC2 Instance Connect.

MySQL Client

Verification of the installed MySQL/MariaDB client.

Connectivity Test

EC2 → RDS connectivity testing and troubleshooting.

📚 Key Concepts Learned

Through this project, I gained practical exposure to:

Amazon EC2

Understanding how to launch and access a Linux-based cloud server.

Amazon RDS

Understanding how AWS provides managed relational database infrastructure.

Bastion Hosts

Understanding the role of an intermediate EC2 server when accessing cloud resources.

Security Groups

Understanding AWS network access control and inbound/outbound traffic rules.

Linux

Working with Amazon Linux through a terminal environment.

MySQL

Using the MySQL-compatible command-line client to test database connectivity.

AWS Networking

Understanding the relationship between:

VPC
 │
 ├── Subnets
 │
 ├── EC2
 │
 ├── RDS
 │
 └── Security Groups
🔒 Security Considerations

No credentials or private keys should be committed to this repository.

Never commit:

.pem files
.env files
AWS access keys
AWS secret keys
database passwords
private keys
credentials

The RDS password used during the connectivity test is not stored in this repository.

🚀 Future Improvements

The project can be extended with:

 Fix EC2 → RDS security-group connectivity
 Successfully connect to RDS
 Create a sample database
 Create tables
 Insert sample records
 Perform CRUD operations
 Run SQL queries
 Configure secure database connectivity
 Add CloudWatch monitoring
 Explore IAM-based access
 Recreate infrastructure using Terraform
 Connect a web application to RDS
🎯 Learning Outcome

This project helped me understand that cloud infrastructure is not only about deploying services.

It also involves understanding:

Compute
   +
Networking
   +
Security
   +
Databases
   +
Linux
   +
Troubleshooting

The connectivity issue encountered during the project provided an opportunity to understand how AWS Security Groups and network configuration affect communication between cloud resources.

👨‍💻 Author

Saketh Raju

B.Tech Computer Science & Engineering (AI & ML)

🏢 Internship

This project was completed as part of my:

Decode Labs Internship

⭐ Project Status

Infrastructure: 🟢 Mostly Completed

EC2: 🟢 Completed

RDS: 🟢 Completed

Connectivity: 🟡 In Progress

Database Operations: ⚪ Pending

⭐ Learning by building, troubleshooting, and understanding.


---

# 4. `.gitignore`

Create `.gitignore` in the root:

```gitignore
# Environment variables
.env
.env.*
!.env.example

# AWS credentials
.aws/
credentials
config

# SSH private keys
*.pem
*.ppk
*.key

# Database files
*.sql.gz
*.dump
*.bak

# Logs
*.log
logs/

# OS files
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/

# Temporary files
*.tmp
*.temp
⚠️ Important

You can include sample-queries.sql because it contains example SQL.

Do not put your actual RDS password inside it.

5. commands/setup-commands.md

Create:

commands/setup-commands.md

Put:

# AWS Setup Commands

## 1. Install MySQL-compatible client

```bash
sudo dnf install mariadb105 -y
2. Verify installation
mysql --version

Expected output:

mysql Ver 15.1 Distrib 10.5.29-MariaDB
3. Connect to RDS
mysql -h <RDS-ENDPOINT> -P 3306 -u admin -p

The password should be entered interactively.

Never place the database password directly inside this file.

4. Exit MySQL
exit;

---

# 6. `sql/sample-queries.sql`

Even though the database connection isn't completed yet, you can prepare the SQL file for the next stage:

```sql
-- Decode Labs AWS RDS Project
-- Sample SQL Queries

-- Create database
CREATE DATABASE decodelabs_demo;

-- Select database
USE decodelabs_demo;

-- Create sample table
CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    role VARCHAR(100),
    email VARCHAR(150)
);

-- Insert sample records
INSERT INTO employees (name, role, email)
VALUES
('Employee One', 'Cloud Intern', 'employee1@example.com'),
('Employee Two', 'Developer Intern', 'employee2@example.com');

-- Display records
SELECT * FROM employees;

-- Count employees
SELECT COUNT(*) AS total_employees
FROM employees;

These are sample queries only; they haven't been executed against your RDS yet.

7. Architecture image

For the best GitHub presentation, put your architecture diagram here:

architecture/aws-architecture.png

I'd make it visually like:

                         AWS CLOUD
                            │
                      ┌─────▼─────┐
                      │    VPC    │
                      └─────┬─────┘
                            │
              ┌─────────────┴─────────────┐
              │                           │
       ┌──────▼───────┐           ┌───────▼──────┐
       │     EC2      │           │     RDS      │
       │   Bastion    │──────────►│    MySQL     │
       │   t3.micro   │  TCP 3306 │  db.t4g.micro│
       └──────┬───────┘           └───────────────┘
              ▲
              │
       EC2 Instance Connect
              │
          Developer
8. What NOT to upload ❌

This is very important for your GitHub.

Do NOT upload:

❌ RDS password
❌ AWS Access Key
❌ AWS Secret Key
❌ .pem private key
❌ SSH private key
❌ .env containing secrets
❌ Database credentials

Also, because you accidentally exposed your RDS password earlier in the chat, change that password before you consider the project publicly documented.

9. Final GitHub structure

Your finished repository should look like:

📦 decodelabs-aws-rds-ec2-bastion
│
├── 📄 README.md
├── 📄 .gitignore
│
├── 📁 architecture
│   └── 🖼️ aws-architecture.png
│
├── 📁 screenshots
│   ├── 🖼️ 01-rds-database.png
│   ├── 🖼️ 02-rds-connectivity.png
│   ├── 🖼️ 03-ec2-bastion.png
│   ├── 🖼️ 04-ec2-terminal.png
│   ├── 🖼️ 05-mysql-client.png
│   └── 🖼️ 06-connection-test.png
│
├── 📁 commands
│   └── 📄 setup-commands.md
│
└── 📁 sql
    └── 📄 sample-queries.sql
⭐ One important recommendation

Since this is an internship project, don't make the README look like you completed things that are still pending. The fact that you deployed EC2 + RDS, configured Linux, installed the client, attempted connectivity, and encountered/troubleshot a real networking issue is already legitimate hands-on work.

Once we fix the EC2 → RDS connection, we can update the README from 🟡 In Progress to 🟢 Completed and add the successful mysql> screenshot. That will make the project substantially stronger.

i will add screen shots in a folder and ypu add all the steps of execution and also comads everything we did here in that readme and also show that i have completed this full task in the readme file 

Yes bro. 👍 If you are going to put all screenshots in one screenshots folder, we can make the README much cleaner.

One correction, though: I wouldn't falsely claim the EC2 → RDS connection was completed, because our actual test returned ERROR 2002. We can still make the README say the full assigned setup task was completed up to the connectivity-testing stage, while documenting the connectivity result honestly. If you later fix the security-group issue and get the mysql> prompt, we can change that section to fully completed.

Here is the README I recommend.

README.md
# ☁️ Decode Labs — AWS RDS MySQL & EC2 Bastion Host Setup

![AWS](https://img.shields.io/badge/AWS-Cloud-orange)
![Amazon EC2](https://img.shields.io/badge/Amazon-EC2-blue)
![Amazon RDS](https://img.shields.io/badge/Amazon-RDS-red)
![MySQL](https://img.shields.io/badge/Database-MySQL-blue)
![Amazon Linux](https://img.shields.io/badge/OS-Amazon%20Linux%202023-green)
![Internship](https://img.shields.io/badge/Decode%20Labs-Internship-purple)

> A hands-on AWS cloud infrastructure project completed as part of my **Decode Labs internship**, involving Amazon RDS MySQL, Amazon EC2, Amazon Linux 2023, security groups, MySQL client configuration, and database connectivity testing.

---

# 📌 Project Overview

This project demonstrates the practical deployment and configuration of AWS infrastructure using **Amazon RDS and Amazon EC2**.

The objective was to create a managed MySQL database using Amazon RDS and configure an Amazon EC2 instance as a bastion host from which the database could be accessed and tested.

Throughout the implementation, I worked with:

- Amazon RDS
- Amazon EC2
- Amazon Linux 2023
- AWS VPC
- AWS Security Groups
- EC2 Instance Connect
- MySQL/MariaDB command-line client
- Linux terminal commands
- RDS connectivity
- Network troubleshooting

This project was completed as part of my **Decode Labs internship** and provided hands-on experience with real AWS infrastructure rather than only theoretical concepts.

---

# 🎯 Objectives

The main objectives of this task were:

- [x] Create an Amazon RDS MySQL database
- [x] Configure the RDS database
- [x] Create an Amazon EC2 instance
- [x] Configure EC2 as a bastion host
- [x] Access the EC2 instance using EC2 Instance Connect
- [x] Prepare Amazon Linux 2023
- [x] Install the MySQL-compatible command-line client
- [x] Verify the MySQL client installation
- [x] Identify the RDS endpoint and port
- [x] Attempt EC2 → RDS connectivity
- [x] Document the implementation and troubleshooting process

---

# 🏗️ Architecture

```text
                         AWS CLOUD
                             │
                             ▼
                         VPC NETWORK
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
       ┌───────────────┐             ┌───────────────┐
       │      EC2      │             │      RDS      │
       │ Bastion Host  │────────────►│     MySQL     │
       │   t3.micro    │   TCP 3306  │  db.t4g.micro │
       └───────────────┘             └───────────────┘
              ▲
              │
              │ EC2 Instance Connect
              │
          Developer

The intended connection flow is:

Developer
    │
    │ EC2 Instance Connect
    ▼
EC2 Bastion Host
    │
    │ MySQL / TCP 3306
    ▼
Amazon RDS MySQL
☁️ AWS Services Used
AWS Service	Purpose
Amazon EC2	Bastion host
Amazon RDS	Managed MySQL database
Amazon VPC	Network environment
Security Groups	Network access control
EC2 Instance Connect	Browser-based EC2 access
🗄️ Step 1 — Create Amazon RDS MySQL Database

An Amazon RDS database was created using the AWS Management Console.

RDS Configuration
Property	Configuration
Database Identifier	database-1
Database Engine	MySQL Community
DB Instance Class	db.t4g.micro
Region	Europe (Stockholm)
Availability Zone	eu-north-1c
Port	3306
Master Username	admin
Network Type	IPv4

The RDS database reached the Available state successfully.

RDS Endpoint

The RDS endpoint was obtained from:

RDS
→ Databases
→ database-1
→ Connect
→ Code snippets

The database uses the standard MySQL port:

3306

The database password is intentionally not included anywhere in this repository.

🔐 Step 2 — Configure RDS Security Group

The RDS database was associated with an AWS Security Group.

The Security Group controls network traffic reaching the database.

The intended rule is:

Protocol: TCP
Port: 3306
Source: EC2 Bastion Security Group

This allows the EC2 bastion host to communicate with the RDS MySQL database.

🖥️ Step 3 — Create EC2 Bastion Host

An EC2 instance was launched to act as a bastion host.

EC2 Configuration
Property	Value
Instance Name	decodelabs-bastion
Instance Type	t3.micro
Operating System	Amazon Linux 2023
Region	Europe (Stockholm)
Availability Zone	eu-north-1b
Username	ec2-user
Purpose	Bastion Host

The instance successfully reached:

Running

with successful instance status checks.

🔑 Step 4 — Access EC2 Using EC2 Instance Connect

Instead of using a local SSH client, the EC2 instance was accessed through the AWS browser-based connection.

The process was:

AWS Console
    ↓
EC2
    ↓
Instances
    ↓
decodelabs-bastion
    ↓
Connect
    ↓
EC2 Instance Connect
    ↓
Connect

The Linux terminal was successfully opened.

Example prompt:

[ec2-user@ip-172-31-44-205 ~]$

This confirmed successful access to the Amazon Linux server.

🐧 Step 5 — Prepare Amazon Linux

The EC2 instance was running Amazon Linux 2023.

The Linux terminal was used to configure the environment and prepare it for database connectivity.

🐬 Step 6 — Install MySQL Client

Initially, the MySQL command-line client was not available.

The following command was used:

mysql --version

The system initially returned:

-bash: mysql: command not found

This confirmed that the MySQL client needed to be installed.

The MariaDB-compatible MySQL client was then installed using:

sudo dnf install mariadb105 -y

After installation, the client was verified:

mysql --version

The installed version was:

mysql Ver 15.1 Distrib 10.5.29-MariaDB

This confirmed that the MySQL-compatible command-line client was successfully installed.

🔗 Step 7 — Identify RDS Connection Details

The RDS connection information was obtained from the AWS RDS console.

The important connection parameters were:

Host:
database-1.cdui8sgwuck0.eu-north-1.rds.amazonaws.com

Port:
3306

Username:
admin

The password was entered interactively and was never stored in the repository.

🔌 Step 8 — Test EC2 → RDS Connectivity

The database connection was tested from the EC2 bastion host.

The command used was:

mysql -h database-1.cdui8sgwuck0.eu-north-1.rds.amazonaws.com -P 3306 -u admin -p

The command requested the RDS master password interactively.

The connection attempt returned:

ERROR 2002 (HY000): Can't connect to MySQL server
🛠️ Step 9 — Troubleshooting

The connectivity test demonstrated that the MySQL client itself was functioning correctly, but the EC2 instance was not able to establish the network connection to the RDS endpoint.

The troubleshooting process identified AWS networking and Security Group configuration as the next area to investigate.

The intended network path is:

EC2
 │
 │ TCP 3306
 ▼
RDS MySQL

The RDS Security Group must allow traffic from the Security Group associated with the EC2 bastion host.

📊 Implementation Status
Component	Status
AWS Environment	✅ Completed
RDS MySQL Deployment	✅ Completed
RDS Configuration	✅ Completed
RDS Security Group Setup	✅ Configured
EC2 Bastion Host	✅ Completed
Amazon Linux 2023	✅ Completed
EC2 Instance Connect	✅ Completed
MySQL/MariaDB Client	✅ Completed
MySQL Client Verification	✅ Completed
RDS Endpoint Identification	✅ Completed
EC2 → RDS Connectivity Test	✅ Tested
Successful RDS Login	⏳ Pending
Database Operations	⏳ Pending
📸 Screenshots

All implementation screenshots are available in the:

screenshots/

folder.

Recommended screenshots:

screenshots/
│
├── 01-rds-database.png
├── 02-rds-connectivity.png
├── 03-ec2-instance.png
├── 04-ec2-connect.png
├── 05-ec2-terminal.png
├── 06-mysql-installation.png
├── 07-mysql-version.png
└── 08-rds-connection-test.png

These screenshots document the actual implementation process from AWS resource creation through connectivity testing.

🧪 Important Commands Used
Check MySQL client
mysql --version
Install MySQL-compatible client
sudo dnf install mariadb105 -y
Verify installation
mysql --version
Connect to RDS
mysql -h <RDS-ENDPOINT> -P 3306 -u admin -p
Exit MySQL
exit;
🔒 Security

Sensitive credentials were not included in this repository.

The following should never be committed:

❌ RDS passwords
❌ AWS access keys
❌ AWS secret keys
❌ Private SSH keys
❌ .pem files
❌ .env files containing credentials
❌ Database credentials

A .gitignore file is included to help prevent accidental exposure of sensitive files.

🧠 What I Learned

This project gave me practical experience with several important cloud concepts.

Amazon EC2

I learned how to deploy and access a Linux-based cloud server.

Amazon RDS

I learned how to deploy and configure a managed relational database using AWS.

Bastion Hosts

I learned how an EC2 instance can act as an intermediate server for accessing infrastructure.

Security Groups

I gained practical understanding of AWS network access control and inbound/outbound rules.

Linux

I worked with Amazon Linux 2023 through the command line.

MySQL

I learned how to install and use a MySQL-compatible command-line client.

Networking

I learned how AWS resources communicate through:

VPC
 │
 ├── Subnets
 │
 ├── Security Groups
 │
 ├── EC2
 │
 └── RDS
Troubleshooting

One of the most valuable parts of the task was encountering a real connectivity issue and investigating whether the problem was related to the database client, credentials, or AWS networking.

🚀 Future Improvements

The next stage of this project is to complete the EC2 → RDS connection and perform actual database operations.

Planned improvements include:

 Correct EC2/RDS Security Group connectivity
 Successfully connect to RDS
 Create a sample database
 Create tables
 Insert sample records
 Execute SQL queries
 Perform CRUD operations
 Configure secure database connectivity
 Add monitoring using CloudWatch
 Explore IAM-based authentication
 Recreate infrastructure using Terraform
 Connect a web application to the RDS database
💼 Internship Context

This project was completed as part of my Decode Labs Internship.

The project helped me move beyond theoretical cloud concepts and gain practical experience with:

AWS
+
Linux
+
Databases
+
Networking
+
Security
+
Troubleshooting
👨‍💻 Author
Saketh Raju

B.Tech Computer Science & Engineering (AI & ML)

Areas of Interest
Cloud Computing
AWS
Artificial Intelligence & Machine Learning
Software Development
Databases
DevOps
⭐ Final Outcome

The AWS infrastructure required for the project was successfully deployed and configured.

Completed
✅ Amazon RDS MySQL
✅ Amazon EC2
✅ Amazon Linux 2023
✅ EC2 Bastion Host
✅ EC2 Instance Connect
✅ MySQL/MariaDB Client
✅ RDS Configuration
✅ Security Group Configuration
✅ Connectivity Testing

The remaining work is to resolve the EC2 → RDS network connectivity and perform database operations.

📚 Technologies
Amazon Web Services
Amazon EC2
Amazon RDS
Amazon VPC
AWS Security Groups
Amazon Linux 2023
MySQL
MariaDB Client
Linux
Bash

⭐ Built as part of my Decode Labs internship — learning cloud infrastructure by building, testing, and troubleshooting real AWS resources.


