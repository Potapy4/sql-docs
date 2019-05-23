---
title: Call Java from SQL Server
titleSuffix: SQL Server Language Extensions
description: Learn how to call Java classes from SQL Server stored procedures using the Java programming language extension in SQL Server 2019.
author: dphansen
ms.author: davidph 
manager: cgronlun
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: ">=sql-server-ver15||=sqlallproducts-allversions"
---
# How to call Java from SQL Server
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[SQL Server Language Extensions](../language-extensions-overview.md) uses the [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) system stored procedure as the interface to call the Java runtime. 

This how-to article explains implementation details for Java classes and methods that execute on SQL Server.

## Where to place Java classes

There are two methods for calling Java classes in SQL Server:

1. Place **.class** or **.jar** files in your [Java classpath](#classpath). 

2. Upload compiled classes in a **.jar** file and other dependencies into the database using the [external library](#external-library) DDL. 

> [!NOTE]
> As a general recommendation, use **.jar** files and not individual **.class** files. This is common practice in Java and will make the overall experience easier. See also, [How to create a jar file from class files](create-a-java-jar-file-from-class-files.md).

<a name="classpath"></a>

## Use Classpath

### Basic principles

The following are some basic principles when executing Java on SQL Server.

* Compiled custom Java classes must exist in **.class** files or **.jar** files in your Java classpath. The [CLASSPATH parameter](#set-classpath) provides the path to the compiled Java files. 

* The Java method you are calling must be provided in the **script** parameter on the stored procedure.

* If the class belongs to a package, the **packageName** must be provided.

* **params** is used to pass parameters to a Java class. Calling a method that requires arguments is not supported. Therefore, parameters the only way to pass argument values to your method. 

> [!NOTE]
> This note restates supported and unsupported operations specific to Java in CTP 3.0.
> * On the stored procedure, input parameters are supported. Output parameters are not.
> * Streaming using the sp_execute_external_script parameter @r_rowsPerRead is not supported.
> * Partitioning using @input_data_1_partition_by_columns is not supported.
> * Parallel processing using @parallel=1 is supported.

### Call Java class

The [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) system stored procedure is the interface used to call the Java runtime. The following example shows an `sp_execute_external_script` using the Java extension, and parameters for specifying path, script, and your custom code.

> [!NOTE]
> Note that you don't need to define which method to call. By default, a method called **execute** is called. This means that you need to follow the [Extensibility SDK for Java in SQL Server](extensibility-sdk-java-sql-server.md) and implement an execute method in your Java class.

```sql
DECLARE @param1 int
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>'
, @input_data_1 = N'<Input Query>'
, @param1 = @param1
```

<a name="set-classpath"></a>

### Set CLASSPATH

Once you have compiled your Java class or classes and created a jar file in your Java classpath, you have two options for providing the classpath to the SQL Server Java extension:

1. Use external libraries

    The easiest option is to make SQL Server automatically find your classes by creating external libraries and pointing the library to a jar. [Use external libraries for Java](#external-library)

2. Register a system environment variable

    You can create a system environment variable and provide the paths to your jar file that contains the classes. Create a system environment variable called **CLASSPATH**.

<a name="external-library"></a>

## Use external library

In SQL Server 2019 CTP 3.0, you can use external libraries for the Java language on Windows and Linux. You can compile your classes into a .jar file and upload the .jar file and other dependencies into the database using the [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) DDL.

Example of how to upload a .jar file with external library:

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

By creating an external library, SQL Server will automatically have access to the Java classes and you do not need to set any special permissions to the classpath.

Example of calling a method in a class from a package uploaded as an external library:

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

For more information, see [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## Next steps

+ [Tutorial: Search for a string using regular expressions in Java](../tutorials/search-for-string-using-regular-expressions-in-java.md)