# KPI Dictionary — Employee Workforce & SAP Access

Numbers below describe the analyzed snapshot and must be rechecked if the source files change.

| KPI | Source/logic | Value | Business objective |
|---|---|---:|---|
| Total Employees | Final employee population | 3,212 | Trusted workforce baseline |
| Employees With SAP | Matched HR employee access records | 378 | Coverage |
| Employees Without SAP | 3,212 − 378 | 2,834 | Coverage |
| SAP Coverage % | 378 / 3,212 | 11.77% | Coverage |
| Total SAP Accounts | Combined SAP audit list | 399 | Inventory |
| Active SAP Accounts | Status = Active (complete SAP list) | 363 | Lifecycle/status |
| Non Active SAP Accounts | Status = Non Active (complete list) | 36 | Lifecycle/status |
| Matched Active Accounts | Matched subset, Active | 344 | Matched-account status |
| Matched Non Active Accounts | Matched subset, Non Active | 34 | Matched-account status |
| Matched Active Rate | 344 / 378 | 91.01% | Matched-account status |
| Overall Active Rate | 363 / 399 | 90.98% | All-account status |
| Unmatched Accounts | SAP not found in HR roster | 21 | Exceptions |
| Unmatched SAP % | 21 / 399 | 5.26% | Exceptions |
| Unmatched Active Accounts | Exception subset, Active | 19 | Priority review |
| Unmatched Non Active Accounts | Exception subset, Non Active | 2 | Priority review |
| Total Job Roles | Distinct role values | 116 | Role analysis |
| Job Roles With SAP | Roles with at least one matched SAP holder | 23 | Role analysis |
| Job Roles Without SAP | 116 − 23 | 93 | Role analysis |
| Share of Roles With SAP | 23 / 116 | 19.83% | Role distribution |
| Average SAP Coverage by Job Role | `AVERAGEX` of coverage under each role filter; skips BLANKs | 29.09% | Role-level coverage |

## Actual DAX supplied in the Power Pivot screenshots

```dax
SAP Coverage % =
DIVIDE(
    [Employees With SAP],
    [Total Employees],
    0
)

Average SAP Coverage by Job Role =
AVERAGEX(
    VALUES(Dim_Job[الوظيفة]),
    [SAP Coverage %]
)
```

The `AVERAGEX` result is **not** equal to the percentage of job roles with access. It averages per-role values across nonblank evaluated rows and treats each included role equally, irrespective of number of employees in that role.

**Validation note:** This document transcribes and interprets the displayed DAX and snapshot. It does not claim independent recalculation of the 29.09% from all underlying row-level values.
