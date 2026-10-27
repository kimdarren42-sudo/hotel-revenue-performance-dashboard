# DAX and validation notes

## Model overview
- `Hotels`: distinct Hotel_ID values; hotel dimension.
- `Dates`: a continuous 2026 calendar; related to fact check-in dates and monthly target start dates.
- `Bookings`: unique Booking_ID values; fact grain = booking.
- `Targets`: one row per Hotel_ID and Month_Start; monthly target fact.
- Relationships: active, one-to-many, single direction from both dimensions toward both facts. **Verify the specific endpoints in Power BI Desktop** before publication.

## Measures

```dax
Completed Revenue =
CALCULATE(
    SUM(Bookings[Revenue]),
    Bookings[Status] = "Completed"
)

Revenue Target =
SUM(Targets[Revenue_Target])

Revenue Variance $ =
[Completed Revenue] - [Revenue Target]

Revenue Variance % =
DIVIDE([Revenue Variance $], [Revenue Target])
```

### Display formatting
Use currency with 0 decimal places for dollar amounts and percentage with two decimal places for variance %. Custom number format strings for positive/negative/zero values, preserving numeric DAX measures:

```text
+$#,##0;-$#,##0;$0
+0.00%;-0.00%;0.00%
```

## Source reconciliation (Q1 2026)

| Test | Expected result |
|---|---:|
| Bookings rows | 72 |
| Unique Booking_ID values | 72 |
| Completed booking rows | 62 |
| Cancelled booking rows | 10 |
| Hotel rows | 3 |
| Monthly target rows | 9 |
| Completed revenue | $38,888 |
| Target revenue | $31,750 |
| Variance | +$7,138 |
| Variance rate | +22.48% |
| Downtown February completed revenue | $4,145 |
| Downtown February target | $3,700 |
| Airport February completed revenue | $3,860 |
| Airport February target | $3,200 |

Checks used: compare completed-only Bookings revenue to DAX, sum monthly targets independently, filter by Hotel_ID and CheckIn_Date month, verify variance recomputes correctly and month/hotel slicers propagate to both fact tables. No physical merge of the monthly targets into transaction-level Bookings.

## Interpretation guardrails

- Q1 results are based on fictional training data.
- Completion status and check-in month define the revenue KPI, not reservation creation date.
- The target records are keyed to month-start dates; daily revenue-versus-target comparisons would be misleading without explicit target allocation.
- Above-target revenue does not establish improved profitability, occupancy, or the cause of performance differences.
