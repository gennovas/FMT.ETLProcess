# FMT - ETL Automation Workflow
[![Microsoft SQL Server](https://img.shields.io/badge/Microsoft-SQL%20Server-blue)](https://learn.microsoft.com/en-us/sql/sql-server/)
[![SQL Integration Service](https://img.shields.io/badge/SSIS-Integration%20Service-orange)](https://learn.microsoft.com/en-us/sql/integration-services/)
[![XLSX](https://img.shields.io/badge/File-XLSX-green)](https://en.wikipedia.org/wiki/Microsoft_Excel#File_formats)
[![CSV](https://img.shields.io/badge/File-CSV-yellow)](https://en.wikipedia.org/wiki/Comma-separated_values)
[![OLE DB](https://img.shields.io/badge/Database-OLEDB-red)](https://learn.microsoft.com/en-us/sql/ado/guide/data/oledb-provider-for-sql-server)
[![ADO.NET](https://img.shields.io/badge/.NET-ADO.NET-blueviolet)](https://learn.microsoft.com/en-us/dotnet/framework/data/adonet/)
[![Flat File](https://img.shields.io/badge/File-FlatFile-lightgrey)](https://en.wikipedia.org/wiki/Flat_file_database)
[![UTF-8](https://img.shields.io/badge/Encoding-UTF--8-brightgreen)](https://en.wikipedia.org/wiki/UTF-8)
[![Unicode](https://img.shields.io/badge/Encoding-Unicode-blue)](https://en.wikipedia.org/wiki/Unicode)
[![Infor CloudSuite Industrial](https://img.shields.io/badge/Infor-CloudSuite%20Industrial-orange)](https://www.infor.com/solutions/cloudsuite-industrial)

# 📌 Project Parameters

This document provides an overview of the project parameters used in the **FMT - ETL Automation Workflow**.  
These parameters are required for proper configuration of file processing and database connections.

---

## ⚙️ Parameters Overview

| **Name**            | **DataType** | **Value**                       | **Sensitive**     | **Required**| **Description**
|---------------------|--------------|---------------------------------|-------------------|-------------|----------------------------------------------------
| **ApplicationName** | `String`     | `FMT - ETL Automation Workflow` | False             | True        | Application name                    
| **FileSpec830**     | `String`     | `830*.csv`                      | False             | True        | File specification for **830** CSV files 
| **FileSpec862**     | `String`     | `862*.csv`                      | False             | True        | File specification for **862** CSV files 
| **FileSpecFS01**    | `String`     | `export??????????????.xlsx`     | False             | True        | File specification for **FS01** Excel files 
| **FileSpecFS02**    | `String`     | `export??????????????*.xlsx`    | False             | True        | File specification for **FS02** Excel files
| **SLSite**          | `String`     | `FMT`                           | False             | True        | SyteLine site reference for processing 
| **SQLDatabaseName** | `String`     | `FMT_PRD_App`                   | False             | True        | Target SQL Database name 
| **SQLServerName**   | `String`     | `FMT-SQLDB`                     | False             | True        | Target SQL Server instance name 

---

## 📂 File Specifications

- **📑 830 Files:** `830*.csv`  
- **📑 862 Files:** `862*.csv`  
- **📑 FS01:** `export??????????????.xlsx`  
- **📑 FS02:** `export??????????????*.xlsx`  

---
## User Defined Type

**1. ExportPlant**
- **Value** = ShipToCode column in (F830, F862), CustLoc column in (FS01, FS02)  
- **Description** = Weekday name
- 
| Value   | Description |
|---------|------------|
| GBJWA   | Thursday   |
| GBJWC   | Wednesday  |
| GK0VH   | Tuesday    |
| PL155D  | Monday     |
| PLF30A  | Friday     |
| PLF31A  | Saturday   |

---
## 🔌 Connections

### 🔷 OLE DB Connections
- **Microsoft.ACE.OLEDB.12.0** → Extended Properties:`"Excel 12.0 Xml;HDR=NO;IMEX=1;"` _(Excel Connection)_ [Download Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/en-us/download/details.aspx?id=54920)
- **SQL Native Client 11.0**

### 🔷 ADO.NET Connections
- **SQLClient Data Provider**

### 🔷 Flat File Connection Properties

| **Name**              | **Value**  | **Description**          
|-----------------------|----------- |--------------------------
| **CodePage**          | `65001`    | UTF-8 encoding           
| **Format**            | `Delimited`| Comma `{,}` delimiter 
| **HeaderRowDelimiter**| `{CR}{LF}` | Line break delimiter    
| **HeaderRowsToSkip**  | `0`        | Number of header rows to skip 

---

## 🗄️ SQL Server Database Connection

- **🖥️ Server:** `FMT-SQLDB`  
- **🗄️ Database:** `FMT_PRD_App`  
- **🏭 Site Code:** `FMT`  

---

## ✅ Usage Notes

- 🔴 **Required** → must be set before running the workflow.  
- 🟢 **Not Sensitive** → no encryption needed for storage.  
- `*` and `?` wildcards are supported in FileSpec patterns.  
- Ensure SQL Server and file system connectivity before execution.  

---
## Package Structure  

**ExportF862-Csv.dtsx**
```
Executables  
├─ Execute SQL Task - Get Export Location  
├─ Execute SQL Task - Validate Export Location  
├─ Execute SQL Task - Get Export Data  
└─ Foreach Loop Container - Read Source File F862  
   ├─ Execute SQL Task - Get Plant Code  
   └─ Foreach Loop Container - Export File  
      ├─ Execute SQL Task - BEGIN TRANSACTION  
      ├─ Data Flow Task - Export File  
      │  ├─ OLE DB Source  
      │  ├─ Data Conversion  
      │  └─ Flat File Destination  
      ├─ Execute SQL Task - Update Exported File Names  
      └─ Execute SQL Task - COMMIT TRANSACTION  
Event Handlers (OnError)  
└─ Executables  
   ├─ Execute SQL Task - Logging Exception Message  
   └─ Execute SQL Task - ROLLBACK TRANSACTION  
```  
**ImportF830-Csv.dtsx**  
```  
Executables  
├─ Execute SQL Task - Get Source File Location  
├─ Execute SQL Task - Validate Source File Location  
├─ Execute SQL Task - Get Imported File Location  
├─ Execute SQL Task - Validate Imported File Location  
├─ Execute SQL Task - Get Exception File Location  
├─ Execute SQL Task - Validate Exception File Location  
└─ Foreach Loop Container - Read F830 Files  
   ├─ Execute SQL Task - BEGIN TRANSACTION  
   ├─ Execute SQL Task - Create File Log  
   ├─ Data Flow Task - Import F830  
   │  ├─ Flat File Source  
   │  ├─ Derived Column  
   │  └─ OLE DB Destination  
   ├─ Execute SQL Task - Perform Forecast Data  
   ├─ Execute SQL Task - Create Forecast  
   ├─ Execute SQL Task - Update File Status  
   ├─ File System Task - Move File To Imported Folder  
   └─ Execute SQL Task - COMMIT TRANSACTION   
Event Handlers (OnError)  
└─ Executables  
   ├─ Execute SQL Task - ROLLBACK TRANSACTION  
   ├─ Execute SQL Task - Logging Exception Message  
   └─ File System Task - Move File To Exception Folder
```  
**ImportF862-Csv.dtsx**  
```  
Executables  
├─ Execute SQL Task - Get Source File Location  
├─ Execute SQL Task - Validate Source File Location  
├─ Execute SQL Task - Get Imported File Location  
├─ Execute SQL Task - Validate Imported File Location  
├─ Execute SQL Task - Get Exception File Location  
├─ Execute SQL Task - Validate Exception File Location  
└─ Foreach Loop Container - Read F862 Files  
   ├─ Execute SQL Task - BEGIN TRANSACTION  
   ├─ Execute SQL Task - Create File Log  
   ├─ Data Flow Task - Import F862  
   │  ├─ Flat File Source  
   │  ├─ Derived Column  
   │  └─ OLE DB Destination  
   ├─ Execute SQL Task - Convert Msg_Ref_Num  
   ├─ Execute SQL Task - Perform Forecast Data  
   ├─ Execute SQL Task - Create Forecast  
   ├─ Execute SQL Task - Update File Status  
   ├─ File System Task - Move File To Imported Folder  
   └─ Execute SQL Task - COMMIT TRANSACTION  
Event Handlers (OnError)  
└─ Executables  
   ├─ Execute SQL Task - ROLLBACK TRANSACTION  
   ├─ Execute SQL Task - Logging Exception Message  
   └─ File System Task - Move File To Exception Folder  
```  
**ImportFS01-Xlsx.dtsx**  
```  
Executables  
├─ Execute SQL Task - Get Source File Location  
├─ Execute SQL Task - Validate Source File Location  
├─ Execute SQL Task - Get Imported File Location  
├─ Execute SQL Task - Validate Imported File Location  
├─ Execute SQL Task - Get Exception File Location  
├─ Execute SQL Task - Validate Exception File Location  
└─ Foreach Loop Container - Read FS01 Files  
   ├─ Execute SQL Task - BEGIN TRANSACTION  
   ├─ Execute SQL Task - Create File Log  
   ├─ Execute SQL Task - Get B1 Value  
   ├─ Script Task - Get B1 Value  
   ├─ Execute SQL Task - Get Excel Data  
   ├─ Script Task - Import FS01 Data  
   ├─ Execute SQL Task - Perform Forecast Data  
   ├─ Execute SQL Task - Create Forecast  
   ├─ Execute SQL Task - Update File Status  
   ├─ File System Task - Move File To Imported Folder  
   └─ Execute SQL Task - COMMIT TRANSACTION  
Event Handlers (OnError)  
└─ Executables  
   ├─ Execute SQL Task - ROLLBACK TRANSACTION  
   ├─ Execute SQL Task - Logging Exception Message  
   └─ File System Task - Move File To Exception Folder  
```  
**ImportFS02-Xlsx.dtsx**  
``` 
Executables  
├─ Execute SQL Task - Get Source File Location  
├─ Execute SQL Task - Validate Source File Location  
├─ Execute SQL Task - Get Imported File Location  
├─ Execute SQL Task - Validate Imported File Location  
├─ Execute SQL Task - Get Exception File Location  
├─ Execute SQL Task - Validate Exception File Location  
└─ Foreach Loop Container - Read FS02 Files  
   ├─ Execute SQL Task - BEGIN TRANSACTION  
   ├─ Execute SQL Task - Create File Log  
   ├─ Execute SQL Task - Get Excel Data  
   ├─ Script Task - Import FS02 Data  
   ├─ Execute SQL Task - Perform Forecast Data  
   ├─ Execute SQL Task - Create Forecast  
   ├─ Execute SQL Task - Update File Status  
   ├─ File System Task - Move File To Imported Folder  
   └─ Execute SQL Task - COMMIT TRANSACTION  
Event Handlers (OnError)  
└─ Executables  
   ├─ Execute SQL Task - ROLLBACK TRANSACTION  
   ├─ Execute SQL Task - Logging Exception Message  
   └─ File System Task - Move File To Exception Folder
``` 
