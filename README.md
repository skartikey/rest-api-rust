# rest-api-rust
RESTful API in Rust

## Prerequisites

Before getting started, ensure you have the following prerequisites installed:

- [Rust](https://www.rust-lang.org/tools/install)
- MySQL database

## Getting Started

### Setting up the Database

1. Create a MySQL database for your project:

    ```sql
    CREATE DATABASE your_database_name;
    ```

2. Copy the `.env.sample` file to `.env` and update the database connection details:

    ```dotenv
    DATABASE_URL=mysql://username:password@localhost/your_database_name
    ```

   Replace `username`, `password`, and `your_database_name` with your MySQL credentials.

### Generating Migration

Run the following command to generate a migration for the `links` table:

```bash
cargo run --bin migration
```

This will create a new migration file in the `migrations` directory.

### Applying Migration

Apply the migration to create the `links` table:

```bash
cargo run --bin migration -- migrate
```

### Starting the Project

1. Install crates:

    ```bash
    cargo build
    ```

2. Run the project:

    ```bash
    cargo run
    ```

The project will start, and you can interact with the API.

### Endpoints

The backend provides two endpoints:

- **GET /links:** Retrieve a list of shared links.
  
  **Success Response:**
  ```json
  [
    {
      "id": 1,
      "link": "https://www.sk.com/about",
      "count": 58,
      "created_at": "2024-02-03T23:05:37Z",
      "updated_at": "2024-02-03T23:07:16Z"
    },
    {
      "id": 2,
      "link": "https://www.sk.com",
      "count": 18,
      "created_at": "2024-02-03T23:16:12Z",
      "updated_at": "2024-02-03T23:16:22Z"
    },
    {
      "id": 3,
      "link": "https://www.sk.com/newsletter",
      "count": 36,
      "created_at": "2024-02-03T23:16:35Z",
      "updated_at": "2024-02-03T23:55:07Z"
    }
  ]
  ```
  
  **Error Response:**
  ```json
  {
    "error": "error that occurred"
  }
  ```

- **POST /links:** Add a new link to the collection.

  **Request Body Schema:**
  ```json
  {
    "link": "https://awesome-link.com"
  }
  ```

  **Success Response:**
  ```json
  {
    "id": 123,
    "link": "https://example.com",
    "count": 1,
    "created_at": "2024-02-03T12:34:56Z",
    "updated_at": "2024-02-03T12:34:56Z"
  }
  ```

  **Error Response:**
  ```json
  {
    "error": "Failed to share the link. Please try again."
  }
  ```

## Project Structure

- **src/:** Source code directory.
- **migrations/:** Directory containing database migration files.
- **Database Schema SQL:**
  ```sql
  CREATE TABLE links (
      id INT AUTO_INCREMENT PRIMARY KEY,
      link VARCHAR(255) NOT NULL,
      count INT DEFAULT 1 NOT NULL,
      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
      updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
  );
  ```

  Adjust the schema according to your requirements.