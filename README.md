# Nairobi Healthcare Access Inequality Analysis

## Problem Statement
Which Nairobi constituencies are most underserved in healthcare access
when adjusting for population density and facility level? This analysis
builds a Healthcare Access Inequality Index (HAII) across all 17 Nairobi
constituencies using 2019 population data and 2017 Ministry of Health
facility data.

## Data Sources
| Dataset | Source | Year | Notes |
|---|---|---|---|
| Health facility register | Kenya Master Health Facility List (KMHFL) via HDX | 2017 | 782 operational facilities after cleaning |
| Administrative boundaries | HDX Kenya COD-AB Level 2 | 2026 | 17 constituency polygons |
| Population data | KNBS 2019 Census — reconstructed constituency layer | 2019 | 5 constituencies direct KNBS; 12 reconstructed from mixed sources |

## Methodology
### Access metric
Facilities per 10,000 people per constituency, weighted by KEPH facility
level (Level 2 = 1, Level 3 = 2, Level 4 = 3, Level 5 = 4, Level 6 = 5).

### Inequality index (HAII)
HAII = Population Pressure / Weighted Access Score per 10,000 people

Normalised to 0–100 scale. Higher score = worse access.

### Data limitation
The public 2019 KNBS release does not publish a clean 17-constituency
population table. The constituency population layer in this analysis is
a reconstruction anchored to the KNBS county total of 4,397,073.
Variance: +4,485 (0.1%). All rows carry explicit source and confidence
labels. Conclusions are reported with sensitivity to confidence levels.

## Key Findings
- **Mathare ranks 1st (HAII 100, high confidence)** — 0.73 facilities
  per 10,000 people against a Nairobi average of 1.96. Population
  density of 68,855 persons per km². Validated by peer-reviewed
  academic research and NGO field reports.
- **71.2% of Nairobi's population** lives in constituencies below
  2 facilities per 10,000 people.
- **75.7% of all Level 4+ hospitals** are concentrated in 5
  constituencies, leaving 6 constituencies with zero hospital-level
  care including Kasarani (780,656 residents).
- **Starehe paradox** — 136 facilities but ranks 12th. Raw facility
  count does not equal access equity when population density is
  accounted for.
- **Kasarani anomaly** — lowest facility density in Nairobi (0.61 per
  10,000) but ranks 8th on HAII due to large geographic area deflating
  population pressure score.

## Policy Recommendations
1. **Mathare** — minimum 2 new Level 3 health centres as immediate
   priority
2. **Kasarani** — 1 new Level 4 county hospital to serve 780,656
   residents currently without hospital-level access
3. **Embakasi cluster** — shared Level 4 facility serving Embakasi
   West, South, and North collectively
4. **Moratorium** on new hospital construction in already well-served
   constituencies until all 6 zero-hospital constituencies are covered
5. **KNBS** to publish clean constituency-level population table from
   2019 census to enable reproducible evidence-based planning

## Visualisations
- `visuals/02_haii_choropleth_binned.html` — interactive HAII map
- `visuals/03_facility_distribution.html` — facility count map
- `visuals/04_haii_ranking_chart.png` — ranked bar chart with
  confidence tiers
- `visuals/05_density_scatter.png` — population density vs facility
  density scatter

## Project Structure
healthcare-access-kenya/
├── data/
│   ├── raw/                  # original unmodified source files
│   └── processed/            # cleaned and merged outputs
├── notebooks/
│   ├── 01_exploration.ipynb  # data loading, cleaning, HAII calculation
│   ├── 02_visualisation.ipynb# maps and charts
│   └── 03_insights.ipynb     # findings and recommendations
├── visuals/                  # all output maps and charts
├── src/                      # utility functions (future)
├── README.md
└── requirements.txt

## Limitations
- Facility data from 2017 — some facilities may have opened or closed
- Population data for 12 of 17 constituencies is reconstructed, not
  official KNBS constituency tables
- HAII does not measure facility quality, staffing, or utilisation
- Private facilities included in counts but affordability not measured

## Reproducibility
```bash
git clone <repo>
cd healthcare-access-kenya
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```
Run notebooks in order: 01 → 02 → 03

## External Validation
Findings are consistent with:
- PMC spatial epidemiology study on TB diagnostic delays in Nairobi (2025)
- USAID SHOPS report documenting MMR of 706/100,000 in Ruaraka
  informal settlements
- Nairobi City County Annual Development Plan 2019/2020
- Baraka HealthNet and SHOFCO field operations in Mathare Valley