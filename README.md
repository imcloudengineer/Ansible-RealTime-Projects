 GitHub repository:

markdown
Copy code
# Ansible End-to-End Project

This project demonstrates an end-to-end automation of setting up MySQL on an AWS EC2 CentOS instance, creating a database and table, installing AWS CLI, configuring credentials, creating an S3 bucket, and writing an Ansible playbook to take MySQL backups and store them in the S3 bucket.

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Project Setup](#project-setup)
3. [Steps](#steps)
    - [Step 1: Install MySQL](#step-1-install-mysql)
    - [Step 2: Create Database and Table](#step-2-create-database-and-table)
    - [Step 3: Install AWS CLI](#step-3-install-aws-cli)
    - [Step 4: Install Ansible](#step-4-install-ansible)
    - [Step 5: Create S3 Bucket](#step-5-create-s3-bucket)
    - [Step 6: Write and Run Ansible Playbook](#step-6-write-and-run-ansible-playbook)
4. [Ansible Playbook](#ansible-playbook)
5. [Conclusion](#conclusion)

## Prerequisites

- AWS account with IAM user having necessary permissions.
- An AWS EC2 instance running CentOS.
- Basic understanding of Ansible and AWS services.
- SSH access to the EC2 instance.

## Project Setup

1. Launch an EC2 instance with CentOS.
2. SSH into the EC2 instance.

## Steps

### Step 1: Install MySQL

Update the instance and install MySQL server:

```bash
sudo yum update -y
sudo yum install mysql-server -y
sudo systemctl start mysqld
sudo systemctl enable mysqld
Step 2: Create Database and Table
Connect to MySQL and create a database and table:

bash
Copy code
mysql -u root -p
Inside MySQL shell:

sql
Copy code
CREATE DATABASE mydatabase;
USE mydatabase;

CREATE TABLE mytable (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    value VARCHAR(255) NOT NULL
);
Step 3: Install AWS CLI
Install AWS CLI and configure credentials:

bash
Copy code
sudo yum install awscli -y
aws configure
# Enter AWS Access Key ID, Secret Access Key, region, and output format
Step 4: Install Ansible
Install Ansible on the EC2 instance:

bash
Copy code
sudo yum install epel-release -y
sudo yum install ansible -y
Step 5: Create S3 Bucket
Create an S3 bucket using AWS CLI:

bash
Copy code
aws s3 mb s3://your-bucket-name
Step 6: Write and Run Ansible Playbook
Create an Ansible playbook to take MySQL backup and store it in S3.

Directory Structure
Copy code
.
├── ansible.cfg
├── backup_playbook.yml
└── inventory
ansible.cfg
ini
Copy code
[defaults]
inventory = inventory
remote_user = centos
private_key_file = path/to/your/private/key.pem
host_key_checking = False
inventory
ini
Copy code
[mysql]
your_ec2_instance_ip
backup_playbook.yml
yaml
Copy code
---
- hosts: mysql
  tasks:
    - name: Take a MySQL dump
      command: mysqldump -u root -p'your_password' mydatabase > /tmp/mydatabase.sql

    - name: Upload the backup to S3
      aws_s3:
        bucket: your-bucket-name
        object: backups/mydatabase.sql
        src: /tmp/mydatabase.sql
        mode: put
      register: upload_result

    - name: Remove local backup file
      file:
        path: /tmp/mydatabase.sql
        state: absent
Run the playbook:

bash
Copy code
ansible-playbook backup_playbook.yml
Conclusion
This project demonstrates how to use Ansible for automating the setup and backup of a MySQL database on an AWS EC2 instance and storing the backup in an S3 bucket. By following the steps outlined, you can ensure that your database backups are automated and securely stored in AWS S3.

Feel free to contribute, raise issues, or suggest improvements to this project.

License
This project is licensed under the MIT License.

arduino
Copy code

This `README.md` provides clear instructions and explanations for setting up and automating the MySQL backup process using Ansible on an AWS EC2 instance, making it easy for others to understand and follow.





