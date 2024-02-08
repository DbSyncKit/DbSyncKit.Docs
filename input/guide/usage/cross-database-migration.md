﻿Title: Cross-Database Migration
Order: 5
BreadcrumbTitle: Cross-Database Migration
NavigationTitle: Cross-Database Migration
ShowInSidebar: true
Xref: usage/cross-database-migration
---

DbSyncKit allows you to perform cross-database migration, syncing data between different database providers. In this guide, we'll walk through a basic example of migrating data from MySQL to MSSQL.

# Setup

Let's start by setting up the necessary variables

```csharp
// Cross-Database Migration Setup
IDatabase Source = new DbSyncKit.MySQL.Connection("localhost", 3306, "SourceChinook", "root", "");
IDatabase Destination = new DbSyncKit.MSSQL.Connection("(localdb)\\MSSQLLocalDB", "DestinationChinook", true);
Synchronization Sync = new Synchronization();
```

# Perform Cross-Database Migration

Now that we have the variables set up, let's perform the cross-database migration. Replace `YourEntity` with the appropriate entity you want to synchronize.

```csharp
// A method to filter out the result data before creating a hashset (optional or you can pass null instead)
private List<YourEntity> FilterData(List<T> data)
{
    // filter your data here
    return data;
}

// Perform Cross-Database Migration
Result<YourEntity> migrationResult = Sync.SyncData<YourEntity>(Source, Destination, FilterData);
```

The migration result provides detailed information about added, edited, and deleted records, along with the change type and data counts.

For a more in-depth understanding of the synchronization process, including setup and interpreting the synchronization result, please refer to the [Basic Synchronization](xref:usage/basic-synchronization) guide.

# Generate SQL Query

To generate the SQL query corresponding to the migration, use the following code:

```csharp
// Generate SQL Query for Cross-Database Migration
var query = Sync.QueryBuilder.GetSqlQueryForSyncData(migrationResult,Sync.ContractFetcher.DestinationQueryGenerationManager);
```


### Importatant

Please note that **SQL queries generated** should be based on the **destination [IDatabase](xref:api-DbSyncKit.DB.Interface.IDatabase)** or [**IQueryGenerator**](xref:api-DbSyncKit.DB.Interface.IQueryGenerator) Instance.

For instance, when fetching data for synchronization using the [DataContractFetcher](xref:api-DbSyncKit.Core.Fetcher.DataContractFetcher) from the [Synchronization](xref:api-DbSyncKit.Core.Synchronization) instance, you can leverage the **IQueryGenerator** instance obtained during the data retrieval process.

Proceed to the [Usage Guide](xref:usage) for more comprehensive guidance on using DbSyncKit with different scenarios.