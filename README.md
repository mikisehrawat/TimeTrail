# ⏱️ TimeTrail

**TimeTrail** is a collaborative, real-time study tracker where users can create or join virtual study rooms, start focused timers, and build a trail of their productivity over time.

Built for students, professionals, and accountability groups who want to log and reflect on their study or work patterns in a shared environment.

---

## 🚀 Features

- 👤 **Role-based Users** – Admins and Regular users
- 🏠 **Create / Join Rooms** – Study with others or solo
- ⏱️ **Start/Stop Timer** – Track focused sessions
- 🧠 **Tag Sessions** – Label your time (e.g., DSA, Reading)
- 📊 **Track Progress** – See total time per room or user
- 🔁 **Join Requests** – Admin approval for room access (optional)
- 🌐 **Future** – Live session updates via WebSocket

---

## 🗃️ Database Schema

### 🔹 `user`
| Field     | Type     | Description                |
|-----------|----------|----------------------------|
| `userid`  | INT      | Primary Key                |
| `role`    | VARCHAR  | 'admin' or 'regular'       |
| `pfp`     | .jpg     | Profile picture            |
| `name`    | VARCHAR  | Full name                  |
| `email`   | VARCHAR  | Unique user email          |
| `password`| VARCHAR  | Hashed password            |

---

### 🔹 `room`
| Field       | Type     | Description              |
|-------------|----------|--------------------------|
| `room_id`   | INT      | Primary Key              |
| `room_name` | VARCHAR  | Room title               |
| `admin_id`  | INT      | FK → `user.userid`       |

---

### 🔹 `connection` (Join Table)
| Field     | Type     | Description               |
|-----------|----------|---------------------------|
| `con_id`  | INT      | Primary Key               |
| `user_id` | INT      | FK → `user.userid`        |
| `room_id` | INT      | FK → `room.room_id`       |
| `is_admin`| boolean  | `true`/`false`            |

---

### 🔹 `study_sessions`
| Field        | Type      | Description                  |
|--------------|-----------|------------------------------|
| `session_id` | INT       | Primary Key                  |
| `user_id`    | INT       | FK → `user.userid`           |
| `room_id`    | INT       | FK → `room.room_id`          |
| `start_time` | DATETIME  | Timer start time             |
| `end_time`   | DATETIME  | Timer stop time              |
| `tag`        | VARCHAR   | Optional label (e.g., DSA)   |

---

### 🔹 `join_requests`
| Field         | Type     | Description                    |
|---------------|----------|--------------------------------|
| `id`          | INT      | Primary Key                    |
| `user_id`     | INT      | FK → `user.userid`             |
| `room_id`     | INT      | FK → `room.room_id`            |
| `status`      | VARCHAR  | 'pending', 'accepted', 'rejected' |
| `requested_at`| DATETIME | Timestamp of the request       |

### 🔹 `Tags`
| Field     | Type     | Description               |
|-----------|----------|---------------------------|
| `tag_id`  | INT      | Primary Key               |
| `room_id` | INT      | FK → `room.room_id`       |
| `tag_name`| TEXT     | tag name                  |
| `description`| TEXT  | Tag Description           |

---

## 🛠 Tech Stack

- **Frontend**: React.js + Tailwind CSS
- **Backend**: Spring Boot
- **Database**: MySQL / PostgreSQL
- **Authentication**: JWT
- **Real-Time (Future)**: WebSockets (Socket.IO / STOMP)

---

## 🧠 Design Principles

- ✅ Normalized DB schema (no arrays/objects in SQL)
- 🔐 Secure auth & password storage
- 🔁 Modular roles and room-user connections
- 💡 Extendable for real-time and analytics

---

## 📈 Future Enhancements

- Real-time timer updates in rooms
- Daily/weekly/monthly study charts
- Leaderboards and competition modes
- Calendar heatmaps for productivity

---

