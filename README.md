# CfD Settlement Trace

How a Contracts for Difference (CfD) generator payment is calculated, tested against real settlement data.

I took Settlement Day 12 April 2026, recalculated three CfD payments from public Elexon and LCCC data, and compared them with the payments LCCC published.

**Live page:** https://nishantrv333.github.io/cfd-settlement-trace/

## What it shows

- **Process flow.** A swimlane of the daily generator payment, from meter to payment.
- **Calculation model.** Three test cases with three negative-price rules to switch between.
- **Findings.** A check across all 73 CfD units, plus a boundary test on 11 April.
- **Impact assessment.** What a change to the negative-price rule would touch, with options.
- **Behind the work.** Worked example, SQL and Python, data catalogue, assumptions log and interface mapping.

## Results

| Test | Unit | Rule that fits | Before loss adjustment | After |
|---|---|---|---|---|
| 1 | Cleve Hill Solar Project (AR4) | Any negative hour | +0.58% | −0.27% |
| 2 | Hornsea Project 2 Phase 1 (AR2) | Six-hour rule | +2.19% | +0.15% |
| 3 | Hornsea Offshore Wind Farm Phase 1 (Investment Contract) | Six-hour rule | +2.71% | −0.08% |

## Files

| File | What it is |
|---|---|
| `index.html` | The page. Self-contained, with the data embedded. |
| `analysis.ipynb` | The SQL check and the Python hourly calculation. |
| `data/` | The public data used, as CSV. |

## Run the notebook

```
pip install duckdb pandas
jupyter notebook analysis.ipynb
```

## Data sources

- LCCC Data Portal: Actual CfD Generation, IMRP actuals, CfD to BM Unit Mapping (Open Government Licence v3.0)
- Elexon Insights API: dataset B1610, settlement run R3 (BMRS data licence)
- EMRS Working Practice WP1, Overview of Settlement, v18.0

Data pulled on 11 November 2026.

## Limits

- The loss adjustment is inferred from published volumes and not yet checked against Elexon's Transmission Loss Multipliers.
- The negative-price rules are taken from public commentary and tested against data. I have not yet confirmed them in the CfD Standard Terms.
- I have not found the contract term that explains why Hornsea One and Walney Extension behave like six-hour-rule contracts.

## Tools

DuckDB SQL and Python (pandas) for the analysis. HTML and JavaScript for the page, built with help from an AI assistant.

Independent work using open data. Not affiliated with Elexon, EMRS or LCCC.
