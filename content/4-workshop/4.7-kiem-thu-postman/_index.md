---
title: "Testing the Local Application with Postman"
weight: 7
pre: " <b> 4.7 </b> "
---

# Testing the Local Application with Postman

## Objectives

Test the Expense Tracker APIs locally using Postman before deploying the application to AWS.

---

## 1. Health Check

Start the Backend:

```bash
node server.js
```

Request:

```text
GET http://localhost:3000/api/health
```

Response:

```json
{
    "status": "ok"
}
```

---

## 2. Register

Request:

```text
POST http://localhost:3000/api/auth/register
```

Body:

```json
{
    "name": "Test User",
    "email": "test@example.com",
    "password": "123456"
}
```

The request creates a new user account in MongoDB Atlas.

---

## 3. Login

Request:

```text
POST http://localhost:3000/api/auth/login
```

Body:

```json
{
    "email": "test@example.com",
    "password": "123456"
}
```

Response:

```json
{
    "message": "Đăng nhập thành công",
    "token": "<TOKEN>",
    "user": {
        "id": "<USER_ID>",
        "name": "Test User",
        "email": "test@example.com"
    }
}
```

The returned Token is used to authenticate the Expense APIs.

---

## 4. Create Expense

Request:

```text
POST http://localhost:3000/api/expenses
```

Header:

```text
Authorization: Bearer <TOKEN>
Content-Type: application/json
```

Body:

```json
{
    "title": "Lunch",
    "amount": 50000,
    "type": "expense",
    "category": "Food",
    "date": "2026-09-27"
}
```

The Backend verifies the JWT and associates the transaction with the authenticated user.

---

## 5. Get Expenses

Request:

```text
GET http://localhost:3000/api/expenses
```

Header:

```text
Authorization: Bearer <TOKEN>
```

The API returns the transactions belonging to the authenticated user.

---

## 6. Summary

Request:

```text
GET http://localhost:3000/api/expenses/summary
```

Header:

```text
Authorization: Bearer <TOKEN>
```

The API returns:

- Total income.
- Total expenses.
- Balance.
- Total transactions.

---

## 7. Category Statistics

Request:

```text
GET http://localhost:3000/api/expenses/summary/category
```

Header:

```text
Authorization: Bearer <TOKEN>
```

The API returns expense statistics grouped by category.

---

## 8. Update Expense

Request:

```text
PUT http://localhost:3000/api/expenses/<ID>
```

Header:

```text
Authorization: Bearer <TOKEN>
Content-Type: application/json
```

Body:

```json
{
    "title": "Dinner",
    "amount": 100000,
    "type": "expense",
    "category": "Food",
    "date": "2026-09-27"
}
```

The API updates the specified transaction belonging to the authenticated user.

---

## 9. Delete Expense

Request:

```text
DELETE http://localhost:3000/api/expenses/<ID>
```

Header:

```text
Authorization: Bearer <TOKEN>
```

The API deletes the specified transaction belonging to the authenticated user.

---

## 10. Test Authentication

Call the Expense API without a Token:

![alt text](/WorkshopAWS/images/4-Workshop/4.7/callapiWithoutJWT.png)

```text
GET http://localhost:3000/api/expenses
```

Response:

```text
401 Unauthorized
```

Then add the JWT:

```text
Authorization: Bearer <TOKEN>
```

![alt text](/WorkshopAWS/images/4-Workshop/4.7/callapiWithJWT.png)

The API can then be accessed after successful authentication.

---

## 11. Result

The main APIs are tested locally using Postman before deployment:

```text
Health Check

Register

Login

Create Expense

Get Expenses

Update Expense

Delete Expense

Summary

Category Statistics

Authentication
```

The local application is ready for the next step: deploying the Backend to Amazon EC2.