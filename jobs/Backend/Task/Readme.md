﻿# Mews Backend Task - Exchange Rate Updater

## Architecture Overview
**This PR** includes the **exchange rate implementation**, built with **.NET 8**, focusing on **overall robustness** while adhering to **best practices**.

This project follows **Clean Architecture** principles to ensure **scalability, maintainability and testability**. The architecture is **intentionally overengineered** to demonstrate a **scalable approach** suitable for **larger applications**.

### **Project Structure**
- `ExchangeRateUpdater.Api` => ASP.NET Core API project (Entry Point)
- `ExchangeRateUpdater.Console` => Console application (Entry Point)
- `ExchangeRateUpdater.Application` => Business logic, CQRS (MediatR), validation
- `ExchangeRateUpdater.Domain` => Core domain models
- `ExchangeRateUpdater.Infrastructure` => External dependencies (HTTP clients, caching)
- `ExchangeRateUpdater.Client` => Auto-generated API client for external services (used by Integration Tests)
- `ExchangeRateUpdater.Api.Tests` => Unit tests for the API layer
- `ExchangeRateUpdater.Application.Tests` => Unit tests for the Application layer
- `ExchangeRateUpdater.Infrastructure.Tests` => Unit tests for the Infrastructure layer
- `ExchangeRateUpdater.IntegrationTests` => End-to-end integration tests

---

## Best Practices used in the project
- CQRS
- Mediator Pattern (via MediatR)
- Dependency Injection
- Centralized Exception Handling
- Logging (Serilog)
- Documented APIs (Swagger)
- NSwag for API Client Generation
- Unit Testing & Integration Testing
- HTTP Resiliency (retries, circuit breakers)
- Caching (In-memory)

---

## Execute Projects
### **Running the API**
```bash
cd ExchangeRateUpdater.Api
dotnet build
dotnet run
```
- The API will start on **http://localhost:5001**
- Swagger UI: **http://localhost:5001/swagger**

### **Running the Console Application**
```bash
cd ExchangeRateUpdater.Console
dotnet build
dotnet run
```

---

## Running Tests
### **Unit Tests**
Navigate to the test project directory and run:
```bash
cd ExchangeRateUpdater.<TestProject>.Tests
dotnet test
```

### **Integration Tests**
Ensure the API is running before executing:
```bash
cd ExchangeRateUpdater.IntegrationTests
dotnet test
```
**Note**: Configure the corresponding `appsettings.json` file with the correct API URL before running integration tests.

---

## Regenerating API Clients for Integration Tests
- If external service definitions (Swagger) change, override the `swagger.json` file in the `scripts` folder.
- Navigate to the `scripts` folder and run:
```bash
./generate-clients.ps1
```
- It will regenerate client in the `ExchangeRateUpdater.Client` project.

---

## Possible Improvements
- **Integrate multiple CNB exchange rate APIs** => Fetch exchange rates from multiple CNB API sources to support a broader range of currencies.
- **Replace `ExceptionHandlingMiddleware`** => Use the `.NET 8`'s built-in `IExceptionHandler` for more standardized error handling (it replaces the `ExceptionHandlingMiddleware`).
- **Autogenerated CNB API Clients** => Use Swagger and NSwag to generate a client for the CNB API automatically.
- **Enhance Client Generation** => Use NSwag even to obtain `swagger.json` specifications without running the app. It enables full automation (even during builds).
- **Load Testing** => Perform load tests to assess performance under high traffic.
- **Expand Testing Coverage** => Extend Integration Test suite and add architecture tests to ensure adherence to Clean Architecture principles.
- **Security Enhancements** => Implement authentication and authorization.
- **Monitoring** => Add health checks and distributed tracing.
- **Deployment** => Containerize the application using Docker for consistent and scalable deployments.
