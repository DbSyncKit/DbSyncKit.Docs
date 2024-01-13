Title: Dependency Injection
Order: 2
BreadcrumbTitle: DI Setup
NavigationTitle: DI Setup
Xref: configuration/di-setup
---

DbSyncKit can be configured using Dependency Injection (DI) to manage the application's services more efficiently. This guide outlines the steps to set up DbSyncKit with DI in your application.

# 1. Add DbSyncKit Services

To configure DbSyncKit with Dependency Injection, add the necessary services to your DI container.

API Reference: [SynchronizationServiceCollectionExtensions](xref:api-DbSyncKit.Core.Extensions.SynchronizationServiceCollectionExtensions)

```csharp
services.AddSynchronizationServices();
```

This method adds the required DbSyncKit services to the IServiceCollection.

# 2. Inject Synchronization

Once the services are added, you can inject the `Synchronization` class into your application components.

API Reference: [Synchronization](xref:api-DbSyncKit.Core.Synchronization)

```csharp
public class YourService
{
    private readonly Synchronization _sync;

    public YourService(Synchronization sync)
    {
        _sync = sync;
    }

    // Use _sync for synchronization tasks
}
```

Now, you can use the injected `Synchronization` instance in your services to perform synchronization tasks.

# 3. Database Configuration

Configure your source and destination databases using DbSyncKit's [IDatabase](xref:api-DbSyncKit.DB.Interface.IDatabase) interface.

## For MSSQL
 Api Ref: [Connection](xref:api-DbSyncKit.MSSQL.Connection)
```csharp
// MSSQL manual database configuration
IDatabase SourceDatabase = new DbSyncKit.MSSQL.Connection("(localdb)\\MSSQLLocalDB", "SourceChinook", true);
IDatabase DestinationDatabase = new DbSyncKit.MSSQL.Connection("(localdb)\\MSSQLLocalDB", "DestinationChinook", true);
```

## For MySQL
Api Ref: [Connection](xref:api-DbSyncKit.MySQL.Connection)
```csharp
// MySQL manual database configuration
IDatabase SourceDatabase = new DbSyncKit.MySQL.Connection("localhost", 3306, "SourceChinook", "root", "");
IDatabase DestinationDatabase = new DbSyncKit.MySQL.Connection("localhost", 3306, "DestinationChinook", "root", "");
```

## For PostgreSQL
Api Ref: [Connection](xref:api-DbSyncKit.PostgreSQL.Connection)
```csharp
// MySQL manual database configuration
IDatabase SourceDatabase = new DbSyncKit.PostgreSQL.Connection("localhost", 5432, "sourceChinook", "postgres", "");
IDatabase DestinationDatabase = new DbSyncKit.PostgreSQL.Connection("localhost", 5432, "destinationChinook", "postgres", "");
```

Replace connection strings and other details according to your actual configurations.


# Next Steps

You have now successfully set up DbSyncKit with Dependency Injection. Proceed to the [Usage Guide](xref:usage) to learn how to perform synchronization tasks with DbSyncKit.
