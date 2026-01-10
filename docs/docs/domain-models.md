# Domain Models – CoopPlayer

This document defines the core domain models for the CoopPlayer SaaS platform.
These models represent the main business entities and their relationships.

---

## 🧑 User

Represents a player or administrator using the platform.

**Attributes:**
- id
- username
- email
- role (PLAYER / ADMIN)
- createdAt

---

## 🎮 Game

Represents a supported game on the platform.

**Attributes:**
- id
- name
- platform
- maxPlayers

---

## 🕒 Session

Represents a scheduled co-op gaming session.

**Attributes:**
- id
- gameId
- hostUserId
- scheduledAt
- duration
- maxPlayers
- status (PLANNED / ACTIVE / COMPLETED / CANCELED)

---

## 👥 SessionParticipant

Represents a user's participation in a session.

**Attributes:**
- id
- sessionId
- userId
- status (JOINED / CONFIRMED / NO_SHOW / LEFT)
- joinedAt

---

## 🔔 Notification

Represents system notifications sent to users.

**Attributes:**
- id
- userId
- type (REMINDER / UPDATE)
- content
- sentAt
- readAt

---

## 🔗 Relationships

- A User can participate in many Sessions
- A Session can have many Participants
- SessionParticipant links Users and Sessions
- A Session belongs to one Game
- A User can receive many Notifications
