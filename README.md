# Multi-Service-Application-Using-Docker-and-AWS

# Multi-Service Application Using Docker and AWS

This project demonstrates a multi-service application built using Node.js, Express.js, PostgreSQL, Docker, and Docker Compose. The application is divided into three microservices: `user`, `blog`, and `comment`. Each service is containerized and communicates with a PostgreSQL database.

## Project Structure

```plaintext
.
├── blog
│   └── server.js  # Blog microservice
├── comment
│   └── server.js  # Comment microservice
├── db
│   └── init.sql   # Database initialization script
├── user
│   └── server.js  # User microservice
├── .env           # Environment variables
├── docker-compose.yml  # Docker Compose configuration
├── package.json   # Node.js dependencies
├── README.md      # Documentation
└── ...            # Other supporting files
```

## Prerequisites

- [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/)
- [Node.js](https://nodejs.org/) and [npm](https://www.npmjs.com/)

## Setup Instructions

1. **Clone the Repository**:

   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. **Environment Variables**:
   - Create a `.env` file in the root directory and add the following variables:

     ```env
     DATABASE_URL=postgresql://user:password@db:5432/main_db
     JWT_SECRET=your-secret-key
     PORT=5000
     ```

3. **Database Initialization**:
   - The `db/init.sql` file contains the SQL script for creating required tables for all services.

4. **Install Dependencies**:
   Run the following command to install the required Node.js dependencies:

   ```bash
   npm install
   ```

5. **Start the Application**:
   - Use Docker Compose to build and run the application:

     ```bash
     docker-compose up --build
     ```

6. **Access the Services**:
   - User Service: `http://localhost:5001`
   - Blog Service: `http://localhost:5002`
   - Comment Service: `http://localhost:5003`

## Services Overview

### 1. User Service
- **Endpoint:** `/register`
  - Method: `POST`
  - Description: Registers a new user.
- **Endpoint:** `/login`
  - Method: `POST`
  - Description: Authenticates a user and returns a JWT token.
- **Endpoint:** `/users/:id`
  - Method: `GET`
  - Description: Fetches user details by ID.

### 2. Blog Service
- **Endpoint:** `/blogs`
  - Method: `POST`
  - Description: Creates a new blog.
- **Endpoint:** `/blogs`
  - Method: `GET`
  - Description: Fetches all blogs.

### 3. Comment Service
- **Endpoint:** `/comments`
  - Method: `POST`
  - Description: Adds a comment to a blog post.
- **Endpoint:** `/comments`
  - Method: `GET`
  - Description: Fetches comments by post ID.

## Docker Configuration

The `docker-compose.yml` file defines the services:

- **User Service**:
  - Runs on port `5001`.
  - Connected to `user_db` in PostgreSQL.
- **Blog Service**:
  - Runs on port `5002`.
  - Connected to `blog_db` in PostgreSQL.
- **Comment Service**:
  - Runs on port `5003`.
  - Connected to `comment_db` in PostgreSQL.
- **Database**:
  - PostgreSQL version `15`.
  - Stores all service data.

## Dependencies

The `package.json` includes:

- `bcrypt`: Password hashing.
- `dotenv`: Environment variable management.
- `express`: Web framework.
- `jsonwebtoken`: JWT authentication.
- `pg`: PostgreSQL client.
- `nodemon`: Development server.

## Running the Application

1. Ensure Docker and Docker Compose are installed and running on your machine.
2. Start the services:

   ```bash
   docker-compose up
   ```

3. Access the services at the respective ports mentioned in the **Services Overview**.

## Testing

- Use tools like [Postman](https://www.postman.com/) or `curl` to test the endpoints.
- Example requests:

  - **Register a User**:

    ```bash
    curl -X POST http://localhost:5001/register \
         -H "Content-Type: application/json" \
         -d '{"username": "testuser", "password": "password123"}'
    ```

  - **Create a Blog**:

    ```bash
    curl -X POST http://localhost:5002/blogs \
         -H "Content-Type: application/json" \
         -d '{"title": "My First Blog", "content": "Hello World!"}'
    ```

## Future Enhancements

- Add authentication to the Blog and Comment services.
- Implement data validation and error handling.
- Use an orchestration tool like Kubernetes for scalability.

## Contributing

Contributions are welcome! Please fork the repository and create a pull request with your changes.

## License

This project is licensed under the MIT License.

