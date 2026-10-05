# Project 2: Discount Impact on Coffee Shop Revenue

Dashboard link: https://public.tableau.com/views/Retail_Analysis_17911731642390/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

Google Sheets Link: https://docs.google.com/spreadsheets/d/1LZugdyf5McV1Jmy1dj4Wnak7DK4EyrZfyFKj45peQZw/edit?usp=sharing

## Context
Goal: start with a real question before analysis, and use more advanced Excel techniques (XLOOKUP, INDEX-MATCH, AVERAGEIF, Power Query-style table restructuring) in the workflow.

## Question
Among transactions with a known discount status, do discounted purchases differ from full-price ones in units sold and revenue — and does the pattern vary by item category?

## What I did

### Cleaning
- Split raw CSV; duplicated worksheet before cleaning (kept raw intact)
- Audited missingness with COUNTBLANK + conditional formatting
- Extracted an item_key from item names using RIGHT/LEN/SEARCH to anchor lookups
- Built a separate item reference table (item, category, item_key, price/unit)
- Reconstructed missing Total Spent (Price × Qty) and Quantity (Spent / Price)
- Filled missing item/category/price via VLOOKUP, XLOOKUP, and INDEX-MATCH
- Filled ~600 missing quantity cells (~4.8%) using AVERAGEIF per item
  (item-level average instead of a blanket average, to reduce skew)
- Remaining unknowns (payment, location, date, discount status) marked "UNSPECIFIED"

### Exploration
- Split transaction date into day / month / year for Case of time-based analysis
- Pivoted discount status (T/F/U) against item category

### Analysis
- Scoped comparison to transactions with known discount status (T/F only)
- Compared discounted vs non-discounted on: total units, total revenue,
  average spend per transaction, and the same broken out by category
- Ran a 3-way check per category (transaction count, avg spend, total revenue)
  to confirm the pattern and flag exceptions

## Findings
- Discount status was evenly distributed (~33% T / 33% F / 33% U). Excluding
  unspecified leaves 8,376 transactions at a ~50/50 T/F split — a fair comparison.
- Discounted transactions generally had lower average spend per transaction
  but higher total revenue than non-discounted ones — consistent with discounts
  driving volume rather than value.
- The pattern held across most categories, with several exception where the
  non-discounted state performed marginally better.
- Some discounted items sold fewer units yet out-earned their non-discounted
  counterparts — same volume-vs-value pattern, viewed from the unit side.

## Recommendation
- Discount selectively, not blanket. Focus on categories where discounting
  drives volume without eroding total revenue.
- For categories that sell well at full price, avoid discounts — they reduce
  margin per sale without a clear revenue gain.
- Treat the current finding as correlational. A controlled A/B test (discount
  one category for a defined period, compare to a matched control) would
  confirm whether the discount itself is causing the volume lift.

## Limitations
- ~33% of rows have unspecified discount status and were excluded from the
  comparison; the analysis is scoped to the remaining 8,376 transactions.
- No discount percentage or discounted price recorded — margin impact can't
  be measured, so this compares volume and revenue only.
- Within-category price diversity (~20 items per category at varied price
  points) may amplify apparent contrasts; part of the T/F difference could
  reflect which items were discounted rather than the discount itself.
- Causation not established — high-revenue categories may have been discounted
  because they were high-revenue, not the reverse.

## What I'd do differently
- Record or derive discount percentage to enable margin analysis.
- Move exploration to SQL for speed and repeatability.
- Design a controlled test rather than comparing observational groups.

## Tools
Excel (cleaning, lookups, AVERAGEIF, pivot tables) · Tableau (dashboard)
