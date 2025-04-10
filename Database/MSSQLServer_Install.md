
---

## ✅ Step-by-Step to Install SQL Server Locally

### 🔹 1. **Download SQL Server Developer Edition (Free)**
Microsoft offers a **free Developer Edition** which is perfect for learning.

- Go to: [https://www.microsoft.com/en-us/sql-server/sql-server-downloads](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- Download the **Developer edition**.
- Run the installer and choose the **Basic** or **Custom** installation (Basic is easier for learning).

> It installs the actual **SQL Server Engine**.

---

### 🔹 2. **Install SQL Server**
Follow the steps in the installer:
- Accept the license
- Choose install location
- Let it install the **SQL Server Engine** + **SQL Server Services**

It will also install:
- SQL Server Database Engine
- SQL Server Browser
- Optionally: SQL Server Agent (you can skip for now)

---

### 🔹 3. **Install SQL Server Management Studio (Already Done ✅)**

You already have SSMS — great! After SQL Server is installed, just **open SSMS**, and when it asks you to **connect to a server**, use:

- **Server type**: Database Engine  
- **Server name**: `localhost` or `.\SQLEXPRESS` (depending on what you installed)
- **Authentication**: Windows Authentication (by default)

Click **Connect**, and now you’re in!

---

### 🔹 4. **Can’t Find Server Name?**
If you’re unsure about the server name, do this:

- Press `Windows + R`, type `services.msc`, and press Enter
- Look for a service called something like:
  - `SQL Server (MSSQLSERVER)`  
  - or `SQL Server (SQLEXPRESS)`
- That tells you what instance is running

Then in SSMS, use:
- `localhost`
- or `.\SQLEXPRESS` (if it’s the Express edition)

---

### 🔹 5. **Create Your First Database**
Once connected, right-click `Databases` → **New Database…** → give it a name → click **OK**.

You're good to go!

-

Creating a database in **Microsoft SQL Server Management Studio (SSMS)** is pretty straightforward. Here's a step-by-step guide:

---

### ✅ **Option 1: Using the GUI (Graphical Interface)**

1. **Open SSMS (SQL Server Management Studio).**
2. **Connect to your SQL Server instance.**
3. In the **Object Explorer**, right-click on the `Databases` folder.
4. Click **New Database...**
5. In the dialog box:
   - Enter the **database name** (e.g., `MyDatabase`)
   - Optionally, you can configure settings like the initial size, file names, etc.
6. Click **OK**.

Your new database will appear under the `Databases` folder.

---

### ✅ **Option 2: Using SQL Query**

If you prefer writing SQL:

```sql
CREATE DATABASE MyDatabase;
```

You can also customize the database files:

```sql
CREATE DATABASE MyDatabase
ON
(
    NAME = MyDatabase_Data,
    FILENAME = 'C:\SQLData\MyDatabase_Data.mdf',
    SIZE = 10MB,
    MAXSIZE = 100MB,
    FILEGROWTH = 5MB
)
LOG ON
(
    NAME = MyDatabase_Log,
    FILENAME = 'C:\SQLData\MyDatabase_Log.ldf',
    SIZE = 5MB,
    MAXSIZE = 25MB,
    FILEGROWTH = 5MB
);
```

> ⚠️ Make sure the folder paths exist and SQL Server has permissions to write to them.

---

### 💡 To verify the database was created:

```sql
SELECT name FROM sys.databases;
```

---