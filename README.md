Task Management API

This is a RESTful API for managing tasks. The API allows users to create, update, delete, and manage tasks, along with user authentication and validation using JSON Web Tokens (JWT) and Joi.

Features:

User Authentication: Users can sign up, log in, and manage their accounts.
Task Management: Users can create, update, view, and delete tasks.
JWT Authentication: Protected routes require valid JWT tokens.
Input Validation: Request bodies are validated using Joi.


Tech Stack:

Backend: Node.js, Express.js
Database: MongoDB
Authentication: JWT
Validation: Joi
Testing: Postman/Swagger


Getting Started:

Prerequisites
Ensure you have the following installed:
Node.js
MongoDB (local or cloud)
Postman or Swagger for testing


Installation:

Clone the repository:
git clone https://github.com/your-repo/task-manager-api.git
Install dependencies:
cd task-manager-api
npm install


Set up environment variables:

Create a .env file in the root directory and configure the following variables:

PORT=5000
MONGO_URI=your_mongo_db_connection_string
JWT_SECRET=your_jwt_secret


Start the server:
node server.js


API Endpoints:


Authentication:
1. Register a new user
Endpoint: /api/user/register
Method: POST
Description: Creates a new user account.
Request Body:
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "123456"
}

Response:
201 Created:
{
  "message": "User created successfully",
  "user": {
    "_id": "63f7bda23dcd9f42f203c92b",
    "name": "John Doe",
    "email": "john@example.com"
  }
}
400 Bad Request if validation fails.
409 Conflict if the email is already registered.

2. Login
Endpoint: /api/user/login
Method: POST
Description: Authenticates a user and returns a JWT.
Request Body:
{
  "email": "john@example.com",
  "password": "123456"
}

Response:
200 OK:
{
  "message": "Login successful",
  "token": "jwt_token_here"
}
401 Unauthorized if credentials are incorrect.


Task Management:

Note: All task-related routes are protected and require a valid JWT token in the Authorization header.

3. Create a new task
Endpoint: /api/tasks/create
Method: POST
Description: Creates a new task for the authenticated user.
Headers:
{
  "Authorization": "Bearer jwt_token_here"
}

Request Body:
{
  "title": "Finish project",
  "description": "Complete the task management project",
  "dueDate": "2024-09-30"
}

Response:
201 Created:
{
  "message": "Task created successfully",
  "task": {
    "_id": "63f7bdc63dcd9f42f203c92c",
    "title": "Finish project",
    "description": "Complete the task management project",
    "dueDate": "2024-09-30",
    "completed": false
  }
}
400 Bad Request if validation fails.


4. Get all tasks
Endpoint: /api/tasks/alltasks
Method: GET
Description: Retrieves all tasks for the authenticated user.
Headers:
{
  "Authorization": "Bearer jwt_token_here"
}

Response:
200 OK:
{
  "tasks": [
    {
      "_id": "63f7bdc63dcd9f42f203c92c",
      "title": "Finish project",
      "description": "Complete the task management project",
      "dueDate": "2024-09-30",
      "completed": false
    }
  ]
}


5. Get a task by ID
Endpoint: /api/tasks/:id
Method: GET
Description: Retrieves a specific task by ID.
Headers:
{
  "Authorization": "Bearer jwt_token_here"
}

Response:
200 OK:
{
  "task": {
    "_id": "63f7bdc63dcd9f42f203c92c",
    "title": "Finish project",
    "description": "Complete the task management project",
    "dueDate": "2024-09-30",
    "completed": false
  }
}
404 Not Found if the task does not exist.


6. Update a task
Endpoint: /api/tasks/update/:id
Method: PUT
Description: Updates a specific task.
Headers:
{
  "Authorization": "Bearer jwt_token_here"
}

Request Body (Partial update allowed):
{
  "title": "Finish project",
  "completed": true
}
Response:
200 OK:
{
  "message": "Task updated successfully",
  "task": {
    "_id": "63f7bdc63dcd9f42f203c92c",
    "title": "Finish project",
    "description": "Complete the task management project",
    "dueDate": "2024-09-30",
    "completed": true
  }
}
400 Bad Request if validation fails.
404 Not Found if the task does not exist.


7. Delete a task
Endpoint: /api/tasks/delete/:id
Method: DELETE
Description: Deletes a specific task.
Headers:
{
  "Authorization": "Bearer jwt_token_here"
}
Response:
200 OK:
{
  "message": "Task deleted successfully"
}
404 Not Found if the task does not exist.


Error Handling:

400 Bad Request: Occurs when the request body contains invalid data or missing required fields.
401 Unauthorized: Occurs when authentication fails or a token is missing/invalid.
404 Not Found: Occurs when a resource (task or user) is not found.


Validation:

All input is validated using Joi. For example, a task creation request requires the following validation:

Title: Required, must be a string.
Description: Optional, must be a string.
Due Date: Optional, must be a valid date.
Completed: Optional, must be a boolean.


Authentication:

This API uses JWT for authentication. After a successful login, a token is provided, which must be included in the Authorization header as Bearer <token> for accessing protected routes.

Running Tests
You can use Postman or Swagger or ThunderClient to test the API endpoints.
# Task-Manager
