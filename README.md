# Restaurants API

This is a .NET 8.0 web API for managing restaurants, following the principles of Clean Architecture.

## Video Course

This solution is part of a video course. 

You can find the course at [https://linktr.ee/fullstack_developer](https://linktr.ee/fullstack_developer). 

The course covers the development of this .NET 8.0 web API for managing restaurants, following the principles of Clean Architecture, in detail.

## Project Structure

- `src/Restaurants.API`: The main API project. This is the entry point of the application.
- `src/Restaurants.Application`: Contains the application logic. This layer is responsible for the application's behavior and policies.
- `src/Restaurants.Domain`: Contains enterprise logic and types. This is the core layer of the application.
- `src/Restaurants.Infrastructure`: Contains infrastructure-related code such as database and file system interactions. This layer supports the higher layers.
- `tests/Restaurants.API.Tests`: Contains unit tests for the API.


## Packages and Libraries

This project uses several NuGet packages and libraries to achieve its functionality:

- **Serilog**: This library is used for logging. It provides a flexible and easy-to-use logging API.

- **MediatR**: This library is used to implement the Command Query Responsibility Segregation (CQRS) pattern. In this solution, commands (which change the state of the system) and queries (which read the state) are separated for clarity and ease of development.

- **Entity Framework**: This is an open-source ORM framework for .NET. It enables developers to work with data using objects of domain-specific classes without focusing on the underlying database tables and columns where this data is stored.

- **Azure Storage Account**: This service is used for handling blobs. Blobs, or Binary Large Objects, are a type of data that can hold large amounts of unstructured data such as text or binary data, including images, documents, streaming media, and archive data.

- **Microsoft Identity Package**: This package is used for handling user identity in the web API. It provides features such as authentication, authorization, identity, and user access control.

Please refer to the official documentation of each package for more details and usage examples.

## Getting Started

### Prerequisites

- .NET 8.0
- Visual Studio 2022 or later

### Building

To build the project, open the `Restaurants.sln` file in Visual Studio and build the solution.

### Running

To run the project, set `Restaurants.API` as the startup project in Visual Studio and start the application.

## API Endpoints

1. `GET /api/restaurants`
   - Parameters: `searchPhrase`, `pageSize`, `pageNumber`, `sortBy`, `sortDirection`
   - Authorization Bearer token

2. `GET /api/restaurants/{id}`
   - Parameters: `id`
   - Authorization: Bearer token

3. `GET /api/restaurants/{id}/dishes`
   - Parameters: `id`
   - Authorization: Bearer token

4. `DELETE /api/restaurants/{id}/dishes`
   - Parameters: `id`

5. `GET /api/restaurants/{id}/dishes/{dishId}`
   - Parameters: `id`, `dishId`

6. `DELETE /api/restaurants/{id}`
   - Parameters: `id`
   - Authorization: Bearer token

7. `POST /api/restaurants`
   - Body: JSON object with properties `Name`, `Description`, `Category`, `HasDelivery`, `ContactEmail`, `ContactNumber`, `City`, `Street`
   - Authorization: Bearer token

## Testing

The tests are located in the `tests/*` directory. You can run them using the test runner in Visual Studio.

## Development Container (`.devcontainer/devcontainer.json`)

The `.devcontainer/devcontainer.json` file defines a **Dev Container** — a fully configured, Docker-based development environment that can be opened directly in Visual Studio Code (via the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)) or in GitHub Codespaces.

Using a dev container means every contributor gets the same toolchain, OS, and dependencies without having to install anything manually on their local machine.

### What each section does in this project

| Section | Purpose |
|---|---|
| `name` | A human-readable label for the container ("Restaurants API .NET 8"). |
| `image` | The base Docker image. Here it is `mcr.microsoft.com/devcontainers/dotnet:1-8.0-jammy` — a Microsoft-provided Ubuntu 22.04 (Jammy) image with the .NET 8 SDK preinstalled. |
| `features` | Extra capabilities installed on top of the base image: **Git** (version control CLI), **GitHub CLI** (`gh`), and **MSSQL** (SQL Server tools and a running SQL Server instance on port 1433). |
| `forwardPorts` | Ports `5000` and `5001` (the ASP.NET development server) and `1433` (SQL Server) are forwarded from inside the container to your local machine so you can reach the API and database normally. |
| `containerEnv` | Sets the `ConnectionStrings__RestaurantsDb` environment variable so the API can connect to the SQL Server instance that the MSSQL feature started inside the same container. |
| `customizations.vscode` | Installs two VS Code extensions automatically (`ms-dotnettools.csharp` for C# language support and `JakubKozera.csharp-dev-tools`) and configures editor settings (Roslyn language server, auto-import completions, format-on-save, and organize-imports-on-save). |
| `postCreateCommand` | Runs **once** after the container is created for the first time: restores NuGet packages (`dotnet restore`), restores local .NET tools (`dotnet tool restore`), and applies any pending Entity Framework migrations to create/update the database. |
| `postStartCommand` | Runs **every time** the container starts: builds the entire solution (`dotnet build`) so you know immediately if anything is broken. |
| `remoteUser` | The container process runs as the non-root `vscode` user for better security. |

### How to use it

1. Install the [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension in VS Code.
2. Open this repository folder in VS Code.
3. When prompted, choose **"Reopen in Container"** (or run the **Dev Containers: Reopen in Container** command from the Command Palette).
4. VS Code will build/pull the image, install features, run `postCreateCommand`, and drop you into a fully ready environment.

Alternatively, open the repository in [GitHub Codespaces](https://github.com/features/codespaces) — the same `devcontainer.json` is used automatically.

 
