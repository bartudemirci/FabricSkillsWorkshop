## 1. Lakehouse Setup

- [ ] 1.1 Create a Lakehouse item named "MedallionLakehouse" in the MirroredDB workspace
- [ ] 1.2 Verify the MirroredDB mirrored database SQL analytics endpoint is accessible

## 2. Bronze Layer — Ingestion

- [ ] 2.1 Create a notebook "01_bronze_ingestion" that reads all tables from the mirrored database SQL endpoint
- [ ] 2.2 Write each table as a Delta table under the bronze folder/schema in the Lakehouse (overwrite mode)
- [ ] 2.3 Verify all expected Adventure Works tables are present in bronze (SalesOrderHeader, SalesOrderDetail, Product, ProductCategory, ProductSubcategory, Customer, Address, CustomerAddress)

## 3. Silver Layer — Transformation

- [ ] 3.1 Create a notebook "02_silver_transformation" that reads from bronze Delta tables
- [ ] 3.2 Join SalesOrderHeader + SalesOrderDetail into silver.sales_orders, filtering null order IDs
- [ ] 3.3 Join Product + ProductSubcategory + ProductCategory into silver.products with flattened hierarchy
- [ ] 3.4 Join Customer + CustomerAddress + Address into silver.customers_with_address
- [ ] 3.5 Write all silver tables as Delta tables in the Lakehouse

## 4. Gold Layer — Aggregation

- [ ] 4.1 Create a notebook "03_gold_aggregation" that reads from silver Delta tables
- [ ] 4.2 Build gold.sales_by_product (total quantity, revenue, order count per product)
- [ ] 4.3 Build gold.sales_by_geography (revenue, order count, customer count per city/state/country)
- [ ] 4.4 Build gold.product_performance (products ranked by revenue with percentiles)
- [ ] 4.5 Build gold.sales_outliers (orders beyond 2 standard deviations from mean)
- [ ] 4.6 Write all gold tables as Delta tables in the Lakehouse

## 5. Analytics

- [ ] 5.1 Create a notebook "04_analytics" with analysis queries on the gold layer
- [ ] 5.2 Add top-selling products query (top N by revenue)
- [ ] 5.3 Add sales per geography breakdown query
- [ ] 5.4 Add outlier analysis query with explanation
- [ ] 5.5 Add category comparison query (revenue, avg order value, product count)
