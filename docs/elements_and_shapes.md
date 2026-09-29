# Design Elements, Shapes & Visual Components

PDF Studio provides a complete vector drafting engine for creating executive documents, stationery, and graphical reports.

---

## 🖋️ Typography & Text

- **Heading (`ComponentType.HEADING`)**: 28pt bold title block with dual-axis auto-fitting.
- **Text (`ComponentType.TEXT`)**: 14pt single/multi-line label with dynamic bounds fitting.
- **Paragraph (`ComponentType.PARAGRAPH`)**: Fixed-width column block that dynamically expands or shrinks its height to prevent clipping. Features automatic multi-page overflow pagination.
- **Clickable URL (`ComponentType.URL`)**: Interactive hyperlink supporting custom anchor text, live linking, and visual link icons (`🔗`).

---

## 📐 Vector Shapes & Curves

All vector shapes scale smoothly without pixelation and support custom fill colors, stroke colors, corner radiuses, and opacities:

- **Triangle (`SHAPE_TRIANGLE`)**: Equilateral, right-angled, or skewed triangles with customizable apex position.
- **Regular Polygon (`SHAPE_POLYGON`)**: 3 to 12-sided polygons (pentagon, hexagon, octagon).
- **Star (`SHAPE_STAR`)**: 4 to 12-point stars with customizable inner/outer radius ratios.
- **Directional Arrow (`SHAPE_ARROW`)**: Up, Down, Left, or Right directional banners.
- **Sinusoidal Wave (`SHAPE_WAVE`)**: Smooth wave section divider with adjustable wave frequency and amplitude.
- **Bézier Path (`SHAPE_BEZIER`)**: Smooth quadratic and cubic vector curves.
- **Diagonal Cut Banner (`SHAPE_DIAGONAL_CUT`)**: Modern geometric angled hero headers.

---

## 📊 Charts & Data Visualization

- **Bar Chart**: Multi-category vertical bar graph with value callouts and custom accent colors.
- **Line Graph**: Continuous trend line with data point dots and gradient area fill.
- **Pie Chart**: Circular sector breakdown with percentage badges and side legends.
- **Donut Chart**: Ring chart with center summary totals and category legends.

---

## 🌿 Decorative Elements & Ornaments

- **Botanical Foliage**: Olive branches, eucalyptus leaves, cherry blossoms, rose blooms, and fern fronds.
- **Celebration Motifs**: Festive diyas, jingle bells, gift boxes, and intertwined hearts.
- **Luxury Page Borders**: Gold filigree, rose gold, geometric art-deco, and subtle double-line margins.
