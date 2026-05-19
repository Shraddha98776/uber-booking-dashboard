# 🚗 Uber Ride Bookings — Power BI Dashboard

> An end-to-end business intelligence dashboard analyzing Uber ride booking data from the NCR (National Capital Region) dataset, built as part of a Data Analyst portfolio project.

---

## 📌 Project Overview

This Power BI project explores ride booking patterns, cancellation behaviour, and revenue trends across a large-scale Uber dataset (~150K records, Jan–Jun 2024). The dashboard is designed to help business stakeholders quickly understand operational performance and identify areas for improvement.

---

## 📊 Dashboard Pages

### 1. Overall Page
A high-level summary of all ride activity across the selected date range.

| Visual | Description |
|--------|-------------|
| Date Range Slicer | Filter all visuals by booking date (Jan 2024 – Jun 2024) |
| Total Booking (KPI Card) | Total number of bookings — 68K |
| Booking Status Breakdown | Pie chart showing Completed, Cancelled by Driver, Cancelled by Customer, No Driver Found, Incomplete |
| Ride Volume Over Time | Area chart showing monthly ride trend (Jan–Jun 2024) |

---

## 🗂️ Dataset Details

| Attribute | Details |
|-----------|---------|
| Source | Uber NCR (National Capital Region) ride dataset |
| Records | ~150,000 rows |
| Date Range | January 2024 – June 2024 |
| Format | CSV / Excel (imported into Power BI) |

### Key Columns Used

- `Booking ID` — Unique ride identifier
- `Date` / `Time` — Ride timestamp
- `Booking Status` — Completed / Cancelled by Driver / Cancelled by Customer / No Driver Found / Incomplete
- `Vehicle Type` — Sedan, SUV, Auto, Bike, etc.
- `Pickup Area` / `Drop Area` — Location information
- `Fare Amount` — Ride fare in INR
- `Trip Distance (km)` — Distance covered
- `Driver Rating` — Customer rating given to driver
- `Payment Method` — Cash / UPI / Card

---

## 🧮 DAX Measures

```dax
-- Total Bookings
Total Booking = COUNTROWS('UberData')

-- Completed Rides
Completed Rides =
    COUNTROWS(FILTER('UberData', 'UberData'[Booking Status] = "Completed"))

-- Completion Rate
Completion Rate =
    DIVIDE([Completed Rides], [Total Booking], 0)

-- Cancellation Rate
Cancellation Rate =
    DIVIDE(
        COUNTROWS(FILTER('UberData',
            'UberData'[Booking Status] IN {"Cancelled by Driver", "Cancelled by Customer"}
        )),
        [Total Booking], 0
    )

-- Total Revenue (Completed rides only)
Total Revenue =
    SUMX(FILTER('UberData', 'UberData'[Booking Status] = "Completed"),
    'UberData'[Fare Amount])

-- Average Fare per Ride
Avg Fare per Ride =
    AVERAGEX(FILTER('UberData', 'UberData'[Booking Status] = "Completed"),
    'UberData'[Fare Amount])

-- Average Driver Rating
Avg Driver Rating = AVERAGE('UberData'[Driver Rating])

-- Month-over-Month Growth %
MoM Growth % =
    VAR CurrentMonth = [Total Booking]
    VAR PrevMonth = CALCULATE([Total Booking], DATEADD('Date'[Date], -1, MONTH))
    RETURN DIVIDE(CurrentMonth - PrevMonth, PrevMonth, 0)
```

---


## 📈 Key Insights

- **62.09%** of all bookings were successfully completed
- **18.07%** were cancelled by drivers — the largest cancellation category
- Ride volume remained consistently above 10K/month from January to May, then dropped sharply in June (partial month data)
- Cancellations by customers (~6.95%) and drivers (~18.07%) together represent ~25% of total bookings — a key area for operational improvement
- Peak demand hours are expected around morning (8–10 AM) and evening (5–8 PM) rush hours
- NCR hotspot pickup areas drive majority of ride volume

---


## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| Power BI Desktop | Dashboard development |
| DAX | Calculated measures and KPIs |
| Power Query (M) | Data cleaning and transformation |
| Excel / CSV | Raw data source |

---

## 📁 Project Structure

```
uber-powerbi-dashboard/
│
├── uber_booking.pbix           # Main Power BI file
├── data/
│   └── uber_ncr_data.csv       # Raw dataset
├── screenshots/
│   └── overall_page.png        # Dashboard screenshot
└── README.md                   # Project documentation
```

---


## ⚠️ Challenges Faced

- **Large dataset handling** — Managing ~150K rows in Power BI required optimizing DAX measures to avoid slow report rendering
- **Date slicer configuration** — Setting up a numeric range slider for dates needed custom formatting in Power Query

---

## 🔮 Future Scope

- **Add more dashboard pages** — Driver Performance page, Revenue Analysis page, Location Heatmap page
- **Geographic map visual** — Plot pickup/drop areas on a Bing Maps visual for spatial insight
- **Predictive analytics** — Integrate Python/R visuals in Power BI to forecast future ride demand
- **Real-time data** — Connect to a live API or streaming dataset for real-time ride monitoring

---
