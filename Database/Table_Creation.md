### Tables for Spice Product Company

### Example SQL to Create These Tables

Here’s how you can create these tables using SQL:

```sql
-- Create Employee Table
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY IDENTITY(1,1),
    FirstName NVARCHAR(50),
    LastName NVARCHAR(50),
    JobTitle NVARCHAR(50),
    HireDate DATE,
    Phone NVARCHAR(15),
    Email NVARCHAR(100)
);

-- Create Product Table
CREATE TABLE Product (
    ProductID INT PRIMARY KEY IDENTITY(1,1),
    ProductName NVARCHAR(100),
    Description NVARCHAR(255),
    Price DECIMAL(10, 2),
    QuantityInStock INT,
    SupplierID INT NULL
);

-- Create Sale Table
CREATE TABLE Sale (
    SaleID INT PRIMARY KEY IDENTITY(1,1),
    SaleDate DATETIME DEFAULT GETDATE(),
    EmployeeID INT,
    TotalAmount DECIMAL(10, 2),
    FOREIGN KEY (EmployeeID) REFERENCES Employee(EmployeeID)
);

-- Create SaleDetails Table
CREATE TABLE SaleDetails (
    SaleDetailID INT PRIMARY KEY IDENTITY(1,1),
    SaleID INT,
    ProductID INT,
    Quantity INT,
    Price DECIMAL(10, 2),
    FOREIGN KEY (SaleID) REFERENCES Sale(SaleID),
    FOREIGN KEY (ProductID) REFERENCES Product(ProductID)
);

-- Create Supplier Table
CREATE TABLE Supplier (
    SupplierID INT PRIMARY KEY IDENTITY(1,1),
    SupplierName NVARCHAR(100),
    ContactName NVARCHAR(50),
    Phone NVARCHAR(15),
    Email NVARCHAR(100),
    Address NVARCHAR(255)
);
```

### 🔍 Next Steps
- Copy the SQL code for the tables you want and paste it into a new query window in SSMS.
- Execute the script to create the tables.

