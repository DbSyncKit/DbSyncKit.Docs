﻿﻿Title: Getting Started
Order: 4
BreadcrumbTitle: Getting Started
NavigationTitle: Getting Started
ShowInSidebar: true
Xref: overview/getting-started
---

To begin using DbSyncKit for your database synchronization needs, follow the steps outlined below. This guide covers the necessary installations and basic setup to get you started quickly.

# 1. Installation

DbSyncKit consists of several packages tailored to different aspects of database synchronization. Ensure you install the following packages based on your requirements:

## Core Packages

- [DbSyncKit.Core](xref:packages/dbsynckit.core)
- [DbSyncKit.DB](xref:packages/dbsynckit.db)

## Database-Specific Packages

Choose the appropriate package based on the database system you are working with:

- For Microsoft SQL Server: [DbSyncKit.MSSQL](xref:packages/dbsynckit.mssql)
- For MySQL: [DbSyncKit.MySQL](xref:packages/dbsynckit.mysql)
- For PostgreSQL: [DbSyncKit.PostgreSQL](xref:packages/dbsynckit.postgresql)
- For SQLite: [DbSyncKit.SQLite](xref:packages/dbsynckit.sqlite)

## Templating Packages

Enhance your synchronization workflows with the Templating feature. Install the Templating package along with database-specific Templating implementations:

- [DbSyncKit.Templates](xref:packages/dbsynckit.templates)
- For Microsoft SQL Server: [DbSyncKit.Templates.MSSQL](xref:packages/dbsynckit.templates.mssql)
- For MySQL: [DbSyncKit.Templates.MySQL](xref:packages/dbsynckit.templates.mysql)
- For PostgreSQL: [DbSyncKit.Templates.PostgreSQL](xref:packages/dbsynckit.templates.postgresql)
- For SQLite: [DbSyncKit.Templates.SQLite](xref:packages/dbsynckit.templates.sqlite)

Install these packages using your preferred package manager. For example, using NuGet:

```bash
dotnet add package DbSyncKit.Core
dotnet add package DbSyncKit.DB
dotnet add package DbSyncKit.MSSQL
dotnet add package DbSyncKit.MySQL
dotnet add package DbSyncKit.PostgreSQL
dotnet add package DbSyncKit.SQLite
dotnet add package DbSyncKit.Templates
dotnet add package DbSyncKit.Templates.MSSQL
dotnet add package DbSyncKit.Templates.MySQL
dotnet add package DbSyncKit.Templates.PostgreSQL
dotnet add package DbSyncKit.Templates.SQLite
```

Ensure your project is configured to use these packages.

# 2. Setup

Once you have installed the required packages, proceed with the initial setup. Configure DbSyncKit according to your synchronization needs by referring to the [Configuration Guide](xref:configuration).

# 3. Usage Guide

Explore the [Usage Guide](xref:usage) for detailed information on utilizing DbSyncKit for various synchronization tasks. This guide covers topics such as basic synchronization, entity configuration, attribute configuration, and more.

Ready to dive in? Start by installing the necessary packages and configuring DbSyncKit for your project!