# crud_restapi_assignment

## Project Overview

This is a Spring Boot CRUD (Create, Read, Update, Delete) application with JWT (JSON Web Token) authentication. It provides RESTful APIs to manage products and user authentication.

## Features

*   User Registration and Login
*   JWT-based Authentication
*   Product Management (CRUD operations)
*   MySQL Database Integration
*   Global Exception Handling

## Prerequisites

Before you begin, ensure you have the following installed:

*   **Java Development Kit (JDK) 17 or higher**
*   **Apache Maven 3.8.x or higher**
*   **MySQL Server 8.0 or higher**
*   **Postman or cURL** for API testing

## Project Setup

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/Hariom-03925/crud_restapi_assignment.git
    cd crud_restapi_assignment
    ```

2.  **Database Configuration (MySQL):**
    *   Ensure your MySQL server is running.
    *   The application will attempt to create the database named `crud` if it doesn't exist (due to `createDatabaseIfNotExist=true` in `application.properties`).
    *   Update the database connection details in `src/main/resources/application.properties` if they differ from your setup:
        ```properties
        spring.datasource.url=jdbc:mysql://localhost:3307/crud?createDatabaseIfNotExist=true
        spring.datasource.username=root
        spring.datasource.password=hariom*123
        ```
    *   `spring.jpa.hibernate.ddl-auto=update` is set to automatically create/update tables based on your JPA entities.

3.  **Build the Project:**
    Navigate to the project root directory and build the project using Maven:
    ```bash
    mvn clean install
    ```

4.  **Run the Application:**
    You can run the Spring Boot application using Maven:
    ```bash
    mvn spring-boot:run
    ```
    The application will start on `http://localhost:8085`.

## API Endpoints

All API endpoints are prefixed with `/api`.

### Authentication

1.  **Register User**
    *   **URL:** `POST /api/auth/register`
    *   **Body (JSON):**
        ```json
        {
            "username": "yourusername",
            "password": "yourpassword"
        }
        ```
    *   **Example cURL:**
        ```bash
        curl -X POST -H "Content-Type: application/json" -d "{\"username\":\"testuser\", \"password\":\"testpassword\"}" http://localhost:8085/api/auth/register
        ```

2.  **Login User & Get JWT Token**
    *   **URL:** `POST /api/auth/login`
    *   **Body (JSON):**
        ```json
        {
            "username": "yourusername",
            "password": "yourpassword"
        }
        ```
    *   **Response:**
        ```json
        {
            "token": "your_jwt_token_here"
        }
        ```
    *   **Example cURL:**
        ```bash
        curl -X POST -H "Content-Type: application/json" -d "{\"username\":\"testuser\", \"password\":\"testpassword\"}" http://localhost:8085/api/auth/login
        ```

### Product Management (Requires JWT Token)

For all product endpoints, you must include the JWT token obtained from the login endpoint in the `Authorization` header as `Bearer <your_jwt_token>`.

1.  **Create Product**
    *   **URL:** `POST /api/products`
    *   **Body (JSON):**
        ```json
        {
            "name": "Laptop",
            "description": "Powerful gaming laptop",
            "price": 1200.00
        }
        ```
    *   **Example cURL:**
        ```bash
        curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer <your_jwt_token>" -d "{\"name\":\"Laptop\", \"description\":\"Powerful gaming laptop\", \"price\":1200.00}" http://localhost:8085/api/products
        ```

2.  **Get All Products**
    *   **URL:** `GET /api/products`
    *   **Example cURL:**
        ```bash
        curl -X GET -H "Authorization: Bearer <your_jwt_token>" http://localhost:8085/api/products
        ```

3.  **Get Product by ID**
    *   **URL:** `GET /api/products/{id}` (e.g., `/api/products/1`)
    *   **Example cURL:**
        ```bash
        curl -X GET -H "Authorization: Bearer <your_jwt_token>" http://localhost:8085/api/products/1
        ```

4.  **Update Product**
    *   **URL:** `PUT /api/products/{id}` (e.g., `/api/products/1`)
    *   **Body (JSON):**
        ```json
        {
            "name": "Updated Laptop",
            "description": "Slim and lightweight laptop",
            "price": 1150.00
        }
        ```
    *   **Example cURL:**
        ```bash
        curl -X PUT -H "Content-Type: application/json" -H "Authorization: Bearer <your_jwt_token>" -d "{\"name\":\"Updated Laptop\", \"description\":\"Slim and lightweight laptop\", \"price\":1150.00}" http://localhost:8085/api/products/1
        ```

5.  **Delete Product**
    *   **URL:** `DELETE /api/products/{id}` (e.g., `/api/products/1`)
    *   **Example cURL:**
        ```bash
        curl -X DELETE -H "Authorization: Bearer <your_jwt_token>" http://localhost:8085/api/products/1
        ```