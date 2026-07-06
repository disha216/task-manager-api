# 🚀 Task Manager API

A RESTful Task Management API built using Django REST Framework (DRF) that allows users to securely manage their tasks.

The project implements JWT (JSON Web Token) Authentication, Role-Based Access Control (RBAC), CRUD Operations, Filtering, Searching, and Pagination.

---

# 📌 Features

## Authentication

- Register a new user
- Login using JWT Authentication
- Generate Access Token & Refresh Token
- Refresh Access Token without logging in again

## Task Management

- Create Task
- View Task
- Update Task
- Delete Task

## Role-Based Access Control (RBAC)

### Admin User

- Can view every task in the database
- Can manage tasks created by any user

### Normal User

- Can create tasks
- Can view only their own tasks
- Cannot view tasks created by other users

## Additional Features

- Filter tasks by status
- Search tasks by title
- Pagination
- Django Admin Panel

---

# 🛠 Tech Stack

| Technology | Purpose |
|------------|---------|
| Python 3.13 | Programming Language |
| Django 5.2.15 | Web Framework |
| Django REST Framework | REST API Development |
| SQLite | Database |
| Simple JWT | Authentication |
| django-filter | Filtering APIs |
| Postman | API Testing |
| Git | Version Control |
| GitHub | Repository Hosting |


---

# 📂 Project Structure

```
task-manager-api/
│
├── accounts/   
├── config/            
├── tasks/              
├── manage.py              
├── requirements.txt      
├── README.md             
└── .gitignore           
```

---

# ⚙️ Installation & Setup

## Step 1: Clone the Repository

```bash
git clone https://github.com/disha216/task-manager-api.git
```

```bash
cd task-manager-api
```

---

## Step 2: Create a Virtual Environment

```bash
python -m venv venv
```

---

## Step 3: Activate the Virtual Environment

### Windows

```bash
venv\Scripts\activate
```

### macOS / Linux

```bash
source venv/bin/activate
```

---

## Step 4: Install Required Packages


```bash
pip install -r requirements.txt
```

---

## Step 5: Apply Migrations


```bash
python manage.py migrate
```

---

## Step 6: Create an Admin (Superuser)

```bash
python manage.py createsuperuser
```

This account can be used to log in to the Django Admin Panel and has permission to view and manage all tasks.

---

## Step 7: Start the Development Server

Run:

```bash
python manage.py runserver
```

If the server starts successfully, you will see something similar to:

```text
Starting development server at http://127.0.0.1:8000/
```


---

# 🧪 Testing the APIs Using Postman

After running the Django development server, the APIs can be tested using **Postman**.

If you do not have Postman installed, download it from:

https://www.postman.com/downloads/

---

# General Steps

For every API request:

1. Open **Postman**.
2. Click **New** → **HTTP Request**.
3. Select the HTTP Method mentioned for the endpoint (GET, POST, PUT, PATCH or DELETE).
4. Enter the Full URL.
5. If the endpoint requires authentication, go to the **Authorization** tab:
   - Select **Bearer Token**
   - Paste the **Access Token** obtained after login.
6. If a Request Body is provided:
   - Click the **Body** tab.
   - Select **raw**.
   - Choose **JSON** from the dropdown.
   - Paste the JSON body provided for that endpoint.
7. Click **Send**.

---

# 👤 Register User

Creates a new user account.

### Method

POST

### Endpoint

```
/api/auth/register/
```

### Full URL

```
http://127.0.0.1:8000/api/auth/register/
```

### Authorization

Not Required

### Request Body

```json
{
    "username": "john",
    "email": "john@gmail.com",
    "password": "password123",
    "confirm_password": "password123"
}
```

### Expected Status

```
201 Created
```

### Response

```json
{
    "message": "User registered successfully."
}
```

---

# 🔐 Login

Logs in an existing user and returns JWT tokens.

### Method

POST

### Endpoint

```
/api/auth/login/
```

### Full URL

```
http://127.0.0.1:8000/api/auth/login/
```

### Authorization

Not Required

### Request Body

```json
{
    "username": "john",
    "password": "password123"
}
```

### Expected Status

```
200 OK
```

### Response

```json
{
    "refresh": "eyJhbGc...............",
    "access": "eyJhbGc..............."
}
```

### Note

- Copy the **Access Token**.
- It is required to access all protected APIs.
- The **Refresh Token** is only used to generate a new Access Token after the current one expires.

---

# 🔄 Refresh Access Token

Generates a new Access Token using the Refresh Token.

### Method

POST

### Endpoint

```
/api/auth/refresh/
```

### Full URL

```
http://127.0.0.1:8000/api/auth/refresh/
```

### Authorization

Not Required

### Request Body

```json
{
    "refresh": "Paste_Your_Refresh_Token_Here"
}
```

### Expected Status

```
200 OK
```

### Response

```json
{
    "access": "New_Access_Token"
}
```

---

# ➕ Create Task

Creates a new task for the logged-in user.

### Method

POST

### Endpoint

```
/api/tasks/
```

### Full URL

```
http://127.0.0.1:8000/api/tasks/
```

### Authorization

Required

### Request Body

```json
{
    "title": "Complete Django Assessment",
    "description": "Finish the DRF project",
    "status": false
}
```

### Expected Status

```
201 Created
```

### Response

```json
{
    "id": 1,
    "title": "Complete Django Assessment",
    "description": "Finish the DRF project",
    "status": false,
    "created_at": "2026-07-06T10:30:15.123456Z",
    "updated_at": "2026-07-06T10:30:15.123456Z",
    "owner": 2
}
```

---

# 📋 Get All Tasks

Returns all tasks of the logged-in user.

If the logged-in user is an **Admin**, all tasks from every user are returned.

### Method

GET

### Endpoint

```
/api/tasks/
```

### Full URL

```
http://127.0.0.1:8000/api/tasks/
```

### Authorization

Required

### Request Body

Not Required

### Expected Status

```
200 OK
```

### Response

```json
{
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 1,
            "title": "Complete Django Assessment",
            "description": "Finish the DRF project",
            "status": false,
            "created_at": "...",
            "updated_at": "...",
            "owner": 2
        }
    ]
}
```

---

# 🔍 Get Task by ID

Returns a specific task.

Replace `<id>` with the Task ID.

Example:

```
/api/tasks/1/
```

### Method

GET

### Endpoint

```
/api/tasks/<id>/
```

### Full URL

```
http://127.0.0.1:8000/api/tasks/1/
```

### Authorization

Required

### Request Body

Not Required

### Expected Status

```
200 OK
```

### Response

```json
{
    "id": 1,
    "title": "Complete Django Assessment",
    "description": "Finish the DRF project",
    "status": false,
    "created_at": "...",
    "updated_at": "...",
    "owner": 2
}
```

---

# ✏️ Update Task (PUT)

Updates all fields of an existing task.

### Method

PUT

### Endpoint

```
/api/tasks/<id>/
```

### Full URL

```
http://127.0.0.1:8000/api/tasks/1/
```

### Authorization

Required

### Request Body

```json
{
    "title": "Updated Task",
    "description": "Updated Description",
    "status": true
}
```

### Expected Status

```
200 OK
```

### Response

Returns the updated task.

---

# 🩹 Partial Update (PATCH)

Updates only selected fields.

### Method

PATCH

### Endpoint

```
/api/tasks/<id>/
```

### Full URL

```
http://127.0.0.1:8000/api/tasks/1/
```

### Authorization

Required

### Request Body

```json
{
    "status": true
}
```

### Expected Status

```
200 OK
```

### Response

Returns the updated task.

---

# 🗑 Delete Task

Deletes an existing task.

### Method

DELETE

### Endpoint

```
/api/tasks/<id>/
```

### Full URL

```
http://127.0.0.1:8000/api/tasks/1/
```

### Authorization

Required

### Request Body

Not Required

### Expected Status

```
204 No Content
```

### Response

No response body is returned.

---

# 🔎 Filter Tasks

Returns tasks based on their completion status.

### Method

GET

### Full URL

```
http://127.0.0.1:8000/api/tasks/?status=true
```

### Authorization

Required

### Request Body

Not Required

### Expected Status

```
200 OK
```

---

# 🔍 Search Tasks

Searches tasks by title.

### Method

GET

### Full URL

```
http://127.0.0.1:8000/api/tasks/?search=django
```

### Authorization

Required

### Request Body

Not Required

### Expected Status

```
200 OK
```

---

# 📄 Pagination

Returns tasks page by page.

### Method

GET

### Full URL

```
http://127.0.0.1:8000/api/tasks/?page=2
```

### Authorization

Required

### Request Body

Not Required

### Expected Status

```
200 OK
```

### Response

```json
{
    "count": 12,
    "next": "http://127.0.0.1:8000/api/tasks/?page=3",
    "previous": "http://127.0.0.1:8000/api/tasks/?page=1",
    "results": [
        ...
    ]
}
```


---

# 👮 Role-Based Access Control (RBAC)

This project implements **Role-Based Access Control (RBAC)** to ensure that users can only access data they are authorized to view.

There are two types of users in this project:

## 1. Admin User

An Admin user has permission to:

- View all tasks created by every user.
- Create new tasks.
- Retrieve any task.
- Update any task.
- Delete any task.

## 2. Normal User

A normal user can:

- Create tasks.
- View only their own tasks.
- Update only their own tasks.
- Delete only their own tasks.

They **cannot** view or manage tasks created by other users.

---

# 🔍 How RBAC is Implemented

The following code is responsible for controlling access:

```python
def get_queryset(self):
    if self.request.user.is_staff:
        return Task.objects.all()

    return Task.objects.filter(owner=self.request.user)
```

### Explanation

If the logged-in user is an **Admin** (`is_staff=True`), all tasks stored in the database are returned.

Otherwise, only tasks where the logged-in user is the owner are returned.

This ensures that every user can access only their own tasks while the Admin can access every task.

---

# 🧪 Testing RBAC Using Postman

Follow the steps below to verify that RBAC is working correctly.

---

## Step 1 - Register User 1

Register a user.

Example

```text
Username: john
Password: password123
```

Login using this account and create two tasks.

Example

```text
Task 1
Task 2
```

---

## Step 2 - Register User 2

Register another user.

Example

```text
Username: alice
Password: password123
```

Login using this account and create two more tasks.

Example

```text
Task 3
Task 4
```

---

## Step 3 - Test User 1

Login as **john**.

Copy the Access Token.

Use that token while sending the request:

```
GET http://127.0.0.1:8000/api/tasks/
```

### Expected Result

Only John's tasks should be returned.

Example

```text
Task 1
Task 2
```

John should **not** be able to see Alice's tasks.

---

## Step 4 - Test User 2

Login as **alice**.

Copy the Access Token.

Send:

```
GET http://127.0.0.1:8000/api/tasks/
```

### Expected Result

Only Alice's tasks should be returned.

Example

```text
Task 3
Task 4
```

Alice should **not** be able to see John's tasks.

---

## Step 5 - Test Admin User

Create a Django Superuser (if not already created):

```bash
python manage.py createsuperuser
```

Login to the Admin account using:

```
POST http://127.0.0.1:8000/api/auth/login/
```

Copy the Access Token.

Now send:

```
GET http://127.0.0.1:8000/api/tasks/
```

### Expected Result

The Admin should be able to view **all tasks**.

Example

```text
Task 1 (John)

Task 2 (John)

Task 3 (Alice)

Task 4 (Alice)
```

This confirms that RBAC is working correctly.

---

# 🖥 Django Admin Panel

The Django Admin Panel provides an interface to manage users and tasks.

Open the following URL in your browser:

```
http://127.0.0.1:8000/admin/
```

Login using the Superuser credentials created earlier.

From the Admin Panel you can:

- View all registered users.
- View all tasks.
- Edit task details.
- Delete tasks.
- Manage application data through the Django Admin interface.

---

# 🚀 Future Improvements

- Add task due dates and priorities.
- Write automated unit tests.
- Dockerize the application.
- Deploy the API to a cloud platform.

---

# 👩‍💻 Author

**Disha Gohil**
