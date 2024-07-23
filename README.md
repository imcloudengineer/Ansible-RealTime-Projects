# Ansible-RealTime-Projects

This project involves automating the setup and backup of a MySQL database on an AWS EC2 instance running CentOS using Ansible. The process begins with setting up MySQL and creating a database and table. Next, the AWS CLI is installed and configured on the instance to enable interactions with AWS services, specifically S3. Ansible is then installed for automation purposes. An S3 bucket is created to store the database backups. Finally, an Ansible playbook is written and executed to automate the process of taking MySQL backups and uploading them to the S3 bucket, ensuring the backups are securely stored and easily retrievable.


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

