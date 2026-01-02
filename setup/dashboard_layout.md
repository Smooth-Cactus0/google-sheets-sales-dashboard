# Dashboard Layout Guide

This document provides the exact cell-by-cell layout for recreating the Sales Dashboard in Google Sheets.

## Sheet Structure

You'll need 2 sheets:
1. **Data** — Raw sales data (import CSV here)
2. **Dashboard** — The visual dashboard

---

## Dashboard Sheet Layout

### Row Heights & Column Widths

| Column | Width (pixels) |
|--------|---------------|
| A | 30 (spacer) |
| B | 180 |
| C | 120 |
| D | 120 |
| E | 30 (spacer) |
| F | 180 |
| G | 120 |
| H | 120 |
| I | 30 (spacer) |

| Rows | Height |
|------|--------|
| 1 | 15 (spacer) |
| 2 | 40 (title) |
| 3 | 30 (subtitle) |
| 4 | 15 (spacer) |
| 5-6 | 25 (filters) |
| 7 | 15 (spacer) |
| 8-12 | 60 (KPI cards) |
| 13 | 15 (spacer) |
| 14-28 | varies (charts) |

---

## Section 1: Header (Rows 2-3)

| Cell | Content | Format |
|------|---------|--------|
| B2 | `Sales Performance Dashboard` | Bold, 20pt, #2C3E50 |
| B3 | `Q1-Q2 2024 Analysis` | Regular, 11pt, #5D6D7E |

---

## Section 2: Filters (Rows 5-6)

| Cell | Content | Format |
|------|---------|--------|
| B5 | `Region:` | Bold, 10pt, right-align |
| C5 | (Dropdown) | Data validation - see formulas.md |
| D5 | `Category:` | Bold, 10pt, right-align |
| E5:F5 | (Dropdown merged) | Data validation - see formulas.md |
| B6 | `Date From:` | Bold, 10pt, right-align |
| C6 | (Date picker) | Date format |
| D6 | `Date To:` | Bold, 10pt, right-align |
| E6:F6 | (Date picker merged) | Date format |

---

## Section 3: KPI Cards (Rows 8-12)

### Card 1: Total Revenue (B8:C12)
| Cell | Content |
|------|---------|
| B8:C8 | `TOTAL REVENUE` (merged, header) |
| B9:C11 | KPI Value (merged, large number) |
| B12:C12 | `vs prev period: +X%` (merged, small) |

**Formatting:**
- Background: #F8F9F9
- Border: 1px solid #E5E8E8, rounded corners effect (use thick bottom border #7FB3D5)
- Header: 9pt, #5D6D7E, uppercase
- Value: 28pt, Bold, #2C3E50
- Change: 9pt, #27AE60 (green) or #E74C3C (red)

### Card 2: Units Sold (D8:E12)
Same structure, different formula

### Card 3: Profit Margin (F8:G12)
Same structure, percentage format

### Card 4: Avg Order Value (H8:I12)
Same structure, currency format

---

## Section 4: Charts (Rows 14-28)

### Chart 1: Revenue by Region (B14:D22)
- **Type:** Vertical Bar Chart
- **Data Range:** Aggregated from QUERY formula
- **Colors:** #7FB3D5 (all bars, or gradient)
- **Position:** B14:D22 (merged area)

### Chart 2: Category Distribution (F14:I22)
- **Type:** Pie Chart (or Donut)
- **Data Range:** Aggregated from QUERY formula  
- **Colors:** #7FB3D5, #82E0AA, #F9E79F, #F5B7B1
- **Position:** F14:I22 (merged area)

### Chart 3: Monthly Trend (B24:D32)
- **Type:** Line Chart
- **Data Range:** Monthly aggregated revenue
- **Colors:** Line #7FB3D5, Points #2C3E50
- **Position:** B24:D32

### Chart 4: Top Sales Reps (F24:I32)
- **Type:** Horizontal Bar Chart
- **Data Range:** Sales rep performance
- **Colors:** #82E0AA
- **Position:** F24:I32

---

## Section 5: Data Table (Optional, Rows 34+)

A filtered view of the raw data based on dropdown selections.

| Cell | Content |
|------|---------|
| B34 | `Detailed Transactions` (section header) |
| B35:I35 | Column headers from Data sheet |
| B36:I50 | `=QUERY(...)` filtered data |

---

## Background Colors

| Area | Color |
|------|-------|
| Entire Dashboard sheet | #FFFFFF (white) |
| KPI Card backgrounds | #F8F9F9 |
| Section headers | #2C3E50 text on white |
| Filter area | Light blue tint #EBF5FB |

---

## Quick Setup Checklist

- [ ] Create `Data` sheet, import CSV
- [ ] Create `Dashboard` sheet
- [ ] Set column widths and row heights
- [ ] Add title and subtitle
- [ ] Create filter dropdowns with data validation
- [ ] Build KPI card structure (merge cells, format)
- [ ] Add KPI formulas
- [ ] Create aggregation area (hidden columns or separate sheet)
- [ ] Insert and configure charts
- [ ] Apply conditional formatting
- [ ] Final styling and polish
