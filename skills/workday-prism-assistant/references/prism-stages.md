# Workday Prism Dataset Stage Reference

This file is an independently authored decision guide for choosing and reasoning about Prism dataset stages.

## Stage selection matrix

| Requirement | Preferred stage | Main effect |
| --- | --- | --- |
| Bring source data into a derived-dataset pipeline | Import | Establishes the pipeline source; Workday creates it automatically where required. |
| Describe/parse external source data | Parse | Interprets source data into tabular fields; Workday creates it automatically for applicable base-dataset flows. |
| Turn each value of a multi-instance field into its own row | Explode | Increases rows based on instance values. |
| Keep only rows that meet conditions | Filter | Reduces rows. |
| Aggregate detailed rows to a higher grain | Group By | Reduces rows and changes grain. |
| Add related columns from another source based on matching keys | Join | Combines fields across pipelines; may multiply rows if key cardinality is not controlled. |
| Select, hide, or adjust dataset fields | Manage Fields | Changes field presentation/selection without being a substitute for business-key transformation. |
| Append similar datasets vertically | Union | Adds rows from another dataset/table using mapped compatible fields. |
| Convert repeated columns into attribute/value rows | Unpivot | Converts columns to rows and reshapes the dataset. |
| Detect data-integrity problems before downstream use | Validation | Applies quality rules such as duplicate/error detection. |

## Import

Use Import as the source stage in a derived dataset. It represents the input table or dataset for a pipeline.

Agent behavior:

- Do not tell users to manually add or remove Import when Workday manages it automatically.
- Focus instead on whether the selected source is the correct object and grain.

## Parse

Use Parse when external source data must be interpreted into a tabular schema in a supported base-dataset flow.

Agent behavior:

- Distinguish parsing raw external data from changing a field type later in a derived transformation.
- Do not imply that Parse is an arbitrary transformation stage that can be added anywhere.

## Explode

Explode converts one row containing a multi-instance field into multiple rows, typically one per instance value.

Example requirement:

A row contains Worker W001 with Cost Centers CC10 and CC20 in a multi-instance field. The desired output is one row for W001/CC10 and one row for W001/CC20.

Use Explode.

Validation checks:

- Compare row count before and after the stage.
- Confirm downstream measures are not double-counted after row multiplication.
- Confirm whether repeated non-exploded values are expected on every generated row.

## Filter

Use Filter to restrict rows based on conditions.

Use basic filter configuration for straightforward criteria and advanced expressions when the logic requires Prism Boolean expressions.

Agent checks:

- Confirm the field type of both sides of a comparison.
- Handle NULL intentionally.
- Confirm whether multiple conditions require AND or OR.
- For date conditions, distinguish advanced Filter-stage date-literal rules from calculated-field expressions.

## Group By

Use Group By when the desired dataset grain is higher than the source grain.

Typical uses:

- Sum transaction values by organization and month.
- Count rows by category.
- Calculate aggregate measures before joining to a higher-grain dataset.

Common summarization concepts include count, minimum, maximum, average, and sum where supported by the field type.

Agent checks:

- State the grouping fields explicitly.
- State the resulting grain explicitly.
- Confirm measures use compatible summarization.
- Be cautious with currency values that may contain multiple currency codes in one group.

## Join

Use Join when the requirement is to combine related columns from two sources based on matching values.

Before recommending a Join, establish:

- Primary pipeline
- Secondary pipeline/source
- Join key on each side
- Grain of each side
- Expected cardinality: one-to-one, many-to-one, one-to-many, or many-to-many
- Desired treatment of unmatched rows

### Join risk model

A Join is safe only when the cardinality matches the expected output grain.

Example:

Primary dataset grain: one row per Worker.
Secondary dataset grain: one row per Worker per Skill.
Requirement: add one Skill Category to each worker.

A direct join can create multiple rows per Worker. The agent should first determine whether the secondary data must be filtered, ranked, or aggregated to one row per Worker.

### Join troubleshooting

When row counts unexpectedly increase:

1. Check duplicate join keys on the secondary side.
2. Check whether both sides are many-to-many.
3. Check whether a Group By or deduplication step is needed before the Join.
4. Check NULL or nonmatching key values.
5. Compare row counts before and after the Join stage.

## Manage Fields

Use Manage Fields to control the fields carried forward in a pipeline and to make supported field-level adjustments.

Use it to reduce unnecessary fields before expensive downstream transformations where appropriate.

Do not use Manage Fields as a substitute for Group By, Join, Union, or type-conversion logic.

## Union

Use Union when the requirement is to append rows from similar sources.

Example:

Dataset A contains 2025 sales rows.
Dataset B contains 2026 sales rows.
Both represent the same business grain and have compatible fields.

Use Union to produce one combined sales dataset.

Agent checks:

- Confirm that the sources represent the same logical grain.
- Confirm field mappings and compatible field types.
- Identify fields present on only one side and how missing values should behave.
- Do not recommend Union when the user actually needs columns from another source; that is a Join problem.

## Unpivot

Use Unpivot when repeated measures are stored across multiple columns and analysis requires them as rows.

Example input shape:

| Worker | Jan_Hours | Feb_Hours | Mar_Hours |
| --- | ---: | ---: | ---: |
| W001 | 160 | 152 | 168 |

Desired analytical shape:

| Worker | Month | Hours |
| --- | --- | ---: |
| W001 | Jan | 160 |
| W001 | Feb | 152 |
| W001 | Mar | 168 |

Use Unpivot.

Agent checks:

- Identify the columns to unpivot.
- Name the generated attribute and value fields clearly.
- Verify downstream grain and row-count increase.

## Validation

Use Validation to detect data-quality issues before production reporting.

Good candidates include:

- Duplicate natural/business keys.
- Missing mandatory identifiers.
- Invalid source values.
- Records that violate pipeline assumptions.

When a validation rule fails, diagnose the upstream source or transformation rather than automatically filtering the bad rows out.

## Recommended stage ordering

There is no universal stage order, but use this reasoning sequence:

1. Remove irrelevant rows early with Filter when doing so does not change required semantics.
2. Normalize types/fields before key-dependent transformations.
3. Aggregate to the correct grain before Join when necessary.
4. Join or Union only after grain and field compatibility are understood.
5. Reshape with Explode or Unpivot deliberately because both can materially change row counts.
6. Validate critical assumptions before publishing.

Always judge the sequence from the business grain and expected downstream use rather than applying a fixed recipe.
