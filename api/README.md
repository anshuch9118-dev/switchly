# Switchly

Switchly is a backend service for managing organizations, projects, and feature flags through REST APIs.

The project is built with Java and Spring Boot and focuses on creating a clean backend structure for managing feature releases without requiring application code changes for every feature update.

## Features

- Create and manage organizations
- Create projects under organizations
- Retrieve all organizations
- Retrieve projects belonging to an organization
- Retrieve a project by its ID
- Create and manage feature flags
- Enable or disable feature flags
- UUID-based resource identification
- Request validation
- Centralized exception handling
- Custom handling for not-found and conflict cases
- Layered backend architecture
- RESTful API design

## How Switchly Works

Switchly organizes resources in the following structure:

    Organization
        |
        └── Project
              |
              └── Feature Flags

For example:

    Zomato
       |
       └── Zomato-Backend
              |
              ├── new-checkout
              ├── dark-mode
              └── payment-v2

This structure allows different organizations to manage their own projects and feature flags independently.

## API Endpoints

### Organizations

Create an organization:

`POST /api/v1/orgs`

Example request:

    {
      "name": "Zomato"
    }

Get all organizations:

`GET /api/v1/orgs`

Get an organization by ID:

`GET /api/v1/orgs/{orgId}`

### Projects

Create a project inside an organization:

`POST /api/v1/orgs/{orgId}/projects`

Example request:

    {
      "name": "Zomato-Backend"
    }

Get all projects for an organization:

`GET /api/v1/orgs/{orgId}/projects`

Get a project by ID:

`GET /api/v1/projects/{projectId}`

### Feature Flags

The backend also provides APIs for working with feature flags.

Current functionality includes:

- Creating feature flags
- Retrieving feature flags
- Updating feature flag state
- Managing flags within projects

## Technology Stack

| Category | Technology |
|---|---|
| Programming Language | Java |
| Backend Framework | Spring Boot |
| Build Tool | Maven |
| API | REST API |
| Validation | Jakarta Validation |
| Data Storage | In-Memory Repository |
| Testing | Spring Boot Test |
| Version Control | Git & GitHub |
| API Testing | Postman |

## Architecture

Switchly follows a layered backend architecture:

    Client
       |
       v
    Controller
       |
       v
    Service
       |
       v
    Repository
       |
       v
    Data Store

### Controller

The controller layer handles HTTP requests and maps them to the appropriate service methods.

### Service

The service layer contains the main business logic of the application.

### Repository

The repository layer handles data access. The current implementation uses in-memory repositories.

### Model

The model layer contains the main domain objects:

- Organization
- Project
- Feature Flag

### DTO

Data Transfer Objects are used to define the structure of incoming API requests and validate request data.

### Exception Handling

The project includes centralized exception handling for consistent API error responses, including cases such as missing resources and conflicts.

## Project Structure

    switchly/
    |
    ├── .mvn/
    │   └── wrapper/
    |
    ├── src/
    │   ├── main/
    │   │   ├── java/live/switchly/api/
    │   │   │
    │   │   ├── controller/
    │   │   │   ├── FlagController.java
    │   │   │   ├── OrganizationController.java
    │   │   │   └── ProjectController.java
    │   │   │
    │   │   ├── dto/
    │   │   │   ├── CreateFlagRequest.java
    │   │   │   ├── CreateOrganizationRequest.java
    │   │   │   ├── CreateProjectRequest.java
    │   │   │   └── UpdateFlagStateRequest.java
    │   │   │
    │   │   ├── exception/
    │   │   │   ├── ConflictException.java
    │   │   │   ├── ErrorResponse.java
    │   │   │   ├── GlobalExceptionHandler.java
    │   │   │   └── NotFoundException.java
    │   │   │
    │   │   ├── model/
    │   │   │   ├── Flag.java
    │   │   │   ├── Organization.java
    │   │   │   └── Project.java
    │   │   │
    │   │   ├── repository/
    │   │   │   ├── FlagRepository.java
    │   │   │   ├── InMemoryFlagRepository.java
    │   │   │   ├── InMemoryOrganizationRepository.java
    │   │   │   ├── InMemoryProjectRepository.java
    │   │   │   ├── OrganizationRepository.java
    │   │   │   └── ProjectRepository.java
    │   │   │
    │   │   ├── service/
    │   │   │   ├── FlagService.java
    │   │   │   ├── OrganizationService.java
    │   │   │   └── ProjectService.java
    │   │   │
    │   │   └── ApiApplication.java
    │   │
    │   └── test/
    |
    ├── .gitattributes
    ├── .gitignore
    ├── pom.xml
    ├── mvnw
    └── mvnw.cmd

## Running Locally

### Prerequisites

Make sure you have the following installed:

- Java
- Git
- VS Code or another Java-compatible IDE

### Clone the Repository

`git clone https://github.com/anshuch9118-dev/switchly.git`

Move into the project directory:

`cd switchly`

### Start the Application

On Windows:

`mvnw.cmd spring-boot:run`

The application will start on:

`http://localhost:8080`

## Testing with Postman

The REST APIs can be tested using Postman.

For example, create an organization:

`POST http://localhost:8080/api/v1/orgs`

Request body:

    {
      "name": "Zomato"
    }

The response will contain the organization's unique ID.

The organization ID can then be used to create a project:

`POST http://localhost:8080/api/v1/orgs/{orgId}/projects`

Example request:

    {
      "name": "Zomato-Backend"
    }

Projects can then be retrieved using:

`GET http://localhost:8080/api/v1/orgs/{orgId}/projects`

## Development Progress

### Completed

- [x] Spring Boot project setup
- [x] REST API structure
- [x] Organization management
- [x] Project management
- [x] Feature flag structure
- [x] Service layer
- [x] Repository layer
- [x] DTO-based request handling
- [x] Request validation
- [x] Custom exceptions
- [x] Global exception handling
- [x] Git and GitHub setup
- [x] API testing with Postman

### Planned

- [ ] Persistent database storage
- [ ] User authentication
- [ ] API key authentication
- [ ] Environment management
- [ ] Feature flag targeting
- [ ] Percentage-based rollouts
- [ ] Frontend dashboard
- [ ] Client SDK
- [ ] Deployment
- [ ] CI/CD

## Why Switchly?

Deploying application code and releasing a feature do not always need to happen at the same time.

Feature flags make it possible to control whether a feature is enabled or disabled without changing and redeploying the application's code.

Switchly is being developed to explore this concept from the backend up, starting with organizations, projects, and feature flags and gradually adding more capabilities.

## Future Direction

The project will gradually expand toward a complete feature flag management platform with capabilities such as:

- Persistent data storage
- Authentication and authorization
- Multiple environments
- Advanced feature targeting
- Percentage-based rollouts
- Web-based management dashboard
- Client SDK
- Deployment and CI/CD

## Repository

GitHub: https://github.com/anshuch9118-dev/switchly

---

Built with Java and Spring Boot while learning and applying REST APIs, layered architecture, backend development, and feature flag concepts.
