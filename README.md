# FMT.ETLProcess

# 📌 Project Parameters — FMT ETL Automation Workflow

This document provides an overview of the project parameters used in the **FMT - ETL Automation Workflow**.  
These parameters are required for proper configuration of file processing and database connections.

---

## ⚙️ Parameters Overview

| **Name**            | **DataType** | **Value**                       | **Sensitive**     | **Required**| **Description**
|---------------------|--------------|---------------------------------|-------------------|-------------|----------------------------------------------------
| **ApplicationName** | `String`     | `FMT - ETL Automation Workflow` | 🟢 Not Sensitive | 🔴 Required | 🏷️ Application / Workflow name                    
| **FileSpec830**     | `String`     | `830*.csv`                      | 🟢 Not Sensitive | 🔴 Required | 📂 File specification for **830** CSV files 
| **FileSpec862**     | `String`     | `862*.csv`                      | 🟢 Not Sensitive | 🔴 Required | 📂 File specification for **862** CSV files 
| **FileSpecFS01**    | `String`     | `export??????????????.xlsx`     | 🟢 Not Sensitive | 🔴 Required | 📊 File specification for **FS01** Excel exports 
| **FileSpecFS02**    | `String`     | `export??????????????*.xlsx`    | 🟢 Not Sensitive | 🔴 Required | 📊 File specification for **FS02** Excel exports 
| **SLSite**          | `String`     | `FMT`                           | 🟢 Not Sensitive | 🔴 Required | 🏭 Site code for processing 
| **SQLDatabaseName** | `String`     | `FMT_PRD_App`                   | 🟢 Not Sensitive | 🔴 Required | 🗄️ Target SQL Database name 
| **SQLServerName**   | `String`     | `FMT-SQLDB`                     | 🟢 Not Sensitive | 🔴 Required | 🖥️ Target SQL Server instance name 

---

## 📂 File Specifications

- **📑 830 Files:** `830*.csv`  
- **📑 862 Files:** `862*.csv`  
- **📑 FS01 Export:** `export??????????????.xlsx`  
- **📑 FS02 Export:** `export??????????????*.xlsx`  

---

## 🔌 Connections

### 🔷 OLE DB Connections
- **Microsoft.ACE.OLEDB.12.0** → Extended Properties:  
  `"Excel 12.0 Xml;HDR=NO;IMEX=1;"` _(Excel Connection)_  
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

## 🗄️ Database Connection

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

✨ **Author:** ETL Automation Team 🚀
