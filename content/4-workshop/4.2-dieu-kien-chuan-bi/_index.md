---
title: "Prerequisites"
weight: 2
pre: " <b> 4.2 </b> "
---

# Prerequisites

### Objectives

Ensure that all required development tools, AWS account access, and source code are available before starting the development and deployment of the Expense Tracker.

---

## 1. Required Tools

The Workshop uses the following tools:

- **Node.js**: Runs the Backend and Frontend of the project.
- **npm**: Manages Node.js packages.
- **Git**: Manages the source code.
- **Visual Studio Code**: Edits the source code.
- **Postman**: Tests REST APIs.
- **MongoDB Atlas**: Provides the database.
- **AWS Management Console**: Manages AWS services.

AWS CLI and Docker are not required for this version of the Workshop.

---

## 2. Check the Local Environment

Open Terminal or PowerShell and check the installed versions:

```bash
node --version
npm --version
git --version
```

### Checkpoint

The commands should return the corresponding installed versions.

---

## 3. Prepare the AWS Account

Sign in to the AWS Management Console.

Select the AWS Region used for the Workshop.

For example:

```text
Asia Pacific (Singapore)

ap-southeast-1
```

### Checkpoint

Confirm that the AWS Console is using the correct Region before creating AWS resources.

---

## 4. Prepare MongoDB Atlas

Create a MongoDB Atlas Cluster and prepare the following:

- Database User.
- Password.
- Connection String.
- Network Access.

The database used by the project is:

```text
expensetracker
```

The main collections are:

```text
users
expenses
statistics
```

![alt text](/WorkshopAWS/images/4-Workshop/4.2/mongodb-database.jpg.png)

---

## 5. Prepare the Source Code

Open the project using Visual Studio Code.

Project structure:

```text
expense-tracker/

├── backend/
├── frontend/
└── lambda-statistics/
```

The Backend contains:

```text
server.js

routes/

models/

middleware/

.env
```

![alt text](/WorkshopAWS/images/4-Workshop/4.2/cau-truc-project.png)

The Frontend contains the Dashboard interface and JavaScript/CSS files.

The Lambda directory contains the source code for statistics processing.

---

## 6. Expected Result

After completing the preparation steps:

- Node.js is installed and working.
- npm is installed and working.
- Git is ready to use.
- Postman is ready for API testing.
- The AWS Account can access the AWS Management Console.
- MongoDB Atlas is configured.
- The Expense Tracker source code is ready.