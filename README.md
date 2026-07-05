# Task Manager API

A RESTful Task Management API built using Django REST Framework (DRF). The API allows users to register, authenticate using JWT, and perform CRUD operations on tasks with role-based access control.

---

## Features

- User Registration
- JWT Authentication (Login & Refresh Token)
- Create, Read, Update and Delete Tasks
- Role-Based Access Control (RBAC)
  - Admin can access all tasks
  - Users can access only their own tasks
- Task Filtering by Status
- Task Search by Title
- Pagination
- Django Admin Panel

---

## Tech Stack

- Python 3.13
- Django 5.2.15
- Django REST Framework
- Simple JWT
- SQLite
- django-filter
- Postman
- Git & GitHub

---

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/disha216/task-manager-api.git
cd task_manager_api
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

### 3. Activate the virtual environment

Windows:

```bash
venv\Scripts\activate
```

Mac/Linux:

```bash
source venv/bin/activate
```

### 4. Install dependencies

```bash
pip install -r requirements.txt
```

### 5. Apply migrations

```bash
python manage.py migrate
```

### 6. Run the development server

```bash
python manage.py runserver
```

Server will start at:

```
http://127.0.0.1:8000/
```

---

## API Endpoints

### Authentication

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register/` | Register a new user |
| POST | `/api/auth/login/` | Login and receive JWT tokens |
| POST | `/api/auth/refresh/` | Refresh access token |

### Tasks

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/tasks/` | List tasks |
| POST | `/api/tasks/` | Create task |
| GET | `/api/tasks/<id>/` | Retrieve task |
| PUT | `/api/tasks/<id>/` | Update task |
| PATCH | `/api/tasks/<id>/` | Partial update |
| DELETE | `/api/tasks/<id>/` | Delete task |

---

## Authentication

Protected endpoints require a JWT Access Token.

Example:

```
Authorization: Bearer <access_token>
```

---

## Filtering

Filter tasks by status.

Example:

```
GET /api/tasks/?status=true
```

---

## Search

Search tasks by title.

Example:

```
GET /api/tasks/?search=task
```

---

## Pagination

Pagination is enabled.

Example:

```
GET /api/tasks/?page=2
```

---

## Testing

The APIs were tested using Postman.

Verified endpoints include:

- Register
- Login
- Refresh Token
- Create Task
- List Tasks
- Retrieve Task
- Update Task
- Delete Task
- Filtering
- Search
- Pagination

---

## Project Structure

```
task_manager_api/
├── accounts/
├── config/
├── tasks/
├── manage.py
├── requirements.txt
├── README.md
└── .gitignore
```

---

## Future Improvements

- Due dates for tasks
- Task priorities
- File attachments
- Unit tests
- Docker support

---

## Author

Disha Gohil
