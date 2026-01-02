# Chart Configuration Guide

Step-by-step instructions for creating each chart in the dashboard.

---

## Chart 1: Revenue by Region (Vertical Bar Chart)

### Data Setup
First, create the aggregation in a hidden area (e.g., Column L-M):

| L | M |
|---|---|
| Region | Revenue |
| North | =SUMIF(Data!B:B,"North",Data!H:H) |
| South | =SUMIF(Data!B:B,"South",Data!H:H) |
| East | =SUMIF(Data!B:B,"East",Data!H:H) |
| West | =SUMIF(Data!B:B,"West",Data!H:H) |

Or use QUERY (cell L1):
```
=QUERY(Data!A:J, "SELECT B, SUM(H) WHERE B IS NOT NULL GROUP BY B ORDER BY SUM(H) DESC LABEL B 'Region', SUM(H) 'Revenue'", 1)
```

### Chart Creation
1. Select data range (L1:M5)
2. Insert → Chart
3. Chart type: **Column chart**

### Chart Settings
**Setup Tab:**
- Chart type: Column chart
- Stacking: None
- Data range: L1:M5
- X-axis: Region
- Series: Revenue

**Customize Tab:**

*Chart style:*
- Background color: White
- Font: Default

*Chart & axis titles:*
- Chart title: "Revenue by Region"
- Title font: 12pt, Bold, #2C3E50
- Horizontal axis: None (remove)
- Vertical axis: "Revenue ($)"

*Series:*
- Color: #7FB3D5 (Pastel Blue)

*Legend:*
- Position: None

*Horizontal axis:*
- Label font: 10pt, #5D6D7E
- Slant labels: None

*Vertical axis:*
- Label font: 9pt, #5D6D7E
- Number format: Currency (no decimals)
- Gridlines: Light gray #E5E8E8

---

## Chart 2: Category Distribution (Pie Chart)

### Data Setup (Column N-O)
```
=QUERY(Data!A:J, "SELECT C, SUM(H) WHERE C IS NOT NULL GROUP BY C ORDER BY SUM(H) DESC LABEL C 'Category', SUM(H) 'Revenue'", 1)
```

### Chart Creation
1. Select data range (N1:O4)
2. Insert → Chart
3. Chart type: **Pie chart**

### Chart Settings
**Setup Tab:**
- Chart type: Pie chart
- Data range: N1:O4
- Label: Category
- Value: Revenue

**Customize Tab:**

*Chart style:*
- Background: White
- 3D: OFF
- Donut hole: 50% (optional, for donut style)

*Pie chart:*
- Slice label: Percentage
- Label font: 9pt, #2C3E50

*Chart & axis titles:*
- Chart title: "Revenue by Category"
- Title font: 12pt, Bold, #2C3E50

*Pie slice colors (in order):*
1. Electronics: #7FB3D5 (Blue)
2. Home Goods: #82E0AA (Green)
3. Apparel: #F9E79F (Yellow)

*Legend:*
- Position: Right
- Font: 9pt, #5D6D7E

---

## Chart 3: Monthly Revenue Trend (Line Chart)

### Data Setup (Column P-Q)
```
=QUERY(Data!A:J, "SELECT MONTH(A)+1, SUM(H) WHERE A IS NOT NULL GROUP BY MONTH(A)+1 ORDER BY MONTH(A)+1 LABEL MONTH(A)+1 'Month', SUM(H) 'Revenue'", 1)
```

Or manual setup:

| P | Q |
|---|---|
| Month | Revenue |
| Jan | =SUMIFS(Data!H:H, Data!A:A, ">=2024-01-01", Data!A:A, "<=2024-01-31") |
| Feb | =SUMIFS(Data!H:H, Data!A:A, ">=2024-02-01", Data!A:A, "<=2024-02-29") |
| Mar | ... |
| Apr | ... |

### Chart Creation
1. Select data range
2. Insert → Chart
3. Chart type: **Line chart**

### Chart Settings
**Customize Tab:**

*Chart style:*
- Background: White

*Series:*
- Line color: #7FB3D5
- Line thickness: 3px
- Point size: 7
- Point shape: Circle
- Point color: #2C3E50

*Chart & axis titles:*
- Chart title: "Monthly Revenue Trend"
- Title font: 12pt, Bold, #2C3E50
- Vertical axis title: "Revenue ($)"

*Gridlines:*
- Major gridline color: #E5E8E8
- Minor gridlines: OFF

*Legend:*
- Position: None

---

## Chart 4: Top Sales Reps (Horizontal Bar Chart)

### Data Setup (Column R-S)
```
=QUERY(Data!A:J, "SELECT E, SUM(H) WHERE E IS NOT NULL GROUP BY E ORDER BY SUM(H) DESC LABEL E 'Sales Rep', SUM(H) 'Revenue'", 1)
```

### Chart Creation
1. Select data range
2. Insert → Chart
3. Chart type: **Bar chart** (horizontal)

### Chart Settings
**Customize Tab:**

*Series:*
- Color: #82E0AA (Pastel Green)

*Chart & axis titles:*
- Chart title: "Sales Rep Performance"
- Title font: 12pt, Bold, #2C3E50
- Horizontal axis title: "Revenue ($)"

*Horizontal axis:*
- Number format: Currency, no decimals

*Legend:*
- Position: None

---

## General Chart Styling Tips

### Consistent Look
- All titles: 12pt, Bold, #2C3E50
- All axis labels: 9pt, #5D6D7E
- All gridlines: #E5E8E8
- Background: White
- No chart borders

### Pastel Color Palette Reference
| Color Name | Hex Code | Use For |
|------------|----------|---------|
| Pastel Blue | #7FB3D5 | Primary bars, lines |
| Pastel Green | #82E0AA | Secondary, positive |
| Pastel Yellow | #F9E79F | Tertiary, caution |
| Pastel Coral | #F5B7B1 | Accent, negative |
| Pastel Purple | #C39BD3 | Additional category |
| Pastel Teal | #76D7C4 | Additional category |

### Chart Positioning
- Leave 1 row gap between sections
- Align chart edges with cell borders
- Make charts span full width of their section
- Keep consistent heights (8-10 rows per chart)

---

## Troubleshooting

**Chart not updating?**
- Check data range includes new rows
- Use open-ended ranges: `A:B` instead of `A1:B10`

**Colors not matching?**
- Use exact hex codes in custom color picker
- Avoid preset colors

**Text too small when printed?**
- Minimum 9pt for any text
- Test with Print Preview
