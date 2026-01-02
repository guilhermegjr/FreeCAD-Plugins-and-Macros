# Cut List to Spreadsheet (FreeCAD Macro)

This FreeCAD macro generates a **clean, aggregated cut list** from a selected assembly or subtree
and writes the result to a Spreadsheet. Optionally, it can export the result to CSV.

## Features

- Recursive traversal of selected objects
- Correct handling of **App::Link** ("Make Link") instances
- Parts are detected as:
  - `PartDesign::Body`
  - Links pointing to a Body (counted as independent instances)
- Aggregation by:
  - Length
  - Width
  - Material (thickness)
- Smart label merging:
  - `Base Left`, `Base Middle`, `Base Right` → `Base Left/Middle/Right`
- Spreadsheet is **fully cleared before regeneration**
- `Enabled` column is always `true`
- Optional CSV export after generation

## Output Columns

| Column   | Description |
|--------|-------------|
| Length | Longest dimension (mm) |
| Width  | Middle dimension (mm) |
| Qty    | Quantity |
| Material | Thickness (mm) |
| Label  | Human-friendly merged label |
| Enabled | Always `true` |

## Using the CSV with Cut List Optimizer

The generated CSV file can be **directly imported** into  
👉 https://www.cutlistoptimizer.com/

This allows you to visually optimize how boards or panels should be cut
to minimize waste.

### How to use it

1. Run the macro and choose **Export to CSV**
2. Open https://www.cutlistoptimizer.com/
3. Select **Import CSV**
4. Map the fields as follows:

| Cut List Optimizer Field | CSV Column |
|------------------------|------------|
| Length                 | Length     |
| Width                  | Width      |
| Quantity               | Qty        |
| Thickness (optional)   | Material   |
| Label / Part name      | Label      |

5. Define your stock sheet sizes (e.g. plywood sheets, boards)
6. Generate the cutting layout

### Notes

- Units are exported in **millimeters**
- Thickness (`Material`) is included for reference and filtering
- The `Enabled` column can be ignored by the optimizer
- Labels like `Base Left/Middle/Right` help identify parts visually
