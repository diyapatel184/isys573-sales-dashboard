# Onboarding Guide — ISYS 573 Sales Dashboard

Welcome to the ISYS 573 Retail Sales Dashboard project. This guide
will get you up and running in under 10 minutes.

## What the Dataset Represents

`data/sales.csv` contains 500 fictional retail transactions from
calendar year 2024, spanning 4 regions (West, East, South, Midwest),
6 product categories, and multiple sales channels (Online, In-Store,
Partner). Each row represents one transaction by one sales rep. The
data is synthetic but realistic — it is used exclusively for
educational purposes in ISYS 573 at SFSU.

**Do not modify `data/sales.csv`** — it is the read-only source of
truth for all charts and KPIs. See `docs/data_dictionary.md` for a
full column reference.

## Running the Dashboard

1. Install dependencies:
pip install -r requirements.txt
2. Generate the dashboard:
python dashboard.py
3. Open the output file in your browser:
open dashboard.html        # macOS
start dashboard.html       # Windows

The dashboard generates a single self-contained HTML file — no web
server required. The **quarter filter dropdown** at the top filters
all charts and KPI cards simultaneously using embedded Plotly JSON
data. Selecting Q1, Q2, Q3, Q4, or Full Year re-renders every chart
client-side with no server round-trip.

## How to Add a New Chart

1. Write a new function in `dashboard.py` following this pattern:
```python
   def build_my_chart(df: pd.DataFrame) -> go.Figure:
       """One-line description of the chart."""
       # transform df, build fig, return fig
       return fig
```
2. Add the chart JSON to `chart_data[q]` inside the
   `for q in quarters` loop in `build_html()`:
```python
   "my_chart": build_my_chart(subset).to_json(),
```
3. Add a placeholder for empty quarters in the same loop.
4. Add a `<div id="chartMyChart">` inside `.charts-grid` in the
   HTML template string.
5. Add a `Plotly.react("chartMyChart", ...)` call inside
   `applyFilter()` in the JavaScript section.
6. Run `pytest tests/ -v` to confirm existing tests still pass.
7. Add at least one pytest test for your new function.

## Running the Test Suite
pytest tests/ -v

Tests live in `tests/test_dashboard.py`. The test suite covers:

- **Data loading** — verifies required columns exist and date
  parsing works correctly
- **Chart functions** — verifies each build_* function returns a
  valid Plotly Figure object with the expected traces
- **KPI calculations** — verifies revenue totals and region
  aggregations are correct
- **Leaderboard function** — verifies build_rep_leaderboard()
  returns correct sales rep rankings sorted descending

All tests must pass before opening a pull request. If you add a new
chart function, add a corresponding test class in
`tests/test_dashboard.py` following the existing patterns.

## Key Contacts

- **Course:** ISYS 573 — Generative AI and LLMs for Business, SFSU
- **Repo:** github.com/diyapatel184/isys573-sales-dashboard
- **Agent:** Claude (Anthropic) — generated this documentation
  in response to Issue #2
