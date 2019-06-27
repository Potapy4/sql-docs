---
title: Install big data tools
titleSuffix: SQL Server big data clusters
description: Learn how to install tools used with SQL Server 2019 big data clusters (preview).
author: rothja 
ms.author: jroth 
manager: jroth
ms.date: 01/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
---

# Install SQL Server 2019 big data tools

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

This article describes the client tools that should be installed for creating, managing, and using SQL Server 2019 big data clusters (preview). The following section provides a list of tools and links to installation instructions. Before deploying a big data cluster, configure the tools marked required on Windows or Linux.

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## Big data cluster tools

The following table lists common big data cluster tools and how to install them:

| Tool | Required | Description | Installation |
|---|---|---|---|
| **mssqlctl** | Yes | Command-line tool for installing and managing a big data cluster. | [Install](deploy-install-mssqlctl.md) |
| **kubectl**<sup>1</sup> | Yes | Command-line tool for monitoring the underlying Kuberentes cluster ([More info](https://kubernetes.io/docs/tasks/tools/install-kubectl/)). | [Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-with-powershell-from-psgallery) \| [Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-native-package-management) |
| **Azure Data Studio (insiders)** | Yes | Cross-platform graphical tool for querying SQL Server ([More info](https://docs.microsoft.com/sql/azure-data-studio/what-is?view=sql-server-ver15)). | [Install](https://aka.ms/azdata-insiders) |
| **SQL Server 2019 extension** | Yes | Extension for Azure Data Studio that supports connecting to the big data cluster. Also provides a Data Virtualization wizard. | [Install](../azure-data-studio/sql-server-2019-extension.md) |
| **Azure CLI**<sup>2</sup> | For AKS | Modern command-line interface for managing Azure services. Used with AKS big data cluster deployments ([More info](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)). | [Install](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) |
| **mssql-cli** | Optional | Modern command-line interface for querying SQL Server ([More info](https://github.com/dbcli/mssql-cli/blob/master/README.rst)). | [Windows](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/windows.md) \| [Linux](https://github.com/dbcli/mssql-cli/blob/master/doc/installation/linux.md) |
| **sqlcmd** | For some scripts | Legacy command-line tool for querying SQL Server ([More info](https://docs.microsoft.com/sql/tools/sqlcmd-utility?view=sql-server-ver15)). | [Windows](https://www.microsoft.com/download/details.aspx?id=36433) \| [Linux](../linux/sql-server-linux-setup-tools.md) |
| **curl** <sup>3</sup> | For some scripts | Command-line tool for transferring data with URLs. | [Windows](https://curl.haxx.se/windows/) \| Linux: install curl package |

<sup>1</sup> You must use kubectl version 1.10 or later. Also, the version of kubectl should be plus or minus one minor version of your Kubernetes cluster. If you want to install a specific version on kubectl client, see [Install kubectl binary via curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl) (on Windows 10, use cmd.exe and not Windows PowerShell to run curl). 

> [!TIP]
> To use kubectl with a previously deployed cluster on Azure Kubernetes Service (AKS), you must set the cluster context with the following Azure CLI command:
>
>    ```azurecli
>    az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>
>    ```

<sup>2</sup> You must be using Azure CLI version 2.0.4 or later. Run `az --version` to find the version if needed.

<sup>3</sup> If you are running on Windows 10, **curl** is already in your PATH when running from a cmd prompt. For other versions of Windows, download **curl** using the link and place it in your PATH.

## Which tools are required?

The previous table provides all of the common tools that are used with big data clusters. Which tools are required depends on your scenario. But in general, the following tools are most important for managing, connecting to, and querying the cluster:

- **mssqlctl**
- **kubectl**
- **Azure Data Studio**
- **SQL Server 2019 extension**

The remaining tools are only required in certain scenarios. **Azure CLI** can be used to manage Azure services associated with AKS deployments. **mssql-cli** is an optional but useful tool that allows you to connect to the SQL Server master instance in the cluster and run queries from the command line. And **sqlcmd** and **curl** are required if you plan to install sample data with the GitHub script.

## Next steps

After configuring the tools, deploy a SQL Server 2019 big data cluster to Kubernetes in the Cloud or on-premises. For more information, see the following deployment articles:

- [Quickstart: Deploy SQL Server big data cluster on Azure Kubernetes Service (AKS)](quickstart-big-data-cluster-deploy.md)
- [How to deploy SQL Server big data clusters on Kubernetes](deployment-guidance.md)

For More info about big data clusters, see [What are SQL Server 2019 big data clusters?](big-data-cluster-overview.md).
