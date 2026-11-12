---
name: financial-statement-analyzer
description: Deterministic, source-mapped analysis of a company financial databook (Excel workbook) into testable KPIs. Use when asked to extract revenue, EBITDA, cash flow or balance-sheet figures from a databook; convert cumulative (3M/6M/9M/12M) reporting into discrete quarters; compute free cash flow, CFO/EBITDA cash conversion, net debt and Net debt / LTM EBITDA; reconcile cash; build an EBITDA bridge; or validate FY2025 and H1 2026 results against tests/fixtures/checkpoints.json. Every value is computed in Python from mapped source cells, carries exact units and provenance, and is exported to outputs/kpi.json under a stable metric ID. Missing inputs are N/A, never zero.
---

# Financial Statement Analyzer

Turn a financial databook (`.xlsx`) into a set of reproducible, auditable KPIs.
Every number in the output must be traceable to a specific workbook cell, be
computed by deterministic Python code, carry an explicit unit, and be testable.

This skill is for **analysis and reconciliation**, not narrative estimation. If a
figure cannot be derived from cells in the workbook, it is reported as `N/A`
with a reason. Nothing is guessed, extrapolated, or filled in.

---

## 1. Non-negotiable rules

1. **Deterministic Python only.** All arithmetic is done in Python scripts
   (never mentally, never in prose, never by an LLM "reading" a number). Use
   `decimal.Decimal` built from the cell's string representation, not `float`.
   Running the pipeline twice on the same workbook must produce a byte-identical
   `outputs/kpi.json` (sorted keys, fixed ordering, no timestamps inside the
   metric payload except in the `run` block — see §9).
2. **Source cell mapping first.** No KPI is computed until a Source Map (§3)
   exists and every input it uses has been confirmed by row label.
3. **Locate by label, not by number.** Row numbers given anywhere (including
   §3.2 of this skill) are *starting hypotheses*. A row is accepted only when its
   label cell matches the expected label pattern. If the label is at a different
   row, use the row where the label is and record the drift. If the label is
   not found, the input is `N/A`.
4. **Exact units and provenance.** Each value records the workbook file hash,
   sheet, cell address, row label, column header, raw cell value, unit, and
   scale. Never silently convert units; any conversion is an explicit, logged
   step.
5. **N/A is not zero.** A missing input is `None` in Python and `null` in JSON
   with `"status": "N/A"` and a `reason`. Any formula with an N/A input yields
   N/A. Never coerce N/A to `0`, never drop it from a sum, never substitute a
   prior-period value. (A cell that genuinely contains `0` or a dash that the
   workbook defines as nil is a real zero and must be recorded as such, with the
   raw cell content kept in provenance.)
6. **Never infer 2026 geographic EBITDA.** EBITDA by geography/segment/region for
   any 2026 period is reported only if the workbook contains it explicitly in a
   labelled cell. It must not be derived by allocation, by applying 2025 shares,
   by revenue mix, or by any other proxy. If absent: `N/A`, reason
   `"not disclosed in workbook; inference prohibited"`.
7. **Checkpoints are student-owned.** `tests/fixtures/checkpoints.json` is
   owned by the student. Read it; never create, edit, overwrite, or "fix" it to
   make tests pass. If it is missing, validation status is `NOT_RUN`, not
   `PASS`.
8. **Label every derived definition.** When two definitions of the same concept
   exist (e.g. two FCFs), both carry distinct metric IDs and human-readable
   labels stating the formula.

---

## 2. Workflow

```
1. Inventory      → list sheets, header rows, period columns, unit captions
2. Source Map     → confirm each required input by row label (§3) → outputs/source_map.json
3. Extract        → read mapped cells into typed records with provenance (§4)
4. Normalise      → units, signs, cumulative → discrete quarters (§5)
5. Compute KPIs   → FCF, conversion, net debt, LTM, leverage (§6)
6. Reconcile      → quarterly sum check, cash reconciliation, EBITDA bridge (§7)
7. Validate       → compare FY2025 and H1 2026 with checkpoints.json (§8)
8. Export         → outputs/kpi.json (§9), then run tests (§10)
```

Do not skip steps. If a step fails, stop and report — do not continue with
partially mapped inputs as if they were complete.

Suggested layout (create only what is needed):

```
skills/financial-statement-analyzer/SKILL.md   # this file
src/fsa/source_map.py      # label search + Source Map
src/fsa/extract.py         # cell reads with provenance
src/fsa/periods.py         # cumulative → discrete, LTM
src/fsa/kpis.py            # KPI formulas
src/fsa/reconcile.py       # checks and bridges
src/fsa/export.py          # kpi.json writer
tests/test_kpis.py         # pytest, reads outputs/kpi.json + checkpoints.json
tests/fixtures/checkpoints.json   # student-owned, read-only for this skill
outputs/source_map.json
outputs/kpi.json
```

---

## 3. Source Map

### 3.1 Procedure

1. Open the workbook with `openpyxl.load_workbook(path, data_only=True)` to read
   cached values. Also open with `data_only=False` to record whether a cell is a
   formula (keep the formula text in provenance). If a cached value is `None`
   for a formula cell, the workbook was not recalculated: report this and treat
   the value as `N/A` — do not evaluate the formula by guesswork.
2. For each sheet, identify:
   - the **label column** (usually A or B) — the first column whose cells are
     mostly non-numeric text;
   - the **header row(s)** carrying period captions (e.g. `1Q 2025`, `6M 2025`,
     `H1 2026`, `12M 2025`, `FY2025`, `30.06.2026`, `31.12.2025`);
   - the **unit caption** (e.g. `RUB mn`, `RUB bn`, `thousand passengers`,
     `%`), usually in a title row or header cell.
3. For each required input, search for its label using a normalised comparison
   (casefold, collapse whitespace, strip footnote markers such as `*`, `(1)`,
   `¹`). Search first at the hypothesised row, then across the whole label column
   of the hypothesised sheet, then across other sheets.
4. Accept a match only if exactly one row matches the label pattern in the
   chosen sheet. Zero matches → `N/A`. Multiple matches → stop and ask the user
   (or disambiguate by the section header above the row, and record how).
5. Write `outputs/source_map.json`: one entry per input with the hypothesis,
   the confirmed location, the matched label text, and a `status` of
   `CONFIRMED`, `RELOCATED` (label found at a different row), or `NOT_FOUND`.

```json
{
  "input_id": "cf.cfo",
  "hypothesis": {"sheet": "Cash Flow", "row": 50},
  "confirmed": {"sheet": "Cash Flow", "row": 50, "label_cell": "B50"},
  "matched_label": "Net cash flows from operating activities",
  "label_pattern": "net cash .* operating activities",
  "status": "CONFIRMED",
  "unit": "RUB mn",
  "notes": ""
}
```

### 3.2 Starting hypotheses (to be confirmed by label)

These are **hypotheses only**. The meaning of each row is established by the
label found in the workbook, never by the row number. The label patterns are
the candidates to test; the Source Map records which (if any) actually applies.

| Sheet (hypothesis)   | Row(s) (hypothesis)        | Candidate label patterns to test                                                                                         |
|----------------------|----------------------------|--------------------------------------------------------------------------------------------------------------------------|
| Revenue              | 21                         | total revenue / revenue                                                                                                  |
| EBITDA               | 11                         | EBITDA (reported / adjusted — record which)                                                                              |
| Cash Flow            | 50, 72                     | net cash from operating activities; net cash used in investing activities; net cash from financing activities; net increase/decrease in cash |
| Financial Position   | 10, 11, 44, 46, 51, 52     | cash and cash equivalents; short-term investments / short-term financial investments; long-term and short-term borrowings (loans and borrowings); long-term and short-term lease liabilities; pension / post-employment obligations |

Rules for this table:

- Do **not** assume, e.g., that Cash Flow row 50 is CFO because it is the first
  listed row. Whatever label sits on row 50 decides what it is.
- If a hypothesised row carries a label not needed by this skill, record it as
  `UNUSED` and continue the label search for the inputs still required.
- Other inputs required by §6–§7 (capex, lease principal repayments, CFF, FX
  effect on cash, opening/closing cash, operating expense lines, operating
  metrics) have **no** row hypothesis: find them purely by label. If not found,
  they are `N/A`.

### 3.3 Required inputs (input IDs)

| Input ID                  | Concept                                                 | Type        |
|---------------------------|---------------------------------------------------------|-------------|
| `pl.revenue`              | Total revenue                                           | flow        |
| `pl.ebitda`               | EBITDA (state reported/adjusted in label)               | flow        |
| `pl.opex.<slug>`          | Each operating expense line present                     | flow        |
| `op.<slug>`               | Each operating metric present (e.g. passengers, ASK, RPK) | flow/stat |
| `cf.cfo`                  | Net cash from operating activities                      | flow        |
| `cf.cfi`                  | Net cash from investing activities                      | flow        |
| `cf.cff`                  | Net cash from financing activities                      | flow        |
| `cf.capex`                | Purchase of PP&E and intangibles (and pre-delivery payments if separately shown — record which lines are included) | flow |
| `cf.lease_principal`      | Repayment of principal portion of lease liabilities     | flow        |
| `cf.fx_effect`            | Effect of exchange rate changes on cash                 | flow        |
| `cf.cash_open` / `cf.cash_close` | Cash at beginning / end of period (CF statement) | stock       |
| `bs.cash`                 | Cash and cash equivalents                               | stock       |
| `bs.st_investments`       | Short-term investments                                  | stock       |
| `bs.borrowings_lt` / `bs.borrowings_st` | Long-/short-term borrowings               | stock       |
| `bs.lease_lt` / `bs.lease_st` | Long-/short-term lease liabilities (IFRS 16)        | stock       |
| `bs.pension`              | Pension / post-employment benefit obligations           | stock       |
| `seg.ebitda.<geo>`        | Geographic EBITDA, only if explicitly disclosed         | flow        |

`<slug>` is the lowercase ASCII snake_case of the matched label (e.g.
`pl.opex.fuel`, `op.passengers_carried`). Slugs must be stable across runs.

---

## 4. Extraction and provenance

Each extracted value is a record:

```python
from dataclasses import dataclass
from decimal import Decimal
from typing import Optional

@dataclass(frozen=True)
class SourceValue:
    input_id: str            # e.g. "cf.cfo"
    period: str              # canonical period key, see §5.1
    value: Optional[Decimal] # None == N/A
    unit: str                # e.g. "RUB mn"
    status: str              # "OK" | "N/A"
    reason: str              # required when status == "N/A"
    workbook_sha256: str
    sheet: str
    cell: str                # e.g. "D50"
    row_label: str           # exact label text as in workbook
    column_header: str       # exact header text as in workbook
    raw: str                 # repr of the raw cell value
    is_formula: bool
    formula: Optional[str]
```

Rules:

- Convert numbers with `Decimal(str(cell.value))`. Parse text numbers only if
  the format is unambiguous (`"1 234,5"` vs `"1,234.5"` — record the rule used).
- Values in parentheses `(123)` are negative. Dashes `-`, `–`, `—` are recorded
  as zero **only** if the workbook uses them as nil in that table (check a
  footnote or consistent usage); otherwise N/A. Empty cells are N/A.
- **Units:** take the unit from the sheet/header caption. If the caption is
  absent, the unit is `"UNKNOWN"` and every KPI using it is flagged. Do not mix
  units in a formula; if `RUB bn` and `RUB mn` must be combined, convert
  explicitly with a logged scale factor (`Decimal(1000)`).
- **Signs:** keep the workbook sign in `value`. Where a formula needs an outflow
  as a positive magnitude, derive it in the formula and document it (see §6).

---

## 5. Periods and cumulative → discrete transformation

### 5.1 Canonical period keys

- Cumulative flows: `3M2025`, `6M2025`, `9M2025`, `12M2025` (= `FY2025`),
  `3M2026`, `6M2026` (= `H1_2026`).
- Discrete quarters: `Q1_2025`, `Q2_2025`, `Q3_2025`, `Q4_2025`, …
- LTM: `LTM_6M2026` etc.
- Stocks (balance sheet): `2025-12-31`, `2026-06-30` (point in time).

Map each workbook column header to exactly one key and store the mapping in
`outputs/source_map.json`. Headers that cannot be mapped unambiguously are
ignored and listed.

### 5.2 Transformation (flows only)

Flow items (P&L, cash flow, flow operating metrics) reported cumulatively are
converted to discrete quarters for **all four quarters**:

```
Q1 = 3M
Q2 = 6M  − 3M
Q3 = 9M  − 6M
Q4 = 12M − 9M
```

- If the workbook already reports discrete quarters, read them directly and
  still run the check below.
- If any cumulative input for a quarter is N/A, that quarter is N/A (and so are
  later quarters that depend on it). Do not back-solve a quarter from the
  others.
- **Never** apply this to stock items (balance-sheet balances, opening/closing
  cash) or to ratios/percentages/averages (margins, load factor, yields): those
  are not additive. Ratios are recomputed per quarter from discrete
  numerators and denominators.

### 5.3 Quarterly sum check

For every flow input and every derived flow KPI with four non-N/A quarters:

```
check.quarter_sum.<input_id>.<YEAR>:  Q1 + Q2 + Q3 + Q4 == FY
```

- With `Decimal` and cumulative source data, the identity is exact by
  construction; test it anyway (it catches column-mapping errors).
- When quarters are read as reported discrete values, allow a rounding
  tolerance of `0.5 × 10^(−d) × 4`, where `d` is the number of decimals shown in
  the source unit (e.g. ±2 for integer `RUB mn`). Record the tolerance used.
- Any failure is a hard error in `kpi.json` (`"status": "FAIL"`) and a failing
  test. If any quarter is N/A the check status is `N/A`, not `PASS`.

---

## 6. KPI definitions

All formulas operate on values in the **same unit and the same period key**.
Each KPI is N/A if any of its inputs is N/A.

### 6.1 Free cash flow — two labelled definitions

| Metric ID stem         | Label                                         | Formula                                                  |
|------------------------|-----------------------------------------------|----------------------------------------------------------|
| `fcf.databook`         | FCF (databook definition: CFO + CFI)          | `cf.cfo + cf.cfi`                                        |
| `fcf.conservative`     | FCF (conservative: CFO − capex − lease principal) | `cf.cfo − capex_outflow − lease_principal_outflow`   |

- `capex_outflow = −cf.capex` when the workbook shows capex as a negative cash
  flow (i.e. the outflow becomes a positive magnitude); `= cf.capex` if the
  workbook presents it as a positive outflow magnitude. Record which convention
  was detected. Same for `lease_principal_outflow`.
- `fcf.conservative` is computed **only where both capex and lease principal
  inputs exist**. If either is missing, it is N/A (do not compute a partial
  version and call it conservative FCF).
- State which capex lines are included (PP&E, intangibles, pre-delivery
  payments, etc.) in the metric's `definition` field.

### 6.2 Cash conversion

```
cash_conversion.cfo_ebitda = cf.cfo / pl.ebitda      (ratio, unit "x"; also report as %)
```

N/A if EBITDA is N/A or zero (zero → reason `"division by zero"`). Computed for
FY, cumulative periods, and discrete quarters from discrete inputs.

### 6.3 Net debt bridge

```
net_debt = borrowings + IFRS16_lease_liabilities − cash − short_term_investments

borrowings               = bs.borrowings_lt + bs.borrowings_st
IFRS16_lease_liabilities = bs.lease_lt + bs.lease_st
cash                     = bs.cash
short_term_investments   = bs.st_investments
```

Export each bridge component as its own metric (`net_debt.borrowings`,
`net_debt.leases`, `net_debt.cash`, `net_debt.st_investments`) and the total
`net_debt.total`, all at the balance-sheet date.

- If `bs.st_investments` is not found, the headline `net_debt.total` is N/A
  (do not assume zero). A variant that explicitly excludes short-term
  investments may be exported only under a distinct ID
  (`net_debt.total_ex_sti`) and label.
- **Pension inclusion policy (explicit):** pension and other post-employment
  obligations are **excluded** from the headline `net_debt.total`. If
  `bs.pension` exists, also export `net_debt.total_incl_pension =
  net_debt.total + bs.pension` with its own ID. If `bs.pension` is not found,
  `net_debt.total_incl_pension` is N/A. The policy is written into the
  `definition` field of both metrics and into `run.policies` in `kpi.json`.

### 6.4 LTM EBITDA and leverage

```
LTM(period P of year Y) = FY(Y−1) + cumulative(P, Y) − cumulative(P, Y−1)
```

Example: `LTM_6M2026 = FY2025 + 6M2026 − 6M2025`.

- If P is the full year, `LTM = FY(Y)`.
- **Never annualise** a partial period (no `H1 × 2`, no `9M × 4/3`). If any of
  the three terms is N/A, LTM is N/A.

```
leverage.net_debt_ltm_ebitda = net_debt.total(at end of P) / ebitda.ltm(P)
```

Unit `"x"`. The balance-sheet date must equal the end of period P. N/A if
either input is N/A, or if LTM EBITDA ≤ 0 (reason
`"non-positive LTM EBITDA; ratio not meaningful"`).

---

## 7. Reconciliations and bridges

### 7.1 Cash reconciliation (when inputs exist)

```
cash_close − cash_open  ==  CFO + CFI + CFF + FX_effect
```

- Use the cash-flow-statement opening/closing balances; if only balance-sheet
  cash exists, use it and note it.
- If the cash flow statement has other explicitly labelled reconciling lines
  (e.g. change in allowance for expected credit losses on cash), include them
  **by label** and list them; never add a plug.
- Tolerance as in §5.3. Report the difference as
  `check.cash_recon.<period>` with `PASS` / `FAIL` / `N/A`. If any input is
  missing, status `N/A` with the missing input IDs.

### 7.2 EBITDA bridge

Explain the change in EBITDA between two periods (e.g. FY2024 → FY2025,
6M2025 → 6M2026) using **only** lines present in the workbook:

```
EBITDA(prior)
 + Δ revenue                     (pl.revenue)
 − Δ each operating expense line (pl.opex.<slug>, sign per workbook)
 = EBITDA(current)
```

- Use only operating expense lines and operating-metric lines that are in the
  Source Map. Do not invent drivers, split lines, or estimate price/volume
  effects from external data.
- A volume/price split of revenue is allowed only if the relevant operating
  metric (e.g. passengers, RPK) and revenue are both present for both periods;
  define the decomposition formula explicitly in the output.
- If the listed lines do not sum to the EBITDA change, show the remainder as an
  explicit `ebitda_bridge.<period>.unreconciled` item (never hide it inside
  another line) and flag it if non-zero beyond tolerance.
- Depreciation, amortisation, impairment and finance items are not EBITDA
  bridge lines.

---

## 8. Validation against checkpoints

Validate the computed KPIs for **FY2025** and **H1 2026** against
`tests/fixtures/checkpoints.json`.

- The file is student-owned and read-only for this skill (§1.7).
- Expected format (if the file differs, adapt the reader, never the file):

```json
{
  "unit_default": "RUB mn",
  "checkpoints": [
    {"metric_id": "pl.ebitda__FY2025", "expected": "123456", "tolerance": "1", "unit": "RUB mn"},
    {"metric_id": "leverage.net_debt_ltm_ebitda__6M2026", "expected": null, "expect_status": "N/A"}
  ]
}
```

- Matching is by `metric_id` only. Comparison uses `Decimal`; tolerance
  defaults to 0 if not given. Units must match exactly or the check fails.
- An expected N/A must match a computed N/A; an expected number never matches a
  computed N/A (and vice versa). N/A is never compared as 0.
- Outcomes per checkpoint: `PASS`, `FAIL`, `MISSING_METRIC` (ID not produced),
  `NOT_RUN` (file absent). Summarise counts in `kpi.json` → `validation`.
- Report every FAIL with expected, actual, difference, and the provenance of the
  inputs. Do not adjust the calculation just to match a checkpoint; investigate
  the Source Map first and explain the cause.

---

## 9. Output: `outputs/kpi.json`

### 9.1 Metric ID grammar (stable)

```
<metric_stem>__<period_key>
```

- `metric_stem`: lowercase dotted path from §3.3 and §6–§7, e.g.
  `pl.revenue`, `pl.ebitda`, `fcf.databook`, `fcf.conservative`,
  `cash_conversion.cfo_ebitda`, `net_debt.total`, `ebitda.ltm`,
  `leverage.net_debt_ltm_ebitda`, `check.quarter_sum.pl.revenue`,
  `check.cash_recon`, `ebitda_bridge.revenue`.
- `period_key`: from §5.1 (`FY2025`, `Q3_2025`, `6M2026`, `LTM_6M2026`,
  `2026-06-30`).
- IDs depend only on concept and period — never on row number, column letter,
  or run order — so they stay stable when the workbook layout shifts.

### 9.2 Schema

```json
{
  "schema_version": "1.0",
  "run": {
    "workbook": "data/databook.xlsx",
    "workbook_sha256": "…",
    "policies": {
      "pension_in_headline_net_debt": false,
      "ltm_method": "FY(Y-1) + cumulative(P,Y) - cumulative(P,Y-1); no annualisation",
      "na_handling": "N/A propagates; never treated as zero",
      "geo_ebitda_2026": "reported only if explicitly disclosed; never inferred"
    }
  },
  "metrics": {
    "fcf.databook__FY2025": {
      "label": "FCF (databook definition: CFO + CFI)",
      "definition": "cf.cfo + cf.cfi",
      "period": "FY2025",
      "value": "45678",
      "unit": "RUB mn",
      "status": "OK",
      "reason": null,
      "inputs": ["cf.cfo__FY2025", "cf.cfi__FY2025"],
      "provenance": [
        {"input_id": "cf.cfo", "sheet": "Cash Flow", "cell": "F50",
         "row_label": "Net cash flows from operating activities",
         "column_header": "12M 2025", "raw": "123456"}
      ]
    },
    "seg.ebitda.international__6M2026": {
      "label": "EBITDA — International (H1 2026)",
      "value": null,
      "unit": "RUB mn",
      "status": "N/A",
      "reason": "not disclosed in workbook; inference prohibited",
      "inputs": [],
      "provenance": []
    }
  },
  "checks": { "check.quarter_sum.pl.revenue__2025": {"status": "PASS", "difference": "0", "tolerance": "0"} },
  "validation": { "source": "tests/fixtures/checkpoints.json", "pass": 0, "fail": 0, "missing_metric": 0, "status": "NOT_RUN" }
}
```

Serialisation rules:

- Numbers are written as **strings** of the `Decimal` value (no float
  round-trip). Ratios keep full precision; any display rounding happens
  elsewhere.
- `json.dump(..., sort_keys=True, indent=2, ensure_ascii=False)` + trailing
  newline. Only `run` may contain environment-dependent fields.
- Raw source values (inputs) are exported too, under their own IDs
  (`cf.cfo__FY2025`, `pl.revenue__Q2_2025`, `bs.cash__2026-06-30`), so tests can
  check them directly.

---

## 10. Tests

Write pytest tests that read `outputs/kpi.json` (and the checkpoints file) and
assert, at minimum:

1. Every metric has `label`, `unit`, `status`, and either a non-null `value`
   with `status == "OK"` or `value is None` with `status == "N/A"` and a
   non-empty `reason`.
2. No metric whose inputs include an N/A has `status == "OK"`.
3. `Q1 + Q2 + Q3 + Q4 == FY` for every flow with four quarters (within the
   recorded tolerance).
4. `ebitda.ltm__6M2026 == pl.ebitda__FY2025 + pl.ebitda__6M2026 −
   pl.ebitda__6M2025` (assert this formula exactly; no annualised half-year is
   ever used).
5. `net_debt.total` equals the sum of its exported bridge components, and
   `net_debt.total_incl_pension − net_debt.total == bs.pension` when both exist.
6. `fcf.databook == cf.cfo + cf.cfi`; `fcf.conservative` is N/A whenever capex
   or lease principal is N/A.
7. Any `seg.ebitda.*__*2026*` metric is either N/A or has provenance pointing to
   a workbook cell with a matching label.
8. Cash reconciliation status is `PASS` or `N/A` (never silently omitted).
9. Checkpoint comparisons for FY2025 and H1 2026 pass; a missing checkpoint file
   yields `NOT_RUN`, not a pass.
10. Running the pipeline twice yields identical `metrics` and `checks`.

---

## 11. Reporting to the user

After a run, report briefly:

- Source Map summary: confirmed / relocated / not found inputs (with old → new
  row for relocations).
- Headline KPIs for FY2025 and H1 2026 with units, plus both FCF definitions
  side by side, clearly labelled.
- All N/A metrics with reasons.
- Check results (quarter sums, cash reconciliation, EBITDA bridge remainder).
- Validation summary against checkpoints, with details of any FAIL.

Never present a number in the report that is not in `outputs/kpi.json`.
