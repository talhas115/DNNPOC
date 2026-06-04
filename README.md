# DNNPOC - DotNetNuke Proof of Concept

This repository contains a pre-compiled instance of **DNN Platform (DotNetNuke) v10.3.2** configured as a Proof of Concept (POC).

## Repository Contents

- **Core DNN Site Files**: All necessary binaries (`/bin`), controls, styles, and configurations are pre-packaged.
- **Database (`App_Data/Database.mdf`)**: The SQL Server Database file for the local DNN installation.
- **Configuration (`web.config`)**: Standard configuration with database connection string pointing to `localhost` using Windows Authentication.

## Prerequisites

To run this project locally, you will need:

1. **IIS (Internet Information Services)**: Enabled on Windows with ASP.NET 4.7/4.8 development features.
2. **SQL Server / SQL Server Express**: A local instance of Microsoft SQL Server configured to support Windows Authentication.
3. **.NET Framework 4.7.2 or higher**: Installed on the host system.

## Setup Instructions

### 1. Attach the Database
1. Open **SQL Server Management Studio (SSMS)** and connect to your local SQL Server instance (e.g., `(local)` or `localhost`).
2. Right-click on **Databases** and select **Attach...**
3. Click **Add...** and navigate to the `App_Data` folder in this project:
   `c:\Websites\DNNPOC\App_Data\Database.mdf`
4. Ensure the database is attached with the name **DNNPOC**.
5. Give the IIS AppPool user (e.g., `IIS_IUSRS` or `IIS APPPOOL\DefaultAppPool`) appropriate read/write permissions on the attached database.

### 2. Configure IIS
1. Open **IIS Manager** (`inetmgr`).
2. Add a new Web Site:
   - **Site name**: `DNNPOC`
   - **Physical path**: Path to this folder (e.g., `c:\Websites\DNNPOC`)
   - **Binding**: Set up a host name (e.g., `dnnpoc.local`) or bind to a specific local port.
3. Configure the Application Pool:
   - Ensure the application pool is set to use **.NET CLR Version v4.0**.
   - Set the Application Pool **Identity** to either `ApplicationPoolIdentity` (ensure it has permissions to files and database) or a custom user account.

### 3. File Permissions
Ensure that the Application Pool Identity (e.g., `IIS_IUSRS` or `IIS APPPOOL\<AppPoolName>`) has **Read & Write** permissions to the website directory so that DNN can write to `App_Data`, `Portals`, and `web.config`.

### 4. Hosts File (Optional)
If you configured a custom host name like `dnnpoc.local`, add it to your Windows hosts file (`C:\Windows\System32\drivers\etc\hosts`):
```text
127.0.0.1    dnnpoc.local
```

---
*Created automatically as part of the repository initialization.*
