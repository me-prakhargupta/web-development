# Node.js Note API

A minimal intelligent Notes backend API built with Node.js, Express, MongoDB Atlas, featuring validation, partial updates, rate limiting, and advanced search.

This project was developed as part of The Skill Guru Foundation – Node.js Developer Internship Assignment.

---

## Features

- Create and manage notes with proper validation  
- Return list of notes, sorted by most recently updated first  
- Partial updates are allowed  
- Advanced search across note (title & content)  
- Rate limiting note creation  

---

## Tech Stack

- Node.js  
- Express  
- TypeScript  
- Dotenv  
- MongoDB & Mongoose  
- MongoDB Atlas  
- Express Rate Limit  

---

## API Endpoints

### Create a Note

**POST** `/notes`

```json
{
  "title": "Meeting Notes",
  "content": "Discussed hiring plan and deadlines"
}





####Something
---

```md
**Rules**
- Title is required
- Content is required
- Trim extra spaces
- Reject empty strings ("  ")
- Rate limited to 5 requests per minute
