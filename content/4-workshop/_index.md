---
title: "Workshop"
date: 2026-08-31
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

# Deploying Expense Tracker on AWS

#### Overview

This Workshop guides the development and deployment of an **Expense Tracker – Personal Expense Management** system on AWS.

The application is developed using **Node.js and Express**, uses **MongoDB Atlas** for data storage, and is deployed on **Amazon EC2** using PM2.

AWS Lambda is used to process expense statistics. Amazon EventBridge Scheduler invokes the Lambda function according to the configured schedule, and Amazon CloudWatch is used to monitor Lambda execution logs.

#### Contents

1. [Workshop Overview](4.1-tong-quan-workshop/)
2. [Prerequisites](4.2-dieu-kien-chuan-bi/)
3. [Building the Backend and Connecting to MongoDB](4.3-xay-dung-backend/)
4. [Building Authentication and JWT](4.4-xay-dung-authentication/)
5. [Building Expense CRUD and Statistics](4.5-xay-dung-expense-crud/)
6. [Building the Frontend and Dashboard](4.6-xay-dung-frontend/)
7. [Testing the Local Application with Postman](4.7-kiem-thu-postman/)
8. [Creating AWS Account, IAM, and Network](4.8-aws-network/)
9. [Deploying Expense Tracker on EC2](4.9-trien-khai-ec2/)
10. [Building AWS Lambda Statistics](4.10-aws-lambda/)
11. [Configuring EventBridge and CloudWatch](4.11-eventbridge-cloudwatch/)
12. [System Testing](4.12-kiem-thu-he-thong/)
13. [Cleaning Up Resources](4.13-don-dep-tai-nguyen/)
