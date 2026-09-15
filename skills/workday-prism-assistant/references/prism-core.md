# Workday Prism Analytics Core Reference

This reference is an independently written technical summary for the `workday-prism-assistant` skill. It is based on publicly available Workday Prism Analytics documentation and is intended to guide AI reasoning, not replace official documentation.

## Data-management workflow

Use this five-phase model when deciding where a requirement belongs:

1. **Acquire data.** Bring Workday or non-Workday data into the Prism Data Catalog. Tables store materialized data. Data change tasks load or change table data and can be scheduled.
2. **Transform data.** Use derived datasets to prepare data for analysis. A derived dataset can calculate fields, combine sources, filter, aggregate, reshape, or validate data through dataset stages.
3. **Apply security.** Configure the security that should govern the Prism data source before exposing the data for analysis.
4. **Make data available for analysis.** Enable a table for analysis or publish a dataset so Workday creates or refreshes the corresponding Prism data source.
5. **Analyze and visualize.** Consume the Prism data source through Workday reporting and analytical experiences such as Discovery Boards.

Architecturally, tables plus data change tasks align mainly with the extract/acquisition part of an ETL pattern, while derived datasets align mainly with transformation. Publishing or enabling for analysis makes the prepared data usable by downstream reporting.

## Core objects

### Data Catalog

The Data Catalog is the working area in which Prism users discover and manage tables and datasets available to them.

### Table

A table stores materialized data in a defined tabular schema. Use a table when the requirement is to persist acquired data that will later be transformed, combined, or analyzed.

Typical table sources include external files, external connections, and Workday custom report data.

### Data change task

A data change task loads or changes data in a table. Use it when acquisition must be repeatable or scheduled rather than performed as a one-time manual load.

When designing an ingestion process, establish whether the expected behavior is replacement, append/incremental loading, or another documented load pattern before recommending implementation details.

### Dataset

A dataset represents data that can be transformed through a pipeline. Derived datasets are especially important because they can use tables or other datasets as inputs and can contain multiple transformation stages.

### Derived dataset

Use a derived dataset when the requirement is to transform, enrich, combine, aggregate, reshape, or validate data before analysis.

A derived dataset is generally preferable to pushing complex preparation logic into a final report when the logic should be reusable or should define the analytical grain of the data source.

### Prism data source

A Prism data source is the analysis-facing representation created from prepared Prism data. Workday reports and analytical tools consume Prism data sources rather than directly consuming every internal Data Catalog object.

## Acquisition choices

Prism documentation describes multiple ways to acquire data, including:

- Uploading supported external files.
- Loading data from an SFTP source.
- Creating a table from a Workday custom report and loading the report data.
- Using supported external-system connections for data change tasks.

The documented connection portfolio includes services such as Amazon Redshift, Amazon S3, Azure Synapse, Azure Blob, BigQuery, Google Cloud Storage, Salesforce, SFTP, and Snowflake. Availability and setup can be version- and tenant-dependent, so verify current public Workday documentation before presenting a connection as enabled in a specific tenant.

## Field types and schema

Schema and field-type decisions affect parsing, joins, calculations, and publishing.

Agent checks:

- Confirm the source field type before writing conversion logic.
- Do not assume text fields containing dates are native Date fields.
- Confirm compatible types on both sides of a join or union.
- Treat destructive schema changes carefully, particularly when stored table data is involved.
- Consider NULL values explicitly because they can affect filters, arithmetic, grouping, joins, and comparisons.

## Lineage and dependencies

Prism provides lineage and dependency views for understanding how tables, datasets, and fields relate.

Use lineage when:

- A source field changed and downstream impact is unclear.
- A dataset cannot be safely deleted or modified without knowing dependents.
- A field value appears incorrect and the transformation origin must be traced.
- A pipeline has multiple derived datasets and the point of transformation is unclear.

## Security model

Do not assume that source Workday field security automatically continues to protect data once that data has been brought into the Prism Data Catalog.

Distinguish two concerns:

1. **Object access**: who can create, view, edit, manage, or own Prism objects such as tables and datasets.
2. **Analysis-facing data security**: which security domains and securing entities govern the published or enabled Prism data source and its rows/fields.

Security should be designed before analysis enablement or dataset publishing. Test published results using representative security contexts rather than testing only with an administrator account.

If the user changes data-source security on an already published dataset, remind them to verify whether the dataset must be republished for the new security configuration to apply.

## Sharing versus data-source security

Sharing a table or dataset controls access to the Prism object for users who work with it. This is not the same as configuring the security of the Prism data source used by report consumers.

The agent should not conflate dataset collaboration permissions with downstream report-data security.

## Publishing

### Tables

A table can be enabled for analysis. Recommend doing this only after the table contains the intended data and appropriate data-source security has been considered.

### Datasets

A dataset is published to make its output available as a Prism data source. Publishing can be manual or scheduled where supported.

For scheduled pipelines, distinguish:

- **Integration/acquisition schedule**: when source data is refreshed or loaded.
- **Dataset publish schedule**: when transformed output is republished for analysis.

Coordinate these schedules so publishing does not run before upstream data preparation is complete.

## Data quality and validation

Use validation as part of the pipeline when quality rules should be enforced before data reaches production reporting.

Common validation concerns include:

- Duplicate business keys.
- Missing mandatory values.
- Invalid values or types.
- Unexpected row-count changes.
- Broken referential relationships before a join.

A good production design includes explicit checks for expected row counts and grain at critical stages.

## Analytic dimensions

Prism supports analytic dimensions for scenarios where external dimension values need to behave more like Workday instance-based analytical dimensions. This can include creating analytic dimension business objects, values, hierarchies, and instance mappings.

Recommend analytic dimensions only when the requirement genuinely needs structured dimension semantics. Do not use them as a default replacement for ordinary text dimensions.

## Deletion and cleanup

Prism supports separate operations for removing data and removing analytical availability, including truncating data, deleting rows, unpublishing datasets, and deleting rows from Prism data sources in supported scenarios.

Before recommending deletion:

- Check lineage and downstream dependencies.
- Distinguish deleting source/working data from unpublishing an analytical data source.
- Confirm whether the user intends to remove all records or only selected records.

## Version-sensitive limits

Workday publishes numeric limits for Prism external data, files, fields, uploads, and publishing. These values can change by release.

Do not hardcode a numeric limit into a recommendation unless the user asks for it and the value is verified against current official Workday documentation or a dated source supplied by the user.

## Design heuristics

Use these heuristics when choosing an implementation:

- Put repeatable source acquisition in tables/data change tasks.
- Put reusable data preparation and grain definition in derived datasets.
- Aggregate before joining when the secondary source is at a more detailed grain than the desired result.
- Validate keys before joining.
- Separate security design from sharing/collaboration permissions.
- Coordinate ingestion and publish schedules.
- Prefer lineage-aware changes over isolated edits to downstream datasets.
