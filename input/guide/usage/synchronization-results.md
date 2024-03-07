﻿Title: Synchronization Results
Order: 3
BreadcrumbTitle: Synchronization Results
NavigationTitle: Synchronization Results
ShowInSidebar: true
Xref: usage/synchronization-results
---

After performing a synchronization operation with DbSyncKit, you receive a [`Result<T>`](xref:api-DbSyncKit.Core.DataContract.Result-T-) object that provides detailed information about the changes made during the process.

# Result Properties

## 1. [Added](xref:api-DbSyncKit.Core.DataContract.Result-T-.Added)

Represents the list of entities that were added during synchronization. Each entity corresponds to a data record added to the destination database.

## 2. [Deleted](xref:api-DbSyncKit.Core.DataContract.Result-T-.Deleted)

Represents the list of entities that were deleted during synchronization. Each entity corresponds to a data record deleted from the destination database.

## 3. [Edited](xref:api-DbSyncKit.Core.DataContract.Result-T-.Edited)

Represents the list of entities that were edited during synchronization.

## 4. [EditedDetailed](xref:api-DbSyncKit.Core.DataContract.Result-T-.EditedDetailed)

Represents the list of entities that were edited during synchronization. Each item in the list is a tuple containing the edited entity and a dictionary of updated properties. The dictionary provides information about the properties that were modified and their new values.


## 5. [SourceDataCount](xref:api-DbSyncKit.Core.DataContract.Result-T-.SourceDataCount)

Represents the count of data records in the source database before synchronization.

## 6. [DestinaionDataCount](xref:api-DbSyncKit.Core.DataContract.Result-T-.DestinaionDataCount)

Represents the count of data records in the destination database before synchronization.

## 7. [ResultChangeType](xref:api-DbSyncKit.Core.DataContract.Result-T-.ResultChangeType)

Indicates the type of change represented by the synchronization result. Possible values are [ChangeType.Added](xref:api-DbSyncKit.Core.Enum.ChangeType.Added), [ChangeType.Edited](xref:api-DbSyncKit.Core.Enum.ChangeType.Edited), [ChangeType.Deleted](xref:api-DbSyncKit.Core.Enum.ChangeType.Deleted).

# Example Usage

Here's an example of how to use the synchronization result:

```csharp
// A method to filter out the result data before creating a hashset (optional or you can pass null instead)
private List<YourEntity> FilterData(List<T> data)
{
    // filter your data here
    return data;
}

// Perform synchronization
Result<YourEntity> syncResult = Sync.SyncData<YourEntity>(SourceDatabase, DestinationDatabase,FilterData);

// Accessing synchronization result properties & getting its count
Console.WriteLine($"Added: {data.Added.Count} EditedDetailed: {data.EditedDetailed.Count} Deleted: {data.Deleted.Count}");
Console.WriteLine($"Total Source Data: {syncResult.SourceDataCount}");
Console.WriteLine($"Total Destination Data: {syncResult.DestinaionDataCount}");
Console.WriteLine($"Change Type: {syncResult.ResultChangeType}");
```

Understanding the synchronization result is crucial for analyzing the impact of the synchronization operation and making informed decisions based on the changes detected.

Continue exploring other topics in the [Usage Guide](xref:usage).