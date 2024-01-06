﻿Title: DbSyncKit.Templates.MySQL
Order: 8
BreadcrumbTitle: DbSyncKit.Templates.MySQL
NavigationTitle: DbSyncKit.Templates.MySQL
ShowInSidebar: true
Xref: packages/dbsynckit.templates.mysql
---

# Introduction

DbSyncKit.Templates.MySQL is a dedicated package providing SQL query templates designed for MySQL databases. It facilitates the generation of SQL queries for synchronization, making the process seamless.

# Installation

To install the DbSyncKit.Templates.MySQL package, use the following NuGet Package Manager command:

```bash
dotnet add package DbSyncKit.Templates.MySQL
```

Ensure that you include the appropriate version based on your project requirements.

# Usage

## Query Templates

The package includes implementations of `IQueryTemplates` for MySQL, offering templates for various SQL queries:

- **Select Template**: `QueryTemplates.SelectTemplate`
- **Insert Template**: `QueryTemplates.InsertTemplate`
- **Update Template**: `QueryTemplates.UpdateTemplate`
- **Delete Template**: `QueryTemplates.DeleteTemplate`
- **Comment Template**: `QueryTemplates.CommentTemplate`

## Integration with DbSyncKit

For more detailed information and examples, refer to the [API Reference](xref:api-DbSyncKit.Templates.MySQL).
