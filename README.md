# Staffing Adequacy and Weekend Conversion Rate in Retail

**Domain:** Retail operations / HR planning  
**Methods:** Exploratory analysis, correlation analysis, z-score anomaly detection, OLS regression  
**Stack:** Python · pandas · numpy · seaborn · matplotlib · scikit-learn.


---

## Business problem

In retail, weekend foot traffic is typically higher than weekdays — but conversion rate (the share of visitors who actually purchase) often drops. The question: is understaffing during weekend afternoons a driver of that gap, and if so, where is the opportunity largest?

## Approach

Using hourly store-level data (entries, conversions, staff on shift, sales) across a 9-month period and 47 stores:

1. **Compute CR gap** — median conversion rate difference (weekend vs weekday) for every store × hour combination, broken down by time slot
2. **Correlate with staffing** — relate staffing coverage (staff per 100 entries) to CR, split by time slot and day type
3. **Score and rank stores** — weight CR gaps by traffic volume to estimate incremental conversion opportunity per store
4. **Validate with OLS** — confirm direction and magnitude of the staffing → CR relationship after controlling for traffic and time slot

## Key findings

- The **15–17 slot is the only one** where 100% of store–hour combinations show a negative CR gap on weekends (mean gap: −6.3pp). Other slots sit around 57–60% negative — consistent with random noise rather than a structural pattern.
- The staffing → CR correlation is **r = 0.49 on weekend afternoons**, vs r ≈ 0.07–0.09 in every other slot and day type. Stores are on average understaffed by ~5.8 staff/100 entries in that slot relative to their weekday levels.
- OLS regression confirms the direction: each additional unit of staffing coverage is associated with **+0.5 extra conversions per hour** (R² = 0.71), after controlling for traffic volume and time slot.
- **Five stores** identified with the largest actionable opportunity — selected on both incremental conversion potential and an aggredible weekday CR baseline. At constant traffic, closing their weekend gap is worth ~**€1M/year in incremental revenue**.

## Repo structure

```
├── data/
│   └── store_hourly_data.csv          # synthetic data matching real structure and distributions
├── outputs/
│   ├── cr_gap_by_slot.png
│   ├── cr_vs_staffing_scatter.png
│   └── store_opportunity_scatter.png
├── staffing_conversion_rate_analysis.ipynb
└── README.md
```

## How to run

```bash
pip install pandas numpy matplotlib seaborn plotly scikit-learn scipy
jupyter notebook staffing_conversion_rate_analysis.ipynb
```

---

## Follow-up

One store implemented a weekend shift redistribution (no additional headcount). The causal impact of that intervention is measured using a Difference-in-Differences approach in the companion repo: [`did-staffing-intervention`](https://github.com/marcomorabito94-mm/did-staffing-intervention).
