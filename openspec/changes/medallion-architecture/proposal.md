## Why

The adventure works SQL database has been mirrored into a Fabric workspace (MirroredDB). We need a medallion architecture (bronze → silver → gold) to transform the raw mirrored tables into clean, analytics-ready datasets. The gold layer will power business analyses such as top-selling products, sales by geography, and outlier detection.

## What Changes

- Ingest all tables from the MirroredDB mirrored database into a bronze layer (raw, as-is)
- Transform and clean data in a silver layer (deduplication, type casting, joins)
- Build aggregated, business-oriented gold layer tables optimized for analytics
- Create analysis notebooks/queries on top of the gold layer for common business questions

## Capabilities

### New Capabilities
- `bronze-ingestion`: Read all tables from the mirrored database and land them as-is into bronze Delta tables in a Lakehouse
- `silver-transformation`: Clean, deduplicate, and normalize bronze tables into silver Delta tables with proper schemas and relationships
- `gold-aggregation`: Build business-oriented aggregated tables (sales summaries, product performance, geography breakdowns) as gold Delta tables
- `analytics-queries`: Create analysis queries and notebooks on the gold layer answering key business questions (top products, sales per geography, outliers)

### Modified Capabilities
<!-- None — this is a greenfield medallion architecture -->

## Impact

- New Lakehouse item(s) in the MirroredDB workspace for bronze/silver/gold layers
- Spark notebooks for ETL transformations between layers
- Dependency on the MirroredDB mirrored database being configured and syncing
- No breaking changes to existing items
