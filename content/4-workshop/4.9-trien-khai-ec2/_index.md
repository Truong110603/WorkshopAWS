---
title: "Deploying Expense Tracker on EC2"
weight: 9
pre: " <b> 4.9 </b> "
---

# Deploying Expense Tracker on EC2

## Objectives

Deploy the Node.js Backend to an Ubuntu EC2 instance and run the application using PM2.

---

## 1. Create an EC2 Instance

Create an EC2 instance using Ubuntu.

The instance is placed in:

```text
expense-tracker-vpc
    ↓
expense-tracker-public-subnet
```

![alt text](/WorkshopAWS/images/4-Workshop/4.9/EC2instances.png)

Security Group:

```text
expense-tracker-sg
```

The following ports are used:

```text
22
3000
```

![alt text](/WorkshopAWS/images/4-Workshop/4.9/EC2instances-2.png)

Port `22` is used for SSH connections.

Port `3000` is used by the Node.js application.

---

## 2. Connect to EC2 Using SSH

Connect to the EC2 instance:

```bash
ssh -i ".\expense-tracker-key.pem" ubuntu@<PUBLIC-IP>
```

![alt text](/WorkshopAWS/images/4-Workshop/4.9/ubuntu.png)

After a successful connection, the terminal is connected to the Ubuntu EC2 instance.

---

## 3. Create the Project Directory

On the EC2 instance, create the project directory:

```bash
mkdir -p ~/expense-tracker

cd ~/expense-tracker
```

The Backend is located at:

```text
~/expense-tracker/backend
```

---

## 4. Install Node.js and npm

Check the installed versions:

```bash
node --version

npm --version
```

Node.js is used to run the Backend application, while npm is used to install and manage the required packages.

---

## 5. Install Backend Packages

Move to the Backend directory:

```bash
cd ~/expense-tracker/backend
```

Install the required packages:

```bash
npm install
```

The packages are installed according to the project's `package.json` file.

---

## 6. Configure Environment Variables

Create the file:

```text
backend/.env
```

Content:

```text
MONGO_URI=<MONGODB_CONNECTION_STRING>

PORT=3000

JWT_SECRET=<SECRET>
```

The `.env` file contains the MongoDB connection string, application port, and JWT secret.

> The actual MongoDB connection string and JWT secret should not be published in the source code or screenshots.

---

## 7. Run the Backend

Start the Backend:

```bash
node server.js
```

Check the application health:

```bash
curl http://localhost:3000/api/health
```

Response:

```json
{
    "status": "ok"
}
```

![alt text](/WorkshopAWS/images/4-Workshop/4.9/pm2status-api-health.png)

The Backend is running successfully on port `3000`.

---

## 8. Install and Configure PM2

Install PM2 globally:

```bash
sudo npm install -g pm2
```

Start the application:

```bash
cd ~/expense-tracker/backend

pm2 start server.js --name expense-tracker
```

Check the application status:

```bash
pm2 status
```

View application logs:

```bash
pm2 logs expense-tracker
```

Restart the application:

```bash
pm2 restart expense-tracker
```

![alt text](/WorkshopAWS/images/4-Workshop/4.9/pm2status.png)

PM2 runs the Node.js application as a background process and allows the application to be restarted when necessary.

---

## 9. Access the Application

Access the application using the EC2 Public IPv4 address:

```text
http://<PUBLIC-IP>:3000/
```

For example:

```text
http://13.251.40.65:3000/
```

The Frontend is served by the Express Backend.

---

## 10. Result

The Expense Tracker Backend is deployed on Amazon EC2 with the following architecture:

```text
Amazon EC2
    ↓
Node.js
    ↓
Express
    ↓
MongoDB Atlas
```

PM2 is used to run the Node.js application as a background process.

The application can be accessed through the EC2 Public IPv4 address on port `3000`.