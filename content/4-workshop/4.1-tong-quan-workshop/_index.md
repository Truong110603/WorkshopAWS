---
title: "Workshop Overview"
weight: 1
pre: " <b> 4.1 </b> "
---

# Workshop Overview

## Objectives

This Workshop guides the development of an **Expense Tracker – Personal Expense Management** system that supports user account management, income and expense transactions, data statistics, and deployment on AWS.

The system is developed locally first, then deployed to AWS and extended with serverless processing functions.

---

## 1. Problem Introduction

Expense Tracker is an application that allows users to track their personal income and expenses.

Each user can:

- Register an account.
- Log in.
- Add transactions.
- View transaction lists.
- Edit transactions.
- Delete transactions.
- Track total income.
- Track total expenses.
- Track the current balance.
- View expense charts by category.

Each user's data is identified using `userId`.

---

## 2. System Architecture

```text
                         ┌──────────────────┐
                         │    EventBridge   │
                         │  Daily Scheduler │
                         └────────┬─────────┘
                                  │
                                  ▼
┌──────────┐              ┌───────────────┐
│  Browser │              │ AWS Lambda    │
│   User   │              │ Statistics    │
└────┬─────┘              └───────┬───────┘
     │                            │
     ▼                            ▼
┌──────────┐              ┌────────────────┐
│   EC2    │─────────────►│ MongoDB Atlas  │
│ Node.js  │              │ expensetracker │
│ Express  │◄─────────────│                │
└────┬─────┘              └────────────────┘
     │
     ▼
┌──────────────┐
│   Dashboard  │
│   Chart.js   │
└──────────────┘

EC2 / Lambda → CloudWatch
```

<!-- IMAGE: Insert the Expense Tracker architecture image here if available -->

---

## 3. System Workflow

### Step 1 – User Accesses the System

Users access the application through a web browser.

The website is served by the Node.js application running on Amazon EC2.

### Step 2 – Registration and Login

Users create an account using their email and password.

After a successful login, the Backend generates a JWT Token.

The token is stored on the Frontend and sent with requests that require authentication.

### Step 3 – Transaction Management

When a user creates a transaction, the Frontend sends a REST API request to the Backend.

The Backend:

1. Validates the JWT.
2. Identifies the user.
3. Retrieves the `userId`.
4. Saves the transaction to MongoDB Atlas.

### Step 4 – Dashboard

The Frontend calls the API to retrieve data.

The Backend queries MongoDB Atlas and returns:

- Total income.
- Total expenses.
- Current balance.
- Transaction list.
- Statistics by category.

The Dashboard uses Chart.js to display expense charts.

![alt text](../../images/4-Workshop/4.2/dashboard.jpg)

### Step 5 – AWS Lambda

AWS Lambda is used to perform data statistics processing.

Lambda connects to MongoDB Atlas, processes data for each user, and stores the results in the `statistics` collection.

### Step 6 – EventBridge

Amazon EventBridge Scheduler invokes the Lambda function according to the configured schedule.

This allows the statistics processing to run automatically.

### Step 7 – CloudWatch

Amazon CloudWatch is used to monitor Lambda logs and related system activities.

---

## 4. AWS Services Used

| Service | Purpose |
|---|---|
| Amazon EC2 | Runs the Node.js Backend |
| Amazon VPC | Provides the AWS network |
| Public Subnet | Hosts the EC2 instance in a public network |
| Internet Gateway | Allows the EC2 instance to communicate with the Internet |
| Security Group | Controls traffic to the EC2 instance |
| IAM | Manages AWS access permissions |
| AWS Lambda | Processes expense statistics |
| EventBridge | Schedules Lambda execution |
| CloudWatch | Monitors logs and system activities |

MongoDB Atlas is used as the database outside the AWS environment.

---

## 5. Technologies Used

- Node.js
- Express.js
- MongoDB Atlas
- Mongoose
- JWT
- bcrypt
- REST API
- HTML
- CSS
- JavaScript
- Chart.js
- PM2
- AWS Lambda

---

## 6. Results

After completing the Workshop:

- The application runs on EC2.
- Users can register and log in.
- JWT protects authenticated APIs.
- Each user can only access their own data.
- Full CRUD functionality for expense transactions is available.
- The Dashboard displays expense statistics.
- Lambda performs automated statistics processing.
- EventBridge invokes Lambda according to the configured schedule.
- CloudWatch stores logs for system monitoring.