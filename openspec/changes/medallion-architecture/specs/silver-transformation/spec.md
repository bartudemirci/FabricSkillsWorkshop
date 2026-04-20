## ADDED Requirements

### Requirement: Clean and normalize sales orders
The system SHALL join SalesOrderHeader and SalesOrderDetail from bronze into a single `silver.sales_orders` table with proper data types, removing duplicates and null order IDs.

#### Scenario: Sales orders joined
- **WHEN** the silver transformation notebook is executed
- **THEN** a `silver.sales_orders` Delta table is created containing header fields (OrderDate, CustomerID, TotalDue) joined with detail fields (ProductID, OrderQty, UnitPrice, LineTotal)

#### Scenario: Null orders filtered
- **WHEN** a row in bronze.SalesOrderHeader has a NULL SalesOrderID
- **THEN** that row is excluded from silver.sales_orders

### Requirement: Clean and normalize products
The system SHALL join Product, ProductSubcategory, and ProductCategory from bronze into a single `silver.products` table with category hierarchy flattened.

#### Scenario: Product hierarchy flattened
- **WHEN** the silver transformation notebook is executed
- **THEN** a `silver.products` Delta table is created with columns including ProductID, Name, ProductNumber, Color, ListPrice, SubcategoryName, CategoryName

### Requirement: Clean and normalize customers with addresses
The system SHALL join Customer, CustomerAddress, and Address from bronze into a `silver.customers_with_address` table.

#### Scenario: Customer addresses resolved
- **WHEN** the silver transformation notebook is executed
- **THEN** a `silver.customers_with_address` Delta table is created with CustomerID, FirstName, LastName, City, StateProvince, CountryRegion
