## CleanArchMvc

Dotnet Core 7 MVC Application with Clean Architecture guidelines

## Description

This project is an MVC application built with Dotnet Core 7, following the Clean Architecture guidelines. It connects to a SQL Server database using Entity Framework Core.

## Prerequisites

Before running this application, make sure you have the following installed:

- Dotnet Core 7 SDK: [Download](https://dotnet.microsoft.com/download/dotnet/7.0)
- Sql Server: Provided by the [docker-compose.yml](./docker-compose.yml)

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/lucasfmarconi/CleanArqvMvc.git
   ```

2. Navigate to the project directory:

   ```bash
   cd CleanArqvMvc
   ```

3. Install the project dependencies:

   ```bash
   dotnet restore
   ```

4. Configure the database connection:

   Open the `appsettings.development.json` file and update the connection string with your SQL Server details.

   ```json
   "ConnectionStrings": {
       "DefaultConnection" : "Data Source=localhost;Initial Catalog=CleanArchMvc;User ID=sa;Password=Strong!106pwd;Connect Timeout=30;Encrypt=False;"
   }
   ```

5. Apply the database migrations:

   ```bash
   cd ./CleanArqvMvc/CleanArchMvc.Infra.Data
   dotnet ef database update --verbose -s ../CleanArchMvc.WebUI/CleanArchMvc.WebUI.csproj
   ```

6. Run the application:

   ```bash
   dotnet run
   ```

   The application will be accessible at `http://localhost:5000`.

## Project Structure

The project follows the Clean Architecture guidelines, which separates the application into layers:

//TODO
- **Presentation Layer (Web)**: Contains the MVC controllers, views, and other web-related components.
- **Application Layer**: Implements the use cases of the application and orchestrates the flow of data between the Presentation and Domain layers.
- **Domain Layer**: Defines the business entities, aggregates, and domain logic.
- **Infrastructure Layer**: Provides implementations for external dependencies such as the database and third-party services.

```
├── src
│   ├── CleanArchMvc.WebUI
│   ├── CleanArchMvc.Application
│   ├── CleanArchMvc.Domain
│   └── CleanArchMvc.Infra.Data
│   └── CleanArchMvc.Infra.IoC
└── tests
    ├── CleanArchMvc.Application.Tests
    ├── CleanArchMvc.Domain.Tests
    └── CleanArchMvc.Infrastructure.Tests
```

## Technologies Used

- Dotnet Core 7
- Entity Framework Core
- SQL Server
- ASP.NET MVC
- HTML/CSS/JavaScript
- Docker
- Docker Compose

## License

This project is licensed under the [MIT License](LICENSE). Feel free to modify and distribute it as needed.