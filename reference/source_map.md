# Source Map

Governed by: `PROJECT_RULES.md` (read 2026-11-12). Produced by the `source-audit` skill. Read-only audit — no KPI values, no computed figures. Workbook values are not reproduced here (§17.1: no number without a metric ID in `outputs/kpi.json`); each source cell is identified by address, kind and cached-value status.

## Workbook

- File: `2026-08__Databook_Aeroflot_ENG_1.xlsx`
- Location audited: git blob from branch `claude/dreamy-gates-aff9hw` (commit cf78592); **not present in the repository root of this branch** (see Escalations)
- Size: 1317755 bytes
- SHA-256 (start / end): `3ebd7863eae6094982d8bcccdaac5e20aae6d06a036233c37542f668036f1fb1` / `3ebd7863eae6094982d8bcccdaac5e20aae6d06a036233c37542f668036f1fb1` — unchanged
- Matches `PROJECT_RULES.md` §0 hash: yes
- Ignored files: none (no `~$*` lock files found)
- Mapping file (§15.3.6): **none exists** — required rows below are taken from `PROJECT_RULES.md` §7 (KPI inputs) and from the owner's request (inventory lists); Russian labels are recorded but cannot be verified against an expected value
- Read mode: `openpyxl.load_workbook(read_only=True, data_only=True)` for cached values, `data_only=False` for formula text; OOXML parts read via `zipfile` for hidden rows/columns. Nothing written, nothing recalculated.
- Workbook-level: 6 external-link parts (`xl/externalLinks/…`) pointing to local file paths (paths not reproduced, §3.5); many defined names refer to external book `[1]`. Only `Headcount` data cells use formulas with external references.

## §0 fact check

| Fact | Expected (§0) | Observed | Status |
|---|---|---|---|
| Source file in repository root | `2026-08__Databook_Aeroflot_ENG_1.xlsx` in root | not in the root of this branch; present only on branch `claude/dreamy-gates-aff9hw` (audited from git blob commit cf78592) | NOT CONFIRMED |
| SHA-256 | `3ebd7863eae6094982d8bcccdaac5e20aae6d06a036233c37542f668036f1fb1` | `3ebd7863eae6094982d8bcccdaac5e20aae6d06a036233c37542f668036f1fb1` | CONFIRMED |
| Core sheets exist | Highlights and Ratios, Cash Flow, Financial Position, Profit and Loss, OCI, EBITDA, Debt Profile, ROIC | all present | CONFIRMED |
| Label columns | B = English, C = selected-language label, D = Russian | B = formula `=IF(Contents!$L$5="РУС",D,C)` (selected language; cached English because `Contents!L5`=`ENG`); C = English constant; D = Russian constant; C and D hidden | NOT CONFIRMED |
| Header row | row 7 on the financial sheets | row 7 on all core sheets (non-core: `AFLT - Regions` uses row 8; `RASK-CASK` has extra table headers in rows 72 and 99) | CONFIRMED |
| Flow period headers | text `3M/6M/9M/12M YYYY` | text YTD headers; on `Operating Expenses` `12М 2023`, `3М 2025`, `6М 2025`, `9М 2025`, `12М 2025`, `3М 2026` use Cyrillic `М` (U+041C); `6M 2026` is Latin. Flow sheets also carry an annual block with integer headers (`2012`…`2025`, columns E–S) | NOT CONFIRMED |
| Balance-sheet headers | datetime values; latest 2026-08-31; previous 2026-03-31; FY-end 2025-12-31 | datetime only in columns BB–BY; columns E–S and U–BA are text (e.g. S7 `31-Dec-2025`, L7 `31-Dec-2018***`, AR7 `1-Jan-2018`). Latest BY7 = 2026-08-31, BX7 = 2026-03-31, BW7 = 2025-12-31 | PARTLY CONFIRMED |
| Annual-only sheets | integer year headers, last `2025`, no interim; `2018` twice (K and L) | confirmed for Highlights and Ratios, Debt Profile, ROIC (row 6 tags K=`IAS 17`, L=`IFRS 16`) | CONFIRMED |
| Unit statements | B7 reads "RUB million, if not stated otherwise" / "mn RUB if not stated otherwise" | present on CF, FP, P&L, ROIC, RASK-CASK, Highlights; EBITDA `RUB million`; Revenue `RUB, mn`; **no unit statement in B7 on `Operating Expenses` and `Debt Profile`** | NOT CONFIRMED |
| Non-numeric placeholders | `-` appears in numeric areas | confirmed (e.g. FP AJ10, CF J15) | CONFIRMED |

## Sheet inventory

| # | Sheet | Visibility | Used range | Hidden rows | Hidden columns | Source rank (§2) | B7 unit statement | Header row |
|---|---|---|---|---|---|---|---|---|
| 1 | `Contents` | visible | `A1:Z40` | 40 | C–D, S–GR, …to XFD | not a core source | `Air Transportation Market` | — |
| 2 | `Glossary` | visible | `A1:T33` | none | C–D, F–N, U–GR, …to XFD | not a core source | — | — |
| 3 | `Market` | visible | `A1:AL46` | none | C–D, U, AM–GR, …to XFD | not a core source | `Russian market overview` | 7 |
| 4 | `Highlights and Ratios` | visible | `A1:Z50` | 42–50 | C–D, V–GR, …to XFD | 1b | `mn RUB if not stated otherwise` | 7 |
| 5 | `AFLT - Operating - abs` | visible | `A1:U160` | none | C–D, V–GR, …to XFD | not a core source | `Metric` | 7 |
| 6 | `AFLT - Operating - %` | visible | `A1:AA160` | none | C–D, V–GR, …to XFD | not a core source | `Metric` | 7 |
| 7 | `AFLT - Regions` | visible | `A1:AN81` | 51–81 | C–D, V–W, AO–GR, …to XFD | not a core source | — | 8 |
| 8 | `Revenue` | visible | `A1:CA56` | 41–56 | C–D, CB–GR, …to XFD | not a core source | `RUB, mn` | 7 |
| 9 | `Operating Expenses` | visible | `A1:CH84` | 66–84 | C–D, CB–GR, …to XFD | not a core source | — | 7 |
| 10 | `EBITDA` | visible | `A1:CA25` | none | C–D, CB–GR, …to XFD | 1b | `RUB million` | 7 |
| 11 | `Financial Position` | visible | `A1:CM87` | 80–87 | C–D, CB–GR, …to XFD | 1a | `RUB million, if not stated otherwise` | 7 |
| 12 | `Profit and Loss, OCI` | visible | `A1:CT86` | 59–86 | C–D, CB–GR, …to XFD | 1a | `RUB million, if not stated otherwise` | 7 |
| 13 | `Cash Flow` | visible | `A1:CJ112` | 103–112 | C–D, CB–GR, …to XFD | 1a | `RUB million, if not stated otherwise` | 7 |
| 14 | `Debt Profile` | visible | `A1:U66` | 34–66 | C–D, V–GR, …to XFD | 1b | — | 7 |
| 15 | `RASK-CASK` | visible | `A1:V125` | none | C–D, V–GR, …to XFD | not a core source | `RUB million, if not stated otherwise` | 7 |
| 16 | `ROIC` | visible | `A1:V38` | 32–38 | C–D, V–GR, …to XFD | 1b | `RUB million, if not stated otherwise` | 7 |
| 17 | `Fleet` | visible | `A1:U73` | 23–25, 31, 36–38 | C–D, V–GR, …to XFD | not a core source | — | 7 |
| 18 | `Headcount` | visible | `A1:U57` | 39–57 | C–D, V–GR, …to XFD | not a core source | `Number of employees` | 7 |
| 19 | `Fuel Consumption` | visible | `A1:CA56` | 16–56 | C–D, CB–GR, …to XFD | not a core source | `Fuel consumption metrics` | 7 |
| 20 | `Share capital` | visible | `A1:O21` | 20–21 | D–E, P–GR, …to XFD | not a core source | `Management` | — |
| 21 | `MCap and EV` | visible | `A1:U40` | none | C–D, V–GR, …to XFD | 1b | `mln RUB if not stated otherwise` | 7 |
| 22 | `Dividends` | visible | `A1:T15` | 15 | C–D, U–GR, …to XFD | not a core source | — | 7 |

Notes: hidden rows on the financial sheets contain no data; hidden rows 23–25, 31, 36–38 on `Fleet` contain retired aircraft types. Columns C (English) and D (Russian) are hidden on every data sheet; column B is a formula that shows one of them. No instruction-like text was found in any cell, defined name or document property. No comments in the file.

## Period headers used

| Sheet | Header row | Period | Column | Raw header | Header type | Status |
|---|---|---|---|---|---|---|
| `Cash Flow` | 7 | H1_2025 | BU | `6M 2025` | text YTD | OK |
| `Cash Flow` | 7 | FY2025 | BW | `12M 2025` | text YTD | OK |
| `Cash Flow` | 7 | H1_2026 | BY | `6M 2026` | text YTD | OK |
| `Highlights and Ratios` | 7 | FY2025 (annual sheet) | S | `2025` | integer year | OK |
| `Financial Position` | 7 | BS_2025_12_31 | BW | `2025-12-31 00:00:00` | datetime | OK |
| `Financial Position` | 7 | BS_2026_03_31 | BX | `2026-03-31 00:00:00` | datetime | OK |
| `Financial Position` | 7 | BS_2026_08_31 | BY | `2026-08-31 00:00:00` | datetime | OK |
| `Debt Profile` | 7 | FY2025 (annual sheet) | S | `2025` | integer year | OK |
| `ROIC` | 7 | FY2025 (annual sheet) | S | `2025` | integer year | OK |
| `Profit and Loss, OCI` | 7 | H1_2025 | BU | `6M 2025` | text YTD | OK |
| `Profit and Loss, OCI` | 7 | FY2025 | BW | `12M 2025` | text YTD | OK |
| `Profit and Loss, OCI` | 7 | H1_2026 | BY | `6M 2026` | text YTD | OK |
| `EBITDA` | 7 | H1_2025 | BU | `6M 2025` | text YTD | OK |
| `EBITDA` | 7 | FY2025 | BW | `12M 2025` | text YTD | OK |
| `EBITDA` | 7 | H1_2026 | BY | `6M 2026` | text YTD | OK |
| `AFLT - Operating - abs` | 7 | FY2025 (annual sheet) | S | `2025` | integer year | OK |
| `RASK-CASK` | 7 | FY2025 (annual sheet) | S | `2025` | integer year | OK |
| `Fuel Consumption` | 7 | H1_2025 | BU | `6M 2025` | text YTD | OK |
| `Fuel Consumption` | 7 | FY2025 | BW | `12M 2025` | text YTD | OK |
| `Fuel Consumption` | 7 | H1_2026 | BY | `6M 2026` | text YTD | OK |
| `AFLT - Regions` | 8 | FY2025 (annual sheet) | — | — | — | LABEL_AMBIGUOUS (duplicate header) |
| `Operating Expenses` | 7 | H1_2025 | BU | `6М 2025` | INVALID | HEADER_AMBIGUOUS |
| `Operating Expenses` | 7 | FY2025 | BW | `12М 2025` | INVALID | HEADER_AMBIGUOUS |
| `Operating Expenses` | 7 | H1_2026 | BY | `6M 2026` | text YTD | OK |

## Required rows

Label status after §15.3.2 normalisation, column B matched within the stated section. "Expected" = `PROJECT_RULES.md` §7 wording for KPI inputs; for inventory rows the expected text is the label requested for listing.

### KPI input (§7)

| Metric ID | Sheet | Section (found) | Expected B | Actual B (raw) | Row | Actual D (raw) | B is formula | Label status | Flow/stock | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| `CFO` | `Cash Flow` | Operating activities (header row 8: `Cash flows from operating activities:`) | `Net cash flows from operating activities` | `Net cash flows from operating activities` | 50 | `Чистая сумма денежных средств от операционной деятельности` | yes | LABEL OK | flow | — |
| `CFI` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Net cash flows from/(used in) investing activities` | `Net cash flows from/(used in) investing activities` | 72 | `Чистая сумма денежных средств, использованных в инвестиционной деятельности` | yes | LABEL OK | flow | — |
| `CAPEX_PPE_INTANG` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Purchases of property, plant and equipment and intangible assets` | `Purchases of property, plant and equipment and intangible assets` | 59 | `Приобретение основных средств, активов в форме права\nпользования, нематериальных активов и капитализированные затраты на ремонты` | yes | LABEL OK | flow | — |
| `CAPEX_PREPAY_AIRCRAFT` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Prepayments for aircraft` | `Prepayments for aircraft` | 63 | `Предоплаты за воздушные суда` | yes | LABEL OK | flow | — |
| `LEASE_PRINCIPAL_IFRS16` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Repayment of the principal element of lease liabilities (IFRS 16)` | `Repayment of the principal element of lease liabilities (IFRS 16)` | 78 | `Выплаты основной суммы долга по аренде (IFRS 16)` | yes | LABEL OK | flow | — |
| `LEASE_PRINCIPAL_IAS17` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Repayment of the principal element of finance lease liabilities (IAS 17)` | `Repayment of the principal element of finance lease liabilities (IAS 17)` | 77 | `Выплаты основной суммы долга по финансовой аренде (IAS 17)` | yes | LABEL OK | flow | — |
| `FCF_DATABOOK_REPORTED` | `Highlights and Ratios` | Highlights (rows 8–35) | `Free cash flow (CFO + CFI)` | `Free cash flow (CFO + CFI)` | 25 | `Free cash flow (CFO + CFI)` | yes | LABEL OK | flow | — |
| `CAPEX_DATABOOK` | `Highlights and Ratios` | Highlights (rows 8–35) | `Capital expenditures**` | `Capital expenditures**` | 24 | `Капитальные вложения**` | yes | LABEL OK | flow | Footnote `**` at row 38 (2012–2013 include deposits). |
| `ST_BORROWINGS` | `Financial Position` | Current liabilities (header row 38: `Current liabilities`) | `ST loans and borrowings and current portion of long-term loans and borrowings` | `ST loans and borrowings and current portion of long-term loans and borrowings` | 46 | `Краткосрочные кредиты и займы и краткосрочная часть долгосрочных ` | yes | LABEL OK | stock | — |
| `LT_BORROWINGS` | `Financial Position` | Non-current liabilities (header row 50: `Non-current liabilities`) | `Long-term loans and borrowings` | `Long-term loans and borrowings` | 51 | `Долгосрочные кредиты и займы` | yes | LABEL OK | stock | — |
| `LEASE_IFRS16_CURRENT` | `Financial Position` | Current liabilities (header row 38: `Current liabilities`) | `Lease liabilities (IFRS 16)` | `Lease liabilities (IFRS 16)` | 44 | `Обязательства по аренде (IFRS 16)` | yes | LABEL OK | stock | — |
| `LEASE_IFRS16_NONCURRENT` | `Financial Position` | Non-current liabilities (header row 50: `Non-current liabilities`) | `Lease liabilities (IFRS 16)` | `Lease liabilities (IFRS 16)` | 52 | `Обязательства по аренде (IFRS 16)` | yes | LABEL OK | stock | — |
| `LEASE_IAS17_CURRENT` | `Financial Position` | Current liabilities (header row 38: `Current liabilities`) | `Finance lease liabilities (IAS 17)` | `Finance lease liabilities (IAS 17)` | 45 | `Финансовая аренда (IAS 17)` | yes | LABEL OK | stock | — |
| `LEASE_IAS17_NONCURRENT` | `Financial Position` | Non-current liabilities (header row 50: `Non-current liabilities`) | `Finance lease liabilities (IAS 17)` | `Finance lease liabilities (IAS 17)` | 53 | `Финансовый лизинг (IAS 17)` | yes | LABEL OK | stock | — |
| `CASH` | `Financial Position` | Current assets (header row 9: `Current assets`) | `Cash and cash equivalents` | `Cash and cash equivalents` | 10 | `Денежные средства и их эквиваленты` | yes | LABEL OK | stock | — |
| `ST_FIN_INVESTMENTS` | `Financial Position` | Current assets (header row 9: `Current assets`) | `Short-term financial investments` | `Short-term financial investments` | 11 | `Краткосрочные финансовые инвестиции` | yes | LABEL OK | stock | — |
| `PENSION_LIABILITIES` | `Debt Profile` | Debt/liquidity rows 14–31 | `Pension liabilities` | `Pension liabilities` | 14 | `Пенсионные обязательства` | yes | LABEL OK | stock | — |
| `PENSION_ROIC_XCHECK` | `ROIC` | Invested capital (header row 19: `Invested capital`) | `Pension obligation – non-current portion` | `Pension obligation – non-current portion` | 21 | `Пенсионные обязательства` | yes | LABEL_AMBIGUOUS | stock | D `Пенсионные обязательства` has no "non-current" qualifier — scope differs from B (§15.3.5). |
| `NET_DEBT_DATABOOK` | `Debt Profile` | Debt/liquidity rows 14–31 | `Net debt` | `Net debt` | 17 | `Чистый долг` | yes | LABEL OK | stock | — |
| `NET_DEBT_EBITDA_DATABOOK` | `Debt Profile` | Debt/liquidity rows 14–31 | `Net debt/EBITDA` | `Net debt/EBITDA` | 27 | `Чистый долг/EBITDA` | yes | LABEL OK | ratio | — |

### Main KPI source (reported)

| Metric ID | Sheet | Section (found) | Expected B | Actual B (raw) | Row | Actual D (raw) | B is formula | Label status | Flow/stock | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| `REVENUE` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `Revenue` | `Revenue` | 10 | `Выручка` | yes | LABEL OK | flow | — |
| `TRAFFIC_REVENUE` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `Traffic revenue` | `Traffic revenue` | 8 | `Выручка от перевозок` | yes | LABEL OK | flow | — |
| `OPERATING_PROFIT` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `Operating profit` | `Operating profit` | 18 | `Операционная прибыль` | yes | LABEL OK | flow | — |
| `PBT` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `Profit/(loss) before income tax` | `Profit/(loss) before income tax` | 26 | `Прибыль/(убыток) до налога` | yes | LABEL OK | flow | — |
| `NET_PROFIT` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `PROFIT/(LOSS) FOR THE YEAR` | `PROFIT/(LOSS) FOR THE YEAR` | 29 | `Прибыль/(убыток) за период` | yes | LABEL OK | flow | — |
| `EBITDA` | `EBITDA` | EBITDA table | `EBITDA` | `EBITDA` | 11 | `EBITDA` | yes | LABEL OK | flow | Footnote row 24: starting from 2025 EBITDA incorporates customs duties — FY2025 vs prior years not like-for-like. |
| `EBITDAR` | `EBITDA` | EBITDA table | `EBITDAR` | `EBITDAR` | 13 | `EBITDAR` | yes | LABEL OK | flow | — |
| `EBITDA_MARGIN_REPORTED` | `EBITDA` | EBITDA table | `EBITDA margin` | `EBITDA margin` | 17 | `EBITDA маржа` | yes | LABEL OK | ratio | Ratio row under B7 "RUB million"; label carries no unit. |
| `OPERATING_MARGIN_REPORTED` | `EBITDA` | EBITDA table | `Operating profit margin` | `Operating profit margin` | 16 | `Рентабельность по операционной прибыли` | yes | LABEL OK | ratio | — |
| `NET_MARGIN_REPORTED` | `EBITDA` | EBITDA table | `Net income margin` | `Net income margin` | 19 | `Чистая прибыль, маржа` | yes | LABEL OK | ratio | — |
| `CFF` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Net cash used in financing activities` | `Net cash used in financing activities` | 89 | `Чистая сумма денежных средств, использованных в финансовой деятельности` | yes | LABEL OK | flow | — |
| `TOTAL_EQUITY` | `Financial Position` | Equity (header row 61: `Equity`) | `TOTAL EQUITY` | `TOTAL EQUITY` | 73 | `ИТОГО КАПИТАЛ` | yes | LABEL OK | stock | — |
| `CFO_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `Net Operating Activities (CFO)` | `Net Operating Activities (CFO)` | 21 | `Операционный денежный поток (CFO)` | yes | LABEL OK | flow | — |
| `CFI_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `Net Investing Activities (CFI)` | `Net Investing Activities (CFI)` | 22 | `Инвестиционный денежный поток (CFI)` | yes | LABEL OK | flow | — |
| `CFF_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `Net Financing Activities (CFF)` | `Net Financing Activities (CFF)` | 23 | `Финансовый денежный поток (CFF)` | yes | LABEL OK | flow | — |
| `REVENUE_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `Revenue` | `Revenue` | 12 | `Выручка` | yes | LABEL OK | flow | — |
| `EBITDA_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `EBITDA` | `EBITDA` | 14 | `EBITDA` | yes | LABEL OK | flow | — |
| `EBITDAR_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `EBITDAR` | `EBITDAR` | 13 | `EBITDAR` | yes | LABEL OK | flow | — |
| `NET_PROFIT_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `Net Profit` | `Net Profit` | 15 | `Чистая прибыль` | yes | LABEL OK | flow | — |
| `NET_DEBT_EBITDA_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `Net Debt/12M EBITDA (х)` | `Net Debt/12M EBITDA (х)` | 33 | `Чистый долг/12M EBITDA (х)` | yes | LABEL OK | ratio | English label contains Cyrillic characters |
| `GROSS_DEBT_EBITDA_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `Gross Debt/EBITDA 12M(х)` | `Gross Debt/EBITDA 12M(х)` | 32 | `Общий долг/EBITDA 12M(х)` | yes | LABEL OK | ratio | English label contains Cyrillic characters |
| `EBITDA_INTEREST_COVER_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `EBITDA/Gross Interest (х)***` | `EBITDA/Gross Interest (х)***` | 31 | `EBITDA/проценты (х)***` | yes | LABEL OK | ratio | English label contains Cyrillic characters |
| `ROIC_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `ROIC (%)` | `ROIC (%)` | 30 | `ROIC (%)` | yes | LABEL OK | ratio | — |
| `BANK_DEBT_EQUITY_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `Bank Debt/Equity (х)` | `Bank Debt/Equity (х)` | 34 | `Банковский долг/EBITDA (х)` | yes | LABEL_AMBIGUOUS | ratio | D `Банковский долг/EBITDA (х)` means bank debt/EBITDA (§15.3.5 example).; English label contains Cyrillic characters |

### Operating metric

| Metric ID | Sheet | Section (found) | Expected B | Actual B (raw) | Row | Actual D (raw) | B is formula | Label status | Flow/stock | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| `PAX_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `PAX, mn` | `PAX, mn` | 8 | `Пассажиропоток, млн пасс.` | yes | LABEL OK | flow | — |
| `RPK_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `RPK, bn` | `RPK, bn` | 9 | `Пассажирооборот, (RPK, млрд пкм)` | yes | LABEL OK | flow | — |
| `PLF_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `PLF, %` | `PLF, %` | 10 | `Занятость кресел, %` | yes | LABEL OK | ratio | % stored as fraction (§6.2.3). |
| `FLEET_HR` | `Highlights and Ratios` | Highlights (rows 8–35) | `Aircraft, #` | `Aircraft, #` | 11 | `Флот, количество ВС` | yes | LABEL OK | stock | — |
| `PAX_GROUP` | `AFLT - Operating - abs` | Aeroflot Group (header row 8: `Aeroflot Group`) | `Passengers carried, thd` | `Passengers carried, thd` | 9 | `Пассажиропоток, тыс.` | yes | LABEL OK | flow | — |
| `RPK_GROUP` | `AFLT - Operating - abs` | Aeroflot Group (header row 8: `Aeroflot Group`) | `Passenger turnover, mn RPK` | `Passenger turnover, mn RPK` | 12 | `Пассажирооборот, млн пкм` | yes | LABEL OK | flow | — |
| `ASK_GROUP` | `AFLT - Operating - abs` | Aeroflot Group (header row 8: `Aeroflot Group`) | `Available seat-kilometers, mn ASK` | `Available seat-kilometers, mn ASK` | 15 | `Предельный пассажирооборот, млн ккм` | yes | LABEL OK | flow | — |
| `PLF_GROUP` | `AFLT - Operating - abs` | Aeroflot Group (header row 8: `Aeroflot Group`) | `Passenger load factor, %` | `Passenger load factor, %` | 18 | `Занятость кресел, %` | yes | LABEL OK | ratio | — |
| `RPK_RC` | `RASK-CASK` | Revenue/traffic table rows 8–34 | `RPK, mn` | `RPK, mn` | 17 | `Пассажирооборот, млн пкм (RPK)` | yes | LABEL OK | flow | — |
| `ASK_RC` | `RASK-CASK` | Revenue/traffic table rows 8–34 | `ASK, mn` | `ASK, mn` | 25 | `Предельный пассажирооборот, млн ккм (ASK)` | yes | LABEL OK | flow | — |
| `YIELD_TRAFFIC` | `RASK-CASK` | Yield (REV/RPK), RUB (header row 36: `Yield (REV/RPK), RUB`) | `Traffic revenue` | — | — | — | no | LABEL_AMBIGUOUS | ratio | Section row 36 `Yield (REV/RPK), RUB` holds no data; rows 37–42 and 43–48 repeat identical labels with no distinguishing header. |
| `RASK_TRAFFIC` | `RASK-CASK` | RASK (REV/ASK), RUB (header row 50: `RASK (REV/ASK), RUB`) | `Traffic revenue` | — | — | — | no | LABEL_AMBIGUOUS | ratio | Rows 51–56 and 57–62 repeat identical labels. |
| `CASK_TOTAL` | `RASK-CASK` | CASK table (header row 99) (header row 99: `RUB `) | `Total CASK` | `Total CASK` | 120 | `Всего операционные расходы` | yes | LABEL_AMBIGUOUS | ratio | D `Всего операционные расходы` (total operating expenses) does not say per-ASK. |
| `CASK_EX_FUEL` | `RASK-CASK` | CASK table (header row 99) (header row 99: `RUB `) | `Ex-fuel CASK` | `Ex-fuel CASK` | 118 | `Операционные расходы, искл ГСМ` | yes | LABEL_AMBIGUOUS | ratio | D `Операционные расходы, искл ГСМ` (opex ex fuel) does not say per-ASK. |
| `ASK_FUEL_SHEET` | `Fuel Consumption` | Fuel metrics rows 8–13 | `Available seat-kilometers, mn ASK` | `Available seat-kilometers, mn ASK` | 9 | `Предельный пассажирооборот, млн ккм` | yes | LABEL OK | flow | Only interim (YTD) source of ASK in the workbook. |
| `ATK_FUEL_SHEET` | `Fuel Consumption` | Fuel metrics rows 8–13 | `Available tonne-kilometers, mn ATK` | `Available tonne-kilometers, mn ATK` | 10 | `Предельный тоннокилометраж, млн ткм` | yes | LABEL OK | flow | — |
| `PAX_REGIONS_TOTAL` | `AFLT - Regions` | PAX, mn (header row 9: `PAX, mn`) | `Total` | `Total ` | 18 | `Итого  ` | yes | LABEL OK | flow | raw label has leading/trailing spaces; Group block (B6 `Aeroflot Group`, columns E–S); header row 8. |
| `RPK_REGIONS_TOTAL` | `AFLT - Regions` | RPK, bn (header row 19: `RPK, bn `) | `Total` | `Total ` | 28 | `Итого  ` | yes | LABEL OK | flow | raw label has leading/trailing spaces; Group block (B6 `Aeroflot Group`, columns E–S); header row 8. |
| `ASK_REGIONS_TOTAL` | `AFLT - Regions` | ASK, bn (header row 29: `ASK, bn `) | `Total` | `Total ` | 38 | `Итого  ` | yes | LABEL OK | flow | raw label has leading/trailing spaces; Group block (B6 `Aeroflot Group`, columns E–S); header row 8. |
| `PLF_REGIONS_TOTAL` | `AFLT - Regions` | PLF, % (header row 39: `PLF, %`) | `Total` | `Total ` | 48 | `Итого  ` | yes | LABEL OK | ratio | raw label has leading/trailing spaces; Group block (B6 `Aeroflot Group`, columns E–S); header row 8. |

### Operating expense line

| Metric ID | Sheet | Section (found) | Expected B | Actual B (raw) | Row | Actual D (raw) | B is formula | Label status | Flow/stock | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| `OPEX_R9` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Aircraft servicing and ground handling` | `Aircraft servicing and ground handling` | 9 | `Обслуживание воздушных судов в аэропортах и на трассе` | yes | LABEL OK | flow | — |
| `OPEX_R10` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Operating lease expenses` | `Operating lease expenses` | 10 | `Операционный лизинг (IAS17)` | yes | LABEL OK | flow | — |
| `OPEX_R11` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Aircraft maintenance ` | `Aircraft maintenance ` | 11 | `Техническое обслуживание воздушных судов` | yes | LABEL OK | flow | raw label has leading/trailing spaces |
| `OPEX_R12` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Sales and marketing expenses` | `Sales and marketing expenses` | 12 | `Коммерческие и маркетинговые расходы` | yes | LABEL OK | flow | — |
| `OPEX_R13` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Communication expenses` | `Communication expenses` | 13 | `Услуги связи и систем бронирования` | yes | LABEL OK | flow | — |
| `OPEX_R14` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Expenses from operations under code-sharing agreements` | `Expenses from operations under code-sharing agreements` | 14 | `Расходы от операций по соглашениям «код-шеринг»` | yes | LABEL OK | flow | — |
| `OPEX_R15` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Administration and general expenses` | `Administration and general expenses` | 15 | `Административные и общехозяйственные расходы` | yes | LABEL OK | flow | — |
| `OPEX_R16` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Passenger services` | `Passenger services` | 16 | `Расходы по обслуживанию пассажиров` | yes | LABEL OK | flow | — |
| `OPEX_R17` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Expenses for in-flight catering` | `Expenses for in-flight catering` | 17 | `Расходы на продукты для производства бортового питания` | yes | LABEL OK | flow | — |
| `OPEX_R18` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Insurance expenses` | `Insurance expenses` | 18 | `Расходы по страхованию` | yes | LABEL OK | flow | — |
| `OPEX_R19` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Customs duties ` | `Customs duties ` | 19 | `Таможенные пошлины` | yes | LABEL OK | flow | raw label has leading/trailing spaces |
| `OPEX_R20` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Cost of duty-free goods sold` | `Cost of duty-free goods sold` | 20 | `Себестоимость товаров для торговли на борту` | yes | LABEL OK | flow | — |
| `OPEX_R21` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Expenditure on variable rental payments not included in lease` | `Expenditure on variable rental payments not included in lease` | 21 | `Расходы по переменным арендным платежам, не включенным в обязательства по аренде` | yes | LABEL OK | flow | — |
| `OPEX_R22` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Short-term rental expenses` | `Short-term rental expenses` | 22 | `Расходы по краткосрочной аренде` | yes | LABEL OK | flow | — |
| `OPEX_R23` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Other expenses ` | `Other expenses ` | 23 | `Прочие расходы` | yes | LABEL OK | flow | raw label has leading/trailing spaces |
| `OPEX_R24` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Operating costs less aircraft fuel, staff costs and depreciation and amortisation` | `Operating costs less aircraft fuel, staff costs and depreciation and amortisation` | 24 | `Операционные расходы, за исключением авиационного топлива, расходов на оплату труда и амортизацию` | yes | LABEL OK | flow | — |
| `OPEX_R25` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Aircraft fuel` | `Aircraft fuel` | 25 | `Авиационное топливо` | yes | LABEL OK | flow | — |
| `OPEX_R26` | `Operating Expenses` | 1. OpEx less staff costs and D&A (header row 8: `1. OpEx less staff costs and D&A`) | `Total operating costs less staff costs and depreciation and amortisation` | `Total operating costs less staff costs and depreciation and amortisation` | 26 | `Операционные расходы, за исключением расходов на оплату труда и амортизацию` | yes | LABEL OK | flow | — |
| `OPEX_R29` | `Operating Expenses` | 2. Staff cost (header row 28: `2. Staff cost`) | `Wages and salaries` | `Wages and salaries` | 29 | `Заработная плата` | yes | LABEL OK | flow | — |
| `OPEX_R30` | `Operating Expenses` | 2. Staff cost (header row 28: `2. Staff cost`) | `Insurance contributions and pension plans` | `Insurance contributions and pension plans` | 30 | `Отчисления на страховые взносы и пенсионные планы` | yes | LABEL OK | flow | — |
| `OPEX_R31` | `Operating Expenses` | 2. Staff cost (header row 28: `2. Staff cost`) | `incl. Pension costs` | `incl. Pension costs` | 31 | `вкл. расходы по пенсионному обеспечению` | yes | LABEL OK | flow | — |
| `OPEX_R32` | `Operating Expenses` | 2. Staff cost (header row 28: `2. Staff cost`) | `        Social security costs ` | `        Social security costs ` | 32 | `        Социальные отчисления во внебюджетные фонды` | yes | LABEL OK | flow | raw label has leading/trailing spaces |
| `OPEX_R33` | `Operating Expenses` | 2. Staff cost (header row 28: `2. Staff cost`) | `Total staff costs` | `Total staff costs` | 33 | `Итого расходы на оплату труда` | yes | LABEL OK | flow | — |
| `OPEX_R36` | `Operating Expenses` | 3. D&A and other (header row 35: `3. D&A and other`) | `Depreciation and amortisation` | `Depreciation and amortisation` | 36 | `Амортизация` | yes | LABEL OK | flow | — |
| `OPEX_R37` | `Operating Expenses` | 3. D&A and other (header row 35: `3. D&A and other`) | `Other operating (expenses)/income, net` | `Other operating (expenses)/income, net` | 37 | `Прочие операционные доходы/(расходы), нетто` | yes | LABEL OK | flow | — |
| `OPEX_R38` | `Operating Expenses` | 3. D&A and other (header row 35: `3. D&A and other`) | `Total` | `Total` | 38 | `Итого` | yes | LABEL OK | flow | — |
| `OPEX_R40` | `Operating Expenses` | Total (row 40) | `Total OpEx` | `Total OpEx` | 40 | `Итого операционные расходы` | yes | LABEL OK | flow | — |
| `PL_OPEX_R12` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `Operating costs, excluding staff costs and depreciation and amortisation` | `Operating costs, excluding staff costs and depreciation and amortisation` | 12 | `Операционные расходы, искл. расходы на персонал и амортизацию` | yes | LABEL OK | flow | — |
| `PL_OPEX_R13` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `Staff costs` | `Staff costs` | 13 | `Расходы на персонал` | yes | LABEL OK | flow | — |
| `PL_OPEX_R14` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `Depreciation and amortisation` | `Depreciation and amortisation` | 14 | `Амортизация` | yes | LABEL OK | flow | — |
| `PL_OPEX_R15` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `Other operating (expenses)/income, net` | `Other operating (expenses)/income, net` | 15 | `Прочие операционные доходы/(расходы) нетто` | yes | LABEL OK | flow | — |
| `PL_OPEX_R16` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `Operating costs ` | `Operating costs ` | 16 | `Операционные расходы ` | yes | LABEL OK | flow | raw label has leading/trailing spaces |

### Cash-flow component

| Metric ID | Sheet | Section (found) | Expected B | Actual B (raw) | Row | Actual D (raw) | B is formula | Label status | Flow/stock | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| `CF_R53` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Deposits placement` | `Deposits placement` | 53 | `Размещение депозитов` | yes | LABEL OK | flow | — |
| `CF_R54` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Purchases of investments and loans issued` | `Purchases of investments and loans issued` | 54 | `Приобретение инвестиций и займы выданные` | yes | LABEL OK | flow | — |
| `CF_R55` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Deposits return` | `Deposits return` | 55 | `Возврат депозитов` | yes | LABEL OK | flow | — |
| `CF_R56` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Proceeds from sale of investments in associates` | `Proceeds from sale of investments in associates` | 56 | `Поступления от продажи инвестиций` | yes | LABEL OK | flow | — |
| `CF_R57` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Proceeds from sale of subsidiary` | `Proceeds from sale of subsidiary` | 57 | `Поступления от продажи дочерней компании` | yes | LABEL OK | flow | — |
| `CF_R58` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Proceeds from sale of property, plant and equipment ` | `Proceeds from sale of property, plant and equipment ` | 58 | `Поступления от продажи основных средств` | yes | LABEL OK | flow | raw label has leading/trailing spaces |
| `CF_R59` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Purchases of property, plant and equipment and intangible assets` | `Purchases of property, plant and equipment and intangible assets` | 59 | `Приобретение основных средств, активов в форме права\nпользования, нематериальных активов и капитализированные затраты на ремонты` | yes | LABEL OK | flow | — |
| `CF_R60` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Proceeds from sale of assets, classified as held for sale` | `Proceeds from sale of assets, classified as held for sale` | 60 | `Поступления от продажи активов, предназначенных для продажи ` | yes | LABEL OK | flow | — |
| `CF_R61` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Interest received` | `Interest received` | 61 | `Проценты полученные` | yes | LABEL OK | flow | — |
| `CF_R62` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Dividends received` | `Dividends received` | 62 | `Дивиденды полученные` | yes | LABEL OK | flow | — |
| `CF_R63` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Prepayments for aircraft` | `Prepayments for aircraft` | 63 | `Предоплаты за воздушные суда` | yes | LABEL OK | flow | — |
| `CF_R64` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Return of prepayments for aircraft` | `Return of prepayments for aircraft` | 64 | `Возврат предоплат за воздушные суда ` | yes | LABEL OK | flow | — |
| `CF_R65` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Payment of lease security deposits` | `Payment of lease security deposits` | 65 | `Выплата страховых депозитов по аренде` | yes | LABEL OK | flow | — |
| `CF_R66` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Return of operating lease security deposits` | `Return of operating lease security deposits` | 66 | `Возврат страховых депозитов по операционной аренде` | yes | LABEL OK | flow | — |
| `CF_R67` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Payments for financial assets under aircraft lease contracts (IFRS 16)` | `Payments for financial assets under aircraft lease contracts (IFRS 16)` | 67 | `Платежи за финансовые активы по договорам аренды (МСФО 16) ` | yes | LABEL OK | flow | — |
| `CF_R68` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Repayment of financial assets under aircraft lease contracts (IFRS 16)` | `Repayment of financial assets under aircraft lease contracts (IFRS 16)` | 68 | `Погашение финансовых активов по договорам аренды (МСФО 16)` | yes | LABEL OK | flow | — |
| `CF_R69` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Purchase of subsidiary` | `Purchase of subsidiary` | 69 | `Приобретение дочерних компаний` | yes | LABEL OK | flow | — |
| `CF_R70` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Placement of borrowings` | `Placement of borrowings` | 70 | `Размещение займов` | yes | LABEL OK | flow | — |
| `CF_R71` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Return of borrowings` | `Return of borrowings` | 71 | `Погашение займов` | yes | LABEL OK | flow | — |
| `CF_R72` | `Cash Flow` | Investing activities (header row 52: `Cash flows from investing activities:`) | `Net cash flows from/(used in) investing activities` | `Net cash flows from/(used in) investing activities` | 72 | `Чистая сумма денежных средств, использованных в инвестиционной деятельности` | yes | LABEL OK | flow | — |
| `CF_R75` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Proceeds from loans and borrowings` | `Proceeds from loans and borrowings` | 75 | `Привлечение кредитов и займов` | yes | LABEL OK | flow | — |
| `CF_R76` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Repayment of loans and borrowings` | `Repayment of loans and borrowings` | 76 | `Погашение кредитов и займов` | yes | LABEL OK | flow | — |
| `CF_R77` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Repayment of the principal element of finance lease liabilities (IAS 17)` | `Repayment of the principal element of finance lease liabilities (IAS 17)` | 77 | `Выплаты основной суммы долга по финансовой аренде (IAS 17)` | yes | LABEL OK | flow | — |
| `CF_R78` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Repayment of the principal element of lease liabilities (IFRS 16)` | `Repayment of the principal element of lease liabilities (IFRS 16)` | 78 | `Выплаты основной суммы долга по аренде (IFRS 16)` | yes | LABEL OK | flow | — |
| `CF_R79` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Interest paid (IAS 17)` | `Interest paid (IAS 17)` | 79 | `Проценты уплаченные (IAS 17)` | yes | LABEL OK | flow | — |
| `CF_R80` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Interest paid except for interest under lease contracts (IFRS 16)` | `Interest paid except for interest under lease contracts (IFRS 16)` | 80 | `Проценты уплаченные, за исключением процентов по договорам аренды (IFRS 16)` | yes | LABEL OK | flow | — |
| `CF_R81` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Interest paid under lease contracts (IFRS 16)` | `Interest paid under lease contracts (IFRS 16)` | 81 | `Проценты, уплаченные по договорам аренды (IFRS 16)` | yes | LABEL OK | flow | — |
| `CF_R82` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Proceeds from disposal of treasury shares` | `Proceeds from disposal of treasury shares` | 82 | `Поступления от продажи собственных акций` | yes | LABEL OK | flow | — |
| `CF_R83` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Proceeds from sale of treasury shares to non-controlling shareholders` | `Proceeds from sale of treasury shares to non-controlling shareholders` | 83 | `Поступления от продажи собственных акций держателям неконтролирующих долей участия` | yes | LABEL OK | flow | — |
| `CF_R84` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Purchase of treasury shares` | `Purchase of treasury shares` | 84 | `Выкуп собственных акций` | yes | LABEL OK | flow | — |
| `CF_R85` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Proceeds from issue of ordinary shares` | `Proceeds from issue of ordinary shares` | 85 | `Поступления от эмиссии обыкновенных акций ` | yes | LABEL OK | flow | — |
| `CF_R86` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Dividends paid` | `Dividends paid` | 86 | `Выплаченные дивиденды` | yes | LABEL OK | flow | — |
| `CF_R87` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Payments for settlement of derivative financial instruments, net` | `Payments for settlement of derivative financial instruments, net` | 87 | `Выплаты по расчетам по производным финансовым инструментам, нетто` | yes | LABEL OK | flow | — |
| `CF_R88` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Proceeds from shareholder contributions in equity` | `Proceeds from shareholder contributions in equity` | 88 | `Поступления от взносов акционеров в капитал` | yes | LABEL OK | flow | — |
| `CF_R89` | `Cash Flow` | Financing activities (header row 74: `Cash flows from financing activities:`) | `Net cash used in financing activities` | `Net cash used in financing activities` | 89 | `Чистая сумма денежных средств, использованных в финансовой деятельности` | yes | LABEL OK | flow | — |

### FX / interest line

| Metric ID | Sheet | Section (found) | Expected B | Actual B (raw) | Row | Actual D (raw) | B is formula | Label status | Flow/stock | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| `FX_EFFECT_ON_CASH` | `Cash Flow` | Cash reconciliation (no header) | `Effect of exchange rate fluctuations on cash and cash equivalents` | `Effect of exchange rate fluctuations on cash and cash equivalents` | 91 | `Влияние изменений валютных курсов на денежные средства и их эквиваленты` | yes | LABEL OK | flow | — |
| `FX_GAIN_LOSS_ADJ` | `Cash Flow` | Operating activities (header row 8: `Cash flows from operating activities:`) | `Foreign exchange (gain)/loss` | `Foreign exchange (gain)/loss` | 26 | `Убыток/(прибыль) от курсовых разниц, нетто` | yes | LABEL OK | flow | — |
| `INTEREST_EXPENSE_ADJ` | `Cash Flow` | Operating activities (header row 8: `Cash flows from operating activities:`) | `Interest expense` | `Interest expense` | 24 | `Процентные расходы ` | yes | LABEL OK | flow | — |
| `INTEREST_INCOME_ADJ` | `Cash Flow` | Operating activities (header row 8: `Cash flows from operating activities:`) | `Interest income` | `Interest income` | 25 | `Процентные доходы ` | yes | LABEL OK | flow | — |
| `FINANCE_INCOME` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `Finance income` | `Finance income` | 21 | `Финансовые доходы` | yes | LABEL OK | flow | — |
| `FINANCE_COSTS` | `Profit and Loss, OCI` | Income statement (rows 8–29) | `Finance costs` | `Finance costs` | 22 | `Финансовые расходы` | yes | LABEL OK | flow | — |
| `OCI_TRANSLATION` | `Profit and Loss, OCI` | OCI (header row 40: `Other comprehensive income/(loss):`) | `Translation from the functional currency to the presentation currency` | `Translation from the functional currency to the presentation currency` | 43 | `Эффект перевода из функциональной валюты в валюту представления отчетности ` | yes | LABEL OK | flow | — |
| `CASH_OPENING_CF` | `Cash Flow` | Cash reconciliation (no header) | `Cash and cash equivalents at the beginning of the year` | `Cash and cash equivalents at the beginning of the year` | 94 | `Денежные средства и их эквиваленты на начало периода` | yes | LABEL OK | stock-in-flow-sheet | — |
| `CASH_CLOSING_CF` | `Cash Flow` | Cash reconciliation (no header) | `Cash and cash equivalents at the end of the year` | `Cash and cash equivalents at the end of the year` | 95 | `Денежные средства и их эквиваленты на конец периода` | yes | LABEL OK | stock-in-flow-sheet | — |
| `INTEREST_ROIC` | `ROIC` | Return (header row 11: `Return`) | `Interest` | `Interest` | 15 | `Процентные расходы` | yes | LABEL OK | flow | — |
| `INTEREST_CAP_OL_ROIC` | `ROIC` | Return (header row 11: `Return`) | `Interest on capitalized operating lease` | `Interest on capitalized operating lease` | 16 | `Проценты по капитализированному операционному лизингу` | yes | LABEL OK | flow | — |

## Source cells

Kind = formula/constant as stored; "Cached" = a cached value exists in the file. All financial data cells on the core sheets are constants.

### KPI input (§7)

| Metric ID | Period | Header cell | Header raw | Source cell | Hidden? | Kind | Formula | Cached value present? | Type | Unit / scale | Unit cell | BS date status | Flags | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `CFO` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU50 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CFO` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW50 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CFO` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY50 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CFI` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU72 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CFI` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW72 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CFI` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY72 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CAPEX_PPE_INTANG` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU59 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CAPEX_PPE_INTANG` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW59 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CAPEX_PPE_INTANG` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY59 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CAPEX_PREPAY_AIRCRAFT` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU63 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CAPEX_PREPAY_AIRCRAFT` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW63 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CAPEX_PREPAY_AIRCRAFT` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY63 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `LEASE_PRINCIPAL_IFRS16` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU78 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `LEASE_PRINCIPAL_IFRS16` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW78 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `LEASE_PRINCIPAL_IFRS16` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY78 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `LEASE_PRINCIPAL_IAS17` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU77 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `LEASE_PRINCIPAL_IAS17` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW77 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `LEASE_PRINCIPAL_IAS17` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY77 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `FCF_DATABOOK_REPORTED` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S25 | no | constant | — | yes | number (int) | RUB million per B7 `mn RUB if not stated otherwise` | 'Highlights and Ratios'!B7 | — | — | OK |
| `CAPEX_DATABOOK` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S24 | no | constant | — | yes | number (int) | RUB million per B7 `mn RUB if not stated otherwise` | 'Highlights and Ratios'!B7 | — | — | OK |
| `ST_BORROWINGS` | BS_2025_12_31 | BW7 | `2025-12-31 00:00:00` | 'Financial Position'!BW46 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BW7 | — | OK |
| `ST_BORROWINGS` | BS_2026_03_31 | BX7 | `2026-03-31 00:00:00` | 'Financial Position'!BX46 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BX7 | — | OK |
| `ST_BORROWINGS` | BS_2026_08_31 | BY7 | `2026-08-31 00:00:00` | 'Financial Position'!BY46 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | UNPROVEN (header-stated; equals file/update date) | BS_DATE_NOT_PERIOD_END; BS_DATE_EQUALS_FILE_DATE | WARNING |
| `LT_BORROWINGS` | BS_2025_12_31 | BW7 | `2025-12-31 00:00:00` | 'Financial Position'!BW51 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BW7 | — | OK |
| `LT_BORROWINGS` | BS_2026_03_31 | BX7 | `2026-03-31 00:00:00` | 'Financial Position'!BX51 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BX7 | — | OK |
| `LT_BORROWINGS` | BS_2026_08_31 | BY7 | `2026-08-31 00:00:00` | 'Financial Position'!BY51 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | UNPROVEN (header-stated; equals file/update date) | BS_DATE_NOT_PERIOD_END; BS_DATE_EQUALS_FILE_DATE | WARNING |
| `LEASE_IFRS16_CURRENT` | BS_2025_12_31 | BW7 | `2025-12-31 00:00:00` | 'Financial Position'!BW44 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BW7 | — | OK |
| `LEASE_IFRS16_CURRENT` | BS_2026_03_31 | BX7 | `2026-03-31 00:00:00` | 'Financial Position'!BX44 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BX7 | — | OK |
| `LEASE_IFRS16_CURRENT` | BS_2026_08_31 | BY7 | `2026-08-31 00:00:00` | 'Financial Position'!BY44 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | UNPROVEN (header-stated; equals file/update date) | BS_DATE_NOT_PERIOD_END; BS_DATE_EQUALS_FILE_DATE | WARNING |
| `LEASE_IFRS16_NONCURRENT` | BS_2025_12_31 | BW7 | `2025-12-31 00:00:00` | 'Financial Position'!BW52 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BW7 | — | OK |
| `LEASE_IFRS16_NONCURRENT` | BS_2026_03_31 | BX7 | `2026-03-31 00:00:00` | 'Financial Position'!BX52 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BX7 | — | OK |
| `LEASE_IFRS16_NONCURRENT` | BS_2026_08_31 | BY7 | `2026-08-31 00:00:00` | 'Financial Position'!BY52 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | UNPROVEN (header-stated; equals file/update date) | BS_DATE_NOT_PERIOD_END; BS_DATE_EQUALS_FILE_DATE | WARNING |
| `LEASE_IAS17_CURRENT` | BS_2025_12_31 | BW7 | `2025-12-31 00:00:00` | 'Financial Position'!BW45 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BW7 | explicit zero (FACT) | OK |
| `LEASE_IAS17_CURRENT` | BS_2026_03_31 | BX7 | `2026-03-31 00:00:00` | 'Financial Position'!BX45 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BX7 | explicit zero (FACT) | OK |
| `LEASE_IAS17_CURRENT` | BS_2026_08_31 | BY7 | `2026-08-31 00:00:00` | 'Financial Position'!BY45 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | UNPROVEN (header-stated; equals file/update date) | explicit zero (FACT); BS_DATE_NOT_PERIOD_END; BS_DATE_EQUALS_FILE_DATE | WARNING |
| `LEASE_IAS17_NONCURRENT` | BS_2025_12_31 | BW7 | `2025-12-31 00:00:00` | 'Financial Position'!BW53 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BW7 | explicit zero (FACT) | OK |
| `LEASE_IAS17_NONCURRENT` | BS_2026_03_31 | BX7 | `2026-03-31 00:00:00` | 'Financial Position'!BX53 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BX7 | explicit zero (FACT) | OK |
| `LEASE_IAS17_NONCURRENT` | BS_2026_08_31 | BY7 | `2026-08-31 00:00:00` | 'Financial Position'!BY53 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | UNPROVEN (header-stated; equals file/update date) | explicit zero (FACT); BS_DATE_NOT_PERIOD_END; BS_DATE_EQUALS_FILE_DATE | WARNING |
| `CASH` | BS_2025_12_31 | BW7 | `2025-12-31 00:00:00` | 'Financial Position'!BW10 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BW7 | — | OK |
| `CASH` | BS_2026_03_31 | BX7 | `2026-03-31 00:00:00` | 'Financial Position'!BX10 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BX7 | — | OK |
| `CASH` | BS_2026_08_31 | BY7 | `2026-08-31 00:00:00` | 'Financial Position'!BY10 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | UNPROVEN (header-stated; equals file/update date) | BS_DATE_NOT_PERIOD_END; BS_DATE_EQUALS_FILE_DATE | WARNING |
| `ST_FIN_INVESTMENTS` | BS_2025_12_31 | BW7 | `2025-12-31 00:00:00` | 'Financial Position'!BW11 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BW7 | — | OK |
| `ST_FIN_INVESTMENTS` | BS_2026_03_31 | BX7 | `2026-03-31 00:00:00` | 'Financial Position'!BX11 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BX7 | — | OK |
| `ST_FIN_INVESTMENTS` | BS_2026_08_31 | BY7 | `2026-08-31 00:00:00` | 'Financial Position'!BY11 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | UNPROVEN (header-stated; equals file/update date) | BS_DATE_NOT_PERIOD_END; BS_DATE_EQUALS_FILE_DATE | WARNING |
| `PENSION_LIABILITIES` | FY2025 (annual sheet) | S7 | `2025` | 'Debt Profile'!S14 | no | constant | — | yes | number (float→Decimal(str)) | — | — | UNPROVEN (integer-year header; §6.1.6 reconciliation not proven) | — | N/A (UNIT_UNDECLARED) |
| `PENSION_ROIC_XCHECK` | FY2025 (annual sheet) | S7 | `2025` | 'ROIC'!S21 | no | constant | — | yes | number (float→Decimal(str)) | RUB million per B7 `RUB million, if not stated otherwise` | 'ROIC'!B7 | UNPROVEN (integer-year header; §6.1.6 reconciliation not proven) | — | N/A (LABEL_AMBIGUOUS) |
| `NET_DEBT_DATABOOK` | FY2025 (annual sheet) | S7 | `2025` | 'Debt Profile'!S17 | no | constant | — | yes | number (float→Decimal(str)) | — | — | UNPROVEN (integer-year header; §6.1.6 reconciliation not proven) | — | N/A (UNIT_UNDECLARED) |
| `NET_DEBT_EBITDA_DATABOOK` | FY2025 (annual sheet) | S7 | `2025` | 'Debt Profile'!S27 | no | constant | — | yes | number (float→Decimal(str)) | — | — | — | — | N/A (UNIT_UNDECLARED) |

### Main KPI source (reported)

| Metric ID | Period | Header cell | Header raw | Source cell | Hidden? | Kind | Formula | Cached value present? | Type | Unit / scale | Unit cell | BS date status | Flags | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `REVENUE` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU10 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `REVENUE` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW10 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `REVENUE` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY10 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `TRAFFIC_REVENUE` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU8 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `TRAFFIC_REVENUE` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW8 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `TRAFFIC_REVENUE` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY8 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `OPERATING_PROFIT` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU18 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `OPERATING_PROFIT` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW18 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `OPERATING_PROFIT` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY18 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PBT` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU26 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PBT` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW26 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PBT` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY26 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `NET_PROFIT` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU29 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | label wording vs period (§15.3.5) | OK |
| `NET_PROFIT` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW29 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `NET_PROFIT` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY29 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | label wording vs period (§15.3.5) | OK |
| `EBITDA` | H1_2025 | BU7 | `6M 2025` | 'EBITDA'!BU11 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million` | 'EBITDA'!B7 | — | — | OK |
| `EBITDA` | FY2025 | BW7 | `12M 2025` | 'EBITDA'!BW11 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million` | 'EBITDA'!B7 | — | — | OK |
| `EBITDA` | H1_2026 | BY7 | `6M 2026` | 'EBITDA'!BY11 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million` | 'EBITDA'!B7 | — | — | OK |
| `EBITDAR` | H1_2025 | BU7 | `6M 2025` | 'EBITDA'!BU13 | no | constant | — | yes | text `-` | RUB million per B7 `RUB million` | 'EBITDA'!B7 | — | — | N/A (DASH_PLACEHOLDER) |
| `EBITDAR` | FY2025 | BW7 | `12M 2025` | 'EBITDA'!BW13 | no | constant | — | yes | text `-` | RUB million per B7 `RUB million` | 'EBITDA'!B7 | — | — | N/A (DASH_PLACEHOLDER) |
| `EBITDAR` | H1_2026 | BY7 | `6M 2026` | 'EBITDA'!BY13 | no | constant | — | yes | text `-` | RUB million per B7 `RUB million` | 'EBITDA'!B7 | — | — | N/A (DASH_PLACEHOLDER) |
| `EBITDA_MARGIN_REPORTED` | H1_2025 | BU7 | `6M 2025` | 'EBITDA'!BU17 | no | constant | — | yes | number (float→Decimal(str)) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `EBITDA_MARGIN_REPORTED` | FY2025 | BW7 | `12M 2025` | 'EBITDA'!BW17 | no | constant | — | yes | number (float→Decimal(str)) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `EBITDA_MARGIN_REPORTED` | H1_2026 | BY7 | `6M 2026` | 'EBITDA'!BY17 | no | constant | — | yes | number (float→Decimal(str)) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPERATING_MARGIN_REPORTED` | H1_2025 | BU7 | `6M 2025` | 'EBITDA'!BU16 | no | constant | — | yes | number (float→Decimal(str)) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPERATING_MARGIN_REPORTED` | FY2025 | BW7 | `12M 2025` | 'EBITDA'!BW16 | no | constant | — | yes | number (float→Decimal(str)) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPERATING_MARGIN_REPORTED` | H1_2026 | BY7 | `6M 2026` | 'EBITDA'!BY16 | no | constant | — | yes | number (float→Decimal(str)) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `NET_MARGIN_REPORTED` | H1_2025 | BU7 | `6M 2025` | 'EBITDA'!BU19 | no | constant | — | yes | number (float→Decimal(str)) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `NET_MARGIN_REPORTED` | FY2025 | BW7 | `12M 2025` | 'EBITDA'!BW19 | no | constant | — | yes | number (float→Decimal(str)) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `NET_MARGIN_REPORTED` | H1_2026 | BY7 | `6M 2026` | 'EBITDA'!BY19 | no | constant | — | yes | number (float→Decimal(str)) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `CFF` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU89 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CFF` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW89 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CFF` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY89 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `TOTAL_EQUITY` | BS_2025_12_31 | BW7 | `2025-12-31 00:00:00` | 'Financial Position'!BW73 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BW7 | — | OK |
| `TOTAL_EQUITY` | BS_2026_03_31 | BX7 | `2026-03-31 00:00:00` | 'Financial Position'!BX73 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | PROVEN by datetime header BX7 | — | OK |
| `TOTAL_EQUITY` | BS_2026_08_31 | BY7 | `2026-08-31 00:00:00` | 'Financial Position'!BY73 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Financial Position'!B7 | UNPROVEN (header-stated; equals file/update date) | BS_DATE_NOT_PERIOD_END; BS_DATE_EQUALS_FILE_DATE | WARNING |
| `CFO_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S21 | no | constant | — | yes | number (int) | RUB million per B7 `mn RUB if not stated otherwise` | 'Highlights and Ratios'!B7 | — | — | OK |
| `CFI_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S22 | no | constant | — | yes | number (int) | RUB million per B7 `mn RUB if not stated otherwise` | 'Highlights and Ratios'!B7 | — | — | OK |
| `CFF_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S23 | no | constant | — | yes | number (int) | RUB million per B7 `mn RUB if not stated otherwise` | 'Highlights and Ratios'!B7 | — | — | OK |
| `REVENUE_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S12 | no | constant | — | yes | number (int) | RUB million per B7 `mn RUB if not stated otherwise` | 'Highlights and Ratios'!B7 | — | — | OK |
| `EBITDA_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S14 | no | constant | — | yes | number (int) | RUB million per B7 `mn RUB if not stated otherwise` | 'Highlights and Ratios'!B7 | — | — | OK |
| `EBITDAR_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S13 | no | constant | — | yes | text `-` | RUB million per B7 `mn RUB if not stated otherwise` | 'Highlights and Ratios'!B7 | — | — | N/A (DASH_PLACEHOLDER) |
| `NET_PROFIT_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S15 | no | constant | — | yes | number (int) | RUB million per B7 `mn RUB if not stated otherwise` | 'Highlights and Ratios'!B7 | — | — | OK |
| `NET_DEBT_EBITDA_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S33 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Net Debt/12M EBITDA (х)` | row label | — | — | OK |
| `GROSS_DEBT_EBITDA_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S32 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Gross Debt/EBITDA 12M(х)` | row label | — | — | OK |
| `EBITDA_INTEREST_COVER_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S31 | no | constant | — | yes | number (float→Decimal(str)) | from row label `EBITDA/Gross Interest (х)***` | row label | — | — | OK |
| `ROIC_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S30 | no | constant | — | yes | text `-` | RUB million per B7 `mn RUB if not stated otherwise` | 'Highlights and Ratios'!B7 | — | — | N/A (DASH_PLACEHOLDER) |
| `BANK_DEBT_EQUITY_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S34 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Bank Debt/Equity (х)` | row label | — | — | N/A (LABEL_AMBIGUOUS) |

### Operating metric

| Metric ID | Period | Header cell | Header raw | Source cell | Hidden? | Kind | Formula | Cached value present? | Type | Unit / scale | Unit cell | BS date status | Flags | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `PAX_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S8 | no | constant | — | yes | number (float→Decimal(str)) | from row label `PAX, mn` | row label | — | — | OK |
| `RPK_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S9 | no | constant | — | yes | number (float→Decimal(str)) | from row label `RPK, bn` | row label | — | — | OK |
| `PLF_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S10 | no | constant | — | yes | number (float→Decimal(str)) | from row label `PLF, %` | row label | — | — | OK |
| `FLEET_HR` | FY2025 (annual sheet) | S7 | `2025` | 'Highlights and Ratios'!S11 | no | constant | — | yes | number (int) | RUB million per B7 `mn RUB if not stated otherwise` | 'Highlights and Ratios'!B7 | UNPROVEN (integer-year header; §6.1.6 reconciliation not proven) | — | WARNING |
| `PAX_GROUP` | FY2025 (annual sheet) | S7 | `2025` | 'AFLT - Operating - abs'!S9 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Passengers carried, thd` | row label | — | — | OK |
| `RPK_GROUP` | FY2025 (annual sheet) | S7 | `2025` | 'AFLT - Operating - abs'!S12 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Passenger turnover, mn RPK` | row label | — | — | OK |
| `ASK_GROUP` | FY2025 (annual sheet) | S7 | `2025` | 'AFLT - Operating - abs'!S15 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Available seat-kilometers, mn ASK` | row label | — | — | OK |
| `PLF_GROUP` | FY2025 (annual sheet) | S7 | `2025` | 'AFLT - Operating - abs'!S18 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Passenger load factor, %` | row label | — | — | OK |
| `RPK_RC` | FY2025 (annual sheet) | S7 | `2025` | 'RASK-CASK'!S17 | no | constant | — | yes | number (float→Decimal(str)) | from row label `RPK, mn` | row label | — | — | OK |
| `ASK_RC` | FY2025 (annual sheet) | S7 | `2025` | 'RASK-CASK'!S25 | no | constant | — | yes | number (float→Decimal(str)) | from row label `ASK, mn` | row label | — | — | OK |
| `YIELD_TRAFFIC` | FY2025 (annual sheet) | S7 | `2025` | — | — | — | — | — | — | RUB per RPK per section label row 36 | 'RASK-CASK'!B36 | — | — | N/A (LABEL_AMBIGUOUS) |
| `RASK_TRAFFIC` | FY2025 (annual sheet) | S7 | `2025` | — | — | — | — | — | — | RUB per ASK per section label row 50 | 'RASK-CASK'!B50 | — | — | N/A (LABEL_AMBIGUOUS) |
| `CASK_TOTAL` | FY2025 (annual sheet) | S7 | `2025` | 'RASK-CASK'!S120 | no | constant | — | yes | number (float→Decimal(str)) | `RUB ` (table header B99) conflicts with B7 `RUB million` | 'RASK-CASK'!B99 vs B7 | — | UNIT_CONFLICT | N/A (LABEL_AMBIGUOUS) |
| `CASK_EX_FUEL` | FY2025 (annual sheet) | S7 | `2025` | 'RASK-CASK'!S118 | no | constant | — | yes | number (float→Decimal(str)) | `RUB ` (table header B99) conflicts with B7 `RUB million` | 'RASK-CASK'!B99 vs B7 | — | UNIT_CONFLICT | N/A (LABEL_AMBIGUOUS) |
| `ASK_FUEL_SHEET` | H1_2025 | BU7 | `6M 2025` | 'Fuel Consumption'!BU9 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Available seat-kilometers, mn ASK` | row label | — | — | OK |
| `ASK_FUEL_SHEET` | FY2025 | BW7 | `12M 2025` | 'Fuel Consumption'!BW9 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Available seat-kilometers, mn ASK` | row label | — | — | OK |
| `ASK_FUEL_SHEET` | H1_2026 | BY7 | `6M 2026` | 'Fuel Consumption'!BY9 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Available seat-kilometers, mn ASK` | row label | — | — | OK |
| `ATK_FUEL_SHEET` | H1_2025 | BU7 | `6M 2025` | 'Fuel Consumption'!BU10 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Available tonne-kilometers, mn ATK` | row label | — | — | OK |
| `ATK_FUEL_SHEET` | FY2025 | BW7 | `12M 2025` | 'Fuel Consumption'!BW10 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Available tonne-kilometers, mn ATK` | row label | — | — | OK |
| `ATK_FUEL_SHEET` | H1_2026 | BY7 | `6M 2026` | 'Fuel Consumption'!BY10 | no | constant | — | yes | number (float→Decimal(str)) | from row label `Available tonne-kilometers, mn ATK` | row label | — | — | OK |
| `PAX_REGIONS_TOTAL` | FY2025 (annual sheet) | — | — | — | — | — | — | — | — | section label `PAX, mn` only (not row label, not B7) | 'AFLT - Regions'!B9 | — | period header repeated in columns S, AL (§6.1.5) | N/A (LABEL_AMBIGUOUS) |
| `RPK_REGIONS_TOTAL` | FY2025 (annual sheet) | — | — | — | — | — | — | — | — | section label `RPK, bn ` only (not row label, not B7) | 'AFLT - Regions'!B19 | — | period header repeated in columns S, AL (§6.1.5) | N/A (LABEL_AMBIGUOUS) |
| `ASK_REGIONS_TOTAL` | FY2025 (annual sheet) | — | — | — | — | — | — | — | — | section label `ASK, bn ` only (not row label, not B7) | 'AFLT - Regions'!B29 | — | period header repeated in columns S, AL (§6.1.5) | N/A (LABEL_AMBIGUOUS) |
| `PLF_REGIONS_TOTAL` | FY2025 (annual sheet) | — | — | — | — | — | — | — | — | section label `PLF, %` only (not row label, not B7) | 'AFLT - Regions'!B39 | — | period header repeated in columns S, AL (§6.1.5) | N/A (LABEL_AMBIGUOUS) |

### Operating expense line

| Metric ID | Period | Header cell | Header raw | Source cell | Hidden? | Kind | Formula | Cached value present? | Type | Unit / scale | Unit cell | BS date status | Flags | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `OPEX_R9` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU9 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R9` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW9 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R9` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY9 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R10` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU10 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation; explicit zero (FACT) | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R10` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW10 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation; explicit zero (FACT) | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R10` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY10 | no | constant | — | yes | text `-` | — | — | — | — | N/A (DASH_PLACEHOLDER) |
| `OPEX_R11` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU11 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R11` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW11 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R11` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY11 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R12` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU12 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R12` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW12 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R12` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY12 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R13` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU13 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R13` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW13 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R13` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY13 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R14` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU14 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R14` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW14 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R14` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY14 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R15` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU15 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R15` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW15 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R15` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY15 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R16` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU16 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R16` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW16 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R16` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY16 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R17` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU17 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R17` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW17 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R17` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY17 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R18` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU18 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R18` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW18 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R18` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY18 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R19` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU19 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R19` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW19 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R19` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY19 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R20` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU20 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation; explicit zero (FACT) | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R20` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW20 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation; explicit zero (FACT) | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R20` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY20 | no | constant | — | yes | number (int) | — | — | — | explicit zero (FACT) | N/A (UNIT_UNDECLARED) |
| `OPEX_R21` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU21 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R21` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW21 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R21` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY21 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R22` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU22 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R22` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW22 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R22` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY22 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R23` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU23 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R23` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW23 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R23` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY23 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R24` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU24 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R24` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW24 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R24` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY24 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R25` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU25 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R25` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW25 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R25` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY25 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R26` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU26 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R26` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW26 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R26` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY26 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R29` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU29 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R29` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW29 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R29` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY29 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R30` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU30 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R30` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW30 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R30` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY30 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R31` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU31 | no | constant | — | yes | text `-` | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R31` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW31 | no | constant | — | yes | text `-` | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R31` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY31 | no | constant | — | yes | text `-` | — | — | — | — | N/A (DASH_PLACEHOLDER) |
| `OPEX_R32` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU32 | no | constant | — | yes | text `-` | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R32` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW32 | no | constant | — | yes | text `-` | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R32` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY32 | no | constant | — | yes | text `-` | — | — | — | — | N/A (DASH_PLACEHOLDER) |
| `OPEX_R33` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU33 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R33` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW33 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R33` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY33 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R36` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU36 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R36` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW36 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R36` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY36 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R37` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU37 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R37` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW37 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R37` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY37 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R38` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU38 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R38` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW38 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R38` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY38 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `OPEX_R40` | H1_2025 | BU7 | `6М 2025` | 'Operating Expenses'!BU40 | no | constant | — | yes | number (int) | — | — | — | header `6М 2025` uses Cyrillic `М` (U+041C) — not a valid `6M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R40` | FY2025 | BW7 | `12М 2025` | 'Operating Expenses'!BW40 | no | constant | — | yes | number (int) | — | — | — | header `12М 2025` uses Cyrillic `М` (U+041C) — not a valid `12M 2025` header after §15.3.2 normalisation | N/A (HEADER_AMBIGUOUS) |
| `OPEX_R40` | H1_2026 | BY7 | `6M 2026` | 'Operating Expenses'!BY40 | no | constant | — | yes | number (int) | — | — | — | — | N/A (UNIT_UNDECLARED) |
| `PL_OPEX_R12` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU12 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R12` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW12 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R12` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY12 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R13` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU13 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R13` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW13 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R13` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY13 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R14` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU14 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R14` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW14 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R14` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY14 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R15` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU15 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R15` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW15 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R15` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY15 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R16` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU16 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R16` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW16 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `PL_OPEX_R16` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY16 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |

### Cash-flow component

| Metric ID | Period | Header cell | Header raw | Source cell | Hidden? | Kind | Formula | Cached value present? | Type | Unit / scale | Unit cell | BS date status | Flags | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `CF_R53` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU53 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R53` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW53 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R53` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY53 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R54` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU54 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R54` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW54 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R54` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY54 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R55` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU55 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R55` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW55 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R55` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY55 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R56` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU56 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R56` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW56 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R56` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY56 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R57` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU57 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R57` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW57 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R57` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY57 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R58` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU58 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R58` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW58 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R58` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY58 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R59` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU59 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R59` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW59 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R59` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY59 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R60` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU60 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R60` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW60 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R60` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY60 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R61` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU61 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R61` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW61 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R61` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY61 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R62` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU62 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R62` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW62 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R62` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY62 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R63` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU63 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R63` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW63 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R63` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY63 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R64` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU64 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R64` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW64 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R64` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY64 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R65` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU65 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R65` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW65 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R65` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY65 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R66` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU66 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R66` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW66 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R66` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY66 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R67` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU67 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R67` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW67 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R67` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY67 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R68` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU68 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R68` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW68 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R68` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY68 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R69` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU69 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R69` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW69 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R69` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY69 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R70` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU70 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R70` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW70 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R70` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY70 | no | empty | — | no | blank | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | N/A (MISSING_CELL) |
| `CF_R71` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU71 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R71` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW71 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R71` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY71 | no | empty | — | no | blank | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | N/A (MISSING_CELL) |
| `CF_R72` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU72 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R72` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW72 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R72` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY72 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R75` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU75 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R75` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW75 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R75` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY75 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R76` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU76 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R76` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW76 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R76` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY76 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R77` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU77 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R77` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW77 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R77` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY77 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R78` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU78 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R78` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW78 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R78` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY78 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R79` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU79 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R79` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW79 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R79` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY79 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R80` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU80 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R80` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW80 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R80` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY80 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R81` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU81 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R81` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW81 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R81` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY81 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R82` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU82 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R82` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW82 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R82` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY82 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R83` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU83 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R83` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW83 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R83` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY83 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R84` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU84 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R84` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW84 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R84` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY84 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R85` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU85 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R85` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW85 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R85` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY85 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R86` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU86 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R86` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW86 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R86` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY86 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R87` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU87 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R87` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW87 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R87` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY87 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R88` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU88 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R88` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW88 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R88` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY88 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | explicit zero (FACT) | OK |
| `CF_R89` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU89 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R89` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW89 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CF_R89` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY89 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |

### FX / interest line

| Metric ID | Period | Header cell | Header raw | Source cell | Hidden? | Kind | Formula | Cached value present? | Type | Unit / scale | Unit cell | BS date status | Flags | Status |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `FX_EFFECT_ON_CASH` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU91 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `FX_EFFECT_ON_CASH` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW91 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `FX_EFFECT_ON_CASH` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY91 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `FX_GAIN_LOSS_ADJ` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU26 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `FX_GAIN_LOSS_ADJ` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW26 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `FX_GAIN_LOSS_ADJ` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY26 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `INTEREST_EXPENSE_ADJ` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU24 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `INTEREST_EXPENSE_ADJ` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW24 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `INTEREST_EXPENSE_ADJ` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY24 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `INTEREST_INCOME_ADJ` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU25 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `INTEREST_INCOME_ADJ` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW25 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `INTEREST_INCOME_ADJ` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY25 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `FINANCE_INCOME` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU21 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `FINANCE_INCOME` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW21 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `FINANCE_INCOME` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY21 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `FINANCE_COSTS` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU22 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `FINANCE_COSTS` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW22 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `FINANCE_COSTS` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY22 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | — | OK |
| `OCI_TRANSLATION` | H1_2025 | BU7 | `6M 2025` | 'Profit and Loss, OCI'!BU43 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | explicit zero (FACT) | OK |
| `OCI_TRANSLATION` | FY2025 | BW7 | `12M 2025` | 'Profit and Loss, OCI'!BW43 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | explicit zero (FACT) | OK |
| `OCI_TRANSLATION` | H1_2026 | BY7 | `6M 2026` | 'Profit and Loss, OCI'!BY43 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Profit and Loss, OCI'!B7 | — | explicit zero (FACT) | OK |
| `CASH_OPENING_CF` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU94 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | label wording vs period (§15.3.5) | OK |
| `CASH_OPENING_CF` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW94 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CASH_OPENING_CF` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY94 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | label wording vs period (§15.3.5) | OK |
| `CASH_CLOSING_CF` | H1_2025 | BU7 | `6M 2025` | 'Cash Flow'!BU95 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | label wording vs period (§15.3.5) | OK |
| `CASH_CLOSING_CF` | FY2025 | BW7 | `12M 2025` | 'Cash Flow'!BW95 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | — | OK |
| `CASH_CLOSING_CF` | H1_2026 | BY7 | `6M 2026` | 'Cash Flow'!BY95 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'Cash Flow'!B7 | — | label wording vs period (§15.3.5) | OK |
| `INTEREST_ROIC` | FY2025 (annual sheet) | S7 | `2025` | 'ROIC'!S15 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'ROIC'!B7 | — | — | OK |
| `INTEREST_CAP_OL_ROIC` | FY2025 (annual sheet) | S7 | `2025` | 'ROIC'!S16 | no | constant | — | yes | number (int) | RUB million per B7 `RUB million, if not stated otherwise` | 'ROIC'!B7 | — | explicit zero (FACT) | OK |

## Balance-sheet dates — proof

| Period ID | Header cell | Raw header | Header type | Evidence | Status |
|---|---|---|---|---|---|
| `_BS_2025_12_31` | `'Financial Position'!BW7` | datetime 2025-12-31 | datetime | Row-7 datetime header on the balance-sheet sheet; quarter-end sequence BB7…BW7; CF 12M 2025 closing cash (BW95) EQUAL to FP BW10 | PROVEN |
| `_BS_2026_03_31` | `'Financial Position'!BX7` | datetime 2026-03-31 | datetime | Row-7 datetime header; CF 3M 2026 closing cash (BX95) EQUAL to FP BX10 | PROVEN |
| `_BS_2026_08_31` | `'Financial Position'!BY7` | datetime 2026-08-31, constant (not a formula), format `d-mmm-yy` | datetime | **Against:** identical to `Contents!Q25` (constant 2026-08-31, labelled by `Contents!N25` `Date of the update`) and to the file's `docProps/core.xml` `dcterms:modified` (2026-08-31). It is not the end of any flow period in the workbook (latest flow column BY7 on every flow sheet is `6M 2026`, ending 30 Jun 2026). CF `6M 2026` closing cash (`'Cash Flow'!BY95`) is EQUAL to FP BY10, and CF `6M 2026` opening cash (BY94) is EQUAL to FP BW10. **For:** it sits in the row-7 balance-sheet header row, typed as a date like its neighbours. | **UNPROVEN** — cannot be shown to be a balance-sheet date rather than the file/update date. Labelled `_BS_2026_08_31` exactly as stated (§6.1.2); flags `BS_DATE_NOT_PERIOD_END`, `BS_DATE_EQUALS_FILE_DATE`; escalated (§16, §18) |
| `_BS_2025_12_31` (Debt Profile / ROIC, header `2025`) | `'Debt Profile'!S7`, `'ROIC'!S7` | integer `2025` | integer year | §6.1.6 needs reconciliation to FP 2025-12-31. One-to-one checks below; lease rows need summation (pending); `Debt Profile` has no unit statement (UNIT_UNDECLARED); `Debt Profile` row 12 has a B/D label mismatch | UNPROVEN |
| FP `S7` `31-Dec-2025` | `'Financial Position'!S7` | text | INVALID (not datetime) | Annual block duplicates the 2025-12-31 balance as text; not used — BW7 is the datetime header for that date | REJECTED (HEADER_AMBIGUOUS) |

### Single-value equality checks (no arithmetic)

| Left | Cell | Right | Cell | Result |
|---|---|---|---|---|
| CF `Cash and cash equivalents at the end of the year`, 12M 2025 | 'Cash Flow'!BW95 | FP `Cash and cash equivalents`, 2025-12-31 | 'Financial Position'!BW10 | EQUAL |
| CF same row, 3M 2026 | 'Cash Flow'!BX95 | FP same row, 2026-03-31 | 'Financial Position'!BX10 | EQUAL |
| CF same row, 6M 2026 (period ends 30 Jun 2026) | 'Cash Flow'!BY95 | FP same row, header 2026-08-31 | 'Financial Position'!BY10 | EQUAL |
| CF same row, 6M 2025 (period ends 30 Jun 2025) | 'Cash Flow'!BU95 | FP same row, header 2025-06-30 | 'Financial Position'!BU10 | EQUAL |
| CF `…at the beginning of the year`, 6M 2026 | 'Cash Flow'!BY94 | FP `Cash and cash equivalents`, 2025-12-31 | 'Financial Position'!BW10 | EQUAL |
| Debt Profile `Short-term debt`, 2025 | 'Debt Profile'!S9 | FP `ST loans and borrowings…`, 2025-12-31 | 'Financial Position'!BW46 | EQUAL |
| Debt Profile `Long-term debt`, 2025 | 'Debt Profile'!S10 | FP `Long-term loans and borrowings`, 2025-12-31 | 'Financial Position'!BW51 | EQUAL |
| Debt Profile `Cash and cash equivalents`, 2025 | 'Debt Profile'!S19 | FP `Cash and cash equivalents`, 2025-12-31 | 'Financial Position'!BW10 | EQUAL |
| Debt Profile `Short-term financial investments`, 2025 | 'Debt Profile'!S20 | FP `Short-term financial investments`, 2025-12-31 | 'Financial Position'!BW11 | EQUAL |

Debt Profile results are informational only: §6.1.6 is not satisfied because lease rows need summation and the sheet has no declared unit.

## 2018: IAS 17 vs IFRS 16 comparability

- Every data sheet carries a standard tag in row 6 (row 7 on `AFLT - Regions`): `IAS 17` for 2012–2018 and `IFRS 16` for 2018–2025 / 2026 interims.
- Annual blocks show **2018 twice**: column K (`IAS 17`) and column L (`IFRS 16`), both with integer header `2018` (Highlights and Ratios, Debt Profile, ROIC, RASK-CASK, Operating sheets, MCap and EV, Dividends; `AFLT - Regions` K/L and AD/AE in row 8). On `Financial Position` K7 = `31-Dec-2018`, L7 = `31-Dec-2018***` (footnote row 77: "Figures updated versus previously reported due to refinement of judgments & estimates").
- Interim blocks show **2018 twice**: AN–AQ (`IAS 17`; `3М/6М/9М/12М 2018`, some with Cyrillic `М`) and AR–AU (`IFRS 16`). On `Financial Position` AR7 = `1-Jan-2018` (IFRS 16 opening), AS–AT hold `-`.
- Consequences: any lookup of period `2018` is `LABEL_AMBIGUOUS` (§6.1.5) until the owner says which column applies. Years ≤2017 are IAS 17 only and 2019+ IFRS 16 only, so no series is like-for-like across the 2018 boundary: under IAS 17 operating lease cost sits in OpEx (`Operating Expenses` row 10 `Operating lease expenses`, D `(IAS17)`); under IFRS 16 it moves to D&A and interest (lease liabilities on FP rows 44/52; `ROIC` row 9 `Operating lease expense` and `EBITDA` row 12 `(-) Operating lease` relate to the IAS 17 basis). EBITDA, EBITDAR, net debt and lease-related cash flows are therefore not comparable across the boundary.
- Additional break: `EBITDA` row 24 footnote — from 2025 EBITDA incorporates customs duties (row 10 `(-) Customs duties`), so FY2025 EBITDA is not like-for-like with 2024 and earlier.

## Route / region availability (annual only)

- `AFLT - Operating - abs` (and `- %`): route split `International routes` / `Domestic routes` for PAX, RPK, ASK, PLF, cargo, TKM, ATK, revenue load factor, flights — for `Aeroflot Group` (rows 8–36) and for the airlines `Aeroflot Airlines` (38–66), `Rossiya Airlines` (68–96), `Aurora Airlines` (99–127), `Pobeda Airlines` (130–158). Columns E–S, integer headers 2012–2025 only: **no interim periods**. Route rows carry no unit in their own label (unit only in the parent label) → `UNIT_UNDECLARED` under §6.2.2.
- `AFLT - Regions`: region split Russia, Europe, Asia, CIS, MEA, Americas, Total scheduled, Charter, Total for PAX (rows 9–18), RPK (19–28), ASK (29–38), PLF (39–48). Two blocks: `Aeroflot Group` (B6; columns E–S) and `Aeroflot Airline` (U6; columns X–AL, labels repeated in V/W). Header row is **8** (row 7 holds the IAS 17/IFRS 16 tags). Integer years 2012–2025 only: **no interim periods**. Year `2025` appears in both S8 and AL8 and `2018` in K/L and AD/AE → `LABEL_AMBIGUOUS` for any period lookup until the owner confirms block scoping. Units only in the section labels (`PAX, mn`, `RPK, bn `, `ASK, bn `, `PLF, %`) → `UNIT_UNDECLARED` for child rows under §6.2.2. Rows 51–81 are hidden and empty.
- No financial figure is split by route or region anywhere in the workbook; per §8.2 none may be allocated.

## Main KPIs and source mapping

No values computed. Formula text is copied from `PROJECT_RULES.md` §7; inputs refer to the metric IDs above.

| KPI (metric ID stem) | Definition (§7) | Inputs | Periods | Reported cross-check (1b) | Readiness |
|---|---|---|---|---|---|
| `FCF_DATABOOK` | CFO + CFI | `CFO`, `CFI` | FY2025, H1 2026 | `FCF_DATABOOK_REPORTED` (H&R row 25, annual) | H1_2025: OK; FY2025: OK; H1_2026: OK |
| `FCF_CONSERVATIVE` | CFO − capex − lease principal (capex = \|PPE&intangibles\| + \|prepayments for aircraft\|; lease principal = \|IFRS 16\| + \|IAS 17\|) | `CFO`, `CAPEX_PPE_INTANG`, `CAPEX_PREPAY_AIRCRAFT`, `LEASE_PRINCIPAL_IFRS16`, `LEASE_PRINCIPAL_IAS17` | FY2025, H1 2026 | `CAPEX_DATABOOK` (H&R row 24) reported separately, not used | H1_2025: OK; FY2025: OK; H1_2026: OK |
| `GROSS_DEBT_EXCL_PENSIONS` | borrowings + lease liabilities | `ST_BORROWINGS`, `LT_BORROWINGS`, `LEASE_IFRS16_CURRENT`, `LEASE_IFRS16_NONCURRENT`, `LEASE_IAS17_CURRENT`, `LEASE_IAS17_NONCURRENT` | BS 2025-12-31, 2026-03-31, 2026-08-31 (unproven) | Debt Profile rows 9–13 (annual) | BS_2025_12_31: OK; BS_2026_03_31: OK; BS_2026_08_31: WARNING |
| `LIQUID_ASSETS` | cash + ST financial investments | `CASH`, `ST_FIN_INVESTMENTS` | as above | Debt Profile rows 19–20 | BS_2025_12_31: OK; BS_2026_03_31: OK; BS_2026_08_31: WARNING |
| `NET_DEBT_EXCL_PENSIONS` | gross debt excl. pensions − liquid assets | the two above | as above | — | as inputs |
| `PENSION_LIABILITIES` | as reported | `PENSION_LIABILITIES` (Debt Profile row 14); cross-check `PENSION_ROIC_XCHECK` | BS 2025-12-31 only (annual); interim = N/A `PENSION_LINE_NOT_IN_SOURCE` | — | FY2025 (annual sheet): N/A (UNIT_UNDECLARED) |
| `NET_DEBT_INCL_PENSIONS` | net debt excl. pensions + pension liabilities | above | BS 2025-12-31 only; interim N/A (§7.2.2) | `NET_DEBT_DATABOOK` (Debt Profile row 17) | FY2025 (annual sheet): N/A (UNIT_UNDECLARED) |
| `REVENUE` | as reported | `REVENUE` | FY2025, H1 2025, H1 2026 | Highlights and Ratios (annual) | H1_2025: OK; FY2025: OK; H1_2026: OK |
| `OPERATING_PROFIT` | as reported | `OPERATING_PROFIT` | FY2025, H1 2025, H1 2026 | Highlights and Ratios (annual) | H1_2025: OK; FY2025: OK; H1_2026: OK |
| `EBITDA` | as reported (EBITDA sheet; customs-duties break 2025) | `EBITDA` | FY2025, H1 2025, H1 2026 | Highlights and Ratios (annual) | H1_2025: OK; FY2025: OK; H1_2026: OK |
| `EBITDAR` | as reported | `EBITDAR` | FY2025, H1 2025, H1 2026 | Highlights and Ratios (annual) | H1_2025: N/A (DASH_PLACEHOLDER); FY2025: N/A (DASH_PLACEHOLDER); H1_2026: N/A (DASH_PLACEHOLDER) |
| `NET_PROFIT` | as reported | `NET_PROFIT` | FY2025, H1 2025, H1 2026 | Highlights and Ratios (annual) | H1_2025: OK; FY2025: OK; H1_2026: OK |
| `CFF` | as reported | `CFF` | FY2025, H1 2025, H1 2026 | Highlights and Ratios (annual) | H1_2025: OK; FY2025: OK; H1_2026: OK |
| Margins (operating / EBITDA / net) | reported ratios on EBITDA sheet | `OPERATING_MARGIN_REPORTED`, `EBITDA_MARGIN_REPORTED`, `NET_MARGIN_REPORTED` | as above | Highlights rows 26–29 | H1_2025: N/A (UNIT_UNDECLARED); FY2025: N/A (UNIT_UNDECLARED); H1_2026: N/A (UNIT_UNDECLARED) |
| Net debt / EBITDA | quoted as reported (§4.3) | `NET_DEBT_EBITDA_DATABOOK`, `NET_DEBT_EBITDA_HR` | FY2025 (annual) | — | FY2025 (annual sheet): N/A (UNIT_UNDECLARED) |
| RPK / ASK / PLF | as reported | `RPK_HR`, `RPK_GROUP`, `RPK_RC`, `ASK_GROUP`, `ASK_RC`, `ASK_FUEL_SHEET`, `PLF_HR`, `PLF_GROUP` | FY2025 annual; ASK also H1 2025/H1 2026 (Fuel sheet only) | — | FY2025 (annual sheet): OK; H1_2025: OK; FY2025: OK; H1_2026: OK |
| Yield / RASK / CASK | as reported (RASK-CASK sheet) | `YIELD_TRAFFIC`, `RASK_TRAFFIC`, `CASK_TOTAL`, `CASK_EX_FUEL` | FY2025 annual only | — | FY2025 (annual sheet): N/A (LABEL_AMBIGUOUS) |

## Rejected sources

| Location | Reason |
|---|---|
| `'Financial Position'`!B43, B54 `Provisions for liabilities` | not a pension proxy (§7.2.2) |
| `'Revenue'` rows 24–38, `'Operating Expenses'` rows 43–63 | share-of-total (%) columns/rows — unsupported dimension (Step 8) |
| `'AFLT - Operating - %'` | growth/percentage sheet — change rows, not absolute values (Step 8) |
| `'AFLT - Regions'`, route rows of `'AFLT - Operating - abs'` | annual-only splits; may be reported only as present, never allocated to financials (§8) |
| Annual block columns E–S on flow sheets (`2025` integer headers) | FY2025 on flow sheets maps to `12M 2025` (§6.1); integer column not used |
| `'Financial Position'`!S7 `31-Dec-2025` (text) | balance-sheet date must come from a datetime header (§6.1); BW7 used |
| Single-quarter / LTM / annualised periods | later CALCULATIONs only (§6.1.3) |
| `'Headcount'` data cells | formulas with external links `[n]`; not a KPI input |
| `'Highlights and Ratios'`!B34 `Bank Debt/Equity (х)` | B/D label mismatch (§15.3.5) |
| `'Debt Profile'`!B12 `Short-term ` (lease) | D reads `Краткосрочные финансовые инвестиции` (ST financial investments) — B/D mismatch (§15.3.5) |
| `'Debt Profile'`!B16 `Cash, cash equivalents and ST investments` | D reads `Денежные средства и их эквиваленты` (cash only) — B/D mismatch (§15.3.5) |
| `'ROIC'`!B14 `Сustoms duties` | English label begins with Cyrillic `С` (U+0421); cannot match `Customs duties` (§15.3.2 does not transliterate) |

## Warnings

- FAIL: LABEL_AMBIGUOUS (B/D mismatch) 'ROIC'!B21/D21: D `Пенсионные обязательства` has no "non-current" qualifier — scope differs from B (§15.3.5).
- FAIL: LABEL_AMBIGUOUS (B/D mismatch) 'Highlights and Ratios'!B34/D34: D `Банковский долг/EBITDA (х)` means bank debt/EBITDA (§15.3.5 example).
- FAIL: LABEL_AMBIGUOUS `Traffic revenue` in 'RASK-CASK' section Yield (REV/RPK), RUB: rows 37, 43
- FAIL: LABEL_AMBIGUOUS `Traffic revenue` in 'RASK-CASK' section RASK (REV/ASK), RUB: rows 51, 57
- FAIL: LABEL_AMBIGUOUS (B/D mismatch) 'RASK-CASK'!B120/D120: D `Всего операционные расходы` (total operating expenses) does not say per-ASK.
- FAIL: LABEL_AMBIGUOUS (B/D mismatch) 'RASK-CASK'!B118/D118: D `Операционные расходы, искл ГСМ` (opex ex fuel) does not say per-ASK.
- FAIL: LABEL_AMBIGUOUS period header FY2025 (annual sheet) repeated in 'AFLT - Regions' row 8: columns S, AL (§6.1.5)
- FAIL: HEADER_AMBIGUOUS 'Operating Expenses'!BU7 = `6М 2025`: Cyrillic `М` (U+041C) instead of Latin `M` — period H1_2025 cannot be mapped (§6.1.5, §15.3.2)
- FAIL: HEADER_AMBIGUOUS 'Operating Expenses'!BW7 = `12М 2025`: Cyrillic `М` (U+041C) instead of Latin `M` — period FY2025 cannot be mapped (§6.1.5, §15.3.2)
- FAIL: No label-to-metric mapping file exists (§15.3.6); Russian labels cannot be verified against expected values
- FAIL: BS_DATE_EQUALS_FILE_DATE: 'Financial Position'!BY7 equals Contents!Q25 (`Date of the update`) and docProps modified date; CF 6M 2026 closing cash equals FP BY10 — balance-sheet date unproven
- FAIL: UNIT_UNDECLARED: 'Operating Expenses' has no unit statement in B7 and line labels carry none — every OpEx line is N/A (§6.2.2)
- FAIL: UNIT_UNDECLARED: 'Debt Profile' has no unit statement in B7 — pension liabilities, net debt and ratios are N/A (§6.2.2)
- FAIL: LABEL_AMBIGUOUS (B/D mismatch) 'Debt Profile'!B12/D12: B `Short-term ` (lease liabilities section) vs D `Краткосрочные финансовые инвестиции` (short-term financial investments) (§15.3.5)
- FAIL: LABEL_AMBIGUOUS (B/D mismatch) 'Debt Profile'!B16/D16: B `Cash, cash equivalents and ST investments` vs D `Денежные средства и их эквиваленты` (cash only) (§15.3.5)
- FAIL: LABEL_NOT_FOUND risk 'ROIC'!B14: English label `Сustoms duties` starts with Cyrillic `С` (U+0421)
- WARNING: §0 fact no longer holds: Source file in repository root — observed: not in the root of this branch; present only on branch `claude/dreamy-gates-aff9hw` (audited from git blob commit cf78592)
- WARNING: §0 fact no longer holds: Label columns — observed: B = formula `=IF(Contents!$L$5="РУС",D,C)` (selected language; cached English because `Contents!L5`=`ENG`); C = English constant; D = Russian constant; C and D hidden
- WARNING: §0 fact no longer holds: Flow period headers — observed: text YTD headers; on `Operating Expenses` `12М 2023`, `3М 2025`, `6М 2025`, `9М 2025`, `12М 2025`, `3М 2026` use Cyrillic `М` (U+041C); `6M 2026` is Latin. Flow sheets also carry an annual block with integer headers (`2012`…`2025`, columns E–S)
- WARNING: §0 fact no longer holds: Balance-sheet headers — observed: datetime only in columns BB–BY; columns E–S and U–BA are text (e.g. S7 `31-Dec-2025`, L7 `31-Dec-2018***`, AR7 `1-Jan-2018`). Latest BY7 = 2026-08-31, BX7 = 2026-03-31, BW7 = 2025-12-31
- WARNING: §0 fact no longer holds: Unit statements — observed: present on CF, FP, P&L, ROIC, RASK-CASK, Highlights; EBITDA `RUB million`; Revenue `RUB, mn`; **no unit statement in B7 on `Operating Expenses` and `Debt Profile`**
- WARNING: Workbook not in the repository root of this branch; audit run on a hash-identical git blob from branch `claude/dreamy-gates-aff9hw` (§15.2.1)
- WARNING: §0 label-column description is wrong: B is the language-switch formula, C is English, D is Russian; matching on B depends on cached results with `Contents!L5`=`ENG`
- WARNING: BS_DATE_NOT_PERIOD_END: 'Financial Position'!BY7 = 2026-08-31 vs `6M 2026` flow period ending 2026-06-30 (§6.1.2)
- WARNING: RASK-CASK: tables in rows 72–93 and 99–123 have their own header rows (72, 99) with unit text `RUB mn…` / `RUB ` that differs from B7
- WARNING: RASK-CASK yield (rows 37–48) and RASK (rows 51–62) blocks repeat identical labels twice with no distinguishing header
- WARNING: EBITDA footnote row 24: from 2025 EBITDA includes customs duties — FY2025 not comparable with earlier years
- INFO: Label wording vs period: `PROFIT/(LOSS) FOR THE YEAR`, `Cash and cash equivalents at the beginning/end of the year` used in 6M columns (§15.3.5)
- INFO: Known source typos kept as written: `Liqudity` (Debt Profile B22), `consumtion` (Fuel B8), `обоотные` (FP D20)
- INFO: External links: 6 external-link parts and defined names referring to `[1]`; no core financial data cell uses a formula

## Escalations for the project owner (§18)

1. **Workbook location (§15.2, §16.1).** The databook is only on branch `claude/dreamy-gates-aff9hw`. May it be added to the repository root of the working branch as the designated source (hash unchanged)?
2. **Balance-sheet date (§6.1.2, §16.1).** `'Financial Position'!BY7` = 2026-08-31 equals the file/update date and the CF `6M 2026` closing cash equals FP BY10. Is BY a 30 Jun 2026 balance with the update date typed into the header, or a genuine 31 Aug 2026 balance? Until confirmed it stays `_BS_2026_08_31` with `BS_DATE_NOT_PERIOD_END` and `BS_DATE_EQUALS_FILE_DATE`.
3. **Mapping file (§15.3.6).** Approve a label-to-metric mapping file (sheet, section, English B label, expected Russian D label, metric ID) — path and content need written approval.
4. **§0 corrections (§16.1).** §0 misdescribes the label columns (B/C), the FP header types (text before column BB) and the flow header characters (Cyrillic `М` on Operating Expenses). Update §0?
5. **Cyrillic `М` headers (§6.1.5, §15.3.2).** Operating Expenses `12М 2025`, `6М 2025` (and others) do not parse. May the normalisation map Cyrillic `М` to Latin `M` for period headers, or must these columns stay N/A?
6. **Units (§6.2.2).** `Operating Expenses` and `Debt Profile` declare no unit; route/region child rows and RASK-CASK sub-tables declare units only in section labels. Which source declares their unit, if any?
7. **Duplicate 2018 and 2025 headers (§6.1.5).** For 2018 use K (IAS 17) or L (IFRS 16)? On `AFLT - Regions` may the Group block (E–S) be selected by the row-6 block header?
8. **B/D label mismatches (§15.3.5).** Debt Profile rows 12 and 16, Highlights row 34, ROIC row 21, RASK-CASK rows 118/120 — how should each be resolved?
9. **Debt Profile / ROIC as `_BS_2025_12_31` (§6.1.6).** Lease rows need summation to reconcile; may that reconciliation be performed in the KPI stage before these stock rows are used?

## Summary

- Required rows: 142 — located with LABEL OK: 136, failed: 6
- Source cells: 350 — N/A (DASH_PLACEHOLDER): 8, N/A (HEADER_AMBIGUOUS): 54, N/A (LABEL_AMBIGUOUS): 10, N/A (MISSING_CELL): 2, N/A (UNIT_UNDECLARED): 36, OK: 230, WARNING: 10
- Overall status: FAIL
