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

**ExportPlant**
- **Value** = ShipToCode column in (F830, F862), CustLoc column in (FS01, FS02)  
- **Description** = Weekday name
  
**Example**
  
| Value   | Description |
|---------|------------|
| GBJWA   | Thursday   |
| GBJWC   | Wednesday  |
| GK0VH   | Tuesday    |
| PL155D  | Monday     |
| PLF30A  | Friday     |
| PLF31A  | Saturday   |

**FordImportPath**
- **Value** = Path name  
- **Description** = Directory

**Example**

| Value         | Description           |
|---------------|---------------------|
| PathException | C:\ETL\ImportException\ |
| PathExportF862| C:\ETL\ExportF862\      |
| PathFrom      | C:\ETL\FordOrder\       |
| PathTo        | C:\ETL\FordImported\    |

**ProductMap**
- **Value** = Product column in FS01, FS02  
- **Description** = SyteLine item code

**Example**

| Value        | Description |
|--------------|------------|
| GN1Z5035E    | SP06-04-N  |
| GN1Z5500A    | SP06-05-N  |
| GN1Z5500C    | SP06-06-N  |
| GN1Z5500D    | SP06-07-N  |
| GN1Z5500E    | SP06-08-N  |
| GN1Z5500F    | SP06-09-N  |
| GN1Z5A757A   | SP06-10-N  |
| GN1Z5A758A   | SP06-11-N  |
| JB3Z17A954B  | SP07-02-N  |
| JB3Z17A954C  | SP07-04-N  |
| MB3Z17A954L  | SP07-05-N  |
| MB3Z17A954M  | SP07-06-N  |
| MB3Z17A955J  | SP07-07-N  |
| MB3Z17A955K  | SP08-04-N  |
| MB3Z6G079G   | SP08-05-N  |

**PlantCodeMap**
- **Value** = CustLoc column in FS01, FS02  
- **Description** = Plant code

**Example**

| Value    | Description |
|----------|------------|
| PL155D   | A155D      |
| PLF30A   | AF30A      |
| PLF31A   | AF31A      |

---
## UET User Fields

| User Field Name | User Data Type | Data Type | Precision | Decimals | Initial Value | Description |
|-----------------|----------------|----------|-----------|----------|---------------|------------|
| Uf_FCType       |                | tinyint  |           |          |  1            |            |
| Uf_FileName     |                | nvarchar | 3800      |          |               |            |

## UET Classes

| Class Name     | Label | Description |
|----------------|-------|------------|
| Uc_Forecast    |       |            |

## UET Class/Field Relationships

| Class Name    | Field Name  |
|---------------|------------|
| Uc_Forecast   | Uf_FCType  |
| Uc_Forecast   | Uf_FileName|

## UET Table/Class Relationships

| Table Name      | Class Name   | Active | Extend All Records | Rule |
|-----------------|-------------|--------|------------------|------|
| forecast_mst    | Uc_Forecast | 1      | 0                |      |

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
---
# Example Files (Raw Links)

## 1. F830
- [830_20250421082805_VP1U53B901 - Orginal.csv](https://raw.githubusercontent.com/gennovas/FMT.ETLProcess/main/Example%20Files/830_20250421082805_VP1U53B901%20-%20Orginal.csv)  
- [830_20250421082805_VP1U53B902 - Orginal.csv](https://raw.githubusercontent.com/gennovas/FMT.ETLProcess/main/Example%20Files/830_20250421082805_VP1U53B902%20-%20Orginal.csv)  

## 2. F862
- [862_20250623081103_VP1U55NW9R.csv](https://raw.githubusercontent.com/gennovas/FMT.ETLProcess/main/Example%20Files/862_20250623081103_VP1U55NW9R.csv)  
- [862_20250623081103_VP1U55NW9S.csv](https://raw.githubusercontent.com/gennovas/FMT.ETLProcess/main/Example%20Files/862_20250623081103_VP1U55NW9S.csv)  

## 3. FS01
- [export20250622220316.xlsx](https://raw.githubusercontent.com/gennovas/FMT.ETLProcess/main/Example%20Files/export20250622220316.xlsx)  
- [export20250622220317.xlsx](https://raw.githubusercontent.com/gennovas/FMT.ETLProcess/main/Example%20Files/export20250622220317.xlsx)  

## 4. FS02
- [export20250622220454 FSST.xlsx](https://raw.githubusercontent.com/gennovas/FMT.ETLProcess/main/Example%20Files/export20250622220454%20FSST.xlsx)  
- [export20250622220455 FSST.xlsx](https://raw.githubusercontent.com/gennovas/FMT.ETLProcess/main/Example%20Files/export20250622220455%20FSST.xlsx)  

---
# Column Mapping

## 1. F830

| Source Column Name   | Source Data Type/Size              | Destination Column Name | Destination Data Type/Size |
|----------------------|------------------------------------|--------------------------|-----------------------------|
| Ctrl_Num             | Unicode string [DT_WSTR]/10        | Ctrl_Num                 | nvarchar/10                 |
| Msg_Num              | Unicode string [DT_WSTR]/10        | Msg_Num                  | nvarchar/10                 |
| Msg_RealseDate       | Unicode string [DT_WSTR]/8         | Msg_RealseDate           | nvarchar/8                  |
| Msg_Purpose          | Unicode string [DT_WSTR]/8         | Msg_Purpose              | nvarchar/8                  |
| ScheduleType         | Unicode string [DT_WSTR]/10        | ScheduleType             | nvarchar/10                 |
| StartDate            | Unicode string [DT_WSTR]/8         | StartDate                | nvarchar/8                  |
| EndDate              | Unicode string [DT_WSTR]/8         | EndDate                  | nvarchar/8                  |
| Note                 | Unicode string [DT_WSTR]/50        | Note                     | nvarchar/50                 |
| ShipToCode           | Unicode string [DT_WSTR]/15        | ShipToCode               | nvarchar/15                 |
| ShipFromCode         | Unicode string [DT_WSTR]/15        | ShipFromCode             | nvarchar/15                 |
| Consignee            | Unicode string [DT_WSTR]/15        | Consignee                | nvarchar/15                 |
| PartNum              | Unicode string [DT_WSTR]/40        | PartNum                  | nvarchar/40                 |
| PO_num               | Unicode string [DT_WSTR]/40        | PO_num                   | nvarchar/40                 |
| ReleaseStatus        | Unicode string [DT_WSTR]/10        | ReleaseStatus            | nvarchar/10                 |
| DockCode             | Unicode string [DT_WSTR]/10        | DockCode                 | nvarchar/10                 |
| LineFeed             | Unicode string [DT_WSTR]/10        | LineFeed                 | nvarchar/10                 |
| ReserveLineFeed      | Unicode string [DT_WSTR]/10        | ReserveLineFeed          | nvarchar/10                 |
| ContactName          | Unicode string [DT_WSTR]/50        | ContactName              | nvarchar/50                 |
| ContactTelephone     | Unicode string [DT_WSTR]/15        | ContactTelephone         | nvarchar/15                 |
| FabAuthQty           | numeric [DT_NUMERIC]               | FabAuthQty               | int                         |
| FabAuthStartDate     | Unicode string [DT_WSTR]/8         | FabAuthStartDate         | nvarchar/8                  |
| FabAuthEndDate       | Unicode string [DT_WSTR]/8         | FabAuthEndDate           | nvarchar/8                  |
| MatAuthQty           | numeric [DT_NUMERIC]               | MatAuthQty               | int                         |
| MatAuthStartDate     | Unicode string [DT_WSTR]/8         | MatAuthStartDate         | nvarchar/8                  |
| MatAuthEndDate       | Unicode string [DT_WSTR]/8         | MatAuthEndDate           | nvarchar/8                  |
| LastReceivedASNNum   | Unicode string [DT_WSTR]/10        | LastReceivedASNNum       | nvarchar/10                 |
| LastShippedQty       | numeric [DT_NUMERIC]               | LastShippedQty           | int                         |
| LastShippedDate      | Unicode string [DT_WSTR]/8         | LastShippedDate          | nvarchar/8                  |
| CumShippedQty        | numeric [DT_NUMERIC]               | CumShippedQty            | int                         |
| CumStartDate         | Unicode string [DT_WSTR]/8         | CumStartDate             | nvarchar/8                  |
| CumEndDate           | Unicode string [DT_WSTR]/8         | CumEndDate               | nvarchar/8                  |
| ForecastCumQty       | numeric [DT_NUMERIC]               | ForecastCumQty           | int                         |
| ForecastNetQty       | numeric [DT_NUMERIC]               | ForecastNetQty           | int                         |
| UOM                  | Unicode string [DT_WSTR]/4         | UOM                      | nvarchar/4                  |
| ForecastStatus       | Unicode string [DT_WSTR]/4         | ForecastStatus           | nvarchar/4                  |
| ForecastDate         | Unicode string [DT_WSTR]/8         | ForecastDate             | nvarchar/8                  |
| FlexFCStartDate      | Unicode string [DT_WSTR]/8         | FlexFCStartDate          | nvarchar/8                  |
| FlexFCEndDate        | Unicode string [DT_WSTR]/8         | FlexFCEndDate            | nvarchar/8                  |
| FCDateQtyBy          | Unicode string [DT_WSTR]/4         | FCDateQtyBy              | nvarchar/4                  |

## 2. F862

| Source Column Name   | Source Data Type/Size              | Destination Column Name | Destination Data Type/Size |
|----------------------|------------------------------------|--------------------------|-----------------------------|
| Ctrl_Num             | Unicode string [DT_WSTR]/10        | Ctrl_Num                 | nvarchar/10                 |
| Msg_Num              | Unicode string [DT_WSTR]/10        | Msg_Num                  | nvarchar/10                 |
| Msg_RealseDate       | Unicode string [DT_WSTR]/8         | Msg_RealseDate           | nvarchar/8                  |
| Msg_Purpose          | Unicode string [DT_WSTR]/8         | Msg_Purpose              | nvarchar/8                  |
| ScheduleType         | Unicode string [DT_WSTR]/10        | ScheduleType             | nvarchar/10                 |
| StartDate            | Unicode string [DT_WSTR]/8         | StartDate                | nvarchar/8                  |
| EndDate              | Unicode string [DT_WSTR]/8         | EndDate                  | nvarchar/8                  |
| Msg_Ref_Num          | Unicode string [DT_WSTR]/15        | Msg_Ref_Num              | nvarchar/15                 |
| **ShipToCode<sup>1</sup><sup>,3</sup>**           | Unicode string [DT_WSTR]/15        | ShipToCode               | nvarchar/15                 |
| ShipFromCode         | Unicode string [DT_WSTR]/15        | ShipFromCode             | nvarchar/15                 |
| Consignee            | Unicode string [DT_WSTR]/15        | Consignee                | nvarchar/15                 |
| **PartNum<sup>2</sup>**              | Unicode string [DT_WSTR]/40        | PartNum                  | nvarchar/40                 |
| PO_num               | Unicode string [DT_WSTR]/40        | PO_num                   | nvarchar/40                 |
| DockCode             | Unicode string [DT_WSTR]/10        | DockCode                 | nvarchar/10                 |
| LineFeed             | Unicode string [DT_WSTR]/10        | LineFeed                 | nvarchar/10                 |
| ReserveLineFeed      | Unicode string [DT_WSTR]/10        | ReserveLineFeed          | nvarchar/10                 |
| ContactName          | Unicode string [DT_WSTR]/50        | ContactName              | nvarchar/50                 |
| ContactTelephone     | Unicode string [DT_WSTR]/15        | ContactTelephone         | nvarchar/15                 |
| LastReceivedASNNum   | Unicode string [DT_WSTR]/10        | LastReceivedASNNum       | nvarchar/10                 |
| LastShippedQty       | numeric [DT_NUMERIC]               | LastShippedQty           | int                         |
| LastShippedDate      | Unicode string [DT_WSTR]/8         | LastShippedDate          | nvarchar/8                  |
| CumShippedQty        | numeric [DT_NUMERIC]               | CumShippedQty            | int                         |
| CumStartDate         | Unicode string [DT_WSTR]/8         | CumStartDate             | nvarchar/8                  |
| CumEndDate           | Unicode string [DT_WSTR]/8         | CumEndDate               | nvarchar/8                  |
| ForecastCumQty       | numeric [DT_NUMERIC]               | ForecastCumQty           | int                         |
| ForecastNetQty       | numeric [DT_NUMERIC]               | ForecastNetQty           | int                         |
| UOM                  | Unicode string [DT_WSTR]/4         | UOM                      | nvarchar/4                  |
| ForecastStatus       | Unicode string [DT_WSTR]/4         | ForecastStatus           | nvarchar/4                  |
| ForecastDate         | Unicode string [DT_WSTR]/8         | ForecastDate             | nvarchar/8                  |
| ForecastTime         | Unicode string [DT_WSTR]/10        | ForecastTime             | nvarchar/10                 |

**<sup>1</sup>ShipToCode** คือ Uf_sPlantShip ใน SyteLine Customer ใช้ในการ Update CustNum และ PlantCode  
**<sup>2</sup>PartNum** คือ SyteLine Item  
**<sup>3</sup>ShipToCode** คือ Value ของ User Defined Type ชื่อ ExportPlant ใช้เพื่อกำหนด Weekday สำหรับคำนวณ ForecastDateNew    

# 3. FS01, FS02

| Source Column Name | Source Data Type/Size | Destination Column Name | Destination Data Type/Size |
|--------------------|------------------------|--------------------------|-----------------------------|
| F1                 | nvarchar/40           | ReqElement               | nvarchar/40 |
| F2                 | nvarchar/15           | OrderDocNo               | nvarchar/15 |
| F3                 | nvarchar/15           | ItemNo                   | nvarchar/15 |
| F4                 | nvarchar/5            | SLNo                     | nvarchar/5 |
| F5                 | nvarchar/40           | Product                  | nvarchar/40 |
| F6                 | nvarchar/15           | CustLoc                  | nvarchar/15 |
| F7                 | nvarchar/15           | ShipFromLoc              | nvarchar/15 |
| F8                 | nvarchar/30           | ShipToLoc                | nvarchar/30 |
| F9                 | nvarchar/30           | GoodRecipient            | nvarchar/30 |
| F10                | date                  | ShipDate                 | date |
| F11                | time                  | ShipTime                 | time |
| F12                | nvarchar/10           | ShipTZ                   | nvarchar/10 |
| F13                | date                  | DelDate                  | date |
| F14                | time                  | DelTime                  | time |
| F15                | nvarchar/10           | DelTZ                    | nvarchar/10 |
| F16                | decimal               | Quantity                 | decimal |
| F17                | nvarchar/5            | UOM                      | nvarchar/5 |
| F18                | nvarchar/20           | ProdChgNo                | nvarchar/20 |
| F19                | nvarchar/20           | MyCustLocNo              | nvarchar/20 |
| F20                | nvarchar/20           | MySTLocDesc              | nvarchar/20 |
| F21                | nvarchar/20           | MyProductNo              | nvarchar/20 |
| F22                | nvarchar/20           | MyProductDesc            | nvarchar/20 |
| F23                | nvarchar/20           | MySFLocNo                | nvarchar/20 |
| F24                | nvarchar/20           | MySFLocDesc              | nvarchar/20 |
| F25                | nvarchar/20           | HeaderState              | nvarchar/20 |
| F26                | nvarchar/20           | ItemState                | nvarchar/20 |
| F27                | nvarchar/20           | SchedLineState           | nvarchar/20 |
| F28                | nvarchar/20           | MyCustLocDesc2           | nvarchar/20 |
| F29                | nvarchar/20           | RefeType                 | nvarchar/20 |
| F30                | nvarchar/20           | ReferenceDoc             | nvarchar/20 |
| F31                | nvarchar/20           | RefItemID                | nvarchar/20 |
| F32                | nvarchar/20           | CustomerBatchNo          | nvarchar/20 |
| F33                | nvarchar/20           | SupplierBatchNo          | nvarchar/20 |
| F34                | nvarchar/20           | MfrPartNo                | nvarchar/20 |
| F35                | nvarchar/20           | Mfr                      | nvarchar/20 |
