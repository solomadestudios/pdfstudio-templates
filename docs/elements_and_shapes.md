# PDF Studio Elements, Shapes & Visual Components Reference

This document provides a comprehensive specification for every design component available in PDF Studio, including its properties, data types, capabilities, usage guidelines, and styling pro-tips.

---

## 🌐 Common Canvas Properties (Shared by All Components)

Every component on the canvas inherits the following spatial, ordering, and state properties:

| Property | Type | Description |
| :--- | :--- | :--- |
| `x`, `y` | `Float` (pt) | Top-left position on the page in typographic points (1 pt = 1/72 inch). |
| `width`, `height` | `Float` (pt) | Component bounding box dimensions. |
| `rotation` | `Float` (deg) | Free rotation angle in degrees from `-360°` to `+360°`. |
| `opacity` | `Float` | Alpha transparency level from `0.0` (invisible) to `1.0` (opaque). |
| `zIndex` | `Int` | Layer stacking order (higher values render in front of lower values). |
| `isLocked` | `Boolean` | Locks position and size to prevent accidental movement during editing. |
| `isVisible` | `Boolean` | Toggles rendering on the interactive canvas and in exported PDFs. |

---

## 1. 🖋️ Typography & Text Components

### `ComponentType.TEXT` — Text Label
Standard single or multi-line label supporting dynamic template expressions.

- **Capabilities:**
  - Mustache variable replacement (`{{customer_name}}`, `{{invoice_date}}`).
  - Custom font families (Default, Serif, Sans-Serif, Monospace, Cursive).
  - Formatting: Bold, Italic, Underline, and Strikethrough.
  - Dual-axis auto-fitting (width and height scale to wrap text snugly).

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `text` | `String` | `"Text Label"` | Text content or variable expression. |
| `fontSize` | `Float` | `14.0` | Font size in points. |
| `fontFamily` | `String` | `"DEFAULT"` | `DEFAULT`, `SERIF`, `SANS_SERIF`, `MONOSPACE`, or custom imported fonts. |
| `textColor` | `Long` | `0xFF000000` | Font color in 32-bit ARGB. |
| `isBold` | `Boolean` | `false` | Toggles bold font weight. |
| `isItalic` | `Boolean` | `false` | Toggles italic slant. |
| `isUnderline` | `Boolean` | `false` | Draws bottom underline. |
| `isStrikethrough` | `Boolean` | `false` | Draws middle strike-through line. |

> **💡 Pro-Tip:** Use `{{key}}` syntax (e.g. `{{client_name}}`) to automatically bind CSV columns during batch PDF generation.

---

### `ComponentType.HEADING` — Document Title & Section Header
Prominent, bold element designed for document titles, invoices, and certificates.

- **Capabilities:**
  - High typographic hierarchy with larger default sizes.
  - Optional colored background highlight card with corner rounding.
  - Alignment: Left, Center, Right, or Justify.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `text` | `String` | `"Heading"` | Title text string. |
| `fontSize` | `Float` | `24.0` | Font size (recommended 18pt–36pt). |
| `fillColor` | `Long` | `TRANSPARENT` | Background banner highlight color. |
| `cornerRadius` | `Float` | `0.0` | Corner arc rounding for background banner. |
| `textAlign` | `String` | `"LEFT"` | `LEFT`, `CENTER`, `RIGHT`, or `JUSTIFY`. |

> **💡 Pro-Tip:** Pair a 24pt heading with a soft pastel background fill and `8pt` corner radius to create eye-catching chapter dividers.

---

### `ComponentType.PARAGRAPH` — Flowing Body Text
Multi-line body text container with automatic line-wrapping and multi-page pagination.

- **Capabilities:**
  - Automatic line wrapping within fixed column width.
  - Height dynamically recalculates when text changes or when width is resized horizontally.
  - Automatic multi-page overflow pagination (`paginateParagraphOverflow`).
  - Configurable line spacing and internal padding.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `text` | `String` | `""` | Multi-line body text. |
| `lineSpacing` | `Float` | `1.3` | Line height multiplier (`1.0` to `2.0`). |
| `padding` | `Float` | `8.0` | Internal padding from container edges. |
| `textAlign` | `String` | `"LEFT"` | `LEFT`, `CENTER`, `RIGHT`, or `JUSTIFY`. |

> **💡 Pro-Tip:** Set `textAlign = "JUSTIFY"` and `lineSpacing = 1.35` for book-quality formal contracts and terms of service.

---

### `ComponentType.URL` — Interactive Hyperlink
Interactive link supporting custom anchor text and visual link icons.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `url` | `String` | `"https://..."`| Target web destination URI. |
| `displayText` | `String` | `""` | Friendly display title (e.g. `"Visit Website"`). |
| `showIcon` | `Boolean` | `true` | Prepends link indicator icon (`🔗`). |
| `showUnderline` | `Boolean` | `true` | Standard hyperlink underline styling. |

---

## 2. 🔷 Basic Vector Shapes

### `SHAPE_RECTANGLE` & `SHAPE_ROUNDED_RECTANGLE`
Versatile vector containers for backgrounds, cards, dividers, and colored panels.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `fillColor` | `Long` | `0xFFE2E8F0` | Interior fill color (ARGB). |
| `strokeColor` | `Long` | `TRANSPARENT` | Border outline color. |
| `strokeWidth` | `Float` | `0.0` | Outline thickness in points (`0` = borderless). |
| `cornerRadius` | `Float` | `0.0` / `12.0`| Corner arc radius (`0` to `120pt`). |
| `lineStyle` | `String` | `"SOLID"` | `"SOLID"` or `"DASHED"`. |

---

### `SHAPE_CIRCLE` — Circle & Oval
Smooth circular or elliptical vector shape for badges, stamps, avatars, and seals.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `width`, `height` | `Float` | `80.0` | Equal dimensions form a circle; unequal form an oval. |
| `fillColor` | `Long` | `0xFF3B82F6` | Interior fill color. |
| `strokeWidth` | `Float` | `0.0` | Border thickness. |

---

### `SHAPE_LINE` — Vector Rule & Divider
Horizontal, vertical, or angled divider lines.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `strokeWidth` | `Float` | `1.5` | Line thickness. |
| `strokeColor` | `Long` | `0xFF94A3B8` | Line color. |
| `lineStyle` | `String` | `"SOLID"` | `"SOLID"` or `"DASHED"` (tear-off indicator). |
| `lineCap` | `String` | `"ROUND"` | `"ROUND"`, `"SQUARE"`, or `"BUTT"`. |

---

## 3. 📐 Advanced Vector Shapes

### `SHAPE_BEZIER` — Bézier Spline Curve
Cubic vector curve controlled by 4 points (P0 Start, P1 Handle, P2 Handle, P3 End).

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `bezierP0x`, `bezierP0y` | `Float` | `0.0, 0.5` | Normalized starting point (`0.0` to `1.0`). |
| `bezierP1x`, `bezierP1y` | `Float` | `0.3, 0.0` | First control handle vector & tension. |
| `bezierP2x`, `bezierP2y` | `Float` | `0.7, 1.0` | Second control handle vector & tension. |
| `bezierP3x`, `bezierP3y` | `Float` | `1.0, 0.5` | Normalized end point (`0.0` to `1.0`). |
| `bezierClosed` | `Boolean` | `false` | Connects endpoints and fills as a solid shape. |

---

### `SHAPE_STAR` — Parametric Star
Multi-pointed star for certificates, award badges, and ratings.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `starPoints` | `Int` | `5` | Point count (`3` to `16`). |
| `innerRadiusRatio` | `Float` | `0.38` | Inner radius ratio (`0.1` = needle-sharp, `0.7` = plump). |

---

### `SHAPE_POLYGON` — Regular Polygon
Regular N-sided polygon (triangle, pentagon, hexagon, octagon).

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `polygonSides` | `Int` | `6` | Number of sides (`3` to `12`). |
| `cornerRadius` | `Float` | `0.0` | Smooth vertex rounding. |

---

### `SHAPE_TRIANGLE` — Custom Apex Triangle
Directional pointer or geometric accent triangle.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `triangleApexX` | `Float` | `0.5` | Peak position (`0.0` = left, `0.5` = center, `1.0` = right). |
| `cornerRadius` | `Float` | `0.0` | Vertex rounding. |

---

### `SHAPE_ARROW` — Directional Arrow
Flowchart and process indicator banner.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `arrowDirection` | `String` | `"RIGHT"` | `"RIGHT"`, `"LEFT"`, `"UP"`, or `"DOWN"`. |
| `arrowHeadRatio` | `Float` | `0.4` | Arrowhead length fraction. |
| `arrowShaftRatio`| `Float` | `0.35` | Shaft thickness fraction. |

---

### `SHAPE_WAVE` — Sinusoidal Wave Banner
Flowing organic wave for modern document headers, footers, and dividers.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `waveAmplitude` | `Float` | `20.0` | Peak wave height in points. |
| `waveFrequency` | `Float` | `1.0` | Number of wave cycles across the width (`0.5` to `8.0`). |
| `wavePhase` | `Float` | `0.0` | Horizontal phase offset. |
| `waveFilled` | `Boolean` | `true` | Fills the entire region beneath the wave crest. |

---

### `SHAPE_ARC` — Donut Ring & Gauge Wedge
Parametric arc segment for progress meters, gauge charts, and donut rings.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `arcStartAngleDeg` | `Float` | `-90.0` | Starting angle in degrees (`0°` = 3 o'clock). |
| `arcSweepAngleDeg` | `Float` | `180.0` | Sweep angle (`10°` to `360°`). |
| `arcInnerRadiusRatio` | `Float` | `0.65` | `0.0` = solid pie wedge; `0.7` = ring arc. |

---

### `SHAPE_DIAGONAL_CUT` — Chamfered Card
Contemporary card with customizable diagonal cuts on each corner.

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `cutTopLeft` / `cutTopRight` | `Float` | `16.0` | Top corner chamfer depths in points. |
| `cutBottomLeft` / `cutBottomRight` | `Float` | `0.0` | Bottom corner chamfer depths in points. |

---

## 4. 📊 Data, Tables & Analytics

### `ComponentType.TABLE` — Data Table
Structured multi-column table supporting formulas, CSV data binding, and cell merging.

- **Capabilities:**
  - Arbitrary cell range merging (`fromRow..toRow`, `fromCol..toCol`).
  - Grid styling: `ALL_BORDERS`, `HORIZONTAL_ONLY`, `VERTICAL_COLUMNS`, or `BORDERLESS`.
  - Zebra striping (alternating row background colors).
  - Bold summary total row (`hasTotalRow = true`).
  - CSV import directly from device storage.
  - Multi-page continuation with repeating header support.

| Property | Type | Description |
| :--- | :--- | :--- |
| `columns` | `List<TableColumn>` | Column definitions (`title`, `widthWeight`, `alignment`). |
| `rows` | `List<TableRow>` | Row data containing cell strings or formulas. |
| `headerBackgroundColor` | `Long` | Header row background color. |
| `alternateRowColor` | `Long` | Alternating zebra background tint. |
| `gridStyle` | `String` | `"ALL_BORDERS"`, `"VERTICAL_COLUMNS"`, `"HORIZONTAL_ONLY"`, `"BORDERLESS"`. |
| `hasTotalRow` | `Boolean` | Applies prominent top/bottom summary borders to the final row. |
| `mergedCells` | `List<MergedCellRange>` | List of merged rectangular cell ranges `(fromRow, toRow, fromCol, toCol)`. |
| `repeatHeaderOnNewPage`| `Boolean` | Repeats table column headers if table splits across multiple pages. |

---

### `ComponentType.CHART` — Vector Charts
Native mathematical charts rendered at 300+ DPI without pixelation.

| Property | Type | Description |
| :--- | :--- | :--- |
| `chartType` | `Enum` | `BAR`, `LINE`, `PIE`, or `DONUT`. |
| `title` | `String` | Top title rendered on the chart card. |
| `labels` | `List<String>` | Category names along the X-axis or legend. |
| `values` | `List<Double>` | Numerical series data. |
| `showLegend` | `Boolean` | Displays category color legend. |
| `showValues` | `Boolean` | Renders numerical data callouts directly on plot bars/slices. |

---

### `ComponentType.KPI_CARD` — Executive Metric Card
Dashboard metric summary with headline values and positive/negative trend badges.

| Property | Type | Description |
| :--- | :--- | :--- |
| `title` | `String` | Card label (e.g. `"Quarterly Revenue"`). |
| `value` | `String` | Main bold metric (e.g. `"$128,450"`). |
| `subtitle` | `String` | Trend comparison text (e.g. `"+14.2% vs last quarter"`). |
| `trendPositive` | `Boolean` | `true` renders emerald green badge; `false` renders crimson red badge. |

---

### `ComponentType.LIST` — Bulleted & Numbered List
Multi-item list with 10 bullet styles and independent symbol coloring.

| Property | Type | Description |
| :--- | :--- | :--- |
| `items` | `List<String>` | List item strings. |
| `bulletStyle` | `String` | `DISC` (•), `CHECKMARK` (✓), `STAR` (★), `ARROW` (➔), `NUMBERED` (1.), `ROMAN` (I.), `ALPHA` (A.). |
| `bulletColor` | `Long` | Color of the bullet marker icon (e.g. emerald checkmark). |
| `bulletIndent` | `Float` | Spacing distance between bullet marker and text. |
| `itemSpacing` | `Float` | Vertical gap between consecutive list items. |

---

## 5. 🖼️ Media, Signatures & Ornaments

### `ComponentType.IMAGE` — Image & Logo Embedding
Embed raster and vector images (JPEG, PNG, WebP) with clip shapes and opacities.

| Property | Type | Description |
| :--- | :--- | :--- |
| `imageUri` / `imageLocalPath` | `String` | Local file path or content URI. |
| `imageShape` | `String` | `RECTANGLE`, `ROUNDED_RECTANGLE`, or `CIRCLE` (avatar clip). |
| `imageContentScale` | `String` | `FIT`, `FILL`, or `CROP`. |
| `cornerRadius` | `Float` | Corner rounding when `imageShape == ROUNDED_RECTANGLE`. |
| `opacity` | `Float` | Transparency (e.g. `0.15` for subtle background watermark logos). |

---

### `ComponentType.SIGNATURE` — Digital Signature
Vector-drawn and timestamped digital signature block.

| Property | Type | Description |
| :--- | :--- | :--- |
| `signaturePath` | `String` | Internal path to cached vector PNG signature. |
| `signerName` | `String` | Printed legal name beneath signature line. |
| `signerTitle` | `String` | Job title or designation (e.g. `"Managing Director"`). |
| `timestamp` | `Long` | Execution timestamp for audit verification. |

---

### `ComponentType.DECORATIVE` — Botanical Foliage & Borders
High-resolution vector ornaments for invitations, luxury certificates, and greetings.

| Motif Category | Available Motifs |
| :--- | :--- |
| **`FOLIAGE`** | `OLIVE_BRANCH`, `EUCALYPTUS`, `CHERRY_BLOSSOM`, `ROSE_BLOOM`, `FERN_LEAF` |
| **`FESTIVAL`** | `FESTIVE_DIYA`, `GIFT_BOX`, `JINGLE_BELLS`, `INTERTWINED_HEARTS`, `WEDDING_RINGS` |
| **`BORDERS`** | `IMAGE_GOLD_FILIGREE`, `IMAGE_ROSE_GOLD`, `IMAGE_GEOMETRIC_ART_DECO`, `DOUBLE_LINE` |
