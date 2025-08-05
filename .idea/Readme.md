# 📚 Study Time Tracker

A real-time web application where users can join study rooms, track their study time with tags, and collaborate in a productive environment. Built with support for roles like Admin and Regular users, this project helps visualize and log time spent on focused work.

---

## 🚀 Features

- 👤 User authentication (Admin / Regular)
- 🏠 Create and join study rooms
- ⏱️ Start and stop personal study timers
- 🧮 Track total study time by user and room
- 🔁 Handle join requests and admin approvals
- 📊 Real-time updates (future scope)

---

## 🗃️ Database Schema Overview

### 🔸 `user` Table
| Field     | Type     | Description                |
|-----------|----------|----------------------------|
| `userid`  | INT      | Primary Key                |
| `role`    | VARCHAR  | 'admin' or 'regular'       |
| `pfp`     | TEXT     | Profile picture URL/blob   |
| `name`    | VARCHAR  | Full name                  |
| `email`   | VARCHAR  | Unique email               |
| `password`| VARCHAR  | Hashed password            |

### 🔸 `room` Table
| Field       | Type     | Description              |
|-------------|----------|--------------------------|
| `room_id`   | INT      | Primary Key              |
| `room_name` | VARCHAR  | Room name                |
| `admin_id`  | INT      | FK → `user.userid`       |

### 🔸 `connection` Table *(User-Room Many-to-Many)*
| Field     | Type     | Description              |
|-----------|----------|--------------------------|
| `con_id`  | INT      | Primary Key              |
| `user_id` | INT      | FK → `user.userid`       |
| `room_id` | INT      | FK → `room.room_id`      |

### 🔸 `study_sessions` Table
| Field        | Type      | Description                      |
|--------------|-----------|----------------------------------|
| `session_id` | INT       | Primary Key                      |
| `user_id`    | INT       | FK → `user.userid`               |
| `room_id`    | INT       | FK → `room.room_id`              |
| `start_time` | DATETIME  | Timer start                      |
| `end_time`   | DATETIME  | Timer stop                       |
| `tag`        | VARCHAR   | Optional tag (e.g., DSA, Math)   |

### 🔸 `join_requests` Table *(Optional)*
| Field         | Type     | Description                    |
|---------------|----------|--------------------------------|
| `id`          | INT      | Primary Key                    |
| `user_id`     | INT      | FK → `user.userid`             |
| `room_id`     | INT      | FK → `room.room_id`            |
| `status`      | VARCHAR  | 'pending', 'accepted', 'rejected' |
| `requested_at`| DATETIME | Request timestamp              |

---

## 📌 Design Principles

- ❌ No object/array storage inside SQL columns (normalized schema)
- ✅ Proper use of foreign keys and join tables
- 🔐 Passwords stored securely (hashing required)
- 🔁 Support for many-to-many user-room mapping
- 🔧 Extendable for WebSocket-based real-time updates

---

## 🛠️ Tech Stack (suggested)

- **Frontend**: React.js
- **Backend**: Spring Boot / Node.js + Express
- **Database**: MySQL / PostgreSQL
- **Auth**: JWT-based authentication
- **Optional**: Socket.IO or WebSocket for real-time updates

---

## 📈 Future Scope

- Live timers visible to all users in the same room
- Leaderboards or time rankings per room
- Calendar view for past study sessions
- Social login & mobile responsiveness

---

## 📂 Folder Structure (example)

