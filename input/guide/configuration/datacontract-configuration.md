Title: DataContract Configuration
Order: 4
BreadcrumbTitle: DataContract Configuration
NavigationTitle: DataContract Configuration
ShowInSidebar: true
Xref: configuration/datacontract-configuration
---

To configure the actual data contract for entities, you can use attributes from the [DbSyncKit.DB.Attributes](xref:api-DbSyncKit.DB.Attributes) namespace. These attributes allow you to customize the behavior of synchronization for each table.

# Available Attributes for Configuration

- [TableName](xref:api-DbSyncKit.DB.Attributes.TableNameAttribute): Specifies the name of the table.
- [TableSchema](xref:api-DbSyncKit.DB.Attributes.TableSchemaAttribute): Specifies the schema of the table.
- [KeyProperty](xref:api-DbSyncKit.DB.Attributes.KeyPropertyAttribute): Defines a property as a key property.
    - [KeyProperty](xref:api-DbSyncKit.DB.Attributes.KeyPropertyAttribute.KeyProperty): Indicates whether the property should be considered as a key property. Default is `true`.
    - [IsPrimaryKey](xref:api-DbSyncKit.DB.Attributes.KeyPropertyAttribute.IsPrimaryKey): Indicates whether the property is a primary key. Default is `false`.
    - [IsComparable](xref:api-DbSyncKit.DB.Attributes.KeyPropertyAttribute.IsComparable): Indicates whether the property should be considered during the comparison process. Default is `false`.

- [ExcludedProperty](xref:api-DbSyncKit.DB.Attributes.ExcludedPropertyAttribute): Excludes a property from specific operations.
    - [Excluded](xref:api-DbSyncKit.DB.Attributes.ExcludedPropertyAttribute.Excluded): Indicates whether the property should be excluded from operations. Default is `true`.

- [GenerateInsertWithID](xref:api-DbSyncKit.DB.Attributes.GenerateInsertWithIDAttribute): Controls the inclusion of the ID property in the insert query generation, allowing fine-tuning of insertion behavior.
    - [GenerateWithID](xref:api-DbSyncKit.DB.Attributes.GenerateInsertWithIDAttribute.GenerateWithID): Determines whether the ID property should be included in the insert query generation. Possible values are `true` (to include the ID property) or `false` (to exclude the ID property).
    - [IncludeIdentityInsert](xref:api-DbSyncKit.DB.Attributes.GenerateInsertWithIDAttribute.IncludeIdentityInsert): Indicates whether to include database-specific SQL statements during insert query generation affecting identity insert behavior. The default value is `true`.

# IDataContract for Identification

The [`IDataContract`](xref:api-DbSyncKit.DB.Interface.IDataContract) interface serves as an identification marker for data contract classes. This interface doesn't include any properties but signifies a specific contract for identification purposes.


# Entity Configuration Examples

Here are some examples showcasing the use of attributes for configuring data contracts within DbSyncKit.

---
## Example 1 (Album)

To configure entities for example `Album` entity, apply attributes from the [DbSyncKit.DB.Attributes](xref:api-DbSyncKit.DB.Attributes) namespace to the entity class.

```csharp
using DbSyncKit.DB.Attributes;
using DbSyncKit.DB.Extensions;
using DbSyncKit.DB.Interface;

[TableName("Album")]
public class Album : IDataContract
{
    [KeyProperty(IsPrimaryKey: true)]
    public int AlbumId { get; set; }
    public string Title { get; set; }
    public int ArtistId { get; set; }

    public Album(DataRow albumInfo)
    {
        // Initialization code for Album properties from DataRow
    }
}
```
---

## Example 2

The `SampleEntity` entity demonstrates the use of various attributes for a more complex scenario.

```csharp
[TableName("SampleEntity"), TableSchema("dbo")]
public class SampleEntity : IDataContract
{
    [KeyProperty(IsPrimaryKey: true), ExcludedProperty]
    public long ID { get; set; }

    [KeyProperty]
    public long HeaderID { get; set; }

    [KeyProperty]
    public long EnumValue { get; set; }

    // Other Additional Properties

    [ExcludedProperty]
    public byte[] VersionNo { get; set; }

    public SampleEntity(DataRow sampleEntity)
    {
        // Initialization code for Entity properties from DataRow
    }
}
```

In the provided example (`SampleEntity` entity), the `ID` property is marked with the [`[ExcludedProperty]`](xref:api-DbSyncKit.DB.Attributes.ExcludedPropertyAttribute) attribute, indicating that this property should be excluded from certain operations, such as data fetching and query generation. The reason for excluding the `ID` property is that it is not required for the specific use case or scenario represented by the `SampleEntity` table.

In database tables, the concept of a primary key is crucial for uniquely identifying each row. In the context of the `SampleEntity` table, the properties `HeaderID` and `EnumValue` are designated as key properties using the `[KeyProperty]` attribute. These key properties serve as the main identifiers for individual rows in the table, allowing the system to distinguish one record from another.

Therefore, by excluding the `ID` property and emphasizing the `HeaderID` and `EnumValue` properties as key properties, the example communicates that the uniqueness and identification of rows in the `SampleEntity` table are achieved through the combination of `HeaderID` and `EnumValue`. The `ID` property, while present in the table, is intentionally excluded from certain operations, reflecting the specific needs and requirements of the data synchronization process for this entity.

The `VersionNo` property is marked with the [`[ExcludedProperty]`](xref:api-DbSyncKit.DB.Attributes.ExcludedPropertyAttribute) attribute, indicating that this property should be excluded from certain operations, especially in the context of Microsoft SQL Server (MSSQL). The decision to exclude `VersionNo` is specific to MSSQL synchronization requirements.

The `VersionNo` property might represent a versioning mechanism or a form of row version tracking in some database scenarios. However, in MSSQL databases, the row versioning might be handled differently, and the `VersionNo` property is not required for synchronization purposes. Therefore, excluding `VersionNo` ensures that the DbSyncKit library operates efficiently with MSSQL databases, focusing on the essential key properties (`HeaderID` and `EnumValue`) to identify and compare rows without considering the version-specific information.

### Note:
This exclusion aligns with the MSSQL-specific considerations for synchronization, where certain properties, like `VersionNo`, may not play a role in determining row changes or uniqueness across different MSSQL instances.

---

## Example 3

In the `SampleEntity` entity, the scenario involves a table where the `ID` property is designated as a primary key but is not set as an identity or auto-incrementing column. This requires the addition of the [`[GenerateInsertWithID(includeIdentityInsert: false)]`](xref:api-DbSyncKit.DB.Attributes.GenerateInsertWithIDAttribute) attribute to control the inclusion of the `ID` property in the insert query generation. By setting `includeIdentityInsert` to `false`, it signifies that the ID values won't be automatically generated by the database, and the application needs to handle the assignment of `ID` values during insert operations.

```csharp

[TableName("SampleEntity"), TableSchema("dbo"), GenerateInsertWithID(includeIdentityInsert: false)]
public class SampleEntity : IDataContract
{
    [KeyProperty(IsPrimaryKey: true)]
    public long ID { get; set; }

    [ExcludedProperty]
    public byte[] VersionNo { get; set; }

    // Other Additional Properties

    public SampleEntity(DataRow entityInfo)
    {
        // Initialization code for Entity properties from DataRow
    }
}
```

This configuration provides the necessary flexibility for managing primary key values manually in scenarios where the database does not handle automatic ID generation.

---

## Example 4 ( pivot )

In the `PlaylistTrack` entity, the scenario involves key properties that need to be compared during synchronization. The `IsComparable` property in the [`[KeyProperty]`](xref:api-DbSyncKit.DB.Attributes.KeyPropertyAttribute) attribute is set to `true` for both `PlaylistId` and `TrackId`.

```csharp
using DbSyncKit.DB.Attributes;
using DbSyncKit.DB.Extensions;
using DbSyncKit.DB.Interface;
using System.Data;

[TableName("PlaylistTrack")]
public class PlaylistTrack : IDataContract
{
    [KeyProperty(isPrimaryKey: true, isComparable: true)]
    public int PlaylistId { get; set; }

    [KeyProperty(isPrimaryKey: true, isComparable: true)]
    public int TrackId { get; set; }

    public PlaylistTrack(DataRow playlistTrackInfo)
    {
        if (playlistTrackInfo == null)
            throw new ArgumentNullException(nameof(playlistTrackInfo));

        PlaylistId = playlistTrackInfo.GetValue<int>("PlaylistId");
        TrackId = playlistTrackInfo.GetValue<int>("TrackId");
    }
}
```

In this example, the `IsComparable` property is set to `true` for both `PlaylistId` and `TrackId` properties, indicating that these key properties should be considered during the comparison process. This ensures that changes in these properties are taken into account during synchronization operations, providing a more granular control over which properties contribute to the detection of differences between rows. This configuration is especially relevant in scenarios like pivot tables, where key properties not only uniquely identify records but also contribute to the data that needs to be compared across different database instances.

It's important to note that if a key property is excluded from comparison (which is the default behavior for key properties), setting `isComparable: true` becomes necessary to include this property in data comparison during synchronization.

---

# Next Steps

Ready to implement data contract configurations in your DbSyncKit project? Continue exploring other guides and documentation to enhance your database synchronization workflow.

Explore the individual packages within DbSyncKit to understand their functionalities and choose the ones that suit your specific database environment:

- [DbSyncKit.Core](xref:packages/dbsynckit.core)
- [DbSyncKit.DB](xref:packages/dbsynckit.db)
- [DbSyncKit.MSSQL](xref:packages/dbsynckit.mssql)
- [DbSyncKit.MySQL](xref:packages/dbsynckit.mysql)
- [DbSyncKit.PostgreSQL](xref:packages/dbsynckit.postgresql)
- [DbSyncKit.Templates](xref:packages/dbsynckit.templates)
