﻿Title: Basic Synchronization
Order: 1
BreadcrumbTitle: Basic Synchronization
NavigationTitle: Basic Synchronization
ShowInSidebar: true
Xref: usage/basic-synchronization
---
In this guide, we'll walk through the process of performing a basic data synchronization operation using DbSyncKit.


# Prerequisites

Before we start, ensure that you have the following:

- [DbSyncKit.Core](xref:packages/DbSyncKit.Core) package installed
- [DbSyncKit.DB](xref:packages/DbSyncKit.DB) package installed
- Appropriate database provider package installed (e.g., [DbSyncKit.MSSQL](xref:packages/DbSyncKit.MSSQL), [DbSyncKit.MySQL](xref:packages/DbSyncKit.MySQL), [DbSyncKit.PostgreSQL](xref:packages/DbSyncKit.PostgreSQL))

# Setup

To begin, let's set up the necessary variables. For detailed setup instructions, refer to the [Setup Guide](xref:configuration).

Here's a brief summary of the variables:

- `IDatabase SourceDatabase`: Represents the source database connection.
- `IDatabase DestinationDatabase`: Represents the destination database connection.
- `Synchronization Sync`: Represents the DbSyncKit synchronization instance.

For detailed instructions on setting up these variables, refer to the [Setup Guide](xref:configuration).

# Perform Synchronization

Now that we have the variables set up, let's perform the synchronization. Replace `YourEntity` with the appropriate entity you want to synchronize.

```csharp
// Perform synchronization
Result<YourEntity> syncResult = Sync.SyncData<YourEntity>(SourceDatabase, DestinationDatabase);
```

The synchronization result provides detailed information about added, edited, and deleted records, along with the change type and data counts.

For more details on interpreting the synchronization result, refer to the [Synchronization Results Guide](xref:usage/synchronization-results).


# Manual Synchronization

To perform synchronization manually, follow these steps:

Certainly! Let's go through each step with detailed explanations and examples:

## 1) Setup
**Explanation:**
The setup step involves initializing variables and configurations necessary for synchronization.

**Code Example:**
```csharp
List<string> excludedProperty = Sync.GetExcludedColumns<YourEntity>();
List<string> columnList = Sync.GetAllColumns<YourEntity>().Except(excludedProperty).ToList();
PropertyInfo[] comparableProperties = Sync.GetComparableProperties<YourEntity>();
PropertyInfo[] keyProperties = Sync.GetKeyProperties<YourEntity>();
    
// Create equality comparers
object keyEqualityComparer = new PropertyEqualityComparer<YourEntity>(keyProperties);
object ComparablePropertiesComparer = new PropertyEqualityComparer<YourEntity>(comparableProperties);
    
// Get the table name
string tableName = Sync.GetTableName<YourEntity>();

// Result
Result<T> result;
```

## 2) Getting Data

In this step, data is retrieved from source and destination databases.

**Code Example:**
```csharp
// Use the synchronization instance to retrieve data
Sync.ContractFetcher.RetrieveDataFromDatabases<YourEntity>(Source, Destination, tableName, columnList, (PropertyEqualityComparer<T>)ComparablePropertiesComparer, out HashSet<T> SourceList, out HashSet<T> DestinationList);
```

## 3) Comparison

This step involves comparing the data from the source and destination databases.

**Code Example:**
```csharp
// Use the synchronization instance to get differences
result = Sync.MismatchIdentifier.GetDifferences<YourEntity>(sourceList, destinationList, (PropertyEqualityComparer<T>)keyEqualityComparer, (PropertyEqualityComparer<T>)ComparablePropertiesComparer);
```

## 4) Generating SQL Queries

This step generates SQL queries for synchronization based on the identified differences.

**Code Example:**
```csharp
Sync.QueryBuilder.GetSqlQueryForSyncData<YourEntity>(syncResult,Sync.ContractFetcher.DestinationQueryGenerationManager);
```

## 5) Cleanup

This step involves cleaning up resources or performing any necessary cleanup operations.

**Code Example:**
```csharp
DbSyncKit.DB.Manager.CacheManager.DisposeType(typeof(YourEntity));
```


---

Continue exploring other topics in the [Usage Guide](xref:usage).
