﻿Title: DbSyncKit.Templates.MSSQL
Order: 7
BreadcrumbTitle: DbSyncKit.Templates.MSSQL
NavigationTitle: DbSyncKit.Templates.MSSQL
ShowInSidebar: true
Xref: packages/dbsynckit.templates.mssql
---

# Introduction

DbSyncKit.Templates.MSSQL is a specialized package offering SQL query templates tailored for Microsoft SQL Server (MSSQL). It simplifies the process of generating SQL queries for synchronization in MSSQL databases.

# Installation

To install the DbSyncKit.Templates.MSSQL package, use the following NuGet Package Manager command:

```bash
dotnet add package DbSyncKit.Templates.MSSQL
```

Make sure to include the appropriate version based on your project requirements.

# Usage

## Query Templates

The package provides implementations of `IQueryTemplates` for MSSQL, offering templates for various SQL queries:

- **Select Template**: `QueryTemplates.SelectTemplate`
- **Insert Template**: `QueryTemplates.InsertTemplate`
- **Update Template**: `QueryTemplates.UpdateTemplate`
- **Delete Template**: `QueryTemplates.DeleteTemplate`
- **Comment Template**: `QueryTemplates.CommentTemplate`

## Integration with DbSyncKit

For more detailed information and examples, refer to the [API Reference](xref:api-DbSyncKit.Templates.MSSQL).
