# 🎵 Tunora — Music Streaming Platform

> A full-featured music streaming backend with role-based access control, artist uploads, and secure authentication — built with Node.js, Express, and MongoDB.


## 📌 Overview

**Tunora** is a production-ready full backend for a music streaming platform, inspired by the core functionality of modern music apps. It supports two distinct user roles — **Listeners** and **Artists** — each with their own set of permissions and capabilities, secured by JWT-based authentication and role-based access control (RBAC).

The backend is built following the **MVC architecture** with a clean separation of concerns across models, controllers, routes, middlewares, and services — making it scalable, maintainable, and easy to extend.

---

## ✨ Key Features

### 👤 For Listeners
- Register and log in with a unique email and username
- Browse and stream music from the platform
- Explore albums and artist profiles

### 🎤 For Artists
- Register as an artist with elevated privileges
- Upload original songs and create albums
- Manage their own music catalog

### 🔐 Authentication & Security
- **JWT-based authentication** with protected routes
- **Role-Based Access Control (RBAC)** — Listener vs. Artist roles enforced at middleware level
- **Unique constraint validation** — no duplicate emails or usernames across the platform
- Passwords securely hashed before storage

### ☁️ Storage
- Dedicated **Storage Service** for handling audio file uploads (cloud-ready)
- Clean separation between business logic and file management

---

## 🏗️ Project Structure

```
tunora-backend/
├── src/
│   ├── controllers/
│   │   ├── auth.controller.js       # Register, login, token handling
│   │   └── music.controller.js      # Music CRUD operations
│   ├── db/
│   │   └── db.js                    # MongoDB connection setup
│   ├── middlewares/
│   │   └── auth.middleware.js       # JWT verification & role guards
│   ├── models/
│   │   ├── user.model.js            # User schema (Listener & Artist)
│   │   ├── album.model.js           # Album schema
│   │   └── music.model.js           # Music/Track schema
│   ├── routes/
│   │   ├── auth.routes.js           # /api/auth/* endpoints
│   │   └── music.routes.js          # /api/music/* endpoints
│   ├── services/
│   │   └── storage.service.js       # File upload & cloud storage logic
│   └── app.js                       # Express app setup & middleware config
├── server.js                        # Entry point
├── .env                             # Environment variables (not committed)
└── package.json
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js v18+
- MongoDB (local or Atlas)
- A cloud storage account (e.g., Cloudinary / AWS S3) for file uploads

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/tanishqjain011/tunora-backend.git
cd tunora-backend

# 2. Install dependencies
npm install

# 3. Set up environment variables
cp .env.example .env
# Fill in your values (see Environment Variables section)

# 4. Start the development server
npm run dev
```

---

## ⚙️ Environment Variables

Create a `.env` file in the root directory:

```env
PORT=3000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_super_secret_jwt_key
JWT_EXPIRES_IN=7d

# Storage (e.g., Cloudinary)
CLOUD_NAME=your_cloud_name
CLOUD_API_KEY=your_api_key
CLOUD_API_SECRET=your_api_secret
```

---

## 📡 Routes & Endpoints

### Auth Routes — `/api/auth`

| Method | Endpoint            | Description                        | Access  |
|--------|---------------------|------------------------------------|---------|
| POST   | `/register`         | Register a new user (Listener)     | Public  |
| POST   | `/register/artist`  | Register as an Artist              | Public  |
| POST   | `/login`            | Login and receive JWT token        | Public  |
| GET    | `/me`               | Get logged-in user's profile       | Private |

### Music Routes — `/api/music`

| Method | Endpoint         | Description                        | Access         |
|--------|------------------|------------------------------------|----------------|
| GET    | `/`              | Get all available tracks           | Private        |
| GET    | `/:id`           | Get a specific track by ID         | Private        |
| POST   | `/upload`        | Upload a new song                  | Artist Only    |
| DELETE | `/:id`           | Delete a track                     | Artist Only    |
| GET    | `/albums`        | Get all albums                     | Private        |
| POST   | `/albums`        | Create a new album                 | Artist Only    |

---

## 🔐 Authentication Flow

```
Client
  │
  ├── POST /api/auth/register  ──► Creates user, hashes password, stores in DB
  │
  ├── POST /api/auth/login     ──► Validates credentials, returns JWT token
  │
  └── Any Protected Route
        │
        └── Authorization: Bearer <token>
              │
              └── auth.middleware.js
                    ├── Verifies JWT
                    ├── Checks role (Listener / Artist)
                    └── Grants or denies access
```

---

## 🧰 Tech Stack

| Layer         | Technology                  |
|---------------|-----------------------------|
| Runtime       | Node.js                     |
| Framework     | Express.js                  |
| Architecture  | MVC (Model-View-Controller) |
| Database      | MongoDB + Mongoose           |
| Auth          | JWT (jsonwebtoken)          |
| Password Hash | bcrypt                      |
| File Storage  | Cloud Storage Service       |
| Environment   | dotenv                      |

---

## 🛣️ Roadmap

- [ ] Add pagination for music listing
- [ ] Implement playlist creation for Listeners
- [ ] Add song search and filter by genre/artist
- [ ] Build a follow system (Listener follows Artist)
- [ ] Streaming with range requests (partial content)
- [ ] Admin dashboard for content moderation

---

## 👨‍💻 Author

**Tanishq Jain**
- GitHub: [@tanishqjain011](https://github.com/tanishqjain011)
Gmail: tanishqjain3526@gmail.com
---
