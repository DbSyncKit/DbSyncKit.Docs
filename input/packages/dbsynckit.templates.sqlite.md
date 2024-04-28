﻿Title: DbSyncKit.Templates.SQLite
Order: 9
BreadcrumbTitle: DbSyncKit.Templates.SQLite
NavigationTitle: DbSyncKit.Templates.SQLite
ShowInSidebar: true
Xref: packages/dbsynckit.templates.sqlite
---

# Introduction

DbSyncKit.Templates.SQLite is a dedicated package providing SQL query templates tailored for SQLite databases. It simplifies the generation of SQL queries for synchronization, streamlining the data synchronization process.

# Installation

To install the DbSyncKit.Templates.SQLite package, use the following NuGet Package Manager command:

```bash
dotnet add package DbSyncKit.Templates.SQLite
```

Make sure to include the appropriate version based on your project requirements.

# Usage

## Query Templates

The package includes implementations of `IQueryTemplates` for SQLite, offering templates for various SQL queries:

- **Select Template**: `QueryTemplates.SelectTemplate`
- **Insert Template**: `QueryTemplates.InsertTemplate`
- **Update Template**: `QueryTemplates.UpdateTemplate`
- **Delete Template**: `QueryTemplates.DeleteTemplate`
- **Comment Template**: `QueryTemplates.CommentTemplate`

## Integration with DbSyncKit

For more detailed information and examples, refer to the [API Reference](xref:api-DbSyncKit.Templates.SQLite).