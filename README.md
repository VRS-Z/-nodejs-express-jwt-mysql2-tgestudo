# User Authentication API with MySQL and JWT

## Project Overview
This project focuses on creating a simple API for user authentication and retrieval of user details. The system allows users to log in using their CPF (Cadastro de Pessoa Física) and password, returning user-specific data and a generated JWT token upon successful login.

## Features
1. **Login System**: Users authenticate with CPF and password.
2. **User Data Retrieval**: After successful login, the system returns:
   - User Name
   - Email
   - Phone Number
   - Date of Birth
   - JWT Token
3. **Validation**:
   - CPF validation using mechanisms like `cpf.validator()`.
   - Password and input validation using Regex.

## Technologies Used
* **Backend**: Node.js with Express
* **Database**: MySQL
* **Authentication**: JWT (JSON Web Token)
* **Validation Tools**:
  - Regex for password and input validation
  - `cpf.validator()` for CPF validation

## Project Structure
```
project-root/
|-- config/             # Database configuration
|-- controllers/        # Handles API logic (Login, Data Retrieval)
|-- models/             # MySQL models for user data
|-- routes/             # API routes
|-- middleware/         # Validation and authentication middlewares
|-- utils/              # Utility functions like regex patterns, CPF validation
|-- .env                # Environment variables (DB credentials, JWT secret)
|-- server.js           # Entry point of the application
```

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/project-repo-name.git
cd project-repo-name
```

### 2. Install Dependencies
Ensure Node.js and MySQL are installed. Run:
```bash
npm install
```

### 3. Configure Environment Variables
Create a `.env` file in the root directory:
```
DB_HOST=your-database-host
DB_USER=your-database-username
DB_PASSWORD=your-database-password
DB_NAME=your-database-name
JWT_SECRET=your-jwt-secret
PORT=3000
```

### 4. Database Setup
Run the SQL script to set up the `users` table:
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cpf VARCHAR(11) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    name VARCHAR(100),
    email VARCHAR(100),
    phone_number VARCHAR(20),
    date_of_birth DATE
);
```

### 5. Start the Server
```bash
npm start
```
The server will be running at `http://localhost:3000`.

## API Endpoints

### 1. Login Endpoint
**URL**: `POST /api/login`

**Request Body**:
```json
{
  "cpf": "12345678900",
  "password": "YourPassword123!"
}
```

**Response**:
```json
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "phone_number": "(11) 99999-9999",
  "date_of_birth": "2000-01-01",
  "token": "JWT_TOKEN_HERE"
}
```

**Validation Rules**:
* CPF: Valid format using `cpf.validator()`
* Password: Regex to ensure strong password security.

### 2. Protected Routes
After login, use the JWT token in the `Authorization` header for accessing protected routes.

## Future Improvements
* Add rate limiting to protect endpoints.
* Implement password hashing using `bcrypt`.
* Extend validation rules for better security.
* Add unit tests.

## License
This project is licensed under the MIT License.

---
Developed by Otávio Franco Mendes, (https://github.com/VRS-Z)

A simple API for user authentication using CPF and password, returning user data and a JWT token. Includes MySQL database, input validation with regex, and CPF validation with cpf.validator(). Built with Node.js and JWT for secure authentication.
