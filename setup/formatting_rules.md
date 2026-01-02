# Conditional Formatting Rules

All conditional formatting rules for the Sales Dashboard.

---

## KPI Cards - Change Indicators

### Positive Change (Green)
**Apply to:** Cells showing % change (e.g., B12, D12, F12, H12)

1. Select cell(s)
2. Format → Conditional formatting
3. Format rules:
   - **Custom formula:** `=B12>0`
   - **Formatting style:** 
     - Text color: #27AE60 (Green)
     - Bold: Yes

### Negative Change (Red)
**Apply to:** Same cells as above

1. Add another rule
2. Format rules:
   - **Custom formula:** `=B12<0`
   - **Formatting style:**
     - Text color: #E74C3C (Red)
     - Bold: Yes

---

## KPI Cards - Value Thresholds

### Revenue Target Highlighting
**Apply to:** Revenue KPI value cell

**Rule 1 - Exceeds Target (Green background)**
- Custom formula: `=B10>=100000`
- Background: #E8F8F5 (light green tint)

**Rule 2 - Below Target (Red background)**
- Custom formula: `=B10<80000`
- Background: #FDEDEC (light red tint)

---

## Data Table - Alternating Colors

**Apply to:** Data table range (e.g., B36:I100)

1. Format → Alternating colors
2. Header: #F4F6F6
3. Color 1: #FFFFFF (white)
4. Color 2: #FAFAFA (very light gray)
5. Footer: None

---

## Data Table - Revenue Color Scale

**Apply to:** Revenue column in data table

1. Format → Conditional formatting
2. Format rules:
   - **Color scale**
   - Min: #FFFFFF (white)
   - Max: #7FB3D5 (pastel blue)

---

## Sales Rep Leaderboard - Ranking Colors

### Top Performer (Gold)
**Apply to:** First row of leaderboard

- Custom formula: `=ROW()=ROW($B$25)` (adjust row number)
- Background: #FEF9E7 (light gold)
- Text: Bold

### Top 3 (Subtle highlight)
**Apply to:** Leaderboard range

- Custom formula: `=ROW()-ROW($B$24)<=3`
- Background: #F8F9F9

---

## Status Indicators

### Performance Status Cell
If you have a cell showing status (On Track / Warning / Behind):

**Rule 1 - On Track**
- Text contains: `✓` or `On Track`
- Text color: #27AE60
- Background: #E8F8F5

**Rule 2 - Warning**
- Text contains: `⚠` or `Warning`
- Text color: #F39C12
- Background: #FEF9E7

**Rule 3 - Behind**
- Text contains: `✗` or `Behind`
- Text color: #E74C3C
- Background: #FDEDEC

---

## Filter Dropdowns - Active State

### Highlight Active Filter
**Apply to:** Filter dropdown cells (C5, F5)

- Custom formula: `=C5<>"All"`
- Background: #EBF5FB (light blue)
- Border: 1px solid #7FB3D5

---

## Month-over-Month Comparison

### Growth Column
**Apply to:** Growth/change column in tables

**Positive Growth:**
- Custom formula: `=G2>0`
- Text color: #27AE60
- Add icon: ▲ (prepend in formula)

**Negative Growth:**
- Custom formula: `=G2<0`
- Text color: #E74C3C
- Add icon: ▼ (prepend in formula)

**Formula for cell with icon:**
```
=IF(G2>0, "▲ "&TEXT(G2,"+0.0%"), IF(G2<0, "▼ "&TEXT(G2,"0.0%"), "— 0.0%"))
```

---

## Data Validation Visual Cues

### Required Fields
**Apply to:** Input cells that need values

- Custom formula: `=ISBLANK(A1)`
- Background: #FDEDEC (light red)

### Valid Entry Confirmation
**Apply to:** Cells after data validation passes

- Custom formula: `=NOT(ISBLANK(A1))`
- Background: #E8F8F5 (light green)

---

## Quick Reference: Color Codes

| Purpose | Color | Hex |
|---------|-------|-----|
| Positive / Success | Green | #27AE60 |
| Positive Background | Light Green | #E8F8F5 |
| Negative / Error | Red | #E74C3C |
| Negative Background | Light Red | #FDEDEC |
| Warning | Orange | #F39C12 |
| Warning Background | Light Yellow | #FEF9E7 |
| Neutral | Gray | #5D6D7E |
| Active/Selected | Blue | #7FB3D5 |
| Active Background | Light Blue | #EBF5FB |
| Header Background | Light Gray | #F4F6F6 |
| Alternating Row | Very Light Gray | #FAFAFA |

---

## Applying Rules Efficiently

### Copy Formatting
1. Select cell with formatting
2. Click "Paint format" tool (roller icon)
3. Click or drag across target cells

### Paste Special - Format Only
1. Copy cell with formatting
2. Select target range
3. Right-click → Paste special → Format only

### Manage Rules
1. Format → Conditional formatting
2. See all rules in sidebar
3. Drag to reorder (top = highest priority)
4. Click rule to edit
5. Hover + click trash to delete

---

## Tips

1. **Order matters:** Rules are evaluated top-to-bottom, first match wins
2. **Use absolute references:** `$A$1` when rule should check same cell for all rows
3. **Use relative references:** `A1` when rule should check each row's own cell
4. **Test with edge cases:** 0, negative, blank, very large numbers
5. **Don't over-format:** Subtle colors > loud colors for professional look
