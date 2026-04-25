# 🏦 Banking Backend System

<div align="center">

![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express.js](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=JSON%20web%20tokens&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

**A production-inspired RESTful banking backend — built to learn real-world backend concepts.**

[Features](#-features) · [Tech Stack](#-tech-stack) · [Getting Started](#-getting-started) · [API Reference](#-api-reference) · [Project Structure](#-project-structure) · [Contributing](#-contributing)

</div>

---

## 📌 Overview

This project simulates the core backend infrastructure of a real bank (think SBI or HDFC). It's built with **Node.js**, **Express**, and **MongoDB**, and covers everything from user authentication to money transfers and transaction ledgers — without any frontend.

> **Goal:** Learn real-world backend development by building something that actually matters.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔐 **Authentication** | Register, login, and logout with JWT-based sessions |
| 🏧 **Account Management** | Create and manage bank accounts per user |
| 💸 **Money Transfers** | Send money between accounts securely |
| 📒 **Transaction Ledger** | Every transaction is recorded and queryable |
| 🔒 **Password Hashing** | Passwords scrambled with `bcryptjs` — never stored in plain text |
| 🍪 **Cookie-based Auth** | Secure HTTP-only cookies for session tokens |
| 📧 **Email Notifications** | Send transactional emails via `nodemailer` |
| 🛡️ **Protected Routes** | Middleware guards for authenticated endpoints |

---

## 🛠 Tech Stack

| Tool | Purpose |
|---|---|
| **Node.js** | JavaScript runtime — runs our server |
| **Express.js** | Web framework — handles routes and HTTP |
| **MongoDB Atlas** | Cloud NoSQL database — stores all data |
| **Mongoose** | ODM — maps JavaScript objects to MongoDB |
| **bcryptjs** | Hashes passwords securely before storing |
| **jsonwebtoken** | Issues and verifies login tokens |
| **cookie-parser** | Reads cookies from incoming requests |
| **nodemailer** | Sends emails (OTP, receipts, alerts) |
| **dotenv** | Loads secrets from `.env` file |
| **nodemon** | Auto-restarts server on file changes (dev) |

---

## 🚀 Getting Started

### Prerequisites

Make sure you have these installed on your machine:

- [Node.js](https://nodejs.org/) (v18 or above recommended)
- [npm](https://www.npmjs.com/)
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) account (free tier works)
- [Postman](https://www.postman.com/) (for testing APIs)

Verify your setup:

```bash
node --version
npm --version
```

---

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/banking-backend.git
cd banking-backend
```

---

### 2. Install Dependencies

```bash
npm install
```

---

### 3. Set Up Environment Variables

Create a `.env` file in the root directory:

```bash
touch .env
```

Add the following variables:

```env
# Server
PORT=5000
NODE_ENV=development

# MongoDB
MONGO_URI=your_mongodb_atlas_connection_string

# JWT
JWT_SECRET=your_super_secret_key
JWT_EXPIRES_IN=7d

# Email (Nodemailer)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_app_password
```

> ⚠️ **Never commit your `.env` file.** It's already included in `.gitignore`.

---

### 4. Run the Server

```bash
# Development mode (with auto-restart)
npm run dev

# Production mode
npm start
```

You should see:

```
✅ Server running on http://localhost:5000
✅ MongoDB connected successfully
```

---

## 📁 Project Structure

```
banking-backend/
│
├── src/
│   ├── config/          ← Database connection (MongoDB setup)
│   ├── controllers/     ← Business logic per route
│   ├── middleware/      ← Auth guards, error handlers
│   ├── models/          ← Mongoose schemas (User, Account, Transaction)
│   ├── routes/          ← API route definitions
│   └── utils/           ← Helpers (email sender, token generator, etc.)
│
├── .env                 ← Secret keys (excluded from Git)
├── .gitignore           ← Git exclusions
├── index.js             ← App entry point
└── package.json         ← Project metadata & dependencies
```

---

## 📡 API Reference

Base URL: `http://localhost:5000/api/v1`

### 🔐 Auth Routes — `/auth`

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| `POST` | `/auth/register` | Register a new user | ❌ |
| `POST` | `/auth/login` | Login and receive token | ❌ |
| `POST` | `/auth/logout` | Logout and clear cookie | ✅ |

#### Register — `POST /auth/register`

```json
{
  "name": "Rohan Sharma",
  "email": "rohan@example.com",
  "password": "securePassword123"
}
```

#### Login — `POST /auth/login`

```json
{
  "email": "rohan@example.com",
  "password": "securePassword123"
}
```

---

### 🏧 Account Routes — `/accounts`

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| `POST` | `/accounts/create` | Create a new bank account | ✅ |
| `GET` | `/accounts/me` | Get your account details | ✅ |
| `GET` | `/accounts/balance` | Check current balance | ✅ |

---

### 💸 Transaction Routes — `/transactions`

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| `POST` | `/transactions/transfer` | Transfer money to another account | ✅ |
| `GET` | `/transactions/history` | Get your full transaction history | ✅ |
| `GET` | `/transactions/:id` | Get a single transaction by ID | ✅ |

#### Transfer — `POST /transactions/transfer`

```json
{
  "toAccountNumber": "ACC1234567890",
  "amount": 500,
  "note": "Rent payment"
}
```

---

## 🔒 How Authentication Works

```
User logs in
     │
     ▼
Server verifies credentials
     │
     ▼
JWT token generated & stored in HTTP-only cookie
     │
     ▼
Every protected request reads cookie → verifies token → grants access
```

- Tokens expire after `7 days` (configurable in `.env`)
- Passwords are **never stored raw** — only bcrypt hashes
- Cookies are `httpOnly` to prevent JavaScript access (XSS protection)

---

## 🧪 Testing with Postman

1. Import the base URL: `http://localhost:5000/api/v1`
2. Hit `POST /auth/register` to create a user
3. Hit `POST /auth/login` — your cookie is set automatically
4. All subsequent requests will be authenticated via the cookie

> 💡 Enable **"Automatically follow redirects"** and **"Send cookies"** in Postman settings.

---

## 📜 Scripts

```bash
npm start       # Start server in production
npm run dev     # Start with nodemon (auto-reload on save)
```

---

## 🤝 Contributing

Contributions are welcome! Here's how:

1. **Fork** this repository
2. **Create** a feature branch: `git checkout -b feature/your-feature-name`
3. **Commit** your changes: `git commit -m "feat: add your feature"`
4. **Push** to your branch: `git push origin feature/your-feature-name`
5. **Open** a Pull Request

Please follow [Conventional Commits](https://www.conventionalcommits.org/) for commit messages.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🙌 Acknowledgements

- Inspired by real banking systems like SBI YONO and HDFC NetBanking
- Built as a learning project to master backend fundamentals
- Special thanks to the open-source community for the amazing tools

---

<div align="center">

Made with ❤️ and ☕ | Learning by building, one commit at a time.

⭐ **Star this repo if it helped you learn something!** ⭐

</div>
