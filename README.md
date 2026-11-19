# Capital Management – Technical Assignment

## Overview

This Power BI assignment covers Risk-Weighted Assets (RWA), capital requirements, and Actual versus Budget reporting for a capital management team. Country managers need access to their assigned countries, while group viewers need a consolidated view.

The solution includes data preparation in Power Query, a star-schema semantic model, DAX measures, interactive reporting, and row-level security (RLS).

## What I implemented

- Loaded and prepared the six supplied CSV files in Power Query, including type conversion, text standardization, and data quality checks.
- Built a star-schema model with five dimensions, a daily 2026 date table, and single-direction relationships to `Fact_Exposure`.
- Created RWA and capital requirement measures, Actual versus Budget comparisons, variances, previous-month analysis, and a rolling three-month average.
- Added dynamic country-based RLS using the supplied user-country mappings, plus a separate Group Viewer role.
- Built report views for financial performance, trends, and investigation of data quality exceptions.

## Main findings

One identical duplicate exposure (`EXP-0021`) was removed after validation, reducing `Fact_Exposure` from 49 to 48 records. `EXP-0011` has missing RWA and capital requirement values; these were left blank and flagged. `CP011` was missing from the counterparty master data, so a provisional “Unknown counterparty” entry was added using the Poland country code present in the source exposure data. Currency codes were standardized and text-formatted amounts converted to numeric values.

The supplied monetary amounts were treated as EUR, as instructed; no additional currency conversion was applied. February Actual RWA remains incomplete because of the missing RWA value.

## Repository guide

- **Power BI project files (`.pbip`, `.Report`, `.SemanticModel`):** data preparation logic, model definitions, measures, RLS, and report definitions. These files are exported separately from Power BI Desktop and should be added to this repository.
- [`docs/implementation-notes.md`](docs/implementation-notes.md): key data preparation, modeling, and security decisions.
- [`docs/findings-and-next-steps.md`](docs/findings-and-next-steps.md): findings, limitations, and possible production improvements.

## Opening the project

Open the `.pbip` file in Power BI Desktop after downloading the complete project folder. Local CSV paths or credentials may need to be updated for a different environment. The input files and sample security identities should only be shared where authorized.

*This is a technical assignment based on supplied sample data, not a production reporting system.*
