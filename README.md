# **Measure Killer**

an external tool for Microsoft Power BI Desktop.

## Cleaning up your Power BI tenant

Measure Killer can help you clean and optimize your tenant and datasets. This can drastically reduce dataset refresh times and thus lower the memory and CPU usage of your Premium capacity. Since we use the XMLA connection, the dataset can remain in the service. Additionally, we only analyze the metadata, we do not read the actual data in your dataset.

## Deleting unused measures

Measure Killer can delete unused measures on its own if the user chooses so. Alternatively it can generate a C# script for the measures to be deleted via Tabular Editor manually.

Deleting unused columns will also improve performance since less RAM will be consumed.

## Deleting unused columns

Measure Killer will generate an M-Code to delete unused columns. This code can be pasted into Power Query's Advanced Editor to remove these columns from the model

## Analyzing reports

For every report analyzed, Measure Killer will generate a comprehensive Excel file to show where an artifact is used. This can be in: Measures, Visuals, Filters, Conditional Formatting, Joins in Power Query, or other parts of a Power BI Report such as Relationships.

Furthermore, Measure Killer can generate a chart to show the number of unused and used columns and measures.

​

​

## What does Measure Killer detect?

- Visuals - including filters applied to visuals, on pages or the whole report.
- Artifacts only used in custom visuals (see compatibility matrix below for details)
- Any kind of measure or relationship
- Columns used exclusively in Power Query, e.g. in joins, appends, references etc.
- Calculated columns
- Calculated tables
- Conditional formatting

​

**What does not work?**

- If you copy whole reports and then only do some minor changes, this can lead to false references.
- If you create new queries from existing queries in Power Query it is possible that MK will reference columns (e.g. selected columns / removing columns) that have already been removed in the existing query.
- If a query B (child) references a query A (parent) via e.g. an append, join etc. and those queries have the same column names. If we now have an M reference in one of these columns in query B it will wrongly flag the same column in query A as used.
- DAX expressions like COUNTROWS that only reference a table are not considered unless there is a column or measure referenced as well.
- Several runs may be necessary to delete all unused columns and measures. (There can be artifacts, that are only referenced in unused measures or columns but are not actually used anywhere in the report.)
- Default titles and subtitles (created by Power BI / default) will not be recognized. If you change the titles in any way they will be detected though.

**Measure Killer Compatibility**

​

**L**** egend**

✅ fully compatible

 ?   limited compatibility

 ✗  currently not working

​

**General**

✅ .pbix (Desktop and Desktop RS)

✅ .pbix (Uploaded to PBI Service)

✅ .pbip (paid versions only)

✅ .pbir (paid versions only)

✅ .pbit (paid versions only)

✅ Thin files

✅ DirectQuery

✅ Composite models

✅ Paginated reports (paid versions only)

✅ Analyze in Excel (paid versions only)

​

✗ Thin files (.pbix live connection) that cannot be download using the Power BI Service - [link](https://learn.microsoft.com/en-us/power-bi/create-reports/service-export-to-pbix#limitations-when-downloading-a-report-pbix-file)

✗ Dashboards

✗ Any type of live connection (SSAS, AAS, Datamarts) - create a local mode (DQ) to make it work!

✗ .bim files / models stored in a folder etc.

✗ Metrics (Goals)

​

**Feature compatibility:**

✅ Row-level security

✅ Calculation groups

✅ Field parameters

✗ KPIs (created in the tabular model)

✗ Object-level security (When an artifact is only used in OLS, Measure Killer will not detect it)

​

**Compatibility of visuals:**

✅ Standard visuals (all, unless listed below)

✅ Icon Map

✅ Zebra BI visuals

✅ HTML VizCreator Cert

✅ HTML VizCreator Flex

✅ Balance Sheet Visual

?  Other custom visuals (We have not tested Measure Killer for all custom visuals)

✗ Q&A visual

✗ Paginated report visual

✗ Metrics (Goals) visual
