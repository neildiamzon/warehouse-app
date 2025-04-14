Here's a GitHub README format that adheres to best practices and uses Markdown to structure the content clearly:

---

# Warehouse App Repository

## Description

This repository contains the backend for the **Warehouse** application, which includes managing user data, inventory, and product information.

---

## Getting Started

### Prerequisites

Before setting up the project, ensure you have the following installed:

- [.NET SDK](https://dotnet.microsoft.com/download) (version 6 or above)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) (for local development)

### Clone the Repository

```bash
git clone https://github.com/your-username/warehouse-app.git
cd warehouse-app
```

### 1. Install EF Core Tools

To manage migrations, install the EF Core CLI tools:

```bash
dotnet tool install --global dotnet-ef
```

### 2. Add Migrations

Generate the necessary migrations for the User and Warehouse databases:

- **Add Users Table Migration:**

```bash
dotnet ef migrations add AddUsersTables --context UserDbContext
```

- **Add Invoice and Product Tables Migration:**

```bash
dotnet ef migrations add AddInvoiceAndProductTables --context WarehouseDbContext
```

### 3. Apply Migrations (Database Deployment)

Once the migrations are created, apply them to the databases:

- **Update Warehouse Database:**

```bash
dotnet ef database update --context WarehouseDbContext
```

- **Update User Database:**

```bash
dotnet ef database update --context UserDbContext
```

---

## Setting Up Dependencies

### 4. Restore Dependencies

Restore all the required packages:

```bash
dotnet restore
```

Alternatively, you can manually add required libraries:

- **Microsoft.AspNetCore.Identity** (for Identity management):

```bash
dotnet add package Microsoft.AspNetCore.Identity.EntityFrameworkCore
```

- **Microsoft.EntityFrameworkCore.SqlServer** (for SQL Server database provider):

```bash
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

---

## Configuration

1. **SQL Server Connection String**

Update your `appsettings.json` file with a valid SQL Server connection string for both the **User** and **Warehouse** databases.

```json
{
  "ConnectionStrings": {
    "UserDBConnection": "Server=your-server;Database=WarehouseUserDB;Trusted_Connection=True;TrustServerCertificate=True;User Id=your-username;Password=your-password;",
    "WarehouseDBConnection": "Server=your-server;Database=WarehouseDB;Trusted_Connection=True;TrustServerCertificate=True;User Id=your-username;Password=your-password;"
  }
}
```

---

insert initial data

USE [WarehouseDB]
GO

INSERT INTO [dbo].[Invoices] 
    ([invoice_id], [invoice_reference_number], [user_id], [customer_name], 
     [shipping_address], [total_cost], [shipped], [invoice_status], [DateCreated])
VALUES
    ('INV-001', 'REF-001', 'USR-1001', 'John Doe', '123 Elm St, Wellington, NZ', 130.50, 'No', 'Pending', GETDATE()),
    ('INV-002', 'REF-002', 'USR-1002', 'Jane Smith', '45 High St, Auckland, NZ', 91.00, 'Yes', 'Shipped', GETDATE()),
    ('INV-003', 'REF-003', 'USR-1003', 'Michael Johnson', '67 Queen St, Christchurch, NZ', 160.00, 'No', 'Processing', GETDATE()),
    ('INV-004', 'REF-004', 'USR-1004', 'Emily Brown', '89 King St, Hamilton, NZ', 115.00, 'No', 'Pending', GETDATE()),
    ('INV-005', 'REF-005', 'USR-1005', 'Daniel Wilson', '23 Victoria St, Dunedin, NZ', 75.50, 'Yes', 'Shipped', GETDATE()),
    ('INV-006', 'REF-006', 'USR-1006', 'Sophia Martinez', '12 George St, Tauranga, NZ', 200.00, 'No', 'Pending', GETDATE()),
    ('INV-007', 'REF-007', 'USR-1007', 'Oliver Lee', '34 Shortland St, Napier, NZ', 50.00, 'Yes', 'Shipped', GETDATE()),
    ('INV-008', 'REF-008', 'USR-1008', 'Emma Harris', '78 Manners St, Palmerston North, NZ', 140.00, 'No', 'Processing', GETDATE()),
    ('INV-009', 'REF-009', 'USR-1009', 'Liam Robinson', '56 Featherston St, Nelson, NZ', 85.00, 'No', 'Pending', GETDATE()),
    ('INV-010', 'REF-010', 'USR-1010', 'Charlotte White', '90 Broadway, Invercargill, NZ', 175.00, 'Yes', 'Shipped', GETDATE());

GO


USE [WarehouseDB]
GO

-- Batch insert products
INSERT INTO [dbo].[Products]
           ([product_code]
           ,[name]
           ,[description]
           ,[price]
           ,[weight]
           ,[uom]
           ,[quantity_per_uom]
           ,[stock_level]
           ,[date_created])
     VALUES
           ('P005', 'Product 5', 'Description of Product 5', 12.99, 0.7, 'kg', 15, 250, GETDATE()),
           ('P006', 'Product 6', 'Description of Product 6', 24.99, 1.2, 'piece', 1, 80, GETDATE()),
           ('P007', 'Product 7', 'Description of Product 7', 8.99, 0.3, 'kg', 10, 500, GETDATE()),
           ('P008', 'Product 8', 'Description of Product 8', 99.99, 5.0, 'box', 1, 20, GETDATE()),
           ('P009', 'Product 9', 'Description of Product 9', 18.49, 0.6, 'liters', 2, 150, GETDATE()),
           ('P010', 'Product 10', 'Description of Product 10', 45.99, 2.5, 'pack', 1, 60, GETDATE()),
           ('P011', 'Product 11', 'Description of Product 11', 5.99, 0.2, 'piece', 1, 1000, GETDATE()),
           ('P012', 'Product 12', 'Description of Product 12', 39.99, 1.8, 'kg', 12, 110, GETDATE()),
           ('P013', 'Product 13', 'Description of Product 13', 55.99, 3.2, 'box', 1, 30, GETDATE()),
           ('P014', 'Product 14', 'Description of Product 14', 21.99, 1.0, 'liters', 2, 200, GETDATE()),
           ('P015', 'Product 15', 'Description of Product 15', 7.49, 0.4, 'pack', 5, 400, GETDATE()),
           ('P016', 'Product 16', 'Description of Product 16', 29.99, 1.3, 'piece', 1, 90, GETDATE()),
           ('P017', 'Product 17', 'Description of Product 17', 14.99, 0.5, 'kg', 8, 350, GETDATE()),
           ('P018', 'Product 18', 'Description of Product 18', 64.99, 4.5, 'box', 1, 25, GETDATE()),
           ('P019', 'Product 19', 'Description of Product 19', 32.99, 2.1, 'kg', 6, 75, GETDATE()),
           ('P020', 'Product 20', 'Description of Product 20', 9.99, 0.9, 'liters', 3, 180, GETDATE());

GO

USE [WarehouseDB]
GO

INSERT INTO [dbo].[InvoiceProducts] 
    ([invoice_id],[product_code], [quantity], [total_price], [unit_price])
VALUES

    ('INV-003', 'P005', 1, 50.00, 50.00),  -- 1 unit of P005 for INV-003
    ('INV-004',  'P006', 1, 25.00, 25.00),  -- 1 unit of P006 for INV-004
    ('INV-004', 'P007', 3, 90.00, 30.00);  -- 3 units of P007 for INV-004

GO
