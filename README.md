# MvcMovie

An ASP.NET Core MVC web application for managing a movie catalog. It follows
Microsoft's [*Get started with ASP.NET Core MVC*](https://learn.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc)
tutorial and demonstrates the MVC pattern, Entity Framework Core, data
validation, and search/filter functionality.

## Features

- **CRUD operations** for movies (create, read, update, delete) via the
  `Movies` controller.
- **Search and filter** — find movies by title and filter the list by genre.
- **Model validation** using data annotations (required fields, string
  lengths, value ranges, and regular-expression rules).
- **Database seeding** — sample movies are inserted automatically on first run
  if the database is empty.
- **EF Core migrations** for managing the database schema.

## Tech stack

- [.NET 10](https://dotnet.microsoft.com/) / ASP.NET Core MVC
- Entity Framework Core 10 (SQL Server provider)
- SQL Server (LocalDB / SQL Server Express)
- Razor views with Bootstrap

## Project structure

```
MvcMovie/
├── Controllers/        # MVC controllers (Movies, Home, HelloWorld)
├── Models/             # Movie entity, view models, and seed data
├── Views/              # Razor views (Movies/, Home/, Shared/, ...)
├── Data/               # MvcMovieContext (EF Core DbContext)
├── Migrations/         # EF Core database migrations
├── Program.cs          # App startup and service configuration
└── appsettings.json    # Configuration and connection strings
```

## The Movie model

Each movie record has the following fields (defined in `Models/Movie.cs`):

| Field         | Type      | Validation                                          |
|---------------|-----------|-----------------------------------------------------|
| `Title`       | string    | Required, 3–60 characters                           |
| `ReleaseDate` | DateTime  | Displayed as a date                                 |
| `Genre`       | string    | Required, max 30 chars, letters/spaces only         |
| `Price`       | decimal   | Range 1–100, stored as `decimal(18,2)`              |
| `Rating`      | string    | Required, max 5 chars                               |

## Getting started

### Prerequisites

- [.NET 10 SDK](https://dotnet.microsoft.com/download)
- A SQL Server instance. The default connection string in `appsettings.json`
  targets a local SQL Server Express instance (`.\SQLEXPRESS`).

### Configure the database

The connection string is defined in `MvcMovie/appsettings.json`:

```json
"ConnectionStrings": {
  "MvcMovieContext": "Server=.\\SQLEXPRESS;Database=MvcMovieContext;Trusted_Connection=True;TrustServerCertificate=True;MultipleActiveResultSets=true"
}
```

Update the `Server=` value if your SQL Server instance uses a different name
(for example `(localdb)\\mssqllocaldb`).

### Run the app

From the repository root:

```bash
cd MvcMovie

# Apply the EF Core migrations to create the database
dotnet ef database update

# Run the application
dotnet run
```

> If you don't have the EF Core tools installed, run
> `dotnet tool install --global dotnet-ef` first.

The app launches in your browser. The default route points to the
`HelloWorld` controller; the movie catalog lives at **`/Movies`**.

On first run the database is seeded with a handful of sample movies
(*When Harry Met Sally*, *Ghostbusters*, *Rio Bravo*, and others).

## Working with migrations

```bash
# Add a new migration after changing the model
dotnet ef migrations add <MigrationName>

# Apply pending migrations to the database
dotnet ef database update
```

## License

This project is based on a Microsoft learning sample and is intended for
educational purposes.
