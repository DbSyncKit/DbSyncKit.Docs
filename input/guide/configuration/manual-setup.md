﻿Title: Manual Setup
Order: 3
BreadcrumbTitle: Manual Setup
NavigationTitle: Manual Setup
ShowInSidebar: true
Xref: configuration/manual-setup
---

DbSyncKit can be configured manually without using Dependency Injection (DI). This guide outlines the steps to set up DbSyncKit manually in your application.

# 1. Query Generator Setup (Optional)

## For MSSQL
API Reference: [QueryGenerator](xref:api-DbSyncKit.MSSQL.QueryGenerator)

```csharp
IQueryGenerator queryGenerator = new DbSyncKit.MSSQL.QueryGenerator();
```

## For MySQL
API Reference: [QueryGenerator](xref:api-DbSyncKit.MySQL.QueryGenerator)

```csharp
IQueryGenerator queryGenerator = new DbSyncKit.MySQL.QueryGenerator();
```

## For PostgreSQL
API Reference: [QueryGenerator](xref:api-DbSyncKit.PostgreSQL.QueryGenerator)

```csharp
IQueryGenerator queryGenerator = new DbSyncKit.PostgreSQL.QueryGenerator();
```

# 2. Synchronization Setup

To set up the synchronization process manually, you'll need to create instances of DbSyncKit components.

API Reference: [Synchronization](xref:api-DbSyncKit.Core.Synchronization)

```csharp
// manual synchronization setup
Synchronization Sync = new Synchronization();
```

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

# 4. Start Synchronization

Once everything is set up, you can start the synchronization process.

Proceed to the [Usage Guide](xref:usage) to learn how to perform synchronization tasks with DbSyncKit.

### Note
Manual setup provides more control but may require additional configuration compared to Dependency Injection (DI).
