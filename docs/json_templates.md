# JSON Template Specifications & API Guide

PDF Studio supports complete bidirectional JSON serialization. You can define templates programmatically, import external schemas, and automate document creation via JSON payloads.

---

## 🏗️ Top-Level Template Structure

```json
{
  "id": "custom_invoice_template",
  "name": "Corporate Invoice & Statement",
  "templateVersion": 1,
  "isPremium": false,
  "inputs": [
    {
      "bindingKey": "customer_name",
      "label": "Customer Name",
      "type": "TEXT",
      "defaultValue": "Acme Corp",
      "required": true
    },
    {
      "bindingKey": "invoice_date",
      "label": "Invoice Date",
      "type": "DATE",
      "defaultValue": "2026-09-30"
    },
    {
      "bindingKey": "items",
      "label": "Line Items",
      "type": "TABLE",
      "tableSchema": [
        { "title": "Item Description", "type": "TEXT", "widthWeight": 2.0 },
        { "title": "Qty", "type": "NUMBER", "widthWeight": 1.0 },
        { "title": "Rate ($)", "type": "NUMBER", "widthWeight": 1.2 },
        { "title": "Amount ($)", "type": "NUMBER", "widthWeight": 1.2 }
      ]
    }
  ],
  "document": {
    "title": "Corporate Invoice",
    "pages": [
      {
        "pageNumber": 1,
        "width": 595.28,
        "height": 841.89,
        "components": []
      }
    ]
  }
}
```

---

## 🎛️ Supported Input Types

| Type | Description | Rendered Control |
| :--- | :--- | :--- |
| `TEXT` | Single-line alphanumeric text string | Outlined Text Field |
| `NUMBER` | Numeric values (integer or floating point) | Numeric keypad input |
| `MULTILINE_TEXT` | Long descriptions, terms, and conditions | Expandable multi-line field |
| `DATE` | Standard ISO date string (`YYYY-MM-DD`) | Material 3 Date Picker |
| `DROPDOWN` | Single selection from predefined `options` | Exposed Dropdown Menu |
| `CHECKBOX` | Boolean toggle (`true` / `false`) | Material Checkbox |
| `IMAGE` | Local photo or company logo | Photo picker / camera upload |
| `SIGNATURE` | Digital drawn signature | Vector finger/stylus signature pad |
| `TABLE` | Dynamic multi-row tabular dataset | Spreadsheet grid with CSV import |

---

## 📦 Batch JSON Dataset Example

When passing datasets to the batch generation engine:

```json
[
  {
    "invoice_number": "INV-2026-001",
    "customer_name": "Acme Global Industries",
    "items": [
      { "Item Description": "Cloud Consultation", "Qty": 2, "Rate ($)": 150.00, "Amount ($)": 300.00 },
      { "Item Description": "Database Migration", "Qty": 1, "Rate ($)": 450.00, "Amount ($)": 450.00 }
    ]
  },
  {
    "invoice_number": "INV-2026-002",
    "customer_name": "Wayne Enterprises",
    "items": [
      { "Item Description": "Hardware Diagnostics", "Qty": 4, "Rate ($)": 75.00, "Amount ($)": 300.00 }
    ]
  }
]
```
