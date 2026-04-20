## ADDED Requirements

### Requirement: Sales by product aggregation
The system SHALL create a `gold.sales_by_product` table aggregating total quantity sold, total revenue, and order count per product.

#### Scenario: Product sales summarized
- **WHEN** the gold aggregation notebook is executed
- **THEN** a `gold.sales_by_product` Delta table is created with columns: ProductID, ProductName, CategoryName, TotalQuantity, TotalRevenue, OrderCount

### Requirement: Sales by geography aggregation
The system SHALL create a `gold.sales_by_geography` table aggregating total revenue and order count per city, state, and country.

#### Scenario: Geography sales summarized
- **WHEN** the gold aggregation notebook is executed
- **THEN** a `gold.sales_by_geography` Delta table is created with columns: CountryRegion, StateProvince, City, TotalRevenue, OrderCount, CustomerCount

### Requirement: Product performance ranking
The system SHALL create a `gold.product_performance` table ranking products by revenue with percentile information.

#### Scenario: Products ranked by revenue
- **WHEN** the gold aggregation notebook is executed
- **THEN** a `gold.product_performance` Delta table is created with columns: ProductID, ProductName, CategoryName, TotalRevenue, RevenueRank, RevenuePercentile

### Requirement: Sales outlier detection
The system SHALL create a `gold.sales_outliers` table identifying orders with amounts significantly above or below the mean (beyond 2 standard deviations).

#### Scenario: Outlier orders identified
- **WHEN** the gold aggregation notebook is executed
- **THEN** a `gold.sales_outliers` Delta table is created containing orders where TotalDue is more than 2 standard deviations from the mean, with columns: SalesOrderID, TotalDue, MeanOrderValue, StdDev, ZScore
