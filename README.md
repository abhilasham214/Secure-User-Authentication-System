# 🔒 Secure User Authentication & Role-Based Access Control (RBAC) System

Developed during my software engineering internship at **Prodigy InfoTech** (`Prodigy_FS_1`), this project is a production-grade **User Authentication and Session Management System** built with **Node.js, Express.js, MongoDB, Mongoose, and EJS**.

---

## 📌 Features

- **🔑 Secure Registration & Login**: User registration with **Bcrypt** password hashing (10 salt rounds).
- **🛡️ Role-Based Access Control (RBAC)**: Supports `user` and `admin` roles with custom middleware authorization.
- **💾 Session Persistence with MongoDB**: Uses `express-session` backed by `connect-mongo` so sessions persist reliably across server restarts.
- **🚪 Protected Routes & Dashboards**: Dedicated `/dashboard` for standard users and `/admin` panel for administrative roles.
- **🔒 Secure Logout**: Clears session store records and redirects safely to login.
- **🎨 Responsive View Rendering**: Server-side rendered views using **EJS** with clean CSS styling.

---

## 🛠️ Project Structure

```text
Secure-User-Authentication-System/
├── routes/
│   ├── auth.js            # Express router for register, login, & logout handlers
│   └── dashboard.js       # Express router for protected user & admin dashboard routes
├── models/
│   └── user.js            # Mongoose Schema for User (username, password, role)
├── views/
│   ├── login.ejs          # Login form template
│   ├── register.ejs       # User registration form template
│   ├── dashboard.ejs      # User dashboard view
│   └── admin.ejs          # Protected Admin panel view
├── public/
│   └── styles.css         # CSS styles for forms and dashboard layouts
├── .env                   # Environment configurations (PORT, MONGO_URI, SESSION_SECRET)
├── server.js              # Express app entry point & session middleware initialization
├── package.json           # Dependencies manifest
└── README.md              # Project documentation
```

---

## ⚙️ Tech Stack

- **Backend**: Node.js, Express.js
- **Database & ORM**: MongoDB, Mongoose
- **Session Management**: `express-session`, `connect-mongo`
- **Security**: `bcryptjs`
- **Template Engine**: EJS (Embedded JavaScript)
- **Environment**: `dotenv`

---

## 🚀 Getting Started

### 1. Clone the repository
```bash
git clone https://github.com/abhilasham214/Secure-User-Authentication-System.git
cd Secure-User-Authentication-System
```

### 2. Install dependencies
```bash
npm install
```

### 3. Environment Setup
Create a `.env` file in the root directory:
```env
PORT=3000
MONGO_URI=mongodb://localhost:27017/secure_auth_db
SESSION_SECRET=super_secret_session_key_123!
```

### 4. Start the Application
```bash
npm start
# or: node server.js
```
Open `http://localhost:3000/login` in your web browser.

---

## 🔐 Authorization Logic Flow

```text
[ Client Request ]
       │
       ▼
[ express-session Check ] ──(No Session)──► Redirect to /login
       │
  (Session Active)
       │
       ▼
[ Role Verification Middleware ] ──(Role != admin on /admin)──► 403 Access Denied
       │
  (Role Authorized)
       │
       ▼
[ Render Protected Dashboard / Admin Panel ]
```

---

## 🛡️ License

This project is licensed under the [MIT License](LICENSE).
