# Bird Strikes Data Analysis (2000-2011)

A Power BI dashboard that analyses 25,000+ wildlife strike reports on US aircraft from 2000 to 2011.
It shows how strikes, damage and cost vary by year, airport, state, phase of flight and weather.
The aim is to show aviation stakeholders where and when bird-strike risk is highest.

## Project Files

| File | Description |
|------|-------------|
| `Bird Strikes_Final.csv` | Strike-level dataset, 25,556 rows x 25 columns (2000-01-02 to 2011-12-31) |
| `Bird_Strike_Dashboard.pbix` | Power BI report with 4 pages: Overview, Cost, Occurance, Effect |
| `Bird_Strike_Dashboard.pdf` | Static 4-page export of the dashboard |

## Dataset

| Column(s) | Description |
|-----------|-------------|
| `Record ID`, `FlightDate` | Unique report ID; date of strike (dd-mm-yyyy) |
| `Airport: Name`, `Origin State` | Airport and US state (`N/A` for non-US airports) |
| `Aircraft: Type`, `Make/Model`, `Number of engines?` | Aircraft details |
| `Aircraft: Airline/Operator`, `Is Aircraft Large?` | Operator and Yes/No size flag |
| `When: Phase of flight` | Approach, Climb, Descent, Landing Roll, Take-off run, Taxi, Parked |
| `Altitude bin`, `Feet above ground` | Altitude band and exact height |
| `Wildlife: Number struck`, `Number Struck Actual` | Count band and exact count |
| `Wildlife: Size`, `Wildlife: Species` | Small/Medium/Large and species (348 values) |
| `Conditions: Precipitation`, `Conditions: Sky` | Weather at the time |
| `Pilot warned of birds or wildlife?` | Y / N |
| `Effect: Impact to flight`, `Effect: Indicated Damage` | Flight impact and damage flag |
| `Cost: Total $`, `Number of people injured` | Cost in dollars; people injured |
| `Remains of wildlife collected?`, `...sent to Smithsonian` | TRUE / FALSE flags |

## Approach

1. **Understand the data**: profile 25 fields; check blanks, duplicates, formats and date range.
2. **Clean and model**: load as table `bird_strikes_db bird_strikes`, transform in Power Query, keep rows with a date and valid engine count.
3. **Measure**: four DAX measures - Number of Bird Strikes, Number of wildlife stuck, Average Altitude, Total Number of People Injured.
4. **Analyse**: trend by year, airline, airport, state; cost by year, state, aircraft size; phase, altitude, weather, warnings, impact.
5. **Report**: four interactive pages with slicers (year, state, airline, engines, size, weather) and page navigation.

## Key Insights

Recomputed from the CSV for the 25,194 rows the dashboard uses.

| Area | Finding |
|------|---------|
| Trend | Strikes rose from 1,349 (2000) to 2,930 (2011), +117.2%. Peak: 3,206 in 2009. |
| Season | July-October holds 52.9% of strikes; August is highest (3,684). |
| Flight phase | Approach 10,305 (40.9%); Approach + Landing Roll = 60.7%. |
| Altitude | 80.8% (20,347) at or below 1,000 ft. Median height 50 ft; average 803.26 ft. |
| Hotspots | Dallas/Fort Worth 802 and Sacramento 676 airports; California 2,486 and Texas 2,404 states. |
| Airlines | Southwest 4,628 (18.4%), American 2,058, Delta 1,349. |
| Cost | $140.15M total. California is highest ($22.64M); large aircraft are 34.9% ($48.88M). |
| Damage | 2,430 strikes (9.7%) caused damage: 15.4% above 1,000 ft vs 8.3% below; 44.4% for large wildlife vs 3.5% for small. |
| Impact | 2,016 strikes (8.0%) affected the flight; 1,076 were precautionary landings. |
| Warnings | Pilots were warned in 42.5% of strikes; impact rate is the same either way (8.0%). |
| People | 21 injured in total; November has the most (6). 61.5% of strikes involve unidentified birds. |

## Tech Stack

- **Power BI Desktop**: model, report pages, slicers, filled map, treemap, combo, donut and scatter charts
- **DAX**: measures for counts, average altitude and injuries
- **Power Query** and **MySQL**: transformation and original data source (per the original README)
- **CSV**: exported dataset

## How to Use

1. Clone or download this repository.
2. Open `Bird_Strike_Dashboard.pbix` in Power BI Desktop (Windows); use the page buttons and slicers.
3. No Power BI? Read `Bird_Strike_Dashboard.pdf` instead.
4. To reuse the data, load the CSV; parse `FlightDate` as dd-mm-yyyy and strip commas from `Cost: Total $`.
