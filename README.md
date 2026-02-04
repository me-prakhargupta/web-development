# Node.js Note API

A minimal intelligent Notes backend API built with Node.js, Express, MongoDB Atlas, featuring validation, partial updates, rate limiting, and advanced search.

This project was developed as part of The Skill Guru Foundation – Node.js Developer Internship Assignment.

# Features

- Create and manage notes with proper validation
- Return list of notes, sorted by most recently updated first
- Partial updates are allowed
- Advanced search across note(title & content)
- Rate limiting note creation

# Tech Stack
- Node.js
- Express 
- TypeScript
- Dotenv
- MongoDB & Mongoose
- MongoDB Atlas
- Express rate limit

# API endpoints

### Create a Note
**POST** `/notes`

{
    "title": "Meeting Notes",
    "content": "Discussed hiring plan and deadlines"
}
    
**Rules**

- Title is required
- Content is required
- Trim extra spaces
- Reject empty strings ("  ")
- Rate limited to 5 requests per minute

### Get All Notes
**GET** `/notes`

**Rules** 
- Returns a list of notes
- Sorted by most recently updated first

### Update a Note
**PUT** `/note/:id`
        
**Rules** 
- Partial updates allowed
- Trims updated fields
- If no actual change is detected, returns a meaningful response
- Automatically updates updatedAt
    
### Search a Note
**GET** `/notes/search?q=`

**Rules** 
- Searches in both title and content
- Case-insensitive
- Ignores extra spaces
- Supports:
-- Prefix matching (meet → meeting)
-- Returns error if query is empty

#Rate Limiting
- Applied only to note creation
- Maximum 5 notes per minute per client
- Prevents abuse while keeping other endpoints unrestricted

#Search Implementation (Important)
- This project uses MongoDB Atlas Search with a compound query
- autocomplete -> to handle prefix search
- e.g: "Meet" -> "Meeting"

- Note: Atlas Search requires an active search index.
- For local MongoDB environments, a regex-based fallback can be used instead.

#Design Decision
- Centralized error handling using a custom AppError
- Standardized success responses using AppResponse
- Search is designed to demonstrate basic intelligence, not just CRUD

#Optional Enhancements
- Added a `DELETE /notes/:id` endpoint as an optional extension to allow note removal.
- This endpoint was not part of the core assignment requirements and is included to demonstrate completeness and standard RESTful practices.

#Environment variable
**Create a .env file (as)**
``` text
PORT=8000
MONGO_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/notes

#Running the project
    npm install
    npm run dev

#Assignment Context
- This project was developed as part of a technical assignment for the Node.js Developer internship at The Skill Guru Foundation.

#Author
- Prakhar Gupta
- Node.js & Backend Developer
