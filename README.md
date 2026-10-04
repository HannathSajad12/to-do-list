# MERN To-Do List

Assignment No. 2 — Web Technology (23CSB40B), S7 CSE, MBCET

A full-stack To-Do List built with **MongoDB, Express.js, React.js and Node.js**.
Users can add, view, edit, complete/uncomplete and delete tasks. The React frontend talks to an Express REST API, which stores data in MongoDB through Mongoose.

**Name:** _your name_  **Roll No:** _your roll number_

## Project structure

```
RollNo_Name_Assignment2_MERN_ToDoList/
├── backend/
│   ├── config/db.js                    MongoDB connection
│   ├── models/Task.js                  Mongoose schema
│   ├── controllers/taskController.js   CRUD logic
│   ├── routes/taskRoutes.js            4 REST endpoints
│   ├── server.js                       Express entry point
│   ├── .env / .env.example             environment variables
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/TaskForm.jsx, TaskItem.jsx
│   │   ├── api.js                      fetch calls to the backend
│   │   └── App.jsx, main.jsx, index.css
│   ├── index.html, vite.config.js, package.json
├── screenshots/
└── README.md
```

## Prerequisites

- [Node.js](https://nodejs.org) v18 or newer
- MongoDB: either **MongoDB Community Server** running locally, or a free **MongoDB Atlas** cluster

## How to run

Use **two terminals**: one for the backend, one for the frontend.

### 1. Backend (port 5000)

```bash
cd backend
npm install
```

The `.env` file holds the MongoDB connection string (copy `.env.example` to `.env` if it is missing):

```
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/todo_app
```

- **Local MongoDB:** keep the URI above and make sure the MongoDB service (`mongod`) is running.
- **MongoDB Atlas:** replace `MONGO_URI` with your Atlas string, e.g.
  `mongodb+srv://<user>:<password>@<cluster>.mongodb.net/todo_app?retryWrites=true&w=majority`

Start the server:

```bash
npm start
```

You should see `MongoDB connected` and `Server running on http://localhost:5000`.

### 2. Frontend (port 3000)

```bash
cd frontend
npm install
npm start
```

Open **http://localhost:3000**. The Vite dev server proxies `/api` calls to `http://localhost:5000`, so no extra CORS or URL setup is needed.

## REST API

| Method | Endpoint         | Description                          | Body                                                  |
|--------|------------------|--------------------------------------|-------------------------------------------------------|
| GET    | `/api/tasks`     | Fetch all tasks (newest first)       | none                                                  |
| POST   | `/api/tasks`     | Add a new task                       | `{ "title": "Buy milk" }`                             |
| PUT    | `/api/tasks/:id` | Update title and/or completed status | `{ "completed": true }` or `{ "title": "New title" }` |
| DELETE | `/api/tasks/:id` | Delete a task                        | none                                                  |

### Task model

| Field       | Type    | Notes              |
|-------------|---------|--------------------|
| `title`     | String  | required, trimmed  |
| `completed` | Boolean | default `false`    |
| `createdAt` | Date    | default `Date.now` |

Quick API test:

```bash
curl -X POST http://localhost:5000/api/tasks -H "Content-Type: application/json" -d '{"title":"Test task"}'
curl http://localhost:5000/api/tasks
```

## Features

- Add a task (empty titles are rejected)
- Tasks load from the database when the page opens
- Checkbox to mark complete / incomplete
- Edit a task title (click **Edit** or double-click the title; Enter saves, Esc cancels)
- Delete button on every task
- UI updates without a page reload; errors are shown on screen

## Screenshots

In the `screenshots/` folder:

1. `1_add_task.png`: adding a task
2. `2_complete_task.png`: marking a task complete
3. `3_delete_task.png`: deleting a task
