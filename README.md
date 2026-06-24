# Task Manager API

A production-ready RESTful API for task management built with **Node.js**, **TypeScript**, **Express.js**, and **MongoDB**.

## Features

- JWT authentication (register, login, protected routes)
- Full CRUD for tasks (create, read, update, delete)
- Filter tasks by status and priority
- Pagination support
- Input validation and error handling
- Security headers with Helmet
- Request logging with Morgan

## Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js |
| Language | TypeScript |
| Framework | Express.js |
| Database | MongoDB + Mongoose |
| Auth | JWT + bcryptjs |
| Security | Helmet, CORS |

## Project Structure

```
src/
├── config/         # Database connection
├── controllers/    # Route handler logic
├── middleware/     # Auth guard, error handler
├── models/         # Mongoose schemas (User, Task)
├── routes/         # Express routers
├── types/          # TypeScript interfaces
└── app.ts          # Entry point
```

## Getting Started

### Prerequisites
- Node.js 18+
- MongoDB (local or Atlas)

### Installation

```bash
# Clone the repo
git clone https://github.com/beniye19/task-manager-api.git
cd task-manager-api

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your MongoDB URI and JWT secret

# Run in development
npm run dev
```

### Environment Variables

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/taskapi
JWT_SECRET=your_super_secret_jwt_key_here
JWT_EXPIRES_IN=7d
NODE_ENV=development
```

## API Endpoints

### Auth

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| POST | `/api/auth/register` | Register a new user | No |
| POST | `/api/auth/login` | Login and get token | No |
| GET | `/api/auth/me` | Get current user | Yes |

### Tasks

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| GET | `/api/tasks` | Get all tasks (paginated) | Yes |
| POST | `/api/tasks` | Create a task | Yes |
| GET | `/api/tasks/:id` | Get a single task | Yes |
| PUT | `/api/tasks/:id` | Update a task | Yes |
| DELETE | `/api/tasks/:id` | Delete a task | Yes |

### Query Parameters (GET /api/tasks)

| Param | Values | Example |
|---|---|---|
| `status` | `todo`, `in-progress`, `done` | `?status=todo` |
| `priority` | `low`, `medium`, `high` | `?priority=high` |
| `page` | number | `?page=2` |
| `limit` | number | `?limit=5` |

## Example Requests

### Register
```json
POST /api/auth/register
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "secret123"
}
```

### Create Task
```json
POST /api/tasks
Authorization: Bearer <token>

{
  "title": "Set up CI/CD pipeline",
  "description": "Configure GitHub Actions for automated deployment",
  "status": "todo",
  "priority": "high"
}
```

### Example Response
```json
{
  "success": true,
  "data": {
    "_id": "64f1a2b3c4d5e6f7a8b9c0d1",
    "title": "Set up CI/CD pipeline",
    "description": "Configure GitHub Actions for automated deployment",
    "status": "todo",
    "priority": "high",
    "user": "64f1a2b3c4d5e6f7a8b9c0d0",
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T10:30:00.000Z"
  }
}
```

## Deployment

The API is deployed on **AWS EC2** and accessible at:
```
http://<your-ec2-ip>:5000
```

## Author

**Benson Mwangi Ngunjiri**  
[github.com/beniye19](https://github.com/beniye19)
