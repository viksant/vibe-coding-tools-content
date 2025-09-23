---
title: "GitHub Copilot C# .NET Core"
description: "Configures GitHub Copilot for C# .NET Core development with Web APIs, Entity Framework, and Azure integration."
category: "configuration"
tags: ["github-copilot", "csharp", "dotnet-core", "web-api", "entity-framework", "azure"]
tech_stack: ["csharp", "dotnet", "entity-framework", "azure", "sql-server", "blazor"]
---

This configuration sets up GitHub Copilot for C# .NET Core development with Web APIs, Entity Framework, and Azure integration.

### Configuration Overview
This setup enables efficient C# .NET Core development using GitHub Copilot, focusing on Web APIs, Entity Framework ORM, and Azure services.

### Prerequisites
- **.NET SDK**: Version 6.0 or higher
- **Visual Studio**: Version 2022 or higher with GitHub Copilot extension installed
- **SQL Server**: Local or Azure SQL Database
- **Azure Account**: For cloud service integration

### Installation & Setup
1. **Install .NET SDK**: Download and install from [Microsoft's .NET Download page](https://dotnet.microsoft.com/download).
2. **Install Visual Studio**: Ensure you have the latest version with the GitHub Copilot extension enabled.
3. **Create a New Project**:
   ```bash
   dotnet new webapi -n MyApiProject
   cd MyApiProject
   ```
4. **Add Entity Framework Core**:
   ```bash
   dotnet add package Microsoft.EntityFrameworkCore.SqlServer
   dotnet add package Microsoft.EntityFrameworkCore.Tools
   ```
5. **Configure Database Context**: Create a new class `AppDbContext.cs`:
   ```csharp
   using Microsoft.EntityFrameworkCore;

   public class AppDbContext : DbContext
   {
       public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) { }
       public DbSet<MyEntity> MyEntities { get; set; }
   }
   ```
6. **Set Up Dependency Injection**: In `Startup.cs`, add the following in `ConfigureServices`:
   ```csharp
   services.AddDbContext<AppDbContext>(options =>
       options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));
   ```
7. **Configure Connection String**: In `appsettings.json`, add:
   ```json
   "ConnectionStrings": {
       "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=MyApiDb;Trusted_Connection=True;"
   }
   ```
8. **Run Migrations**:
   ```bash
   dotnet ef migrations add InitialCreate
   dotnet ef database update
   ```
9. **Deploy to Azure**: Use the Azure CLI to create a new web app and deploy:
   ```bash
   az webapp create --resource-group MyResourceGroup --plan MyAppServicePlan --name MyUniqueAppName --runtime "DOTNETCORE|6.0"
   ```

### File Structure
```
MyApiProject/
├── Controllers/
│   └── MyEntityController.cs
├── Models/
│   └── MyEntity.cs
├── Data/
│   └── AppDbContext.cs
├── Migrations/
├── Properties/
├── appsettings.json
├── MyApiProject.csproj
└── Startup.cs
```

### Key Configuration Files
- **`appsettings.json`**: Configuration settings for the application.
- **`Startup.cs`**: Main configuration for services and middleware.
- **`MyEntityController.cs`**: API controller for handling requests.

### Advanced Options
- **Enable CORS**: In `Startup.cs`, add:
   ```csharp
   services.AddCors(options =>
   {
       options.AddPolicy("AllowAllOrigins", builder =>
           builder.AllowAnyOrigin().AllowAnyMethod().AllowAnyHeader());
   });
   ```
- **Logging Configuration**: Enhance logging in `appsettings.json`:
   ```json
   "Logging": {
       "LogLevel": {
           "Default": "Information",
           "Microsoft": "Warning",
           "Microsoft.Hosting.Lifetime": "Information"
       }
   }
   ```

### Troubleshooting
- **Common Issues**:
  - **Database Connection Errors**: Ensure SQL Server is running and the connection string is correct.
  - **Migrations Fail**: Check for pending migrations and ensure the database is accessible.
  - **CORS Issues**: Verify that CORS is configured correctly in `Startup.cs`.

### Best Practices
- **Use DTOs**: Implement Data Transfer Objects to decouple your API from the database model.
- **Version Your API**: Use versioning in your API routes to manage changes effectively.
- **Automate Testing**: Implement unit and integration tests to ensure code quality.

### Performance Tuning and Workflow Optimization Tips
- **Use Asynchronous Programming**: Implement `async` methods in your controllers for better scalability.
- **Optimize Database Queries**: Use `Include` for related data and avoid N+1 query issues.
- **Leverage GitHub Copilot**: Utilize Copilot for generating boilerplate code and reducing development time.