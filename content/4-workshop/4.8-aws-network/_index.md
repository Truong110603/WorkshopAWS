---
title: "Creating AWS Account, IAM, and Network"
weight: 8
pre: " <b> 4.8 </b> "
---

# Creating AWS Account, IAM, and Network

## Objectives

Prepare the AWS environment for EC2 and related services.

---

## 1. Region

The AWS Region used in this Workshop is:

```text
Singapore    ap-southeast-1
```

All AWS resources in the Workshop are created in this Region.

---

## 2. IAM

IAM is used to manage access permissions to AWS resources.

The AWS services used in the Workshop are:

```text
EC2

VPC

Lambda

EventBridge

CloudWatch

IAM
```

The project does not use CloudTrail.

---

## 3. Create VPC

Create a VPC with the following configuration:

![alt text](/WorkshopAWS/images/4-Workshop/4.8/vpc.png)

```text
Name: expense-tracker-vpc

IPv4 CIDR: 10.0.0.0/16
```

The VPC provides the network environment for the Expense Tracker application.

---

## 4. Public Subnet

Create a Public Subnet:

```text
Name: expense-tracker-public-subnet

CIDR: 10.0.1.0/24
```

The Subnet belongs to:

```text
expense-tracker-vpc
```

![alt text](/WorkshopAWS/images/4-Workshop/4.8/subnet.png)

The EC2 instance is placed in this Public Subnet so that it can receive Internet traffic through the Internet Gateway.

---

## 5. Internet Gateway

Create an Internet Gateway:

```text
expense-tracker-igw
```

Attach the Internet Gateway to:

```text
expense-tracker-vpc
```

![alt text](/WorkshopAWS/images/4-Workshop/4.8/internetgate.png)

The Internet Gateway provides connectivity between the VPC and the Internet.

---

## 6. Route Table

Create a Route Table for the Public Subnet.

Add the following route:

```text
Destination: 0.0.0.0/0

Target: Internet Gateway
```

![alt text](/WorkshopAWS/images/4-Workshop/4.8/route-table.png)

Associate the Route Table with:

```text
expense-tracker-public-subnet
```

This route allows traffic from the Public Subnet to access the Internet through the Internet Gateway.

---

## 7. Security Group

Create a Security Group:

```text
expense-tracker-sg
```

Configure the following Inbound Rules:

| Type | Port | Purpose |
|---|---:|---|
| SSH | 22 | Connect to EC2 |
| Custom TCP | 3000 | Node.js application |

![alt text](/WorkshopAWS/images/4-Workshop/4.8/security-gr.png)

Port `22` is used for SSH connections to the EC2 instance.

Port `3000` is used by the Node.js application.

---

## 8. Network Architecture

```text
Internet

    │

    ▼

Internet Gateway

    │

    ▼

VPC

    │

    ▼

Public Subnet

    │

    ▼

EC2

    │

    ▼

Node.js :3000
```

The EC2 instance runs the Node.js Backend inside the Public Subnet.

---

## 9. Result

The AWS network environment is ready for creating the EC2 instance and deploying the Expense Tracker Backend.

The configured network components include:

```text
VPC
│
├── Public Subnet
│
├── Internet Gateway
│
├── Route Table
│
└── Security Group
```

The next step is to create the EC2 instance and deploy the Backend application.