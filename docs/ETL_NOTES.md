# Power Query (M) — Transformation Notes

This document explains the intent and risk of the transformations performed in the workbook. It does **not** include employee records, credentials, or unredacted source files.

## 1. HR preparation

| Step | Applied approach | Why |
|---|---|---|
| Remove source sequencing column | Removed non-business row index | Avoid unused reporting columns |
| Normalize text | `Text.Trim`, `Text.Clean`, removal of unnecessary whitespace and control characters | Consistent matching/grouping |
| Standardize emails | Lowercase, whitespace removal, expected domain consistency | Better formatting within the data source |
| Normalize phone numbers | Removed parentheses, spaces, punctuation; standardized country-code prefix | Reduced format differences |
| Normalize Arabic jobs | Removed tatweel, corrected spacing/punctuation, separated secondment status | Group equivalent roles |
| Standardize organization labels | Cleaned department/sector/subdepartment fields and targeted variants | Reduce duplicate category labels |
| Deduplicate | `Table.Distinct` applied on the final employee query | Source 3,215 rows to final 3,212 |

## 2. SAP extraction

- Split Active and Non Active lists, then renamed their columns to a common schema.
- Added `Status`, removed missing SAP IDs, appended tables into `SAP_Users`.
- Derived the HR matching identifier from the SAP ID text **after a period**.
- Cleaned text fields before matching.

## 3. Model-building merges

`Fact_Employee_Access` uses **three left-outer merges** to incorporate job keys, department keys, and SAP identity/status. An extract of the actual M joining pattern:

```powerquery
#"Merged Queries2" = Table.NestedJoin(
    #"Removed Other Columns", {"رقم"},
    SAP_Users, {"Employee ID"},
    "SAP_Users", JoinKind.LeftOuter
)
```

A separate `SAP_Unmatched_Users` query matches the **other way around**—from SAP accounts to HR—then keeps accounts with no HR record match.

## 4. Data quality and refresh risks

1. **Employee ID:** ensure all HR identifiers have consistent types (text is often safest if leading zeroes are possible).
2. **Identifier extraction:** review SAP IDs without the expected delimiter or whose suffix is not an employee ID.
3. **Cardinality:** identify repeated SAP employee IDs, which might multiply joined employee rows.
4. **Deduplication:** three exact duplicate rows were removed, but also validate unique employee IDs and dimension keys.
5. **Email standardization:** check that replacing domains does not alter valid nonstandard emails.
6. **Source snapshots:** refresh HR and SAP extracts from comparable dates before drawing conclusions.
7. **Reconciliation:** unmatched SAP accounts may be service identities, stale HR data, external users, mapping problems or issues requiring access review. They should not automatically be disabled.
