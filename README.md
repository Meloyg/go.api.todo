# Go API - Todo Application

A simple RESTful API built with Go and Fiber framework for managing todo items.

## Features

- Create new todos
- List all todos
- Mark todos as completed
- Delete todos
- In-memory storage
- Hot reload development with Air

## Tech Stack

- **Go** 1.25.4
- **Fiber v2** - Fast HTTP web framework
- **Air** - Live reload for Go apps

## Prerequisites

- Go 1.25.4 or higher
- Air (for development with hot reload)

## Installation

1. Clone the repository:

```bash
git clone https://github.com/Meloyg/go.api.todo.git
cd go-api
```

2. Install dependencies:

```bash
go mod download
```

3. (Optional) Install Air for hot reload:

```bash
go install github.com/air-verse/air@latest
```

## Running the Application

### Standard Mode

```bash
go run main.go
```

### Development Mode (with hot reload)

```bash
air
```

The server will start on `http://localhost:4000`

## API Endpoints

### Get All Todos

```http
GET /
```

**Response:**

```json
[
  {
    "id": 1,
    "completed": false,
    "body": "Buy groceries"
  }
]
```

### Create a Todo

```http
POST /api/todos
Content-Type: application/json

{
  "body": "Buy groceries"
}
```

**Response:** `201 Created`

```json
{
  "id": 1,
  "completed": false,
  "body": "Buy groceries"
}
```

**Error Response:** `400 Bad Request`

```json
{
  "error": "Todo body is required."
}
```

### Mark Todo as Completed

```http
PATCH /api/todos/:id
```

**Response:** `200 OK`

```json
{
  "id": 1,
  "completed": true,
  "body": "Buy groceries"
}
```

**Error Response:** `404 Not Found`

```json
{
  "error": "Todo not found."
}
```

### Delete a Todo

```http
DELETE /api/todos/:id
```

**Response:** `200 OK`

```json
{
  "message": "deleted todo"
}
```

**Error Response:** `404 Not Found`

```json
{
  "error": "Todo not found."
}
```

## Project Structure

```
.
├── main.go          # Main application file with API routes
├── go.mod           # Go module dependencies
├── go.sum           # Dependency checksums
├── air.toml         # Air configuration for hot reload
├── .gitignore       # Git ignore rules
└── README.md        # Project documentation
```

## Data Model

### Todo

```go
type Todo struct {
    ID        int    `json:"id"`
    Completed bool   `json:"completed"`
    Body      string `json:"body"`
}
```

## Development

This project uses Air for hot reload during development. The configuration is stored in `air.toml`. Any changes to `.go` files will automatically rebuild and restart the server.

## Notes

- This application uses in-memory storage. All data will be lost when the server restarts.
- The API currently has no authentication or authorization.
- For production use, consider adding:
  - Persistent database storage (PostgreSQL, MongoDB, etc.)
  - Authentication and authorization
  - Input validation and sanitization
  - Rate limiting
  - CORS configuration
  - Logging middleware
  - Error handling middleware

## License

This project is open source and available under the MIT License.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Repository

[https://github.com/Meloyg/go.api.todo](https://github.com/Meloyg/go.api.todo)
