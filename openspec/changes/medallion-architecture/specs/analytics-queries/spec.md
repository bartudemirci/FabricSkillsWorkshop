## ADDED Requirements

### Requirement: Top-selling products query
The system SHALL provide a query that returns the top N best-selling products by revenue from the gold layer.

#### Scenario: Top 10 products by revenue
- **WHEN** the analytics notebook executes the top-selling products query with N=10
- **THEN** the result contains the 10 products with highest TotalRevenue, including ProductName, CategoryName, TotalRevenue, and TotalQuantity

### Requirement: Sales per geography query
The system SHALL provide a query that breaks down sales by country, state, and city from the gold layer.

#### Scenario: Sales breakdown by country
- **WHEN** the analytics notebook executes the geography query grouped by CountryRegion
- **THEN** the result shows TotalRevenue, OrderCount, and CustomerCount per country, ordered by TotalRevenue descending

### Requirement: Outlier analysis query
The system SHALL provide a query that retrieves and explains sales outliers from the gold layer.

#### Scenario: Display outlier orders
- **WHEN** the analytics notebook executes the outlier query
- **THEN** the result shows outlier orders with SalesOrderID, TotalDue, ZScore, and whether each is above or below the mean

### Requirement: Category comparison query
The system SHALL provide a query comparing product categories by total revenue, average order value, and product count.

#### Scenario: Category performance comparison
- **WHEN** the analytics notebook executes the category comparison query
- **THEN** the result shows each CategoryName with TotalRevenue, AvgOrderValue, ProductCount, ordered by TotalRevenue descending
