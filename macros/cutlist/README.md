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

## How to use

1. Open your FreeCAD document
2. Select an assembly, group, or subtree in the **Model Tree**
3. Run the macro
4. The spreadsheet **CutList** will be created or updated
5. You will be asked if you want to export the result to CSV

## Notes

- The macro is safe to re-run multiple times
- Old spreadsheet data is always wiped
- No Pad/Sketch names are ever used as labels

## Tested with

- FreeCAD 0.21+
- macOS (Apple Silicon & Intel)
