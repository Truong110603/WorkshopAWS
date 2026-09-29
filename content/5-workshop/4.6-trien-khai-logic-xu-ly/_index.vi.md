---
title: "Triển khai ứng dụng Backend"
weight: 6
pre: " <b> 4.6 </b> "
---


## Triển khai Backend Node.js

Các bước:

1. Upload source code lên EC2.
2. Cài Node.js.
3. npm install.
4. Cấu hình file .env.
5. Chạy ứng dụng bằng PM2.

Backend cung cấp API:

- POST /api/auth/register
- POST /api/auth/login
- GET /api/expenses
- POST /api/expenses
- PUT /api/expenses/:id
- DELETE /api/expenses/:id

