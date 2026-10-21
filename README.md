# Hospital Executive Dashboard

A single-file, interactive dashboard that turns a Healthcare Data Analytics notebook into something a hospital leadership team can read in a couple of minutes. Open the HTML file in any browser and you're done. There is nothing to install, no server and no internet connection needed.

**Deliverable:** `healthcare_executive_dashboard.html`
**Source:** `Notebook.ipynb` (the completed analytics project)
**Reporting period:** May 2019 – May 2024 (61 months)

---

## Why this exists

The notebook holds the analysis, but it's written for analysts. Management doesn't want to scroll through loading, cleaning and code cells. They want to know what is happening, why it matters and what to keep an eye on.

So the dashboard uses the notebook only as its source of numbers and findings. It does not reproduce the notebook. There is no code, no methodology and no walkthrough in it.

---

## What's on the dashboard

### 1. Header
Title, reporting period and a few quick chips: 54,966 admissions, 6 conditions, 5 insurance providers.

### 2. KPI cards
| KPI | Value |
|---|---|
| Patient admissions | 54,966 |
| Total billing | ≈ $1.41B (average billing × admissions, so an approximation) |
| Average billing per admission | $25,595 (median $25,544) |
| Average patient age | 51.5 years (range 13–89) |
| Largest insurance provider | Cigna, 11,139 admissions (20.3%) |
| Selected segment | Updates when you click a condition or provider |

### 3. Executive summary
Six short insights for management, written in plain language.

### 4. Key business insights
Built from the notebook's five business questions, each with a chart, a short finding and what it means for the business.

- **Conditions:** admissions are almost perfectly balanced. Arthritis leads with 9,218 and Asthma is lowest with 9,095, a gap of only about 1.3%. No single condition dominates demand.
- **Insurance mix:** Cigna (11,139), Medicare (11,039), UnitedHealthcare (11,014), Blue Cross (10,952) and Aetna (10,822). No provider is dominant, so payer concentration risk is low.
- **Patient age:** mean 51.5, median 52, middle half of patients between 35 and 68. The population is broad rather than concentrated in one age band.
- **Senior (60+) cost:** $25,563.59 average billing, essentially the same as the overall average (about −0.1%). Seniors are not costing more per admission in this data.
- **Billing over time:** monthly average billing stays in a narrow band of roughly $24.9K–$26.3K. The chart shows the first and last five months of the period against the overall average.

### 5. Ad-hoc insights
The notebook contains one ad-hoc analysis, **Emergency Department capacity planning (emergency admissions per month)**. The code is there but it was never run, so there is no output. The dashboard shows this section as **"Result pending"** and does not invent figures.

### 6. Management takeaways
Four cards, each with **What's happening / Why it matters / What to watch**.

---

## Interactivity

- **Click to focus** on any condition or insurance provider. The selected-segment KPI updates to match.
- **Hover tooltips** on every chart element.
- **Patients / % share toggle** on the conditions chart.
- **Reset selection** button to clear the focus.
- **Responsive layout** that works on desktop, tablet and phone.

---

## What it doesn't do, and why

I'd rather be upfront about the gaps than have anyone find them in a meeting.

| You might expect | What actually happens | Reason |
|---|---|---|
| Department filter | Not included | The notebook has no Department column |
| Gender and year filters | Not included | The raw CSV wasn't available, only notebook outputs. Filtering needs row-level data |
| KPIs that recalculate on every filter | Only the selected-segment KPI changes | Same reason: no row-level data |
| Three ad-hoc analyses | One, shown as pending | The notebook only contains one, and it has no output |
| Full 61-month trend | First and last five months only | Those are the only months visible in the notebook output |
| Exact total billing | ≈ $1.41B | Calculated as average × admissions |

---

## Data notes

- Raw data had **55,500 rows**. After removing **534 duplicates**, **54,966** remain, and every figure on the dashboard uses the cleaned set.
- Negative billing amounts were treated as errors and replaced with the mean billing amount.
- Every number comes from the notebook's outputs. Nothing was estimated or invented, with the one exception of the total-billing approximation above.

---

## Tech notes

- Plain HTML, CSS and vanilla JavaScript in one file. There are no external libraries, CDNs or fonts, so it works offline.
- Charts are hand-built inline SVG.
- Data lives in a handful of constants near the bottom of the script (`COND`, `INS`, `AVG`, `SENIOR`, `FIRST`, `LAST`, `AGE`), so updating a number is a one-line change.
- Each chart is drawn by its own render function (`renderCond`, `renderIns`, `renderAge`, `renderCmp`, `renderTrend`), and `renderAll` redraws everything.

---

## How to open it

https://rahulbitmesramnc.github.io/Healthcare-data-Analytics-Project/
---

## Making it complete

Add `healthcare_dataset.csv` (the original data file) and the dashboard can be extended to include:

1. Gender and year filters, plus any other column that exists in the data
2. KPIs that recalculate with every filter
3. The full 61-month billing trend
4. The emergency admissions analysis, with real numbers
5. A medical-condition × insurance cross view

The numbers on this version would be recomputed from the raw rows and checked against the notebook's results.
