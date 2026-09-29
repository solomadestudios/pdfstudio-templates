# Batch PDF Generation & Mail Merge (CSV Automation)

PDF Studio includes a high-speed batch generation engine capable of rendering hundreds of personalized PDF documents from tabular CSV or JSON datasets in a single operation.

---

## 🚀 Key Capabilities

- **CSV Tabular Datasets**: Select a `.csv` file via the system file picker or paste raw CSV text directly into the batch console.
- **Automatic Multi-Row Invoice Grouping**: Multiple CSV rows sharing the same identifier (e.g., `invoice_number`, `order_id`, or `student_id`) are automatically aggregated into a single PDF document containing a multi-row line-item table.
- **Pre-Flight Validation**: Automatic verification of required template fields, numerical types, and email patterns prior to generation.
- **Flexible Packaging**: Export as individual PDFs, a combined multi-page PDF, or a single compressed `.zip` archive.
- **Custom Filename Patterns**: Tokenized patterns such as `Invoice_{invoice_number}_{client_name}.pdf` with automatic collision handling.

---

## 📄 CSV Format Example: Multi-Row Invoices

To generate invoices with dynamic line items, repeat the primary document key (`invoice_number`, `invoice_date`, `client_name`) on each row, providing distinct line items for `Description`, `Quantity`, and `Unit Price`:

```csv
invoice_number,invoice_date,client_name,client_email,Description,Quantity,Unit Price
INV-2026-001,2026-09-10,Acme Global,billing@acme.com,Cloud Architecture Consultation,2,150.00
INV-2026-001,2026-09-10,Acme Global,billing@acme.com,Kubernetes Cluster Deployment,1,450.00
INV-2026-002,2026-09-11,Wayne Enterprises,accounts@wayne.com,Vector Engine Pipeline R&D,3,75.00
INV-2026-002,2026-09-11,Wayne Enterprises,accounts@wayne.com,Security Penetration Testing,1,600.00
```

### What Happens During Generation:
1. Rows 1 and 2 share `INV-2026-001` ➔ Generates **one** invoice for *Acme Global* with a 2-row table and a total of `$750.00`.
2. Rows 3 and 4 share `INV-2026-002` ➔ Generates **one** invoice for *Wayne Enterprises* with a 2-row table and a total of `$825.00`.

---

## 🏷️ Filename Pattern Tokens

Customize the output naming convention in the Batch Generation dialog:

| Token | Description | Example Replacement |
| :--- | :--- | :--- |
| `{invoice_number}` | Extracted variable value | `INV-2026-001` |
| `{client_name}` | Sanitized client name | `Acme_Global` |
| `{index}` | 1-based generation sequence index | `001`, `002` |
| `{template_name}` | Base template title | `Modern_Invoice` |

*Example Pattern:* `Invoice_{invoice_number}_{client_name}.pdf`  
*Generated Output:* `Invoice_INV-2026-001_Acme_Global.pdf`

---

## 💾 Storage Location
All batch exports are saved to your device's standard Documents directory:
`Documents/PdfStudio/Batch_<TemplateName>_<timestamp>/`
