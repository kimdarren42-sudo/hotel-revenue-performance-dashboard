# Portfolio publication handoff

This package contains the original Power BI Desktop report (`Hotel_Performance_Dashboard.pbix`), the three simulated source CSV files, final screenshots, README, and documented DAX validation.

## Verified before packaging

- `.pbix` is a readable Power BI ZIP-based project package with no internal archive errors.
- Report definition has **DATA VALIDATION** and **EXECUTIVE OVERVIEW** pages.
- Executive page definition includes four Card visuals, line and clustered-bar charts, and two slicers.
- Source CSVs were independently reconciled with the documented Q1 performance figures.
- The reviewed Model View screenshot shows four visually active one-to-many single-direction relationships between the dimensions and two fact tables.

## Relationships verified by project author

The project author inspected **Manage relationships** in Power BI Desktop on October 27, 2026 and confirmed these mappings:
- `Hotels[Hotel_ID]` (1) → `Bookings[Hotel_ID]` (*)
- `Hotels[Hotel_ID]` (1) → `Targets[Hotel_ID]` (*)
- `Dates[Date]` (1) → `Bookings[CheckIn_Date]` (*)
- `Dates[Date]` (1) → `Targets[Month_Start]` (*)

The author confirmed **active**, **single-direction** relationships from the dimensions to facts, with **one-to-many** cardinalities.

## Final opening checks (for publisher or reviewer)

1. Confirm the default Executive Overview view is set to all hotels and all Q1 months, with $38,888 completed revenue, $31,750 target, +$7,138 variance, and +22.48% variance.
2. If reopening on another machine, change the Power Query CSV source paths to the local `data/` folder and refresh; the report may contain the original author's local file paths.
3. Optional: capture a wider resolution dashboard screenshot for GitHub. The current authentic screenshot is sufficient for the README.

## Publishing to GitHub

1. Create a repository such as `hotel-revenue-powerbi-dashboard`.
2. Upload **the contents of this package**, including the `.pbix` file and the `data/` and `screenshots/` folders (preserve relative paths).
3. Check that README screenshots render and `.pbix` downloads correctly.
4. State that this is a **simulated project using fictional data**; do not claim the analysis reflects a live hotel business.
5. Do not upload credentials, nonpublic personal data, or real customer records.

## Suggested repository description

> Power BI hotel revenue dashboard using dimensional modeling, DAX KPIs, slicers, and validated Q1 actual-versus-target reporting (simulated dataset).
