# Implementation Notes

## Data preparation

I loaded the six supplied CSV files in Power Query. I kept raw exposure and counterparty queries separate from the reporting tables and added four validation queries for duplicate exposures, missing financial values, unmatched counterparties, and currency formatting. These validation queries are not loaded into the semantic model.

After confirming `EXP-0021` was an identical duplicate, I removed the duplicate in the reporting fact table. Text fields and currency codes were standardized, and comma-separated monetary values were converted to numeric types. Missing RWA and capital requirement values were retained rather than replaced with zero. The `DQ_Status` field can show multiple issues for the same exposure.

## Semantic model and measures

The model follows a star schema with five dimensions and single-direction relationships to `Fact_Exposure`. A daily 2026 date table supports the time-based measures.

- Actual and Budget measures explicitly select their respective scenarios so they can be compared regardless of the scenario slicer selection.
- Variance measures return blank when either scenario is unavailable, rather than showing a potentially misleading comparison.
- The rolling three-month Actual RWA average considers only months with available Actual RWA data.
- The separate capital buffer measure adds 2.5% of RWA. The original Capital Requirement % calculation has not been changed.
- Monetary values are treated as EUR in line with the assignment's additional requirement; PLN and SEK currency codes do not trigger further conversion.

## Report and access control

The report provides Actual versus Budget analysis, trend measures, and detail-level investigation of exceptions. Dynamic Country Manager RLS uses a user-to-country mapping table to support single- or multi-country access. A separate Group Viewer role supports consolidated access.

I tested the RLS behavior using the supplied sample users and Power BI Desktop's **View as** option. Power BI Service access and role assignments would need to be validated before production use.
