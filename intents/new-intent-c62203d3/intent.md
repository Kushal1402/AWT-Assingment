# Domain Summary: Salesforce Sales Cloud

## Overview
This domain contains Salesforce Sales Cloud data for comprehensive sales operations analysis.

## Source Database
- **salesforce_sales_cloud.db** - Bronze layer source data

## Key Entities (15 Tables)

### Core Sales Objects
- **Account** - Customer and partner organizations (31 fields)
- **Contact** - Individual contacts at accounts (24 fields)
- **Lead** - Prospective customers (30 fields)
- **Opportunity** - Sales deals and pipeline (25 fields)

### Product & Pricing
- **Product2** - Product catalog
- **Pricebook2** - Pricing structures
- **PricebookEntry** - Product pricing entries
- **OpportunityLineItem** - Products on opportunities
- **Quote** - Customer quotes

### Marketing & Engagement
- **Campaign** - Marketing campaigns with ROI metrics
- **CampaignMember** - Campaign participation tracking

### Activity & History
- **Task** - Activities and follow-ups
- **OpportunityHistory** - Opportunity stage changes
- **OpportunityContactRole** - Contact roles in deals

### System
- **User** - Salesforce users and ownership

## Use Cases
- Sales pipeline and forecasting analysis
- Campaign ROI and marketing attribution
- Customer relationship tracking
- Product and pricing analytics
- Sales team performance metrics
