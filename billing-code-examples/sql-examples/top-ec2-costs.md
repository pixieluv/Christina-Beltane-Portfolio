# Top 10 EC2 Instance Costs

### **The Business Problem**

Amazon EC2 is often the largest and most complex component of cloud spend. To effectively optimize it, we needed to move beyond the high-level total and identify the specific *types* of EC2 usage (e.g., instance hours for a specific family, data transfer, EBS volumes) that were contributing the most to the bill.

### **The Approach**

This query filters the entire AWS Cost and Usage Report (CUR) for records specifically related to "AmazonEC2". It then groups the data by the `line_item_line_item_description`, which provides a granular breakdown of the specific usage type. By summing the cost for each type and limiting the result to the top 10, this query provides a highly focused and actionable list for deeper cost analysis.

### **The SQL Query**

```sql
-- Select the product code and the detailed usage description.
SELECT
    line_item_product_code,
    line_item_line_item_description,
    -- Sum the costs for each unique usage type.
    round(sum(line_item_unblended_cost), 2) AS cost
FROM
    your-table.cost-and-usage-reports
-- Filter for records related to Amazon EC2 within a specific time period.
WHERE
    line_item_product_code LIKE '%AmazonEC2%'
    AND month = '1'
    AND year = '2025'
-- Group by the unique usage types to aggregate costs.
GROUP BY
    line_item_product_code,
    line_item_line_item_description
-- Order to find the highest costs first.
ORDER BY
    cost DESC
-- Limit to the top 10 most expensive items.
LIMIT 10;