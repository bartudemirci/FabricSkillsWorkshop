## ADDED Requirements

### Requirement: Ingest all mirrored tables to bronze
The system SHALL read every table from the MirroredDB mirrored database SQL analytics endpoint and write them as Delta tables in the bronze layer of the Lakehouse, preserving original column names and data types.

#### Scenario: Full bronze ingestion
- **WHEN** the bronze ingestion notebook is executed
- **THEN** all tables from the mirrored database are written as Delta tables under the bronze schema/folder in the Lakehouse

#### Scenario: Table names preserved
- **WHEN** a table named `SalesOrderHeader` exists in the mirrored database
- **THEN** a corresponding Delta table `bronze.SalesOrderHeader` is created in the Lakehouse with identical columns

### Requirement: Bronze tables are overwritten on re-run
The system SHALL use overwrite mode when writing bronze tables so that re-running ingestion produces a fresh snapshot.

#### Scenario: Re-run overwrites existing data
- **WHEN** the bronze ingestion notebook is executed a second time
- **THEN** existing bronze Delta tables are overwritten with current mirrored data
