# Data Contract — Aeroflot databook → KPI stage

Governed by `PROJECT_RULES.md`; companion to `reference/source_map.md` (generated 2026-11-12). Defines what the KPI stage (`app/`, `outputs/kpi.json`) may read and how. Contains no values.

## 1. Source

| Item | Contract |
|---|---|
| File | exactly one real `.xlsx` in the repository root, `~$*` ignored; currently `2026-08__Databook_Aeroflot_ENG_1.xlsx` (§15.1–15.2) |
| Hash | SHA-256 must equal `3ebd7863eae6094982d8bcccdaac5e20aae6d06a036233c37542f668036f1fb1` (§0) or the run is flagged (§13.3) |
| Open mode | `load_workbook(path, read_only=True, data_only=True)`; formula text only via `data_only=False`, never evaluated; never saved (§13) |
| Language | `Contents!L5` must read `ENG`; it is never changed (§13.1). Column B labels are cached results of `=IF(Contents!$L$5="РУС",D,C)`; the KPI stage asserts B == C for every matched row |
| Values | cached values only; every financial data cell on core sheets is a constant |

## 2. Row location

- Match English label in column **B**, scoped to sheet + section (table below), unique within the section (§15.3.4). Read and store D (Russian) for verification.
- Normalisation: NFC, NBSP→space, trim, collapse whitespace, case-fold; keep `*` markers and typos (§15.3.2).
- Outcomes: 0 matches → `N/A (LABEL_NOT_FOUND)`; >1 → `N/A (LABEL_AMBIGUOUS)`; B/D mismatch → `N/A (LABEL_AMBIGUOUS)`.
- Cached row numbers below are hints only and are re-verified on every run (§15.3.3).

| Metric ID | Sheet | Section (rows) | English label (B) | Row hint | Flow/stock |
|---|---|---|---|---|---|
| `CFO` | `Cash Flow` | Operating activities (8–50) | `Net cash flows from operating activities` | 50 | flow |
| `CFI` | `Cash Flow` | Investing activities (52–72) | `Net cash flows from/(used in) investing activities` | 72 | flow |
| `CAPEX_PPE_INTANG` | `Cash Flow` | Investing activities (52–72) | `Purchases of property, plant and equipment and intangible assets` | 59 | flow |
| `CAPEX_PREPAY_AIRCRAFT` | `Cash Flow` | Investing activities (52–72) | `Prepayments for aircraft` | 63 | flow |
| `LEASE_PRINCIPAL_IFRS16` | `Cash Flow` | Financing activities (74–89) | `Repayment of the principal element of lease liabilities (IFRS 16)` | 78 | flow |
| `LEASE_PRINCIPAL_IAS17` | `Cash Flow` | Financing activities (74–89) | `Repayment of the principal element of finance lease liabilities (IAS 17)` | 77 | flow |
| `FCF_DATABOOK_REPORTED` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `Free cash flow (CFO + CFI)` | 25 | flow |
| `CAPEX_DATABOOK` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `Capital expenditures**` | 24 | flow |
| `ST_BORROWINGS` | `Financial Position` | Current liabilities (38–49) | `ST loans and borrowings and current portion of long-term loans and borrowings` | 46 | stock |
| `LT_BORROWINGS` | `Financial Position` | Non-current liabilities (50–59) | `Long-term loans and borrowings` | 51 | stock |
| `LEASE_IFRS16_CURRENT` | `Financial Position` | Current liabilities (38–49) | `Lease liabilities (IFRS 16)` | 44 | stock |
| `LEASE_IFRS16_NONCURRENT` | `Financial Position` | Non-current liabilities (50–59) | `Lease liabilities (IFRS 16)` | 52 | stock |
| `LEASE_IAS17_CURRENT` | `Financial Position` | Current liabilities (38–49) | `Finance lease liabilities (IAS 17)` | 45 | stock |
| `LEASE_IAS17_NONCURRENT` | `Financial Position` | Non-current liabilities (50–59) | `Finance lease liabilities (IAS 17)` | 53 | stock |
| `CASH` | `Financial Position` | Current assets (9–20) | `Cash and cash equivalents` | 10 | stock |
| `ST_FIN_INVESTMENTS` | `Financial Position` | Current assets (9–20) | `Short-term financial investments` | 11 | stock |
| `PENSION_LIABILITIES` | `Debt Profile` | Debt/liquidity rows 14–31 (14–31) | `Pension liabilities` | 14 | stock |
| `PENSION_ROIC_XCHECK` | `ROIC` | Invested capital (19–25) | `Pension obligation – non-current portion` | 21 | stock |
| `NET_DEBT_DATABOOK` | `Debt Profile` | Debt/liquidity rows 14–31 (14–31) | `Net debt` | 17 | stock |
| `NET_DEBT_EBITDA_DATABOOK` | `Debt Profile` | Debt/liquidity rows 14–31 (14–31) | `Net debt/EBITDA` | 27 | ratio |
| `REVENUE` | `Profit and Loss, OCI` | Income statement (rows 8–29) (8–29) | `Revenue` | 10 | flow |
| `TRAFFIC_REVENUE` | `Profit and Loss, OCI` | Income statement (rows 8–29) (8–29) | `Traffic revenue` | 8 | flow |
| `OPERATING_PROFIT` | `Profit and Loss, OCI` | Income statement (rows 8–29) (8–29) | `Operating profit` | 18 | flow |
| `PBT` | `Profit and Loss, OCI` | Income statement (rows 8–29) (8–29) | `Profit/(loss) before income tax` | 26 | flow |
| `NET_PROFIT` | `Profit and Loss, OCI` | Income statement (rows 8–29) (8–29) | `PROFIT/(LOSS) FOR THE YEAR` | 29 | flow |
| `EBITDA` | `EBITDA` | EBITDA table (8–23) | `EBITDA` | 11 | flow |
| `EBITDAR` | `EBITDA` | EBITDA table (8–23) | `EBITDAR` | 13 | flow |
| `EBITDA_MARGIN_REPORTED` | `EBITDA` | EBITDA table (8–23) | `EBITDA margin` | 17 | ratio |
| `OPERATING_MARGIN_REPORTED` | `EBITDA` | EBITDA table (8–23) | `Operating profit margin` | 16 | ratio |
| `NET_MARGIN_REPORTED` | `EBITDA` | EBITDA table (8–23) | `Net income margin` | 19 | ratio |
| `CFF` | `Cash Flow` | Financing activities (74–89) | `Net cash used in financing activities` | 89 | flow |
| `TOTAL_EQUITY` | `Financial Position` | Equity (61–73) | `TOTAL EQUITY` | 73 | stock |
| `CFO_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `Net Operating Activities (CFO)` | 21 | flow |
| `CFI_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `Net Investing Activities (CFI)` | 22 | flow |
| `CFF_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `Net Financing Activities (CFF)` | 23 | flow |
| `REVENUE_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `Revenue` | 12 | flow |
| `EBITDA_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `EBITDA` | 14 | flow |
| `EBITDAR_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `EBITDAR` | 13 | flow |
| `NET_PROFIT_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `Net Profit` | 15 | flow |
| `NET_DEBT_EBITDA_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `Net Debt/12M EBITDA (х)` | 33 | ratio |
| `GROSS_DEBT_EBITDA_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `Gross Debt/EBITDA 12M(х)` | 32 | ratio |
| `EBITDA_INTEREST_COVER_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `EBITDA/Gross Interest (х)***` | 31 | ratio |
| `ROIC_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `ROIC (%)` | 30 | ratio |
| `BANK_DEBT_EQUITY_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `Bank Debt/Equity (х)` | 34 | ratio |
| `PAX_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `PAX, mn` | 8 | flow |
| `RPK_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `RPK, bn` | 9 | flow |
| `PLF_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `PLF, %` | 10 | ratio |
| `FLEET_HR` | `Highlights and Ratios` | Highlights (rows 8–35) (8–35) | `Aircraft, #` | 11 | stock |
| `PAX_GROUP` | `AFLT - Operating - abs` | Aeroflot Group (8–36) | `Passengers carried, thd` | 9 | flow |
| `RPK_GROUP` | `AFLT - Operating - abs` | Aeroflot Group (8–36) | `Passenger turnover, mn RPK` | 12 | flow |
| `ASK_GROUP` | `AFLT - Operating - abs` | Aeroflot Group (8–36) | `Available seat-kilometers, mn ASK` | 15 | flow |
| `PLF_GROUP` | `AFLT - Operating - abs` | Aeroflot Group (8–36) | `Passenger load factor, %` | 18 | ratio |
| `RPK_RC` | `RASK-CASK` | Revenue/traffic table rows 8–34 (8–34) | `RPK, mn` | 17 | flow |
| `ASK_RC` | `RASK-CASK` | Revenue/traffic table rows 8–34 (8–34) | `ASK, mn` | 25 | flow |
| `YIELD_TRAFFIC` | `RASK-CASK` | Yield (REV/RPK), RUB (36–48) | `Traffic revenue` | — | ratio |
| `RASK_TRAFFIC` | `RASK-CASK` | RASK (REV/ASK), RUB (50–62) | `Traffic revenue` | — | ratio |
| `CASK_TOTAL` | `RASK-CASK` | CASK table (header row 99) (99–123) | `Total CASK` | 120 | ratio |
| `CASK_EX_FUEL` | `RASK-CASK` | CASK table (header row 99) (99–123) | `Ex-fuel CASK` | 118 | ratio |
| `ASK_FUEL_SHEET` | `Fuel Consumption` | Fuel metrics rows 8–13 (8–13) | `Available seat-kilometers, mn ASK` | 9 | flow |
| `ATK_FUEL_SHEET` | `Fuel Consumption` | Fuel metrics rows 8–13 (8–13) | `Available tonne-kilometers, mn ATK` | 10 | flow |
| `PAX_REGIONS_TOTAL` | `AFLT - Regions` | PAX, mn (9–18) | `Total` | 18 | flow |
| `RPK_REGIONS_TOTAL` | `AFLT - Regions` | RPK, bn (19–28) | `Total` | 28 | flow |
| `ASK_REGIONS_TOTAL` | `AFLT - Regions` | ASK, bn (29–38) | `Total` | 38 | flow |
| `PLF_REGIONS_TOTAL` | `AFLT - Regions` | PLF, % (39–48) | `Total` | 48 | ratio |
| `FX_EFFECT_ON_CASH` | `Cash Flow` | Cash reconciliation (no header) (90–95) | `Effect of exchange rate fluctuations on cash and cash equivalents` | 91 | flow |
| `FX_GAIN_LOSS_ADJ` | `Cash Flow` | Operating activities (8–50) | `Foreign exchange (gain)/loss` | 26 | flow |
| `INTEREST_EXPENSE_ADJ` | `Cash Flow` | Operating activities (8–50) | `Interest expense` | 24 | flow |
| `INTEREST_INCOME_ADJ` | `Cash Flow` | Operating activities (8–50) | `Interest income` | 25 | flow |
| `FINANCE_INCOME` | `Profit and Loss, OCI` | Income statement (rows 8–29) (8–29) | `Finance income` | 21 | flow |
| `FINANCE_COSTS` | `Profit and Loss, OCI` | Income statement (rows 8–29) (8–29) | `Finance costs` | 22 | flow |
| `OCI_TRANSLATION` | `Profit and Loss, OCI` | OCI (40–47) | `Translation from the functional currency to the presentation currency` | 43 | flow |
| `CASH_OPENING_CF` | `Cash Flow` | Cash reconciliation (no header) (90–95) | `Cash and cash equivalents at the beginning of the year` | 94 | stock-in-flow-sheet |
| `CASH_CLOSING_CF` | `Cash Flow` | Cash reconciliation (no header) (90–95) | `Cash and cash equivalents at the end of the year` | 95 | stock-in-flow-sheet |
| `INTEREST_ROIC` | `ROIC` | Return (11–16) | `Interest` | 15 | flow |
| `INTEREST_CAP_OL_ROIC` | `ROIC` | Return (11–16) | `Interest on capitalized operating lease` | 16 | flow |

Operating-expense lines and cash-flow components are located the same way; see `source_map.md` for each row.

## 3. Periods and columns

Columns are found by parsing the header row, never by letter (§6.1.5). Column letters are current hints.

| Period ID suffix | Meaning | Sheets | Header row | Header must parse to | Column hint |
|---|---|---|---|---|---|
| `_FY2025` | 12 months to 31 Dec 2025 | Cash Flow, P&L, EBITDA, Revenue, Operating Expenses, Fuel Consumption | 7 | text `12M 2025` (Latin M) | BW |
| `_FY2025` | annual | Highlights and Ratios, Debt Profile (flow/ratio rows), ROIC (flow rows), RASK-CASK, AFLT - Operating - abs | 7 | integer `2025` | S |
| `_FY2025` | annual | AFLT - Regions | 8 | integer `2025` — duplicated S8/AL8: block selection needs owner approval | S (Group) |
| `_H1_2025` | YTD to 30 Jun 2025 (input to LTM only) | flow sheets | 7 | text `6M 2025` | BU |
| `_H1_2026` | YTD to 30 Jun 2026 | flow sheets | 7 | text `6M 2026` | BY |
| `_BS_2025_12_31` | balance at 31 Dec 2025 | Financial Position | 7 | datetime 2025-12-31 | BW |
| `_BS_2026_03_31` | balance at 31 Mar 2026 | Financial Position | 7 | datetime 2026-03-31 | BX |
| `_BS_2026_08_31` | balance per header 31 Aug 2026 — **unproven**, equals file date | Financial Position | 7 | datetime 2026-08-31 | BY |
| `_BS_2025_12_31` | balance from annual sheets | Debt Profile, ROIC (stock rows) | 7 | integer `2025` — only after §6.1.6 reconciliation | S |

Rules: flows and stocks never share a period type (§6.1.1); YTD columns are cumulative; quarters/LTM are separately named CALCULATIONs (§6.1.3); H1 flows are never annualised; a header that is not one of the three formats (e.g. Cyrillic `12М 2025`, text `31-Dec-2025`) is `HEADER_AMBIGUOUS`.

## 4. Field schema (one record per source cell)

| Field | Type | Notes |
|---|---|---|
| `metric_id` | string | stem + period suffix, e.g. `CFO_FY2025` |
| `evidence_label` | enum | `FACT` for source cells (§4) |
| `workbook` | string | file name |
| `workbook_sha256` | string | hash at read time |
| `sheet` | string | exact sheet name |
| `cell` | string | e.g. `'Cash Flow'!BW50` |
| `section` | string | section header text and row |
| `label_en` | string | raw column-B text |
| `label_ru` | string | raw column-D text |
| `header_cell` | string | e.g. `BW7` |
| `header_raw` | string | as read (text / int / ISO date) |
| `period_id` | string | mapped period |
| `cell_kind` | enum | `formula` / `constant` / `empty` |
| `formula_text` | string|null | only when formula |
| `cached_value_present` | bool |  |
| `value_raw` | string | `str(x)` of the stored value, converted with `Decimal(str(x))` (§12.1.2) |
| `display_format` | string | number format |
| `unit` | string | e.g. `RUB million`, `mn RPK`, `fraction` |
| `unit_source_cell` | string | B7 or the row label cell (§6.2.2) |
| `flow_or_stock` | enum | `flow` / `stock` / `ratio` |
| `sign_as_stored` | bool | always true; no flips (§12.3) |
| `status` | enum | `OK` / `N/A` |
| `na_reason` | enum|null | §11 code |
| `flags` | list | e.g. `BS_DATE_NOT_PERIOD_END`, `BS_DATE_EQUALS_FILE_DATE`, `SUSPECT_ZERO`, `UNIT_CONFLICT`, `HIDDEN_CELL` |

## 5. Value rules

- `-` → `N/A (DASH_PLACEHOLDER)`; blank → `N/A (MISSING_CELL)`; text/error → `N/A (NON_NUMERIC)`; numeric `0` is a FACT unless contradicted (`SUSPECT_ZERO`, §11.5). N/A is never 0 and propagates as `INPUT_NA` (§11).
- Numbers: `Decimal(str(x))`; no float arithmetic; full precision stored as strings; rounding only at presentation, `ROUND_HALF_UP` (§12).
- Units: row-label unit overrides B7; no unit → `N/A (UNIT_UNDECLARED)`; `%` rows stored as fractions (§6.2).
- Signs: as stored; capex and lease principal used as magnitudes only after checking stored value ≤ 0, otherwise `SIGN_AMBIGUOUS` (§12.3.2).

## 6. Known blockers for the KPI stage (from the audit)

1. **Workbook location (§15.2, §16.1).** The databook is only on branch `claude/dreamy-gates-aff9hw`. May it be added to the repository root of the working branch as the designated source (hash unchanged)?
2. **Balance-sheet date (§6.1.2, §16.1).** `'Financial Position'!BY7` = 2026-08-31 equals the file/update date and the CF `6M 2026` closing cash equals FP BY10. Is BY a 30 Jun 2026 balance with the update date typed into the header, or a genuine 31 Aug 2026 balance? Until confirmed it stays `_BS_2026_08_31` with `BS_DATE_NOT_PERIOD_END` and `BS_DATE_EQUALS_FILE_DATE`.
3. **Mapping file (§15.3.6).** Approve a label-to-metric mapping file (sheet, section, English B label, expected Russian D label, metric ID) — path and content need written approval.
4. **§0 corrections (§16.1).** §0 misdescribes the label columns (B/C), the FP header types (text before column BB) and the flow header characters (Cyrillic `М` on Operating Expenses). Update §0?
5. **Cyrillic `М` headers (§6.1.5, §15.3.2).** Operating Expenses `12М 2025`, `6М 2025` (and others) do not parse. May the normalisation map Cyrillic `М` to Latin `M` for period headers, or must these columns stay N/A?
6. **Units (§6.2.2).** `Operating Expenses` and `Debt Profile` declare no unit; route/region child rows and RASK-CASK sub-tables declare units only in section labels. Which source declares their unit, if any?
7. **Duplicate 2018 and 2025 headers (§6.1.5).** For 2018 use K (IAS 17) or L (IFRS 16)? On `AFLT - Regions` may the Group block (E–S) be selected by the row-6 block header?
8. **B/D label mismatches (§15.3.5).** Debt Profile rows 12 and 16, Highlights row 34, ROIC row 21, RASK-CASK rows 118/120 — how should each be resolved?
9. **Debt Profile / ROIC as `_BS_2025_12_31` (§6.1.6).** Lease rows need summation to reconcile; may that reconciliation be performed in the KPI stage before these stock rows are used?

## 7. Reason codes

`MISSING_CELL`, `DASH_PLACEHOLDER`, `LABEL_NOT_FOUND`, `LABEL_AMBIGUOUS`, `HEADER_AMBIGUOUS`, `UNIT_UNDECLARED`, `PERIOD_MISMATCH`, `NON_NUMERIC`, `PENSION_LINE_NOT_IN_SOURCE`, `SIGN_AMBIGUOUS`, `INPUT_NA`, `SUSPECT_ZERO` (§11); audit flags `BS_DATE_NOT_PERIOD_END`, `BS_DATE_EQUALS_FILE_DATE`, `UNIT_CONFLICT`, `HASH_MISMATCH`.
