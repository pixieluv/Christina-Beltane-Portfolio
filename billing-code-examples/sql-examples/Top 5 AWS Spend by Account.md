### **The Business Problem**

After identifying the top spending products, the next logical question is, "Which teams or business units are driving that spend?" This query helps answer that by identifying the top 5 highest-spending AWS accounts for a given month. In many organizations, accounts are mapped to specific teams, environments (e.g., production, staging), or business units, making this a critical tool for chargeback and accountability.

### **The Approach**

This query is similar to the product spend analysis but changes the grouping dimension. It filters the AWS Cost and Usage Report (CUR) for a specific month, groups all costs by the line\_item\_usage\_account\_id, and uses a LIMIT 5 clause to return a "leaderboard" of the highest-spending accounts. This provides an immediate, actionable list for targeted FinOps conversations.

### **The SQL Query**

\-- Select the usage account ID for grouping.  
SELECT  
    line\_item\_usage\_account\_id,  
    \-- Sum the unblended cost and round for readability.  
    round(sum(line\_item\_unblended\_cost), 2\) AS cost  
FROM  
    your-table.cost-and-usage-reports  
\-- Filter for a specific month and year to analyze.  
WHERE  
    month \= '1'  
    AND year \= '2025'  
\-- Group the results to aggregate costs by account.  
GROUP BY  
    line\_item\_usage\_account\_id  
\-- Order the results to find the highest costs first.  
ORDER BY  
    cost DESC  
\-- Limit the output to the top 5 spenders.  
LIMIT 5;

### **Future Enhancements**

* \[ \] Add screenshot of the real-world query output for visual proof.