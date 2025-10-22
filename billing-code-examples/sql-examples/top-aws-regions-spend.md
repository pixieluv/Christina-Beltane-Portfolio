## **Top 3 AWS Regions by Spend**
---

### **The Business Problem**

For a global company, understanding the geographical distribution of cloud costs is crucial for financial planning, identifying performance bottlenecks, and making strategic decisions about data residency and latency. This query provides a high-level view of where infrastructure spending is concentrated by identifying the top 3 highest-spending AWS Availability Zones for a given month.

### **The Approach**

This query filters the AWS Cost and Usage Report (CUR) for a specific month and excludes any entries where an Availability Zone is not specified. It then groups all costs by the `line_item_availability_zone` identifier and uses a `LIMIT 3` clause to return a "leaderboard" of the most expensive zones. This helps leadership quickly understand where the bulk of infrastructure is deployed and where costs are concentrated globally.

### **The SQL Query**

```sql
-- Select the year, month, and availability zone for grouping.
SELECT
    year,
    month,
    line_item_availability_zone,
    -- Sum the unblended cost and round for readability.
    round(sum(line_item_unblended_cost), 2) AS cost
FROM
    your-table.cost-and-usage-reports
-- Filter for a specific month and year, excluding null/empty zones.
WHERE
    month = '1'
    AND year = '2025'
    AND line_item_availability_zone != ''
-- Group the results to aggregate costs by availability zone.
GROUP BY
    year,
    month,
    line_item_availability_zone
-- Order the results to find the highest costs first.
ORDER BY
    cost DESC
-- Limit the output to the top 3 spending zones.
LIMIT 3;