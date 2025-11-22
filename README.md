<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>
# Task Manager API

A simple RESTful API for managing tasks built with Laravel. This project provides complete CRUD operations for task management without any frontend interface.

## Features

- ✅ Create new tasks
- ✅ View all tasks
- ✅ View single task
- ✅ Update existing tasks
- ✅ Delete tasks
- ✅ JSON responses
- ✅ Input validation

## Technology Stack

- **Framework**: Laravel 10/11
- **Database**: MySQL/SQLite
- **API Testing**: Postman
- **Architecture**: RESTful API

## Database Schema

### Tasks Table

| Field | Type | Required | Default |
|-------|------|----------|---------|
| id | integer | auto | - |
| title | string | yes | - |
| description | text | no | null |
| is_completed | boolean | no | false |
| created_at | timestamp | auto | - |
| updated_at | timestamp | auto | - |

## Installation

### Prerequisites

- PHP >= 8.1
- Composer
- MySQL or SQLite

### Setup Steps

1. **Clone the repository**
```bash
git clone <repository-url>
cd task-manager-api
```

2. **Install dependencies**
```bash
composer install
```

3. **Configure environment**
```bash
cp .env.example .env
php artisan key:generate
```

4. **Configure database in `.env`**
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=task_manager
DB_USERNAME=root
DB_PASSWORD=
```

5. **Run migrations**
```bash
php artisan migrate
```

6. **Start the server**
```bash
php artisan serve
```

The API will be available at `http://127.0.0.1:8000`

## API Endpoints

### Base URL
```
http://127.0.0.1:8000/api
```

### Endpoints Overview

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /tasks | Get all tasks |
| POST | /tasks | Create a new task |
| GET | /tasks/{id} | Get a specific task |
| PUT/PATCH | /tasks/{id} | Update a task |
| DELETE | /tasks/{id} | Delete a task |

## API Documentation

### 1. Get All Tasks

**Request:**
```http
GET /api/tasks
```

**Response:**
```json
[
  {
    "id": 1,
    "title": "Buy groceries",
    "description": "Milk, Eggs, Bread",
    "is_completed": false,
    "created_at": "2024-01-01T10:00:00.000000Z",
    "updated_at": "2024-01-01T10:00:00.000000Z"
  }
]
```

### 2. Create a New Task

**Request:**
```http
POST /api/tasks
Content-Type: application/json

{
  "title": "Buy groceries",
  "description": "Milk, Eggs, Bread",
  "is_completed": false
}
```

**Validation Rules:**
- `title`: required, string, max 255 characters
- `description`: optional, string
- `is_completed`: optional, boolean

**Response (201 Created):**
```json
{
  "id": 1,
  "title": "Buy groceries",
  "description": "Milk, Eggs, Bread",
  "is_completed": false,
  "created_at": "2024-01-01T10:00:00.000000Z",
  "updated_at": "2024-01-01T10:00:00.000000Z"
}
```

### 3. Get a Specific Task

**Request:**
```http
GET /api/tasks/1
```

**Response (200 OK):**
```json
{
  "id": 1,
  "title": "Buy groceries",
  "description": "Milk, Eggs, Bread",
  "is_completed": false,
  "created_at": "2024-01-01T10:00:00.000000Z",
  "updated_at": "2024-01-01T10:00:00.000000Z"
}
```

**Response (404 Not Found):**
```json
{
  "message": "Task not found"
}
```

### 4. Update a Task

**Request:**
```http
PUT /api/tasks/1
Content-Type: application/json

{
  "title": "Buy groceries",
  "description": "Milk, Eggs, Bread, Cheese",
  "is_completed": true
}
```

**Note:** You can update one or more fields. All fields are optional in the update request.

**Response (200 OK):**
```json
{
  "id": 1,
  "title": "Buy groceries",
  "description": "Milk, Eggs, Bread, Cheese",
  "is_completed": true,
  "created_at": "2024-01-01T10:00:00.000000Z",
  "updated_at": "2024-01-01T10:30:00.000000Z"
}
```

### 5. Delete a Task

**Request:**
```http
DELETE /api/tasks/1
```

**Response (200 OK):**
```json
{
  "message": "Task deleted successfully"
}
```

**Response (404 Not Found):**
```json
{
  "message": "Task not found"
}
```

## Testing with Postman

1. **Import the API endpoints** into Postman
2. **Set the base URL**: `http://127.0.0.1:8000/api`
3. **Test each endpoint** following the documentation above

### Example Postman Collection Structure

```
Task Manager API
├── Get All Tasks (GET)
├── Create Task (POST)
├── Get Single Task (GET)
├── Update Task (PUT)
└── Delete Task (DELETE)
```

## Project Structure

```
app/
├── Http/
│   └── Controllers/
│       └── TaskController.php    # Main API controller
├── Models/
│   └── Task.php                  # Task model
database/
├── migrations/
│   └── xxxx_create_tasks_table.php
routes/
├── api.php                       # API routes
```

## Error Handling

The API returns appropriate HTTP status codes:

- `200 OK`: Successful GET, PUT, DELETE
- `201 Created`: Successful POST
- `404 Not Found`: Resource not found
- `422 Unprocessable Entity`: Validation errors

### Validation Error Example

**Request:**
```json
{
  "description": "No title provided"
}
```

**Response (422):**
```json
{
  "message": "The title field is required.",
  "errors": {
    "title": [
      "The title field is required."
    ]
  }
}
```
