## **Kubernetes Cluster Spend Summary**
---

### **The Business Problem**

As our use of containerization grew, we needed to understand the total infrastructure cost associated with our Kubernetes clusters. Since pods and nodes are ephemeral, tracking this spend requires a robust tagging strategy. This query provides a summary of costs for all resources that have been correctly tagged as belonging to a specific Kubernetes cluster.

### **The Approach**

This query filters the entire AWS Cost and Usage Report (CUR) for resources that have the `resource_tags_user_service` set to 'kubernetes'. It then groups these resources by their specific cluster name (found in the `resource_tags_user_kubernetes_cluster` tag) to provide a clear, cost-per-cluster summary. This allows for direct chargeback and helps identify which clusters are the most expensive to operate.

### **The SQL Query**

```sql
-- Select the tags that identify the service and cluster.
SELECT
    resource_tags_user_service,
    resource_tags_user_kubernetes_cluster,
    -- Sum the key cost and usage metrics for each cluster.
    ROUND(SUM(line_item_usage_amount), 0) AS Usage_Total,
    ROUND(SUM(line_item_blended_cost), 2) AS Unblended_Cost,
    -- Calculate total cost including discounts.
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