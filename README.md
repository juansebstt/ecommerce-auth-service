# E-commerce Auth Service

## Overview

The **E-commerce Auth Service** is a Spring Boot-based microservice responsible for handling user authentication and authorization. It manages user registration, login, password management, and JWT token generation for secure communication across the e-commerce platform.

## Features

- **User Registration**: Allows new users to create an account with email and password.
- **User Login**: Authenticates users and provides JWT tokens for subsequent requests.
- **Token Validation**: Validates JWT tokens for secured endpoints across the system.
- **Password Management**: Supports password hashing and reset functionalities.
- **Integration with Other Services**: Works seamlessly with other microservices, such as the
  [Payment Service](https://github.com/juansebstt/ecommerce-payment-service) and [API Gateway]([https://github.com/juansebstt/ecommerce-payment-service](https://github.com/juansebstt/ecommerce-api-gateway))

## Technologies Used

- **Java 17**
- **Spring Boot**
- **Spring Security** - For authentication and authorization.
- **JWT** - For token generation and validation.
- **Maven** - For dependency management and build tool.
- **PostgreSQL** - For storing user information (optional based on your setup).
- Postman: For testing endpoints.

## Prerequisites

Before running this service, ensure you have the following installed:

- **Java 17**
- **Maven** (for building the project)
- A running instance of PostgreSQL (if used for user data storage).

## Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/juansebstt/ecommerce-auth-service
    ```

2. Navigate to the project directory:

    ```bash
    cd ecommerce-auth-service
    ```

3. Build the project using Maven:

    ```bash
    mvn clean install
    ```

4. Run the project:

    ```bash
    mvn spring-boot:run
    ```


## Configuration

The Auth Service uses a configuration file for managing properties like database connection, JWT settings, etc. Here are the key configuration options from `application.yaml`:

```yaml
server:
  port: 8081

spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/yourdb
    username: yourusername
    password: yourpassword
  jwt:
    secret: your_jwt_secret
    expiration: 3600  # token expiration time in seconds
```

- Replace the `url`, `username`, and `password` with your actual database credentials.
- Configure your JWT secret for signing tokens.

## Usage

Once the Auth Service is running, it can handle authentication requests through the following endpoints:

- **User Registration**: `POST /auth/register`
- **User Login**: `POST /auth/login`
- **Token Validation**: The service will validate tokens issued during login for requests made to protected routes in other services.

## Inter-Service Communication

The Auth Service connects with the following microservices:

- **E-commerce API Gateway**: The gateway routes authentication requests to this service. It handles user registration and login through the `/auth` endpoint.
- **E-commerce Payment Service**: The Auth Service provides JWT tokens that are required for secure payment processing and user authentication on payment requests.

## Testing

You can test the Auth Service using Postman or any other API client. For the login request, you need to provide the user credentials:

```
POST /auth/login
Content-Type: application/json

{
  "username": "yourusername",
  "password": "yourpassword"
}

```

If successful, you'll receive a JWT token that should be used in the Authorization header for subsequent requests:

```
Authorization: Bearer <your-jwt-token>
```

## Contributing

Feel free to submit pull requests or open issues if you find bugs or want to contribute to the project.