# World-Population-Dashboard
- An interactive Power BI dashboard built using  World Bank open data, visualizing global  population trends from 1960 to 2024

## 📌 Visuals Included
- 🗺️ **Map** — Population size by country as bubbles
- 📊 **Bar Chart** — Top 10 most populous countries
- 📈 **Line Chart** — Population growth trends over time
- 📅 **Year Slicer** — Filter all visuals by year (1960–2024)

---

## 💡 Key Insights
- China and India are the world's most populous countries
- India overtook China in population around 2023
- Global population has grown significantly since 1966

---

## 🛠️ Tools Used
- Microsoft Power BI Desktop (Free)
- Power Query (built into Power BI)

---

## 📂 Data Source
- [World Bank Open Data](https://data.worldbank.org/indicator/SP.POP.TOTL)
- Indicator: SP.POP.TOTL (Total Population)
- Coverage: 200+ countries, 1960–2024
- Format: CSV

---

## 🚀 Step by Step — How I Built This

### Step 1 — Download the Data
1. Go to World Bank Open Data
2. Search for SP.POP.TOTL
3. Download as CSV

### Step 2 — Load into Power BI
1. Open Power BI Desktop
2. Click Home → Get Data → Text/CSV
3. Select your downloaded CSV file
4. Click Transform Data to open Power Query

### Step 3 — Clean the Data in Power Query
The World Bank CSV has metadata rows at top
that need to be removed first:

1. Click Home → Remove Top Rows → enter 4
2. Click Home → Use First Row as Headers
3. You should now see proper column names

### Step 4 — Unpivot Year Columns
The years (1960–2024) are spread across 
columns. We need to unpivot them:

1. Select all year columns (1960 to 2024)
   - Click 1960 column
   - Hold Shift
   - Click last year column
2. Right click → Unpivot Columns
3. Rename columns:
   - Attribute → Year
   - Value → Population

### Step 5 — Fix Data Types
1. Click Year column → Data Type → Whole Number
2. Click Population column → Data Type → Whole Number

### Step 6 — Remove Regional Groupings
World Bank data includes regional aggregates
(not real countries). Remove them using a
Custom Column:

1. Click Add Column → Custom Column
2. Name it IsCountry
3. Enter this formula:
Text.Length([Country Code]) = 3
and not List.Contains({
"WLD","IBT","LMY","MIC","IBD","EAR",
"UMC","LMC","LTE","EAS","EAP","TEA",
"HIC","OED","SAS","TSA","IDA","PST",
"CSS","OSS","LDC","PRE","SSA","SSF",
"NAC","LAC","MEA","MNA","ECA","ECS",
"INX","AFR","AFE","AFW","IDX","TSS",
"FCS","LCN","TLA","HPC","EUU","TEC",
"EMU","ARB","CEB","SST","NOC","OEC",
"ANR","TMN","IDB","LIC"
}, [Country Code])

5. Filter IsCountry column → keep only TRUE
6. Delete IsCountry column
7. Click Close & Apply

### Step 7 — Build the Map Visual
1. Click blank canvas area
2. Select Map visual from Visualizations pane
3. Drag Country Name → Location
4. Drag Population → Bubble Size

### Step 8 — Build the Bar Chart (Top 10)
1. Click blank canvas area
2. Select Clustered Bar Chart
3. Drag Country Name → Y-axis
4. Drag Population → X-axis
5. In Filters pane → Filters on this visual
6. Drag Country Name → set Filter Type to Top N
7. Set Top 10 by Sum of Population
8. Click Apply Filter

### Step 9 — Add Year Slicer
1. Click blank canvas area
2. Select Slicer visual
3. Drag Year → Field
4. Format → Slicer Settings → Style → Between
   (gives a nice range slider)

### Step 10 — Build the Line Chart
1. Click blank canvas area
2. Select Line Chart visual
3. Drag Year → X-axis
4. Drag Population → Y-axis
5. Drag Country Name → Legend
6. Filter to show only:
   - China
   - India
   - United States
   - Indonesia
   - Brazil

### Step 11 — Final Polish
1. Add title: Insert → Text Box
   → Type World Population Dashboard
2. Resize and arrange all visuals neatly
3. Press Ctrl + S to save

---

## ⚠️ Common Issues & Fixes

| Problem | Fix |
|---|---|
| Bar chart shows regions not countries | Add IsCountry custom column filter |
| Years showing as decimals | Change Year data type to Whole Number |
| Map not showing bubbles | Make sure Country Name is in Location field |
| Too many lines in line chart | Filter Country Name to 5 countries only |

---

## 📥 How to View This Dashboard
1. Download Power BI Desktop for free from
   https://powerbi.microsoft.com/desktop
2. Download `World Population Dashboard.pbix`
   from this repository
3. Open the .pbix file in Power BI Desktop
4. Explore the interactive dashboard!

---

## 🎓 What I Learned
- Importing and cleaning real world data
- Using Power Query for data transformation
- Unpivoting columns for better data structure
- Building interactive visuals in Power BI
- Filtering and removing unwanted data
- Creating a complete dashboard from scratch

---

## 👤 Author
- GitHub: [@gowri8akula](https://github.com/gowri8akula)

---

## 📄 License
This project is open source and available
under the MIT License
