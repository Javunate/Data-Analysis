-- Context
First portfolio project. Goal: get comfortable with the full flow — 
clean → explore → analyze → visualize — on a messy coffee shop dataset.

Dashboard link:https://public.tableau.com/views/Cafe_Sales_17882417552310/Dashboard?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link
Google Sheets Link: https://docs.google.com/spreadsheets/d/1LSbvcamPsdxEnOT8mopPm2ZJkjggn8a7q5IK0czhJJ8/edit?usp=sharing

-- Question
Which items and days drive the most revenue?

-- What I did
- Split raw CSV, duplicated worksheet before cleaning (kept raw intact)
- Audited missingness with COUNTBLANK + conditional formatting
- Repaired missing values: reconstructed Price×Qty, inferred item by price/unit, 
  filled remaining gaps with "Unspecified"
- Engineered date features (day, week, month, period)
- Pivots + charts, dashboarded in Tableau

--Findings
- Salad drove the most revenue (3,819 sold) but Cake sold more units (3,914) — 
  the gap comes from a ~$2 price difference. High volume ≠ high revenue.
- Coffee was the 2nd most-bought item but 3rd lowest in income — a high-traffic, 
  low-margin product.
- Revenue peaked in June, then October.
- Thursday and Friday were the strongest days of the week.
- End-of-month (31st) days distort the daily trend — R² drops when included.

-- Recommendation
- Coffee is high-volume, low-margin. Test a small price increase (or bundle 
  with a higher-margin item like Cake) rather than discounting — it's already 
  selling without a promo.
- Salad and Cake carry revenue. Feature them in Thursday/Friday promotions, 
  when spend is already highest.
- Exclude the 31st from daily trend analysis, or analyze weekly instead — 
  it distorts the pattern.

-- What I'd do differently
- Ask the question *before* cleaning
- Move to SQL for exploration next time