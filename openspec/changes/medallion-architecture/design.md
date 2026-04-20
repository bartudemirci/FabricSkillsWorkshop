## Context

An adventure works SQL database has been mirrored into a Fabric workspace called MirroredDB (workspace ID: `27a7b3cb-0878-4d2b-9dd6-182ca3feb47e`, mirrored database ID: `93b631b1-07cd-4fd5-84b2-50c141a1786b`). The mirrored database automatically syncs tables from the source SQL database. We need to build a medallion architecture on top of this mirrored data using a Fabric Lakehouse and Spark notebooks.

## Goals / Non-Goals

**Goals:**
- Build a three-layer medallion architecture (bronze → silver → gold) in a Fabric Lakehouse
- Ingest all mirrored tables into bronze as raw Delta tables
- Clean and normalize data in silver with proper schemas
- Create business-ready aggregated gold tables for analytics
- Provide ready-to-run analysis queries for common business questions

**Non-Goals:**
- Real-time streaming / CDC processing (we rely on mirroring sync)
- Building a full Power BI dashboard (only queries/notebooks for now)
- Automating the pipeline with scheduled triggers (manual execution first)
- Modifying the source SQL database

## Decisions

### Single Lakehouse for all layers
Use one Lakehouse with schema separation (bronze/silver/gold schemas or folder prefixes) rather than three separate Lakehouses. This simplifies cross-layer queries and reduces item sprawl.

**Alternative considered**: Separate Lakehouses per layer — rejected for complexity in a workshop/demo scenario.

### Spark notebooks for transformations
Use PySpark notebooks for all ETL between layers. Notebooks allow interactive development and are well-supported in Fabric.

**Alternative considered**: Dataflows Gen2 — rejected because Spark gives more control over complex transformations and is better for the medallion pattern.

### Read from mirrored database SQL endpoint
Bronze layer reads from the mirrored database's SQL analytics endpoint using Spark JDBC, landing data as Delta tables in the Lakehouse.

### Adventure Works table mapping
- **Bronze**: All tables from the mirrored database, as-is (SalesOrderHeader, SalesOrderDetail, Product, ProductCategory, ProductSubcategory, Customer, Address, CustomerAddress, etc.)
- **Silver**: Cleaned and joined tables (sales_orders, products, customers_with_address)
- **Gold**: Aggregated tables (sales_by_product, sales_by_geography, product_performance, sales_outliers)

## Risks / Trade-offs

- [Mirroring not configured] → User must configure the SQL source connection in the Fabric portal before bronze ingestion will work
- [Trial capacity limits] → Trial capacity has resource limits; large tables may need pagination or filtering
- [Schema drift] → If source tables change, bronze ingestion may need updates. Mitigation: bronze stores raw data as-is, schema evolution handled in silver
