# ❄️ Snowy Analytics: Global Ski Resorts Dashboard

An interactive **Power BI** dashboard that analyzes ski resorts around the world by location, terrain difficulty, lifts, elevation, and amenities.

---

## Project Overview

**Snowy Analytics** turns raw ski resort data into a single-page interactive dashboard. It answers questions like:

- Which countries have the most ski resorts?
- Which resorts are best for beginners and which for experts?
- How big is each resort in terms of slopes, lifts, and elevation?
- Which resorts offer night skiing, summer skiing, or child-friendly facilities?

---

## Business Problem

Ski resorts differ a lot in size, difficulty, infrastructure, and amenities, and this information is scattered across many places. This causes problems for:

- **Travelers:** hard to compare resorts and choose by skill level and group type.
- **Travel agencies:** no quick way to decide which resorts to promote for families, beginners, or experts.
- **Resort operators and investors:** no easy benchmark against competitors.
- **Marketing teams:** hard to find market gaps and unique selling points.

Without one consolidated view, decisions depend on guesswork and slow manual research.

---

## Dashboard Goal

Give users **one interactive view** of the global ski resort market so they can:

1. See a quick market snapshot (resorts, countries, continents).
2. Compare resorts by slopes, lifts, and elevation.
3. Find resorts by amenity (child-friendly, night skiing, summer skiing).
4. Filter everything by continent.
5. Make faster, data-driven decisions.

---

## Data Source

- **Provider:** Maven Analytics, Data Playground
- **Dataset:** Ski Resorts
- **Link:** https://mavenanalytics.io/data-playground/ski-resorts

| Table | Description | Key Fields |
|-------|-------------|------------|
| `resorts` | One row per resort (25 columns) | Resort, Country, Continent, Price, Season, Highest/Lowest point, Beginner/Intermediate/Difficult/Total slopes, Lifts, Child friendly, Snowparks, Nightskiing, Summer skiing |
| `snow` | Monthly snow data | Month, Latitude, Longitude, Snow |

---

## Project Workflow

1. **Collect data:** download `resorts.csv` and `snow.csv` from Maven Analytics.
2. **Import and clean:** load the CSVs in Power Query, promote headers, and set correct data types.
3. **Build the data model:** create the `DimDate` table and connect `snow[Month]` to `DimDate[Date]`.
4. **Write DAX measures:** create KPI measures in a separate `_Measure` table.
5. **Design the dashboard:** add KPI cards, charts, and a continent slicer, with a themed background.
6. **Extract insights:** use the visuals to answer the business questions.

---

## Data Model

| Table | Purpose |
|-------|---------|
| `resorts` | Resort characteristics |
| `snow` | Monthly snow records |
| `DimDate` | Calculated date table (Year, Month Number, Month Name) |
| `_Measure` | Stores all DAX measures |

**Relationship:** `snow[Month]` → `DimDate[Date]`

---

## Key DAX Measures

```DAX
Total Resorts          = DISTINCTCOUNT(Resorts[ID])
Total Countries        = DISTINCTCOUNT(Resorts[Country])
Total Continents       = DISTINCTCOUNT(Resorts[Continent])
Child Friendly Resorts = CALCULATE(DISTINCTCOUNT(Resorts[ID]), Resorts[Child friendly] = "Yes")
Night Skiing Resorts   = CALCULATE(DISTINCTCOUNT(Resorts[ID]), Resorts[Nightskiing] = "Yes")
Summer Skiing Resorts  = CALCULATE(DISTINCTCOUNT(Resorts[ID]), Resorts[Summer skiing] = "Yes")
```

---

## Dashboard Features

**KPI cards:** Total Resorts, Total Countries, Total Continents, Child Friendly, Night Skiing, Summer Skiing

| Visual | Type | Purpose |
|--------|------|---------|
| Top 10 Countries with most Ski Resorts | Column chart | Market concentration |
| Resorts for Beginners | Line chart | Beginner slopes per resort |
| Resorts for Experts | Line chart | Difficult slopes per resort |
| Slopes by Resort | Line chart | Beginner, intermediate, difficult, and total slopes |
| Highest and Lowest point by Resort | Column chart | Elevation range |
| Lifts by Resort | Column chart | Surface, chair, gondola, and total lifts |

**Slicer:** Continent filter that updates the whole dashboard.

---

## Business Insights

- **Market concentration:** a few countries hold most of the resorts, which shows where supply and competition are highest.
- **Skill-level fit:** the beginner and expert charts show which resorts suit learners and which suit advanced skiers.
- **Resort scale:** slopes and lifts show which resorts have the biggest terrain and best access.
- **Elevation:** a high peak and large vertical drop usually mean more varied terrain and a longer season.
- **Amenity gaps:** night skiing, summer skiing, and child-friendly facilities are available at only some resorts, so they act as differentiators.
- **Regional view:** the continent slicer shows how the offering changes by region.

---

## Business Impact

| Stakeholder | Impact |
|-------------|--------|
| Travelers | Less research time and a resort that matches their skill and group |
| Travel agencies | Targeted packages (family, beginner, expert, night-ski, summer-ski) |
| Resort operators | Benchmark against competitors and find where to invest |
| Investors | Spot underserved regions and amenity gaps |
| Marketing teams | Focus messaging on real differentiators |

**Overall value:** one reusable view replaces scattered manual comparison, so decisions are faster and based on data.

---

## Tools Used

- Power BI Desktop
- Power Query (M)
- DAX
- Data Modeling

---

## How to Run This Project

1. Download the dataset from https://mavenanalytics.io/data-playground/ski-resorts
2. Open `SNOWY_ANALYTICS.pbit` in Power BI Desktop.
3. Point the data sources to your local `resorts.csv` and `snow.csv` (Transform data → Data source settings).
4. Click **Load** and explore the dashboard.

```
├── SNOWY_ANALYTICS.pbit
├── README.md
└── images/Snowy Analytics.png
```

---

## Dashboard Preview

![Snowy Analytics Dashboard](images/Snowy%20Analytics.png)

---

## Author

**Ansh Sharma**

- GitHub: [anshanalytics](https://github.com/anshanalytics)
- LinkedIn: [Ansh Sharma](https://www.linkedin.com/in/ansh-sharma-02445b360)
