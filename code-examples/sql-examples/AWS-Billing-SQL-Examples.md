# Introduction

This document contains a collection of SQL queries I have written to analyze cloud infrastructure costs, resource utilization, and operational health. Each query is presented as a mini-case study, outlining the business problem, the analytical approach, and the commented SQL code used to generate the insights.

> \[!NOTE\]
> The table and column names (`your-table.cost-and-usage-reports`, `line_item_product_code`, etc.) have been generalized for this public portfolio but reflect the structure of standard AWS Cost and Usage Reports (CUR).

---

### **1. Top 5 AWS Product Spend by Month**

* **The Business Problem:** We needed to quickly identify our biggest areas of cloud expenditure on a monthly basis to focus our cost optimization efforts effectively.
* **The Approach:** This query groups all costs by the AWS product code for a specific month, calculates the total cost for each product, and orders the results to show the top 5 highest spenders.

```sql
-- Select the year, month, and product code for grouping.
SELECT
    year,
    month,
    line_item_product_code,
    -- Sum the unblended cost and round to two decimal places for readability.
    round(sum(line_item_unblended_cost), 2) AS cost
FROM
    your-table.cost-and-usage-reports
-- Filter for a specific month and year to analyze.
WHERE
    month = '1' AND year = '2025'
-- Group the results to aggregate costs by product.
GROUP BY
    year,
    month,
    line_item_product_code
-- Order the results to find the highest costs first.
ORDER BY
    cost DESC
-- Limit the output to the top 5 spenders.
LIMIT 5;

---

### **2. Service Tagging Status by Account**

* **The Business Problem:** To drive financial accountability, we needed to track the adoption of our resource tagging policy. We needed to know what percentage of resources in a given AWS account were correctly tagged with a "service" tag.
* **The Approach:** This query focuses on a single AWS account and product. It counts the total number of resources, how many have a service tag, how many are missing one, and then calculates the completion percentage. This provides a clear, actionable metric for engineering teams.

```sql
-- Select the time period and account/product for analysis.
SELECT
    year,
    month,
    line_item_usage_account_id AS awsAccount,
    line_item_product_code AS awsProduct,
    -- Count resources where the service tag is present.
    COUNT(CASE WHEN resource_tags_user_service != '' THEN 1 END) AS serviceTagComplete,
    -- Count resources where the service tag is missing.
    COUNT(CASE WHEN resource_tags_user_service = '' THEN 1 END) AS serviceTagMissing,
    -- Count all unique resources.
    COUNT(CASE WHEN line_item_resource_id <> '' THEN 1 END) AS resourceCount,
    -- Calculate the completion percentage.
    ROUND((serviceTagComplete * 100) / resourceCount, 0) AS Tag_Complete_Percent
FROM
    your-table.cost-and-usage-reports
-- Filter for a specific time and account, and only include actual resources.
WHERE
    month = '1' AND year = '2025'
    AND awsAccount = '123456789012' -- Example AWS Account ID
    AND line_item_resource_id <> ''
-- Group the results for aggregation.
GROUP BY
    year,
    month,
    awsAccount,
    awsProduct
-- Order by the number of missing tags to prioritize the biggest problems.
ORDER BY
    serviceTagMissing DESC;
```
---

### **3. Top 10 EC2 Instance Costs**

* **The Business Problem:** Amazon EC2 is often the largest component of cloud spend. We needed to identify the specific types of EC2 usage (e.g., instance hours, data transfer) that were contributing the most to the bill.
* **The Approach:** This query filters all usage data for records related to "AmazonEC2", groups it by the specific line item description (which describes the type of usage), and sums the cost to find the top 10 most expensive items.

```sql
-- Select the product code and the detailed usage description.
SELECT
    line_item_product_code,
    line_item_line_item_description,
    -- Sum the costs for each usage type.
    round(sum(line_item_unblended_cost), 2) AS cost
FROM
    your-table.cost-and-usage-reports
-- Filter for records related to Amazon EC2 within a specific time period.
WHERE
    line_item_product_code LIKE '%AmazonEC2%'
    AND month = '1'
    AND year = '2025'
-- Group by the unique usage types.
GROUP BY
    line_item_product_code,
    line_item_line_item_description
-- Order to find the highest costs.
ORDER BY
    cost DESC
-- Limit to the top 10.
LIMIT 10;
```
---

### **4. Kubernetes Cluster Spend Summary**

* **The Business Problem:** We needed to understand the total infrastructure cost associated with our Kubernetes clusters, which were identified by a specific resource tag.
* **The Approach:** This query filters the entire cost and usage report for resources that have the `resource_tags_user_service` set to 'kubernetes'. It then groups these resources by their specific cluster name (`resource_tags_user_kubernetes_cluster`) to provide a cost-per-cluster summary.

```sql
-- Select the tags that identify the service and cluster.
SELECT
    resource_tags_user_service,
    resource_tags_user_kubernetes_cluster,
    -- Sum the key cost and usage metrics for each cluster.
    ROUND(SUM(line_item_usage_amount), 0) AS Usage_Total,
    ROUND(SUM(line_item_blended_cost), 2) AS Unblended_Cost,
    ROUND(SUM(line_item_blended_cost + discount_total_discount), 2) AS Total_Cost
FROM
    your-table.cost-and-usage-reports
-- Filter for actual resources within a specific month that are tagged as 'kubernetes'.
WHERE
    line_item_resource_id <> ''
    AND month = '1'
    AND year = '2025'
    AND resource_tags_user_service = 'kubernetes'
-- Group by cluster to aggregate the costs.
GROUP BY
    resource_tags_user_kubernetes_cluster,
    resource_tags_user_service
-- Order by cluster name for readability.
ORDER BY
    resource_tags_user_kubernetes_cluster;
```
---

### **5. Savings Plan Coverage Analysis**

* **The Business Problem:** To ensure we were maximizing our cost-saving commitments with AWS, we needed to analyze which resources were being correctly covered by our Savings Plans.
* **The Approach:** This query filters the cost and usage report for line items specifically marked as `SavingsPlanCoveredUsage`. It then groups this data to show which accounts and product types are benefiting from the plan, comparing the on-demand cost to the effective cost paid under the plan.

```sql
-- Select identifying information about the billing period, account, and Savings Plan.
SELECT
    bill_billing_period_start_date,
    line_item_usage_account_id,
    savings_plan_savings_plan_a_r_n,
    line_item_product_code,
    line_item_usage_type,
    -- Sum the usage amount.
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