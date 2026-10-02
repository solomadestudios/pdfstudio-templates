# Formula Engine & Math Guide

PDF Studio includes a built-in mathematical, financial, and expression calculation engine ([`FormulaEngine.kt`](https://github.com/solomadestudios/PDFStudio)). Formulas can be embedded in **Mustache Tags** (`{{ ... }}`), **Table Column Formulas**, **Cell Formulas** (starting with `=`), **KPI Cards**, and **Headings / Labels**.

---

## 🧮 How Formulas Work

Unlike static spreadsheet software that relies on fragile cell coordinates (e.g. `C1:C10`), PDF Studio's formula engine is **data-driven and semantic**:

1. **In Templates & Text Elements**: Wrap expressions in mustache tags:
   ```mustache
   {{quantity * unit_price}}
   {{SUM(items.total)}}
   ```
2. **In Table Columns & Cells**: Write formula expressions directly or start with `=`:
   ```
   quantity * unit_price
   =price * qty
   =SUM(total)
   ```

Formulas calculate dynamically in real-time when generating documents, filling templates, or running batch CSV/JSON exports.

---

## 📋 Supported Aggregate & Summary Functions

Aggregate over all line items in a table (bound to `items` or by column name):

| Function | Syntax | Description | Example |
| :--- | :--- | :--- | :--- |
| **SUM** | `SUM(items.field)` or `SUM(column_name)` | Sums numeric values across all rows for the specified column. | `{{SUM(items.total)}}`<br>`=SUM(amount)` |
| **AVG / AVERAGE** | `AVG(items.field)` or `AVG(column_name)` | Computes the arithmetic mean across all rows. | `{{AVG(items.price)}}`<br>`=AVG(unit_cost)` |
| **MIN** | `MIN(items.field)` or `MIN(column_name)` | Returns the lowest numeric value in the column. | `{{MIN(items.discount)}}` |
| **MAX** | `MAX(items.field)` or `MAX(column_name)` | Returns the highest numeric value in the column. | `{{MAX(items.total)}}` |
| **COUNT** | `COUNT(items)` or `COUNT(column_name)` | Counts the total number of line items or populated rows. | `{{COUNT(items)}}` |
| **ROUND** | `ROUND(value, decimals)` | Rounds a number to the given decimal places (default 2). | `{{ROUND(tax_amount, 2)}}` |
| **ABS** | `ABS(value)` | Returns the absolute positive value. | `{{ABS(balance_due)}}` |

---

## ⚡ Row & Arithmetic Calculations

Full algebraic operator support (`+`, `-`, `*`, `/`, `%`, `^`) with parenthetical precedence:

### 1. Row Subtotals (In Table Columns)
Set a table column's formula to multiply columns:
```
price * quantity
```
*Aliases also supported: `rate * hours`, `unit_cost * qty`, `col2 * col3`, or `b * c`.*

### 2. Tax, Discount & Surcharges
Calculate taxes or percentage discounts dynamically:
```mustache
{{subtotal * 0.18}}
{{(subtotal - discount) * 1.18}}
{{base_salary + bonus - deductions}}
```

### 3. Exponentiation & Complex Math
```mustache
{{principal * (1 + rate / 100) ^ years}}
```

---

## 🔀 Conditional Branching (`IF`)

Use `IF(condition, true_value, false_value)` for dynamic discounts, tax exemptions, and status labels:

- **Tiered Volume Discount**:
  ```mustache
  {{IF(subtotal > 1000, subtotal * 0.90, subtotal)}}
  ```
  *(Applies 10% discount if subtotal exceeds $1,000, otherwise keeps original subtotal)*

- **Conditional Tax Exemption**:
  ```mustache
  {{IF(is_tax_exempt == true, 0, subtotal * 0.18)}}
  ```

- **Pass / Fail Grading**:
  ```mustache
  {{IF(score >= 50, "PASS", "FAIL")}}
  ```

---

## 🎨 Number & Currency Formatting (`FORMAT`)

Format raw numbers into localized currency, percentage, or clean decimals using `FORMAT(value, "MASK")`:

```mustache
{{FORMAT(total_amount, "CURRENCY_USD")}}   --> $1,450.00
{{FORMAT(total_amount, "CURRENCY_INR")}}   --> ₹1,450.00
{{FORMAT(total_amount, "CURRENCY_EUR")}}   --> €1,450.00
{{FORMAT(total_amount, "CURRENCY_GBP")}}   --> £1,450.00
{{FORMAT(total_amount, "CURRENCY_JPY")}}   --> ¥1,450
{{FORMAT(tax_rate, "PERCENT")}}           --> 18.0%
{{FORMAT(item_count, "INTEGER")}}         --> 42
{{FORMAT(measurement, "NUMBER")}}         --> 1,234.56
```

---

## 💡 Pro-Tips

1. **Flexible Field Names**:
   The engine automatically normalizes case, spaces, and underscores:
   - `items.unit_price`, `items.Unit Price`, and `items.unitprice` all resolve identically.
2. **Auto-Calculated Totals**:
   If a table has a column titled `Total` or `Amount` and columns for `Price`/`Rate` and `Quantity`/`Qty`, the engine automatically computes `price * quantity` even without an explicit formula!
3. **Non-Numeric Safety**:
   Any cell containing text, currency symbols (`$`, `₹`, `€`), or commas is automatically cleaned and parsed safely without throwing errors.
