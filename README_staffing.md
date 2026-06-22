# Staffing Adequacy and Weekend Conversion Rate in Retail

**Domain:** Retail operations / HR planning  
**Methods:** Exploratory analysis, correlation analysis, z-score anomaly detection, OLS regression  
**Stack:** Python · pandas · numpy · seaborn · matplotlib · plotly · scikit-learn

---

## Business problem

In retail, weekend foot traffic is typically higher than weekdays — but conversion rate (the share of visitors who actually purchase) often drops. The question: is understaffing during weekend afternoons a driver of that gap, and if so, where is the opportunity largest?

## Approach

Using hourly store-level data (entries, conversions, staff on shift, sales) across a 9-month period and 47 stores:

1. **Compute CR gap** — median conversion rate difference (weekend vs weekday) for every store × hour combination
2. **Correlate with staffing** — relate staffing coverage (staff per 100 entries) to CR, split by time slot and day type
3. **Score and rank stores** — weight CR gaps by traffic volume to estimate incremental conversion opportunity
4. **Validate with OLS** — confirm direction and significance of the staffing → CR relationship

## Key findings

- All store × hour combinations in the **15–17 slot show a negative CR gap on weekends** — consistent across the entire store network
- The staffing → CR correlation is **strongest in that slot on weekends**, suggesting this is where reallocating staff has the highest return
- **Five stores** identified with the largest opportunity; at constant traffic, closing their CR gap is worth ~**€1M/year in incremental revenue**

## Repo structure

```
├── data/
│   └── store_hourly_data.csv       # synthetic data matching real structure
├── outputs/
│   ├── cr_gap_by_slot.png
│   ├── cr_vs_staffing_scatter.png
│   └── top_stores_opportunity.png
├── staffing_conversion_rate_analysis.ipynb
└── README.md
```

## How to run

```bash
pip install pandas numpy matplotlib seaborn plotly scikit-learn
jupyter notebook staffing_conversion_rate_analysis.ipynb
```

---

## Follow-up

One store implemented a shift redistribution on weekends (no new headcount). The causal impact is measured using a Difference-in-Differences approach in the companion repo: [`did-staffing-intervention`](../did-staffing-intervention).
