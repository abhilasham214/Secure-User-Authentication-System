# Secure User Authentication and Role-Based Access Control (RBAC) System

Developed as part of an engineering internship at Prodigy InfoTech (`Prodigy_FS_1`), this application is an enterprise-grade User Authentication, Session Management, and Role-Based Access Control system built using Node.js, Express, MongoDB, Mongoose, and EJS.

## System Architecture

```text
+-------------------------------------------------------------------+
|                           Client Request                          |
+-------------------------------------------------------------------+
                                  |
                                  v
+-------------------------------------------------------------------+
|                     Express Router Middleware                     |
|                        (routes/auth.js)                           |
+-------------------------------------------------------------------+
                                  |
                 +----------------+----------------+
                 |                                 |
                 v                                 v
+---------------------------------+ +-------------------------------+
|    Bcrypt Password Hashing      | |    MongoDB Session Store      |
|    (10 Salt Rounds Hashing)     | |  (connect-mongo Persistence)  |
+---------------------------------+ +-------------------------------+
                                  |
                                  v
+-------------------------------------------------------------------+
|               Role Verification Middleware (RBAC)                 |
|             Checks User Role ('user' vs 'admin')                  |
+-------------------------------------------------------------------+
                 |                                 |
        (Role == 'user')                    (Role == 'admin')
                 v                                 v
+---------------------------------+ +-------------------------------+
|     Protected User Dashboard    | |     Protected Admin Panel     |
|          (/dashboard)           | |            (/admin)           |
+---------------------------------+ +-------------------------------+
```

## Key Features

- Password Hashing Security: Password verification using Bcrypt with 10 salt rounds to prevent credential exposure.
- Role-Based Access Control (RBAC): Middleware layer validating access privileges for standard `user` and elevated `admin` roles.
- Persistent Session Management: Integration of `express-session` with `connect-mongo` ensuring session state survives server restarts.
- Protected Routing: Guarded endpoints redirecting unauthenticated or unauthorized requests.
- Server-Side Rendering: Clean EJS templates for authentication portals and control dashboards.

## Repository Structure

```text
Secure-User-Authentication-System/
├── routes/
│   ├── auth.js            # Authentication routes (register, login, logout)
│   └── dashboard.js       # Protected application and admin routes
├── models/
│   └── User.js            # Mongoose User model definition
├── views/
│   ├── login.ejs          # Login form view
│   ├── register.ejs       # Registration form view
│   ├── dashboard.ejs      # User dashboard view
│   └── admin.ejs          # Administrator panel view
├── public/
│   └── styles.css         # Component and layout stylesheets
├── .env                   # Environment variable definitions
├── server.js              # Server initialization and middleware pipeline
├── package.json           # Dependencies manifest
└── README.md              # Project documentation
```

## Tech Stack

- Backend Framework: Node.js, Express.js
- Database & ORM: MongoDB, Mongoose
- Security & Authentication: `bcryptjs`, `express-session`, `connect-mongo`
- Templating Engine: EJS
- Environment Configuration: `dotenv`

## Local Setup and Installation

### Prerequisites

- Node.js (v14.0.0 or higher)
- MongoDB instance running locally or accessible via URI string

### Setup Guide

1. Clone the repository:
   ```bash
   git clone https://github.com/abhilasham214/Secure-User-Authentication-System.git
   cd Secure-User-Authentication-System
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Configure environment variables by creating a `.env` file in the root folder:
   ```env
   PORT=3000
   MONGO_URI=mongodb://localhost:27017/secure_auth_db
   SESSION_SECRET=your_strong_session_secret_key
   ```

4. Start the application server:
   ```bash
   npm start
   # Alternative execution:
   node server.js
   ```

5. Open your browser and navigate to `http://localhost:3000/login`.

## Security Implementations

- Password Salting and Hashing: Uses `bcrypt.hash(password, 10)` prior to user creation in MongoDB.
- Session Isolation: Session IDs stored securely in database stores; destroyed completely on logout (`req.session.destroy()`).
- Authorization Middleware: Validates `req.session.userId` and `req.session.role` before rendering protected views.

## License

This repository is distributed under standard open-source terms.
