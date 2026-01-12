# API Design – CoopPlayer (MVP)

This document defines the REST API design for the CoopPlayer SaaS platform.

## Principles
- RESTful design
- Stateless requests
- API-first approach
- Backend owns business logic

## Authentication

### POST /auth/register
Creates a new user account.

Request:
{
  "username": "string",
  "email": "string",
  "password": "string"
}

Response:
{
  "id": "uuid",
  "token": "jwt"
}

### POST /auth/login
Authenticates a user.

Request:
{
  "email": "string",
  "password": "string"
}

Response:
{
  "token": "jwt"
}

## Games

### GET /games
Returns supported games.

Response:
[
  {
    "id": "uuid",
    "name": "string",
    "platform": "PC | PS | Xbox",
    "minPlayers": 2,
    "maxPlayers": 4
  }
]

## Sessions

### POST /sessions
Creates a new session.

Request:
{
  "gameId": "uuid",
  "scheduledAt": "ISO-8601",
  "duration": 120
}

Response:
{
  "id": "uuid",
  "status": "PLANNED"
}

### GET /sessions
Lists available sessions.

### GET /sessions/{id}
Returns session details.

### POST /sessions/{id}/join
Joins a session.

### POST /sessions/{id}/leave
Leaves a session.

### POST /sessions/{id}/cancel
Cancels a session (host only).

## Rules
- User cannot join the same session twice
- Session must meet minimum players before activation
- Only host can cancel a session
