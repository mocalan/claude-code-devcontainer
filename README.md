# Claude Code DevContainer Template

> "I'm sorry Claude, I'm afraid I can't do that"
>
> -- <cite>Docker</cite>

A minimal environment template for running Claude Code in containment

## Features

-   Simple Go HTTP server with "Hello World" endpoint
-   PostgreSQL database connection example
-   DevContainer setup for consistent development environment
-   Docker Compose configuration for PostgreSQL
-   Claude Code CLI pre-installed for AI-assisted development

## Quick Start

### Using DevContainers (Recommended)

1. Open in VS Code with Remote-Containers extension
2. VS Code will automatically build and start the development environment
3. Claude Code CLI is available for AI-assisted development:
    ```bash
    claude-code --help
    ```
4. Run the application:
    ```bash
    go run main.go
    ```

### Manual Setup

1. Start PostgreSQL:

    ```bash
    docker-compose -f .devcontainer/docker-compose.devcontainer.yml up postgres -d
    ```

2. Run the Go application:

    ```bash
    go run main.go
    ```

3. Visit http://localhost:8080 to see "Hello World!"

## Project Structure

```
go-template/
├── .devcontainer/              # DevContainer configuration
│   ├── devcontainer.json     # VS Code dev container settings
│   ├── Dockerfile            # Development environment
│   └── docker-compose.devcontainer.yml  # Services (PostgreSQL)
├── main.go                   # Simple Go application
├── go.mod                    # Go module definition
└── README.md                 # This file
```

## Environment Variables

-   `DATABASE_URL`: PostgreSQL connection string (default: `postgres://postgres@localhost:5432/postgres?sslmode=disable`)
-   `PORT`: HTTP server port (default: `8080`)

## Database Connection

The application includes a basic PostgreSQL connection example. When running in the DevContainer, it automatically connects to the PostgreSQL service.

## Extending This Template

This template provides a minimal foundation. You can extend it by:

-   Adding more HTTP handlers
-   Implementing database models and queries
-   Adding authentication and authorization
-   Including testing framework
-   Adding configuration management
-   Implementing logging and monitoring

## License

MIT License
