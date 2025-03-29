---

## Entity Relationship Diagram (ERD) for Omega Manufacturing’s Order Processing System

## Overview


This document outlines the Dataverse schema for the Order Processing System at Omega Manufacturing. The schema defines the core tables (entities), their key fields with data types, and the relationships between them. The design is created to centralize order processing and inventory management into one secure, structured, and scalable database. This integration will support automation, reduce manual errors, and provide real‑time insights, thereby addressing the challenges Omega Manufacturing currently faces.

Omega Manufacturing experiences delays, errors, and a lack of real‑time visibility due to using multiple tools such as spreadsheets and email for order processing. With this well-structured ERD, information flows seamlessly between departments and supports efficient workflows and data accuracy.

---

## 1. Core Tables (Entities) & Fields

Below are the key tables along with the important fields and their data types. Each table is designed to capture information related to customers, products, orders, and inventory.

### 🔴 1. Customer  
Stores all customer-related information.

| **Field Name** | **Data Type**         | **Description**                         |
| -------------- | --------------------- | --------------------------------------- |
| CustomerID     | Unique Identifier     | Primary key; unique customer ID         |
| FirstName      | Text                  | Customer's first name                   |
| LastName       | Text                  | Customer's last name                    |
| Email          | Text                  | Customer's email address                |
| Phone          | Text                  | Customer's contact number               |
| Address        | Text                  | Street address                          |
| City           | Text                  | City name                               |
| State          | Text                  | State or region                         |
| PostalCode     | Text                  | Zip or postal code                      |
| Country        | Text                  | Country name                            |

---

### 🟢 2. Product  
Stores details of all products available in inventory.

| **Field Name**   | **Data Type**         | **Description**                                                   |
| ---------------- | --------------------- | ----------------------------------------------------------------- |
| ProductID        | Unique Identifier     | Primary key; unique product ID                                    |
| ProductName      | Text                  | Name of the product                                               |
| Description      | Text                  | A brief description of the product                                |
| UnitPrice        | Currency              | Price per unit                                                    |
| Category         | Choice                | Product category such as Raw Materials or Finished Goods          |

---

### 🔵 3. Customer Order  
Tracks individual orders placed by customers.

| **Field Name** | **Data Type**         | **Description**                                       |
| -------------- | --------------------- | ----------------------------------------------------- |
| OrderID        | Unique Identifier     | Primary key; unique order ID                           |
| CustomerID     | Unique Identifier     | Foreign key referencing Customer(CustomerID)         |
| OrderDate      | Date/Time             | Date and time when the order was placed                |
| OrderStatus    | Choice                | Order status (e.g., Pending, Shipped, Delivered, Canceled) |
| OrderTotal     | Currency              | Total amount for the order                             |

---

### 🟡 4. Order Item  
Contains details for each product included in an order.

| **Field Name**   | **Data Type**         | **Description**                                                   |
| ---------------- | --------------------- | ----------------------------------------------------------------- |
| OrderItemID      | Unique Identifier     | Primary key; unique identifier for the order item                 |
| OrderID          | Unique Identifier     | Foreign key referencing Customer Order(OrderID)                   |
| ProductID        | Unique Identifier     | Foreign key referencing Product(ProductID)                        |
| Quantity         | Number                | Quantity of the product ordered                                   |
| UnitPrice        | Currency              | Price per unit at order time                                        |
| ExtendedPrice    | Currency              | Total price (Quantity multiplied by UnitPrice)                      |

---

### 🟣 5. Inventory  
Manages current stock levels for each product.

| **Field Name**      | **Data Type**         | **Description**                                                |
| ------------------- | --------------------- | -------------------------------------------------------------- |
| ProductID           | Unique Identifier     | Primary key and foreign key referencing Product(ProductID)     |
| StockLevel          | Number                | Current available quantity in stock                             |
| LastUpdated         | Date/Time             | Date and time when the stock level was last updated              |
| Location            | Text                  | Physical location of the inventory (if applicable)               |

---

## 2. Relationships Between Tables

Understanding how these entities are connected is essential for a unified data structure:

| **Relationship**                             | **Description**                                                                              |
| -------------------------------------------- | -------------------------------------------------------------------------------------------- |
| Customer ↔ Customer Order                      | One customer can have many orders. The Customer Order table uses CustomerID to link each order to its customer. |
| Customer Order ↔ Order Item                    | One order can contain multiple items. Each Order Item is linked to a particular order using OrderID.  |
| Product ↔ Order Item                           | A product can appear in many order items. The Order Item table uses ProductID to reference the corresponding product. |
| Product ↔ Inventory                            | Each product has one corresponding inventory record. The ProductID matches in both tables to ensure accurate stock information. |

---

## 3. Entity Relationship Diagram (ERD)

The diagram below visually represents the relationships among these key entities. Each box represents a core table, and the connecting lines illustrate the relationships between them.

```
                 +---------------------+         +---------------------+         +---------------------+
   |       🔴 Customer   |         |      🔵 Order       |         |     🟡 OrderItem    |
   |---------------------|         |---------------------|         |---------------------|
   | CustomerID (PK)     | 1     N | OrderID (PK)        | 1     N | OrderItemID (PK)    |
   | FirstName           |────────>| CustomerID (FK)     |────────>| OrderID (FK)        |
   | LastName            |         | OrderDate           |         | ProductID (FK)      |
   | Email               |         | OrderStatus         |         | Quantity            |
   | Phone               |         | OrderTotal          |         | UnitPrice           |
   | Address             |         +---------------------+         | ExtendedPrice       |
   +---------------------+                                       +---------------------+
                                                                                
                                                                                
            +---------------------+                                +---------------------+
            |      🟢 Product     |                                |     🟣 Inventory    |
            |---------------------|                                |---------------------|
         N  | ProductID (PK)      |◄───────────── 1               | ProductID (PK,FK)    |
            | ProductName         |                                | StockLevel          |
            | Description         |                                | LastUpdated         |
            | UnitPrice           |                                | Location            |
            | Category            |                                +---------------------+
            +---------------------+

```
---

##  Conclusion

This well-structured Dataverse schema for the Inventory Management System provides a robust foundation for automating Omega Manufacturing’s order processing and inventory tracking. By centralizing all critical data into one secure repository, this design ensures accuracy, eliminates manual errors, and allows for real‑time reporting and analytics. The relationships between the Customer, Product, Customer Order, Order Item, and Inventory tables ensure seamless data flow across departments.

Implementing this ERD through Microsoft Power Platform will empower your organization with automated workflows, reduce operational inefficiencies, and provide the actionable insights needed for better decision-making. With this design, Omega Manufacturing is well-prepared for digital transformation, supporting scalable growth and improved customer satisfaction.


[Power_Platform_Use_Case[2].pptx](https://github.com/user-attachments/files/19516750/Power_Platform_Use_Case.2.pptx)
