﻿Title: DbSyncKit.Templates.PostgreSQL
Order: 9
BreadcrumbTitle: DbSyncKit.Templates.PostgreSQL
NavigationTitle: DbSyncKit.Templates.PostgreSQL
ShowInSidebar: true
Xref: packages/dbsynckit.templates.postgresql
---

# Introduction

DbSyncKit.Templates.PostgreSQL is a dedicated package providing SQL query templates tailored for PostgreSQL databases. It simplifies the generation of SQL queries for synchronization, streamlining the data synchronization process.

# Installation

To install the DbSyncKit.Templates.PostgreSQL package, use the following NuGet Package Manager command:

```bash
dotnet add package DbSyncKit.Templates.PostgreSQL
```

Make sure to include the appropriate version based on your project requirements.

# Usage

## Query Templates

The package includes implementations of `IQueryTemplates` for PostgreSQL, offering templates for various SQL queries:

- **Select Template**: `QueryTemplates.SelectTemplate`
- **Insert Template**: `QueryTemplates.InsertTemplate`
- **Update Template**: `QueryTemplates.UpdateTemplate`
- **Delete Template**: `QueryTemplates.DeleteTemplate`
- **Comment Template**: `QueryTemplates.CommentTemplate`

## Integration with DbSyncKit

For more detailed information and examples, refer to the [API Reference](xref:api-DbSyncKit.Templates.PostgreSQL).