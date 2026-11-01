# Publication checklist — Employee Workforce & SAP Access Analytics

Complete the checks below **before publicly committing** the Excel workbook. An unchecked item is not a claim that it has been verified.

## 1. Authorization and data protection

- [ ] Confirm that permission covers the **full `workbook/Employee SAP Project.xlsx` file**, not only dashboard screenshots and aggregate statistics.
- [ ] Review the workbook’s **visible and hidden sheets, Power Query (M) definitions, Power Pivot model tables, PivotTable caches, connections, source paths, external links and file metadata**.
- [ ] Confirm there are no credentials, secrets or personal/internal records outside the approved publication scope.
- [ ] Confirm dashboard images are approved for public display, including department/sector labels and summary SAP account information.
- [ ] Confirm separate raw HR and SAP source extracts are **not** included in the repository.

## 2. Dashboard and KPI validation

- [x] The corrected SAP Exceptions screenshot shows **19 Active** and **2 Non Active** unmatched accounts.
- [x] README distinguishes **29.09% average role-level SAP coverage** from **19.83% share of job roles with SAP**.
- [ ] Validate KPIs, employee–SAP matching logic and join cardinality against the final workbook.
- [ ] Confirm the Exceptions-page slicer scope is clear: status filters its chart, while top KPIs show overall totals.

## 3. Repository publication checks

- [ ] `README.md` renders in the repository root and its Mermaid architecture displays correctly.
- [ ] All dashboard and data-model images under `images/` load with the names referenced in README.
- [ ] Both `docs/ETL_NOTES.md` and `docs/KPI_DICTIONARY.md` open.
- [ ] `workbook/Employee SAP Project.xlsx` opens correctly, and the README link works.
- [ ] `.gitignore` excludes unrelated data exports and preserves only the intended workbook exception.
- [ ] Only reviewed files are present in the GitHub upload list **before committing**.

## Publication disclosure

The repository is intended to include project documentation, approved dashboard screenshots, and a downloadable Excel workbook for portfolio review. Separate raw HR and SAP source exports are not provided. The workbook may contain transformed or cached analytical data and must undergo full publication-scope review before being committed to a public repository.

This is a historical analytical snapshot. Unmatched identities are reconciliation exceptions rather than confirmed unauthorized access; recommendations are proposed, not implemented remediation.
