---
title: "Building the Frontend and Dashboard"
weight: 6
pre: " <b> 4.6 </b> "
---

# Building the Frontend and Dashboard

## Objectives

Build the user interface for the Expense Tracker and connect the Frontend to the Backend APIs.

---

## 1. Frontend Structure

The Frontend has the following structure:

```text
frontend/

├── index.html
├── login.html
├── register.html
├── app.js
├── login.js
├── register.js
└── style.css
```

---

## 2. Register

The Register page contains:

```text
Name

Email

Password
```

![alt text](/WorkshopAWS/images/4-Workshop/4.6/signup.png)

---

## 3. Login

The Login page contains:

```text
Email

Password
```

![Login Screen](/WorkshopAWS/images/4-Workshop/4.6/Login.png)

After a successful login, the JWT Token is stored in Local Storage:

```javascript
localStorage.setItem("token", data.token);
```

User information is also stored in Local Storage:

```javascript
localStorage.setItem(
    "user",
    JSON.stringify(data.user)
);
```

---

## 4. Sending JWT

When calling APIs that require authentication, the Frontend retrieves the Token:

```javascript
const token = localStorage.getItem("token");
```

The Token is sent through the Authorization Header:

```javascript
headers: {
    "Authorization": `Bearer ${token}`
}
```

The Backend uses this Token to authenticate the current user before processing the request.

---

## 5. Dashboard

The Dashboard displays:

- User name.
- Balance.
- Total Income.
- Total Expense.
- Transaction list.
- AWS Lambda Statistics
- Add transaction form.
- Expense chart by Category.

![alt text](/WorkshopAWS/images/4-Workshop/4.6/dashbroadfull.png)

---

## 6. Chart.js

Add Chart.js to the Frontend:

```html
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
```

The chart data is retrieved from:

```text
GET http://localhost:3000/api/expenses/summary/category
```

![alt text](/WorkshopAWS/images/4-Workshop/4.6/Chart.png)

The Frontend uses the retrieved data to create a Doughnut Chart showing the expense distribution by Category.

---

## 7. Adding a Transaction

The transaction form contains:

```text
Title

Amount

Type

Category

Date
```

The Frontend sends the transaction data to:

```text
POST http://localhost:3000/api/expenses
```

The request includes the JWT Token in the Authorization Header.

![alt text](/WorkshopAWS/images/4-Workshop/4.6/add_trans.png)

After the transaction is successfully added, the Dashboard reloads the transaction list and updated statistics.

---
## 8. Automatic Expense Statistics

* Allows users to view the expense statistics directly.

![alt text](/WorkshopAWS/images/4-Workshop/4.6/Lambda_Statistics.png)
---
## 9. Recent Transactions

![alt text](/WorkshopAWS/images/4-Workshop/4.6/recent_trans.png)

The Recent Transactions section allows users to view their latest transactions directly on the Dashboard.

---

## 10. Logout

When the user logs out, the stored authentication information is removed:

```javascript
localStorage.removeItem("token");

localStorage.removeItem("user");
```

![alt text](/WorkshopAWS/images/4-Workshop/4.6/logout.png)

After logout, the user is redirected to the Login page.

---

## 11. Result

The completed Frontend provides the following flow:

```text
Register
   ↓
Login
   ↓
Dashboard
   ├── Balance
   ├── Income
   ├── Expense
   ├── Chart
   └── Transactions
```

The Frontend uses REST APIs to exchange data with the Backend.

The Dashboard displays data retrieved from MongoDB Atlas through the Backend APIs.