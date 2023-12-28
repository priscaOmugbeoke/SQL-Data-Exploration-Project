# SQL Data Exploration Project for AJAX Foods Export & Import Company

## Table of Content
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Details of Database Tables and Attributes](#details-of-database-tables-and-attributes)
- [Tools](#tools)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#results/findings)

### Project Overview

This project is aimed to provide comprehensive insights into the operational dynamics of the organization, delving into the intricacies of its supply chain and marketing processese over the last one year. By analysing various ascpect of this company, I seek to gain insight into trends, acquire a profound understanding of the company's performance metrics, and formulate strategic recommendations driven by data analytics. 

### Data Source

The database on which the SQL queries are performed is the Northwind database which is a sample database used by Microsoft to demonstrate the features of some of its products, including SQL Server and Microsoft Access. The database contains the sales data for Northwind Traders, a fictitious specialty foods exportimport company. The database is made up of 8 tables. Key tables within the Northwind database (AJAX Foods Export & Import Company for this project) include: Customers, Orders, OrderDetails, Products, Employees, Categories, Suppliers and Shippers. 

### Details of Database Tables and Attributes


**Customers:** This table contains the CustomerID, CustomerName, ContactName, Address, City, PostalCode and Country.

**Orders:** This table contains the OrderID, CustomerID, EmployeeID, OrderDate and ShipperID.

**OrderDetails:** This table contains the OrderDetailID, OrderID, ProductID	and Quantity.

**Products:** This table contains the products the company offers. Attributes of this tables includes ProductID, ProductName, SupplierID, CategoryID, Unit and Price.

**Employees:** This table contains details of the employees. The attributes includes; EmployeeID, LastName, FirstName, BirthDate, Photo	and Notes.

**Categories:** This table classifies different product types into various categories. The attributes includes CategoryID, CategoryName and Description.

**Suppliers:** Information about the suppliers providing products to the company. Attributes includes SupplierID, SupplierName, ContactName, Address, City, PostalCode, Country,PhoneNumber

**Shippers:** Details about shipping companies responsible for delivering orders. Attributes includes ShipperID, ShipperName and Phone



### Tools
- SQL
- SQL Server [see database](https://www.w3schools.com/sql)


### Exploratory Data Analysis

1.	Listing of employee first name and last name with their date of birth.

2.	All contact’s name and full address for suppliers located in Japan, Spain, and Sweden.

3.	Customer’s name and city for all customers outside of Portugal, Switzerland, and Finland.

4.	The average, sum, maximum, and minimum per unit cost across all products in their product line.

5.	Suppliers name based in Stockholm, Sweden; Ann Arbor, USA; and Germany.

6.	The number of customers in each city in the UK with the name of the city. 

7.	The product name, category name, supplier name for products priced greater than 30 and sorted by supplier name. 

8.	The number of products supplied by each supplier for products priced less than 30 showing the number of products and SupplierID. Each supplier must supply at least two products. 

9.	A listing of the customer’s name, last name of employee who accepted the order for all orders from customers based in the United States and Canada and shipped through United Package sorted alphabetically by customer name.


### Data Analysis

Listing of employee first name and last name with their date of birth.
```SQL Statements
SELECT FirstName, LastName, BirthDate FROM Employees;
```

Listing of employee first name and last name with their date of birth.
```SQL Statements
SELECT FirstName, LastName, BirthDate FROM Employees;
```

All contact’s name and full address for suppliers located in Japan, Spain, and Sweden.
```SQL Statements
SELECT ContactName, Address, City, PostalCode, Country FROM Suppliers
WHERE Country = 'Japan' OR Country = 'Spain' OR Country = 'Sweden';
```

Customer’s name and city for all customers outside of Portugal, Switzerland, and Finland.
```SQL Statements
SELECT CustomerName, City FROM Customers
WHERE Country NOT IN ('Portugal','Switzerland','Finland');
```

The average, sum, maximum, and minimum per unit cost across all products in their product line.
```SQL Statements
Per product:
SELECT ProductName, avg(Price) As [AverageCost], sum(Price) AS [TotalCost], max(Price) AS [MaximumCost], min(Price) as [MinimumCost]
FROM Products
GROUP BY ProductName;
```

Suppliers name based in Stockholm, Sweden; Ann Arbor, USA; and Germany.
```SQL StatementsSELECT SupplierName, City, Country FROM Suppliers
WHERE City = 'Stockholm' AND Country = 'Sweden' OR (City = 'Ann Arbor' AND Country = 'USA') OR Country = 'Germany';
```

The number of customers in each city in the UK with the name of the city. 
```SQL Statements
SELECT City, COUNT(CustomerID) AS [Number of Customers] 
FROM Customers
WHERE Country = 'UK'
GROUP BY City;
```

The product name, category name, supplier name for products priced greater than 30 and sorted by supplier name. 
```SQL Statements
SELECT Products.ProductName,Categories.CategoryName,Suppliers.SupplierName,Products.Price
FROM Products,Categories,Suppliers
WHERE Price > 30
AND Products.CategoryID = Categories.CategoryID
AND Products.SupplierID = Suppliers.SupplierID
ORDER BY SupplierName
```


The number of products supplied by each supplier for products priced less than 30 showing the number of products and SupplierID. Each supplier must supply at least two products. 
```SQL Statements
SELECT Suppliers.SupplierID, Suppliers.SupplierName,COUNT(ProductID) AS [Number of Products]
FROM Products,Suppliers
WHERE Products.Price < 30
AND Products.SupplierID = Suppliers.SupplierID
GROUP BY Suppliers.SupplierID, Suppliers.SupplierName 
HAVING COUNT(ProductID) >= 2;
```

A listing of the customer’s name, last name of employee who accepted the order for all orders from customers based in the United States and Canada and shipped through United Package sorted alphabetically by customer name.
```SQL Statements
SELECT Customers.CustomerName, Employees.LastName AS [EmployeeLastName], Customers.Country, Shippers.ShipperName
FROM Orders, Customers, Employees, Shippers
WHERE Customers.CustomerID = Orders.CustomerID
AND Employees.EmployeeID = Orders.EmployeeID
AND Orders.ShipperID = Shippers.ShipperID
AND Customers.Country IN ("USA","Canada")
AND ShipperName = 'United Package'
ORDER BY CustomerName;
```


### Results/Findings
The data requested by the CEO and operational manager will help them in informed decision-making and strategic planning for AJAX foods export & import company in the following ways;
- Enables better HR management, facilitates employee engagement, and supports compliance with HR policies.

- Facilitates efficient communication, coordination, and relationship management with suppliers in key locations.

- Supports targeted marketing efforts and provides insights into the geographic distribution of the customer base.

- Helps in pricing strategies, cost management, and identification of cost outliers

- Aids in supplier relationship management and ensures effective coordination in key regions.

- Provides insights into the distribution of the customer base, supporting regional business development and marketing strategies.

- Identifies high-value products and suppliers, supporting strategic decisions on product offerings and supplier relationships.

- Helps in managing relationships with suppliers providing lower-cost products and optimizing the product portfolio.

- Supports order tracking, customer service, and ensures efficient order fulfillment for specific regions and shipping methods.

