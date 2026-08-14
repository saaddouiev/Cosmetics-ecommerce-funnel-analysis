# REES46 E-commerce Funnel & Cart Abandonment Analysis

## The question
Where in the purchase funnel are cosmetics e-commerce users dropping off, 
and is cart abandonment recoverable?

## Primary Metric

**User-level Purchase Conversion Rate**: % of distinct users who completed ≥1 purchase, out of all distinct users who viewed a product, across the full dataset window.

## Setup
- Dataset: REES46 open e-commerce behavior data (cosmetics category)
- Tools: Python (Pandas, Plotly), PostgreSQL
- Approach: funnel conversion, purchase timing, cart sit-time, and 
  true-abandonment analysis, each isolated to a single clearly defined 
  population to keep metrics comparable

## Key findings

### 1- A Multi-Session, 11-Day Purchase Journey

<img width="1298" height="450" alt="funnel" src="https://github.com/user-attachments/assets/7b492860-597a-458c-9ba2-eb7102a56702" />

- **6.92%** overall user-level funnel conversion
- Session-level cart→purchase conversion is only **15.36%**, most 
  purchases happen in a *later* session, not the one where the item 
  was added to cart
- Average full purchase journey: **~11 days**

### 2- Product-Specific Recovery Isn't Possible

  <img width="1298" height="450" alt="newplot" src="https://github.com/user-attachments/assets/4714b64d-1b66-44e0-8127-634cd882f021" />

- Items sit in cart **8.2 days** on average before removal
- Only **1.44%** of users who truly abandon a product (strict single-
  population definition) ever return to buy that same product
- ~30% of abandoners buy *something* eventually but not the item 
  they abandoned

<img width="1298" height="450" alt="what_happens_to_abandoned_items" src="https://github.com/user-attachments/assets/0064029a-0b6f-4c44-8264-8a7cfe4d4eac" />

## Two theories I tested and disproved
- Unbranded traffic drag down conversion: not supported by the data
- High-volume brands underperform on conversion:  not supported either

## The insight
This isn't a funnel problem, it's a return-window problem. 
Customers aren't rejecting the product, only 15.36% of cart-adds convert in the same session, and the ones who do come back mostly buy something else (1.44% return for the exact item, 30% buy anything within 11 days). The cart itself becomes irrelevant faster than the customer does.

## Recommendations

| Priority | Recommendation | Stakeholder Team |
|---|---|---|
| 1 | Re-engagement should target the return, not the SKU, broad "welcome back" triggers, category recs, and generic incentives inside the 8-day cart-sit window reach the 30% who are actually convertible; product-specific reminders are optimizing for a population that's already down to 1.44% | Marketing |
| 2 | Cart persistence is a technical lever, not just a marketing one, with cross-session purchase as the dominant purchase journey, any friction that breaks cart continuity across devices (no persistence, no account-linking prompt at add-to-cart) is quietly harming demand that's still there roughly a week later | Product |
  
<img width="1298" height="350" alt="strategic_11days_window" src="https://github.com/user-attachments/assets/66ce1d7f-fa0c-40e3-bbd3-c90c40455405" />

## Files
- `/sql/funnel_analysis.sql` — full query set, ordered narratively 
  (funnel → timing → cart sit-time → true abandonment)
- `/charts/` — interactive Plotly exports (funnel, cart removal/recovery, 
  session-level Sankey)
