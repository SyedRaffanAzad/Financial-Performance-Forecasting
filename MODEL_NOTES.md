# Data dictionary and modeling assumptions

## Raw Data

Each row represents one month and business segment. The four segments are Retail, Wholesale, Online and Other. Amounts are positive whole USD at input. Calculations use full precision and Excel formats display whole dollars.

| Field | Definition |
| --- | --- |
| Month | First calendar day of the reporting month, stored as an Excel date |
| Segment | Business segment associated with the row |
| Revenue | Simulated sales recognized in the month |
| COGS | Simulated direct cost of goods sold |
| Operating expenses | Simulated overhead and sales expenses |
| Budget revenue | Planned revenue for the same month and segment |
| Budget COGS | Planned direct cost for the same month and segment |
| Budget OpEx | Planned operating expenses for the same month and segment |

## Calculation conventions

- Gross profit equals revenue less COGS. Operating profit is gross profit less operating expenses. Net profit is operating profit less modeled tax.
- Tax equals 25% of positive monthly operating profit by default. Loss months have no tax benefit or loss carryforward. The tax rate is editable and applies to actuals, budget and forecast. When filtered, tax is estimated on the selected segment's monthly results, so net profit across individual filters can differ from the consolidated figure.
- Annual profit is the sum of monthly profits. Annual margins are calculated from annual totals. Ratios display zero when the denominator is zero.
- Revenue and net profit variance equal actual less budget. COGS and OpEx variance equal budget less actual. A positive result is favorable for each measure.
- Forecast revenue and OpEx apply the selected growth rates to the corresponding FY2025 month. Forecast COGS applies the prior-year month’s COGS ratio plus the scenario shift, bounded between 0% and 100%, to forecast revenue.
- The simplified income statement excludes interest, other non-operating items, balance sheet movements and cash flow.

## Default scenarios

| Scenario | Revenue growth | COGS rate shift | OpEx growth |
| --- | ---: | ---: | ---: |
| Base | +12% | 0 pp | +6% |
| Upside | +20% | −2 pp | +8% |
| Downside | −10% | +2 pp | +5% |
| Custom | −10% | 0 pp | +5% |


## Model integrity controls

Model Checks evaluates the selected segment and scenario and displays an overall PASS or FAIL. The monthly detail compares raw actuals with the income statement, ties actuals across the reports, recomputes P&L and forecast arithmetic, and checks dashboard chart inputs. The summary checks annual totals, dashboard KPIs and the active scenario's assumptions and results. The tolerances are $0.01 for amounts and 0.000001 for ratios. An error in a checked calculation triggers a FAIL.
