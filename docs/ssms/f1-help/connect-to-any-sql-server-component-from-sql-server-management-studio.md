---
title: Connect to Any SQL Server Component
description: "Connect to Any SQL Server Component from SQL Server Management Studio"
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: ui-reference
helpviewer_keywords: 
  - "connections [SQL Server], SQL Server Management Studio"
  - "saving connections"
  - "components [SQL Server], connections"
  - "SQL Server Management Studio [SQL Server], connections"
author: markingmyname
ms.author: maghan
ms.reviewer: ""
ms.custom: seo-lt-2019
ms.date: 01/19/2017
---

# Connect to any SQL Server component from SQL Server Management Studio

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] provides functionality for managing every component of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] to connect to:  

- An instance of the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)].  

- [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)].  

- [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  

- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  

Although [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] allows you to work with queries without first establishing a connection to a data source, most other tasks require a connection. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] provides the **Connect to Server** dialog box to configure connection properties to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] components. When [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] starts, it opens the **Connect to Server** dialog box and prompts you to connect to a server. The **Connect to Server** dialog box retains the connection settings from the last time it was used.

> [!NOTE]
> This feature can be turned off so no connection is automatically initiated. For more information, see [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md).

## Save connections

You can save connections to specific servers in Registered Servers, or you can save connections in projects with Solution Explorer.  

### Save connections in Registered Servers  

When you register a server, [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] saves the connection information in Registered Servers. To connect to a registered server, double-select the server name in Registered Servers. Object Explorer then opens a connection to the server.  

### Save connections in Solution Explorer

Solution Explorer allows you to store related queries, scripts, connections, and other associated information in a project. Each script project contains a node called **Connections**, where you can save one or more connections. To add a connection, right-select **Connections**, and then select **New Connection**. To access a saved connection, expand **Connections** and double-select the connection. 

[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] opens a query window associated with that connection. When saved, scripts retain their association to a specific connection.  
  
## See also

- [Use SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
- [Object Explorer](../../ssms/object/object-explorer.md)  
