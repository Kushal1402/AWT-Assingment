# Execution Plan: Product Financial Analysis - Last 2 Months

## Data Architecture

### Staging Layer
**stg_opportunity_line_items.sql**
- Source: `OpportunityLineItem` joined with `Opportunity` and `Product2`
- Grain: One row per opportunity line item
- Key transformations:
  - Calculate gross revenue (Quantity × UnitPrice)
  - Calculate net revenue (TotalPrice after discount)
  - Calculate discount amount and discount percentage
  - Determine analysis_date (ServiceDate or CloseDate for won opportunities)
  - Filter to date range: 2025-12-01 to 2026-01-31
  - Extract month/year for time-based analysis
- Key columns:
  - line_item_id, opportunity_id, product_id
  - product_name, product_code, product_family
  - quantity, unit_price, total_price, discount_pct, discount_amount
  - gross_revenue, net_revenue
  - analysis_date, analysis_month, analysis_year
  - stage_name, is_won

### Mart Layer
**mart_product_financial_analysis.sql**
- Source: `stg_opportunity_line_items`
- Grain: One row per product with aggregated financial metrics
- Key metrics:
  - Total quantity sold
  - Total gross revenue
  - Total net revenue
  - Total discount amount
  - Average unit price
  - Average discount percentage
  - Number of transactions
  - Revenue rank within product family
- Dimensions: product_name, product_code, product_family

**mart_product_family_performance.sql**
- Source: `stg_opportunity_line_items`
- Grain: One row per product family
- Key metrics:
  - Total quantity sold by family
  - Total gross revenue by family
  - Total net revenue by family
  - Total discount amount by family
  - Average discount percentage by family
  - Product count per family
  - Revenue contribution percentage

**mart_monthly_product_trends.sql**
- Source: `stg_opportunity_line_items`
- Grain: One row per product per month
- Key metrics:
  - Monthly quantity sold
  - Monthly gross revenue
  - Monthly net revenue
  - Month-over-month growth rates
- Dimensions: product_name, product_code, analysis_month, analysis_year

## Implementation Steps

### Phase 1: Staging Model
1. Create `stg_opportunity_line_items.sql` with:
   - Join OpportunityLineItem → Opportunity → Product2
   - Calculate revenue metrics and discount analytics
   - Apply date filters (Dec 2025 - Jan 2026)
   - Add time dimensions (month, year)

### Phase 2: Mart Models
2. Create `mart_product_financial_analysis.sql`:
   - Aggregate metrics by product
   - Calculate rankings and performance indicators

3. Create `mart_product_family_performance.sql`:
   - Aggregate metrics by product family
   - Calculate family-level contribution percentages

4. Create `mart_monthly_product_trends.sql`:
   - Aggregate metrics by product and month
   - Calculate month-over-month growth

### Phase 3: Validation
5. Validate models with `dbt compile` and `dbt run`
6. Query results to verify:
   - Total revenue matches source data
   - All products from the time period are included
   - Discount calculations are accurate
   - Monthly totals reconcile

## Key Business Logic

### Date Logic
```sql
CASE
  WHEN oli.ServiceDate IS NOT NULL THEN oli.ServiceDate
  WHEN o.IsWon = 1 AND o.CloseDate IS NOT NULL THEN o.CloseDate
  ELSE NULL
END as analysis_date
```

### Revenue Calculations
- **Gross Revenue**: `Quantity × UnitPrice`
- **Net Revenue**: `TotalPrice` (already includes discount)
- **Discount Amount**: `Gross Revenue - Net Revenue`
- **Discount Percentage**: `(Discount Amount / Gross Revenue) × 100`

### Time Period Filter
```sql
WHERE analysis_date >= '2025-12-01'
  AND analysis_date <= '2026-01-31'
  AND o.IsWon = 1
```

## Expected Outputs
1. **Product-level analysis**: ~15-20 unique products with detailed financials
2. **Product family analysis**: 5 families (Cameras, Controllers, IoT Devices, Services, Accessories)
3. **Monthly trends**: 2 months of time-series data per product
4. **Key insights**: Top revenue generators, discount patterns, growth trends

## Testing & Validation
- Row count validation: Verify staging model captures all line items in date range
- Revenue reconciliation: Sum of mart revenue = sum of staging revenue
- Discount logic validation: Spot-check discount calculations against source
- Date range validation: Ensure no records outside Dec 2025 - Jan 2026
