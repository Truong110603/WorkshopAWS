---
title: "Proposal"
weight: 2
pre: " <b> 2. </b> "
---

# BUILDING AND DEPLOYING A PERSONAL EXPENSE TRACKER APPLICATION ON AWS

## 1. General Information

* **Project Title:** Building and Deploying a Personal Expense Tracker Application on AWS.
* **Author:** Nguyễn Xuân Trường
* **Context:** In modern life, tracking and managing personal income and expenses play an important role in financial planning. However, manual record-keeping makes it difficult for users to summarize financial data and evaluate spending habits. This project develops an Expense Tracker application using Node.js, Express.js, and MongoDB Atlas. The backend is deployed on Amazon EC2, while AWS Lambda, Amazon EventBridge, and Amazon CloudWatch are used to automate statistical tasks and monitor system operations.

## 2. Problem Statement and Objectives

### 2.1. Context and Problem

* **System Purpose:** The system provides a personal finance management platform that allows users to register, log in, and create, view, update, and delete income and expense transactions. The application summarizes financial data to display total income, total expenses, balance, and spending charts by category. In addition, AWS Lambda performs automated expense statistics according to a schedule configured through Amazon EventBridge, while Amazon CloudWatch records execution logs for monitoring and troubleshooting.
* **Target Users:** Individuals, students, and employees who need to track income, manage expenses, and plan their personal finances.
* **Problem Solved:** The system reduces dependence on manual bookkeeping, helps users summarize financial data efficiently, provides a visual interface for monitoring income and expenses, and deploys the application in a cloud environment accessible through the Internet.

### 2.2. Specific Objectives

* **Expected Outputs:**
  * Develop user registration and login functionality using JWT for authentication and bcrypt for password hashing.
  * Build a backend using Node.js and Express.js to provide APIs for managing income and expense transactions.
  * Develop a web interface using HTML, CSS, and JavaScript, with Chart.js for visualizing financial data.
  * Use MongoDB Atlas to store user information and transaction records.
  * Deploy the frontend and backend on an Ubuntu-based Amazon EC2 instance and use PM2 to manage the Node.js process.
  * Develop an AWS Lambda function to process expense statistics and use Amazon EventBridge Scheduler to trigger scheduled tasks.
  * Use Amazon CloudWatch Logs to monitor Lambda execution logs and support troubleshooting.

* **Success Criteria:**
  * Users can log in and perform the supported transaction management operations.
  * Transaction data is stored in MongoDB Atlas and retrieved according to the authenticated user's account.
  * The dashboard displays total income, total expenses, balance, and spending analysis charts.
  * The application is accessible through the EC2 instance's public address when the instance and network configuration are operational.
  * The Lambda function successfully executes the statistical task and records its processing results.
  * Execution logs are available in CloudWatch for monitoring and troubleshooting.

## 3. Architecture and Technical Design

### Architecture Diagram

![Figure 1 – Expense Tracker System Architecture](/WorkshopAWS/images/4-Workshop/4.2/Exspense_Tracker_Architecture_Diagram.drawio.png)
*Figure 1 – Expense Tracker System Architecture*

### 3.1. AWS Services and Technologies

* **Amazon EC2:** Provides a virtual server running Ubuntu to host the Expense Tracker application. The Node.js/Express.js backend and frontend files are served from this instance.
* **Amazon VPC:** Provides a logically isolated network environment for AWS resources. The EC2 instance is placed in an appropriate subnet to communicate over the Internet according to the network configuration.
* **Public Subnet:** Hosts the EC2 instance with a public IP address, allowing users to access the application according to the configured routing and security rules.
* **Internet Gateway:** Enables communication between the VPC and the Internet when used with an appropriate route table and network configuration.
* **Route Table:** Determines network traffic routes, including the default route to the Internet through the Internet Gateway.
* **Security Group:** Controls inbound and outbound traffic for the EC2 instance. Only the ports required for deployment are opened, such as SSH for server administration and the application port for web access.
* **Node.js and Express.js:** Provide the backend runtime and framework for handling HTTP requests, authenticating users, and exposing APIs for expense management.
* **PM2:** Manages the Node.js process on EC2, allowing the application status to be monitored, logs to be inspected, and the application to be restarted when necessary.
* **MongoDB Atlas:** A cloud database used to store account information, transactions, and application statistics. MongoDB Atlas is an external database service, not an AWS service.
* **AWS Lambda:** Executes expense statistics tasks without requiring a dedicated server to remain running for those tasks.
* **Amazon EventBridge Scheduler:** Triggers the Lambda function according to the configured schedule, automating the statistical process.
* **Amazon CloudWatch:** Collects Lambda execution logs, helping monitor processing results and identify errors.
* **HTML, CSS, JavaScript, and Chart.js:** Build the user interface and provide charts for summarizing income and expenses.

### 3.2. Security and Access Management

* **User Authentication:** Use JWT to authenticate API requests and bcrypt to hash passwords before storing them.
* **Transaction Data Protection:** The backend identifies users through validated authentication information and restricts transaction queries to the corresponding account.
* **AWS Permissions Management:** Use IAM roles and appropriate permission policies when granting access to AWS services, following the Least Privilege principle.
* **EC2 Network Security:** Configure Security Groups to allow only the required ports. SSH access should be restricted to the administrator's IP address, and unnecessary public access should be avoided.
* **Connection Information Protection:** Store the MongoDB Atlas connection string and sensitive configuration variables in an appropriate environment configuration. Do not expose passwords or JWT secrets in public source code.
* **System Monitoring:** Use CloudWatch Logs to monitor Lambda operations and troubleshoot errors. Logs should not contain passwords, tokens, or other sensitive user information.

## 4. Potential Risks and Mitigation

* **Risk 1: EC2 Instance Failure or Application Downtime**
  * *Mitigation:* Use PM2 to manage the Node.js process, inspect application status, and review error logs. Configure PM2 to start with the operating system to help restore the application after an EC2 reboot.

* **Risk 2: Failure to Connect to MongoDB Atlas**
  * *Mitigation:* Verify the environment connection string, database credentials, Atlas Network Access configuration, and network connectivity from EC2. Allow only the necessary IP addresses to access the database.

* **Risk 3: Users Accessing or Modifying Another User's Data**
  * *Mitigation:* Validate JWTs in the backend and use the authenticated user's identity in database queries. Do not trust a `userId` supplied by the client without verification.

* **Risk 4: Lambda Execution Failure or Incorrect Statistics**
  * *Mitigation:* Review the statistical logic, MongoDB Atlas connectivity, environment variables, and CloudWatch logs. Test the function with populated datasets, empty datasets, and database connection failures.

* **Risk 5: Repeated Scheduled Executions or Duplicate Statistics**
  * *Mitigation:* Design database writes to handle repeated executions safely, clearly identify each statistical period, and use suitable identifiers to prevent duplicate records.

* **Risk 6: Insecure HTTP Access or Incorrect Port Configuration**
  * *Mitigation:* Configure Security Groups according to the principle of least privilege. For production use, consider enabling HTTPS and restricting direct access to the backend port.

## 5. Implementation Lab Steps

The project is implemented through the following steps:

* **Step 1:** Prepare the development environment and install Node.js, npm, and the required tools.
* **Step 2:** Build the backend using Node.js and Express.js and configure the connection to MongoDB Atlas.
* **Step 3:** Implement user registration, login, JWT authentication, and password hashing with bcrypt.
* **Step 4:** Develop transaction management APIs, including creating, retrieving, updating, deleting, and summarizing income and expense records.
* **Step 5:** Build the frontend using HTML, CSS, and JavaScript, and use Chart.js to visualize financial data.
* **Step 6:** Test the APIs and main application functions locally before deploying to AWS.
* **Step 7:** Create and configure a VPC, public subnet, Internet Gateway, route table, and Security Group for the EC2 instance.
* **Step 8:** Launch an Ubuntu-based EC2 instance, install Node.js and the required dependencies, deploy the application, and use PM2 to manage the backend process.
* **Step 9:** Verify the connection from EC2 to MongoDB Atlas and test login, transaction management, and dashboard functionality in the AWS environment.
* **Step 10:** Develop an AWS Lambda function to process expense statistics and test its execution results.
* **Step 11:** Configure Amazon EventBridge Scheduler to trigger the Lambda function periodically.
* **Step 12:** Use Amazon CloudWatch Logs to inspect execution logs, verify processing results, and troubleshoot errors.
* **Step 13:** Test the entire system, evaluate the deployment results, and clean up unused AWS resources.

## 6. Personal Contributions and Results

* **Expense Tracker Development:** Implement user authentication, transaction management, and a dashboard for summarizing personal income and expenses.
* **AWS Application Deployment:** Deploy the application on Ubuntu-based EC2, configure the network, and use PM2 to manage the backend process.
* **Cloud Database Integration:** Connect the application to MongoDB Atlas to store and retrieve user and transaction data.
* **Automated Statistics:** Develop a Lambda function to process expense data and integrate EventBridge Scheduler to trigger the function according to a schedule.
* **Execution Monitoring:** Use CloudWatch Logs to inspect Lambda activity, record processing results, and help identify errors.
* **AWS Skills Development:** Gain practical experience with EC2, VPC, subnets, Internet Gateway, route tables, Security Groups, IAM, Lambda, EventBridge, and CloudWatch through a practical application project.
