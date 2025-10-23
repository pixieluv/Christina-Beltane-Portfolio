#  Percentage of tagged versus untagged resources in AWS

### **The Business Problem**

Cost accountability is impossible without accurate data. A foundational step in any FinOps practice is ensuring all cloud resources are "tagged" with the name of the service or team that owns them. This query is designed to measure the success of a tagging initiative by calculating the percentage of tagged versus untagged resources for a specific AWS account.

### **The Approach**

This query focuses on a single AWS account and groups resources by `line_item_product_code`. Using conditional `COUNT` functions, it calculates the number of resources with a service tag and those without. It then calculates the completion percentage, providing a clear metric to track the progress of the tagging program and identify which teams or products need the most attention.

### **The SQL Query**

```sql
-- Select the identifiers for our report: year, month, account, and product.
SELECT
    year,
    month,
    line_item_usage_account_id AS awsAccount,
    line_item_product_code AS awsProduct,

    -- Conditionally count resources that have a service tag applied.
    COUNT(
        CASE WHEN resource_tags_user_service != '' THEN 1
        END
    ) AS serviceTagComplete,

    -- Conditionally count resources where the service tag is missing.
    COUNT(
        CASE WHEN resource_tags_user_service = '' THEN 1
        END
    ) AS serviceTagMissing,

    -- Count the total number of resources that have a resource ID.
    COUNT(
        CASE WHEN line_item_resource_id <> '' THEN 1
        END
    ) AS resourceCount,

    -- Calculate the percentage of resources that are correctly tagged.
    ROUND((serviceTagComplete * 100) / resourceCount, 0) AS Tag_Complete_Percent,
    ROUND((serviceTagMissing * 100) / resourceCount, 0) AS Tag_Missing_Percent

-- Specify the data source, in this case the AWS Cost and Usage Report table.
FROM
    your-table.cost-and-usage-reports -- Generalized table name

-- Filter the data to focus on a specific time period and account for a targeted analysis.
WHERE
    month = '1' AND year = '2025' -- Example time period
    AND awsAccount = '123456789012' -- Example Account ID for targeted reporting
    AND line_item_resource_id <> '' -- Exclude line items that are not actual resources

-- Group the results to aggregate the counts by product within the specified account.
GROUP BY
    year,
    month,
    awsAccount,
    awsProduct

-- Order the results to immediately highlight the products with the most missing tags.
ORDER BY
    serviceTagMissing DESC;