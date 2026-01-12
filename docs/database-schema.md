# Database Schema (ERD) – CoopPlayer

This document defines the database schema for the CoopPlayer MVP.
The schema is designed to support the core domain models and system flows.

---

## 🧑 users

Stores platform users (players and admins).

| Column        | Type        | Notes |
|--------------|-------------|------|
| id           | UUID (PK)   | Primary key |
| username     | VARCHAR     | Unique |
| email        | VARCHAR     | Unique |
| role         | ENUM        | PLAYER / ADMIN |
| created_at   | TIMESTAMP   | |

---

## 🎮 games

Represents supported games on the platform.

| Column        | Type        | Notes |
|--------------|-------------|------|
| id           | UUID (PK)   | |
| name         | VARCHAR     | |
| platform     | VARCHAR     | PC / PS / Xbox / Cross |
| min_players  | INT         | |
| max_players  | INT         | |

---

## 🕒 sessions

Scheduled co-op gaming sessions.

| Column        | Type        | Notes |
|--------------|-------------|------|
| id            | UUID (PK)   | |
| game_id       | UUID (FK)   | → games.id |
| host_user_id  | UUID (FK)   | → users.id |
| scheduled_at  | TIMESTAMP   | |
| duration      | INT         | minutes |
| status        | ENUM        | PLANNED / ACTIVE / COMPLETED / CANCELED |

---

## 👥 session_participants

Links users to sessions.

| Column        | Type        | Notes |
|--------------|-------------|------|
| id            | UUID (PK)   | |
| session_id    | UUID (FK)   | → sessions.id |
| user_id       | UUID (FK)   | → users.id |
| joined_at     | TIMESTAMP   | |
| status        | ENUM        | CONFIRMED / LEFT / NO_SHOW |

---

## 🔔 notifications (Optional – MVP+)

Stores user notifications.

| Column        | Type        | Notes |
|--------------|-------------|------|
| id        | UUID (PK) | |
| user_id   | UUID (FK) | → users.id |
| type      | VARCHAR   | REMINDER / UPDATE |
| content   | TEXT      | |
| sent_at   | TIMESTAMP | |
| read_at   | TIMESTAMP | nullable |

---

## 🔗 Relationships Summary

- users 1 ── * sessions (as host)
- users 1 ── * session_participants
- sessions 1 ── * session_participants
- sessions * ── 1 games
- users 1 ── * notifications
