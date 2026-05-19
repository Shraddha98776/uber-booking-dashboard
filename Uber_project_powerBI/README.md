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
        COUNTROWS(
            FILTER(
                'UberData',
                'UberData'[Booking Status]
                    IN {"Cancelled by Driver", "Cancelled by Customer"}
            )
        ),
        [Total Booking],
        0
    )

-- Total Revenue
Total Revenue =
    SUMX(
        FILTER('UberData', 'UberData'[Booking Status] = "Completed"),
        'UberData'[Fare Amount]
    )
```

---

## 📈 Key Insights

- **62.09%** of all bookings were successfully completed
- **18.07%** were cancelled by drivers — the largest cancellation category
- Ride volume remained consistently above 10K/month from January to May
- Customer and driver cancellations together represent ~25% of total bookings
- Peak demand hours were observed during morning and evening rush hours

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| Power BI Desktop | Dashboard development |
| DAX | Calculated measures and KPIs |
| Power Query | Data cleaning and transformation |
| Excel / CSV | Raw data source |

---

## 📁 Project Structure

```text
uber-booking-dashboard/
│
├── uber_booking.pbix
├── Screenshots/
│   ├── overall-dashboard.png
│   └── cancellation-dashboard.png
└── README.md
```

---

## 📸 Dashboard Screenshots

### Overall Dashboard
![Overall Dashboard](Screenshots/overall-dashboard.png)

### Cancellation Dashboard
![Cancellation Dashboard](Screenshots/cancellation-dashboard.png)

---

## ⚠️ Challenges Faced

- Handling large datasets efficiently in Power BI
- Optimizing DAX measures for performance
- Configuring dynamic date slicers and filters

---

## 🔮 Future Scope

- Add Driver Performance Dashboard
- Add Revenue Analysis Page
- Integrate predictive analytics
- Build real-time streaming dashboard

---

## 👩‍💻 Author

**Shraddha Pawar**

GitHub: https://github.com/Shraddha98776