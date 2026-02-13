# Customer Laptop Purchase Orders - Test Data Summary

## Overview
This dataset contains 25 sample laptop purchase orders for testing and analysis purposes.

**File**: `customer_laptop_orders.csv`
**Records**: 25 orders
**Date Range**: January 15, 2024 - March 15, 2024
**Total Fields**: 30 columns

---

## Data Structure

### Customer Information (7 fields)
- customer_id, customer_name, customer_email, customer_phone
- customer_city, customer_state, customer_country
- **Coverage**: 25 unique customers across 20 US cities

### Order Details (8 fields)
- order_id, order_date, quantity, delivery_date
- payment_method, payment_status, order_status, warranty_years
- **Order IDs**: PO-2024-001 through PO-2024-025

### Laptop Specifications (8 fields)
- laptop_brand, laptop_model, processor, ram_gb
- storage_type, storage_gb, screen_size_inches, graphics_card, operating_system
- **Brands**: Dell (5), Apple (6), Lenovo (5), HP (6), ASUS (3), MSI (1), Acer (1)

### Financial Details (7 fields)
- unit_price, discount_percent, tax_percent, shipping_cost, total_amount
- **Price Range**: $549.99 - $3,499.00
- **Discount Range**: 0% - 15%
- **Tax Range**: 0% - 10%

### Sales Information (2 fields)
- sales_rep_id, sales_rep_name
- **Sales Reps**: Sarah Johnson (REP-001), Michael Chen (REP-002), David Park (REP-003)

---

## Key Statistics

### Order Distribution
- **Total Orders**: 25
- **Total Units Sold**: 51 laptops
- **Average Order Value**: ~$1,800
- **Total Revenue**: ~$56,000

### Order Status Breakdown
- **Delivered**: 16 orders (64%)
- **Shipped**: 4 orders (16%)
- **Processing**: 4 orders (16%)
- **Pending**: 1 order (4%)

### Payment Methods
- **Credit Card**: 15 orders (60%)
- **PayPal**: 4 orders (16%)
- **Purchase Order**: 3 orders (12%)
- **Wire Transfer**: 3 orders (12%)

### Payment Status
- **Paid**: 24 orders (96%)
- **Pending**: 1 order (4%)

### Brand Popularity
1. HP - 6 orders (24%)
2. Apple - 6 orders (24%)
3. Dell - 5 orders (20%)
4. Lenovo - 5 orders (20%)
5. ASUS - 3 orders (12%)

### Geographic Distribution
**Top States by Order Volume:**
- Texas (TX): 5 orders
- California (CA): 4 orders
- Pennsylvania (PA), Ohio (OH), North Carolina (NC): 1 order each

### Warranty Coverage
- **1 Year**: 7 laptops (Apple products)
- **2 Years**: 13 laptops
- **3 Years**: 5 laptops (business-grade models)

### Processor Types
- **Intel**: 17 laptops (68%)
- **Apple Silicon (M2/M3)**: 6 laptops (24%)
- **AMD**: 4 laptops (16%)

### RAM Configuration
- **8 GB**: 6 laptops
- **16 GB**: 16 laptops (most common)
- **32 GB**: 2 laptops
- **36 GB**: 1 laptop (high-end MacBook Pro)

---

## Use Cases

This dataset is ideal for:
- **Sales Analysis**: Revenue trends, rep performance, discount effectiveness
- **Customer Segmentation**: Geographic distribution, purchase patterns
- **Inventory Planning**: Brand/model popularity, specification preferences
- **Financial Reporting**: Tax calculations, shipping costs, payment methods
- **Operational Metrics**: Order fulfillment times, warranty tracking
- **Data Pipeline Testing**: ETL processes, data quality checks, transformations

---

## Data Quality Notes

- All records have complete data (no nulls in required fields)
- Email addresses follow standard format: firstname.lastname@email.com
- Phone numbers use consistent format: 555-01XX
- Order IDs follow sequential pattern: PO-2024-XXX
- Dates are realistic with logical delivery timelines (7-14 days post-order)
- Pricing reflects realistic market values for each laptop configuration
- Tax rates vary by state, reflecting actual US state tax rates

---

**Generated**: February 13, 2026
**Purpose**: Testing and validation for data analytics pipeline
