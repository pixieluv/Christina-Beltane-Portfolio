# Savings Plan Coverage Analysis

### **The Business Problem**

To ensure we were maximizing our cost-saving commitments with AWS, we needed to analyze which resources were being correctly covered by our Savings Plans. This query provides a detailed breakdown of the usage that received a Savings Plan discount, comparing the on-demand cost to the actual effective cost paid.

### **The Approach**

This query filters the AWS Cost and Usage Report (CUR) for line items specifically marked as `SavingsPlanCoveredUsage`. It then groups this data by account, plan ARN, product, and usage type to provide a granular view of where the savings are being applied. This is critical for validating that the correct resources are covered and for identifying opportunities to expand Savings Plan coverage.

### **The SQL Query**

```sql
-- Select identifying information about the billing period, account, and Savings Plan.
SELECT
    bill_billing_period_start_date,
    line_item_usage_account_id,
    savings_plan_savings_plan_a_r_n,
    line_item_product_code,
    line_item_usage_type,
    -- Sum the usage amount for the covered resources.
    sum(line_item_usage_amount) AS Usage,
    -- Sum the cost if we had paid on-demand prices.
    ROUND(sum(pricing_public_on_demand_cost), 2) AS On_Demand_Cost,
    -- Sum the actual cost we paid with the Savings Plan.
    ROUND(sum(savings_plan_savings_plan_effective_cost), 2) AS Savings_Plan_Cost
FROM
    your-table.cost-and-usage-reports
-- Filter for only the usage that was covered by a Savings Plan in a specific period.
WHERE
    line_item_line_item_Type LIKE 'SavingsPlanCoveredUsage'
    AND month = '1'
    AND year = '2025'
-- Group by various attributes to get a detailed breakdown.
GROUP BY
    bill_billing_period_start_date,
    line_item_usage_account_id,
    savings_plan_savings_plan_a_r_n,
    line_item_product_code,
    line_item_usage_type
LIMIT 20;