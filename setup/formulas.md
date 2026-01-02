# Google Sheets Formulas Reference

All formulas needed for the Sales Performance Dashboard.

---

## Filter Dropdowns (Data Validation)

### Region Dropdown (Cell C5)
**Data Validation Settings:**
- Criteria: List from a range
- Range: `=UNIQUE(Data!B2:B)`

Or use manual list: `All, North, South, East, West`

### Category Dropdown (Cell F5)
**Data Validation Settings:**
- Criteria: List from a range  
- Range: `=UNIQUE(Data!C2:C)`

Or use manual list: `All, Electronics, Home Goods, Apparel`

---

## KPI Card Formulas

### Total Revenue (Cell B10)
```
=IF(C5="All",
  IF(F5="All",
    SUM(Data!H2:H),
    SUMIF(Data!C2:C, F5, Data!H2:H)
  ),
  IF(F5="All",
    SUMIF(Data!B2:B, C5, Data!H2:H),
    SUMIFS(Data!H2:H, Data!B2:B, C5, Data!C2:C, F5)
  )
)
```

**Simplified version (if filters in C5 and F5):**
```
=SUMIFS(Data!H:H, 
  Data!B:B, IF(C5="All","*",C5), 
  Data!C:C, IF(F5="All","*",F5))
```

**Display format:** Currency, no decimals, with `$` and `K` or `M` suffix
```
=TEXT(B10/1000,"$#,##0")&"K"
```

---

### Units Sold (Cell D10)
```
=SUMIFS(Data!F:F, 
  Data!B:B, IF(C5="All","*",C5), 
  Data!C:C, IF(F5="All","*",F5))
```

**Display format:** Number with comma separator
```
=TEXT(D10,"#,##0")
```

---

### Profit Margin (Cell F10)
```
=SUMIFS(Data!H:H, Data!B:B, IF(C5="All","*",C5), Data!C:C, IF(F5="All","*",F5)) 
 - SUMIFS(Data!I:I, Data!B:B, IF(C5="All","*",C5), Data!C:C, IF(F5="All","*",F5))
```

Then divide by revenue for percentage:
```
=(Revenue - Cost) / Revenue
```

**Complete formula:**
```
=IFERROR(
  (SUMIFS(Data!H:H,Data!B:B,IF(C5="All","*",C5),Data!C:C,IF(F5="All","*",F5))
   -SUMIFS(Data!I:I,Data!B:B,IF(C5="All","*",C5),Data!C:C,IF(F5="All","*",F5)))
  /SUMIFS(Data!H:H,Data!B:B,IF(C5="All","*",C5),Data!C:C,IF(F5="All","*",F5)),
  0)
```

**Display format:** Percentage with 1 decimal: `40.2%`

---

### Average Order Value (Cell H10)
```
=IFERROR(
  SUMIFS(Data!H:H,Data!B:B,IF(C5="All","*",C5),Data!C:C,IF(F5="All","*",F5))
  /COUNTIFS(Data!B:B,IF(C5="All","*",C5),Data!C:C,IF(F5="All","*",F5)),
  0)
```

**Display format:** Currency with 2 decimals: `$128.50`

---

## Chart Data Aggregations

Create a hidden section (columns L-P) or a separate `Calcs` sheet for chart data.

### Revenue by Region (for Bar Chart)
```
=QUERY(Data!A:J, 
  "SELECT B, SUM(H) 
   WHERE B IS NOT NULL 
   GROUP BY B 
   ORDER BY SUM(H) DESC 
   LABEL B 'Region', SUM(H) 'Revenue'", 1)
```

### Revenue by Category (for Pie Chart)
```
=QUERY(Data!A:J, 
  "SELECT C, SUM(H) 
   WHERE C IS NOT NULL 
   GROUP BY C 
   ORDER BY SUM(H) DESC 
   LABEL C 'Category', SUM(H) 'Revenue'", 1)
```

### Monthly Revenue (for Line Chart)
```
=QUERY(Data!A:J, 
  "SELECT MONTH(A)+1, SUM(H) 
   WHERE A IS NOT NULL 
   GROUP BY MONTH(A)+1 
   ORDER BY MONTH(A)+1 
   LABEL MONTH(A)+1 'Month', SUM(H) 'Revenue'", 1)
```

### Sales Rep Performance (for Horizontal Bar)
```
=QUERY(Data!A:J, 
  "SELECT E, SUM(H) 
   WHERE E IS NOT NULL 
   GROUP BY E 
   ORDER BY SUM(H) DESC 
   LABEL E 'Sales Rep', SUM(H) 'Revenue'", 1)
```

---

## Conditional Formatting Formulas

### KPI Change Indicator (Green if positive)
Apply to change percentage cells:
- **Green text (#27AE60):** Custom formula `=B12>0`
- **Red text (#E74C3C):** Custom formula `=B12<0`

### Performance Status
```
=IF(ActualValue>=Target,"✓",IF(ActualValue>=Target*0.8,"⚠","✗"))
```

### Data Bars (for tables)
Use built-in conditional formatting → Color scale or Data bars

---

## Utility Formulas

### Current Period Revenue (for comparison)
```
=SUMIFS(Data!H:H, 
  Data!A:A, ">="&DATE(YEAR(TODAY()),MONTH(TODAY()),1),
  Data!A:A, "<="&EOMONTH(TODAY(),0))
```

### Previous Period Revenue
```
=SUMIFS(Data!H:H, 
  Data!A:A, ">="&EOMONTH(TODAY(),-2)+1,
  Data!A:A, "<="&EOMONTH(TODAY(),-1))
```

### Period-over-Period Change
```
=IFERROR((CurrentPeriod-PreviousPeriod)/PreviousPeriod, 0)
```

### Sparkline (in a cell)
```
=SPARKLINE(L2:L7, {"charttype","column"; "color","#7FB3D5"})
```

---

## Tips

1. **Named Ranges:** Create named ranges for cleaner formulas
   - `SalesData` → `Data!A2:J`
   - `RegionFilter` → `Dashboard!C5`
   - `CategoryFilter` → `Dashboard!F5`

2. **Error Handling:** Always wrap division in `IFERROR()`

3. **Wildcards:** Use `"*"` in SUMIFS for "All" selection

4. **QUERY is powerful:** Use it for complex aggregations instead of multiple SUMIFS

5. **Array Formulas:** Use `ARRAYFORMULA()` for calculations that span ranges
