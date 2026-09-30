---
title: "Building Authentication and JWT"
weight: 4
pre: " <b> 4.4 </b> "
---

# Building Authentication and JWT

## Objectives

Add user registration, login, and authentication functionality to the Expense Tracker.

---

## 1. Install Required Packages

In the Backend directory, install the required packages:

```bash
npm install bcryptjs jsonwebtoken
```

---

## 2. User Model

Create:

```text
backend/models/User.js
```

The User model contains the following information:

```text
name
email
password
createdAt
```

The password is hashed using `bcryptjs` before being stored in MongoDB.

---

## 3. Register API

The Register API uses the following endpoint:

```text
POST http://localhost:3000/api/auth/register
```

Request:

```json
{
    "name": "Test User",
    "email": "test@gmail.com",
    "password": "123456"
}
```

![alt text](../../images/4-Workshop/4.5/Post_API.png)

The Backend performs the following operations:

1. Validate the input data.
2. Check whether the email already exists.
3. Hash the password using bcrypt.
4. Create a new User document.
5. Store the user in MongoDB Atlas.
6. Return the registration result.

---

## 4. Login API

The Login API uses the following endpoint:

```text
POST http://localhost:3000/api/auth/login
```

Request:

```json
{
    "email": "test@gmail.com",
    "password": "123456"
}
```

After successful authentication, the Backend generates a JWT:

```javascript
const token = jwt.sign(
    {
        userId: user._id,
        email: user.email
    },
    process.env.JWT_SECRET,
    {
        expiresIn: "1d"
    }
);
```

The response contains:

```text
token
user
```

The Frontend stores the token in `localStorage` and uses it when sending requests that require authentication.

---

## 5. Authentication Middleware

Create:

```text
backend/middleware/authMiddleware.js
```

The middleware reads the JWT from the Authorization header:

```text
Authorization: Bearer <TOKEN>
```

After verifying the token, the decoded user information is stored in:

```javascript
req.user = decoded;
```

The Expense APIs use this middleware to verify that the user is authenticated.

---

## 6. User ID

When creating an Expense, the `userId` is obtained from the authenticated JWT:

```javascript
userId: req.user.userId
```

The `userId` is not taken directly from the data submitted by the Frontend.

The data relationship is:

```text
User
 │
 └── userId
       │
       ├── Expense
       ├── Expense
       └── Expense
```

This ensures that each transaction is associated with the corresponding user account.

---

## 7. Authentication Workflow

The complete authentication flow is:

```text
Register
    ↓
Login
    ↓
JWT Token
    ↓
Authentication Middleware
    ↓
Expense API
```

---

## 8. Result

The Authentication functionality is completed with:

- User registration.
- User login.
- Password hashing using bcrypt.
- JWT token generation.
- JWT authentication middleware.
- User-specific transaction management.

Each transaction is associated with the corresponding user account through `userId`.