# Node.js Note API

A minimal intelligent Notes backend API built with Node.js, Express, and MongoDB Atlas.  
Features include validation, partial updates, rate limiting, and advanced search.

This project was developed as part of The Skill Guru Foundation — Node.js Developer Internship Assignment.

---

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [API endpoints](#api-endpoints)
  - [Create a Note](#create-a-note)
  - [Get All Notes](#get-all-notes)
  - [Update a Note](#update-a-note)
  - [Search Notes](#search-notes)
  - [Delete a Note (optional)](#delete-a-note-optional)
- [Rate Limiting](#rate-limiting)
- [Search Implementation (Important)](#search-implementation-important)
- [Design Decisions](#design-decisions)
- [Optional Enhancements](#optional-enhancements)
- [Environment Variables](#environment-variables)
- [Running the Project](#running-the-project)
- [Assignment Context](#assignment-context)
- [Author](#author)

---

## Features

- Create and manage notes with proper validation
- Return list of notes, sorted by most recently updated first
- Partial updates are allowed
- Advanced search across note title and content
- Rate limiting for note creation

## Tech Stack

- Node.js
- Express
- TypeScript
- Dotenv
- MongoDB & Mongoose
- MongoDB Atlas
- express-rate-limit

---

## API endpoints

### Create a Note
POST `/notes`

Request body (JSON):
```json
{
  "title": "Meeting Notes",
  "content": "Discussed hiring plan and deadlines"
}
```

Rules:
- `title` is required
- `content` is required
- Trim extra spaces
- Reject empty strings (e.g. `"   "`)
- Rate-limited: maximum 5 requests per minute per client

---

### Get All Notes
GET `/notes`

Rules:
- Returns a list of notes
- Sorted by `updatedAt` — most recently updated first

---

### Update a Note
PUT `/notes/:id`

Rules:
- Partial updates allowed (only the provided fields are changed)
- Trim updated fields
- If no actual change is detected, returns a meaningful response (e.g., 200 with a message or 304-like semantic)
- `updatedAt` is automatically updated

---

### Search Notes
GET `/notes/search?q=<query>`

Rules:
- Searches both `title` and `content`
- Case-insensitive
- Ignores extra spaces in query
- Supports prefix matching (e.g., `meet` → matches `meeting`)
- Returns an error if the query is empty

---

### Delete a Note (optional)
DELETE `/notes/:id`

Notes:
- This endpoint is included as an optional enhancement to allow note removal.
- It was not part of the core assignment but demonstrates standard RESTful completeness.

---

## Rate Limiting

- Applied only to note creation (`POST /notes`)
- Maximum 5 notes per minute per client
- Prevents abuse while keeping other endpoints unrestricted

---

## Search Implementation (Important)

- This project uses MongoDB Atlas Search with a compound query and `autocomplete` to handle prefix matching.
  - Example: `"Meet"` → matches `"Meeting"`
- Atlas Search requires an active search index in your Atlas cluster.
- For local MongoDB environments, a regex-based fallback can be used instead.

---

## Design Decisions

- Centralized error handling using a custom `AppError`
- Standardized success responses using `AppResponse`
- Search is designed to demonstrate basic intelligence beyond simple CRUD

---

## Optional Enhancements

- `DELETE /notes/:id` endpoint to remove notes (included as an optional extension)

---

## Environment Variables

Create a `.env` file in the project root with the following variables:

```env
PORT=8000
MONGO_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/notes
```

Keep your credentials private and do not commit `.env` to source control.

---

## Running the Project

```bash
# Install dependencies
npm install

# Run in development mode
npm run dev

# Build (if applicable) and start
npm run build
npm start
```

---

## Assignment Context

This project was developed as part of a technical assignment for the Node.js Developer internship at The Skill Guru Foundation.

---

## Author

**Prakhar Gupta**  
Node.js & Backend Developer
