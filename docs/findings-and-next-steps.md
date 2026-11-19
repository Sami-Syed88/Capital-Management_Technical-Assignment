# Findings, Limitations and Next Steps

## Data quality findings

| Finding | Action taken |
| --- | --- |
| `EXP-0021` appeared twice with identical records | Removed one verified duplicate; fact record count changed from 49 to 48. |
| `EXP-0011` had blank RWA and CapitalRequirement | Preserved the blanks and flagged the record in `DQ_Status`. |
| `CP011` was absent from the counterparty master | Added a provisional “Unknown counterparty” dimension record using the PL country code shown in the source fact data. |
| Currency formatting was inconsistent (`eur` versus `EUR`) | Standardized codes using Power Query text transformations. |
| An exposure amount was stored as text with thousands separators | Removed separators and converted it to a numeric type. |
| PLN and SEK appeared in the Currency field | Did not convert amounts again because the supplied monetary values are already in EUR. |

## Known limitations

- February Actual RWA is incomplete because `EXP-0011` has a missing RWA value. Related figures should be interpreted with this limitation in mind.
- `CP011` still needs complete, authoritative counterparty master data. The added row is a reporting workaround, not a master-data correction.
- The supplied sample covers a limited number of reporting months, so trend analysis is limited to those months.
- The provided security email addresses are demonstration identities, not confirmed production users.

## If this were moved to production

I would work with the Data Engineering team to move large-scale validation, exception logging, source reconciliation, and counterparty master-data management upstream.

As the Power BI Developer, I would focus on a governed reusable semantic model, appropriate RLS and security-group access, source control through Git/Azure DevOps, and deployment pipelines across Development, Test, and Production. Incremental refresh and model optimization would be assessed based on actual data volumes and performance requirements.
