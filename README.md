# 🏦 Banking Backend System

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express.js](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=JSON%20web%20tokens&logoColor=white)

A RESTful banking backend built with Node.js, Express, and MongoDB. Covers authentication, account management, money transfers, and transaction history.

---

## ✨ Features

- 🔐 User Registration & Login (JWT Auth)
- 🏧 Bank Account Creation
- 💸 Money Transfers Between Accounts
- 📒 Transaction Ledger & History
- 🛡️ Protected Routes via Middleware
- 📧 Email Notifications

---

## 🛠 Tech Stack

| Package | Purpose |
|---|---|
| `express` | Web server & routing |
| `mongoose` | MongoDB object modeling |
| `bcryptjs` | Password hashing |
| `jsonwebtoken` | Auth tokens |
| `cookie-parser` | Cookie handling |
| `nodemailer` | Sending emails |
| `dotenv` | Environment variables |
| `nodemon` | Dev auto-restart |

---

## 🚀 Getting Started

```bash
git clone https://github.com/your-username/banking-backend.git
cd banking-backend
npm install
```

Create a `.env` file:

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key
```

Run the server:

```bash
npm run dev
```

---

## 📁 Project Structure

```
banking-backend/
├── src/
│   ├── config/        ← DB connection
│   ├── controllers/   ← Route logic
│   ├── middleware/    ← Auth guards
│   ├── models/        ← DB schemas
│   ├── routes/        ← API endpoints
│   └── utils/         ← Helper functions
├── .env
├── index.js
└── package.json
```

---

## 📡 API Routes

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/auth/register` | Register a user |
| `POST` | `/auth/login` | Login |
| `POST` | `/accounts/create` | Create bank account |
| `GET` | `/accounts/balance` | Check balance |
| `POST` | `/transactions/transfer` | Transfer money |
| `GET` | `/transactions/history` | Transaction history |

---

## 📄 License

MIT © 2024
