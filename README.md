# Normalisation

Browser-based teaching material for database normalisation. Two self-contained HTML
pages, no build step, no internet connection required — open either file in a browser.

| File | What it is |
|---|---|
| [`index.html`](index.html) | **Normalisation Lab** — an interactive explainer that walks one database from unnormalised form through 1NF, 2NF, 3NF, BCNF, 4NF and 5NF, with a six-case "Which normal form?" quiz for the class. |
| [`sparklegems-solution.html`](sparklegems-solution.html) | **SparkleGems worked solution** — Question Lab 2 solved end to end: UNF → 1NF → 2NF → 3NF → BCNF, with functional dependencies, SQL DDL, seed data and a lossless-join proof. |

## Running it

Double-click either HTML file, or serve the folder:

```bash
python3 -m http.server 8000
```

Keep the `assets/` folder next to the HTML files — both pages load the logo from it.

Use the top tabs or the left/right arrow keys to move between stages. The lab has a
**Presenter view** for projectors; the solution has **Show all steps** and **Print / PDF**
for handouts.

## The SparkleGems exercise

SparkleGems records every jewellery sale in one table that mixes order, customer, product
and designer facts. The solution page decomposes it into five relations:

```
Customer(CustomerID, CustomerName, CustomerPhone, CustomerAddress)
Designer(DesignerID, DesignerName, DesignerPhone)
Orders(OrderID, OrderDate, CustomerID, DesignerID)
Item(ItemID, ItemName, Material, Price)
OrderItem(OrderID, ItemID, Quantity)
```

The 3NF design is already in BCNF — every determinant is a candidate key. The BCNF stage
shows the determinant audit that proves it, plus a hypothetical failure case so the
3NF-passes-but-BCNF-fails shape is still on the page.

Two assumptions are stated on the page rather than left implicit:

- `Price` is the **unit price** of a piece, not the line total. `LineTotal = Quantity × Price`
  is derived and never stored.
- `CustomerID → DesignerID` holds in all five sample rows but is **rejected** as a
  coincidence of a small sample, not a business rule.

### Note on the source spreadsheet

In the original `.xlsx`, the multi-value `Quantity` cells were silently coerced by Excel
into date serials (45658, 45689) carrying the number format `d, m`. Decoded back, those
are `1, 1` and `1, 2` — the quantities used throughout the solution.
