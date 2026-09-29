# Formula Engine & Math Guide

PDF Studio includes a built-in mathematical and financial calculation engine. Formulas can be embedded in **Table Cells**, **Document Headings**, **Summary Labels**, and **KPI Cards**.

---

## 🧮 Syntax & Usage

Formulas always begin with an equals sign (`=`):
```
=SUM(C1:C10)
```

Formulas update dynamically in real time whenever values or variables change.

---

## 📋 Supported Functions

### 1. Statistical & Aggregate Functions

| Function | Syntax | Description | Example |
| :--- | :--- | :--- | :--- |
| **SUM** | `=SUM(range)` | Sums all numeric values in a rectangular cell range. | `=SUM(D1:D15)` |
| **AVG** | `=AVG(range)` | Computes the arithmetic mean of numeric cells. | `=AVG(C1:C8)` |
| **MIN** | `=MIN(range)` | Finds the lowest numeric value in the range. | `=MIN(B2:B20)` |
| **MAX** | `=MAX(range)` | Finds the highest numeric value in the range. | `=MAX(B2:B20)` |
| **COUNT** | `=COUNT(range)` | Counts non-empty numeric cells in the range. | `=COUNT(A1:A50)` |

### 2. Arithmetic & Financial Calculations

The formula engine supports standard algebraic operators (`+`, `-`, `*`, `/`, `^`, `%`) and parenthetical groupings:

- **Row Subtotals**:
  ```
  =B2 * C2
  ```
  *(Multiplies Quantity in B2 by Unit Price in C2)*

- **Tax & Discount Calculation**:
  ```
  =D10 * 1.18
  ```
  *(Applies 18% VAT / GST to subtotal in cell D10)*

- **Discount Application**:
  ```
  =(D10 + D11) * 0.90
  ```
  *(Applies a 10% commercial discount to total sum)*

- **Complex Algebraic Formulas**:
  ```
  =(A1 + B1) / (C1 - D1) * 100
  ```

---

## 📊 Range Syntax

- **Column Range**: `A1:A5` evaluates cells A1, A2, A3, A4, A5.
- **2D Rectangular Range**: `A1:C3` evaluates a 3x3 matrix across columns A, B, C.
- **Multiple Arguments**: `=SUM(A1:A3, B1:B3)` evaluates both ranges.

---

## 💡 Pro-Tips
- You can format formula results directly using currency or percentage notations:  
  `Total: $=SUM(D1:D5)` evaluates to `Total: $1,450.00`.
- Cells containing invalid text or non-numeric values are safely skipped without breaking calculation results.
