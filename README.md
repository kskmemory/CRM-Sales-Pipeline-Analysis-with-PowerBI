# Predictive Analytics for CRM Sales Performance by Sales Pipeline
The dataset represents a comprehensive sales pipeline for a company specializing in computer hardware. It consists of four key tables:

Accounts: Information about customer accounts, including their size, location, and other demographic details.

Products: Details of the hardware products offered, including specifications and categories.

Sales Teams: Information about the company’s sales representatives and their regional or team assignments.

Sales Pipeline: Tracks sales opportunities, including deal stages, values, and timelines.

Additionally, a Meta Data table provides descriptions and context for the columns across all tables, ensuring clarity in data interpretation. This dataset supports insights into sales performance, customer segmentation, and team effectiveness.



# CRM Sales Pipeline Analysis with PowerBI
<img width="1160" height="650" alt="image" src="https://github.com/user-attachments/assets/cb7d5e22-e5c4-455c-a3f3-fbe4c35c353e" />


# DAX Expressions used in the project :

Conversion Percentage = 
DIVIDE(
    COUNTROWS(FILTER('TableName', 'TableName'[Deal Stage] = "Won")),
    COUNTROWS('TableName')
) * 100
To calculate the average closed deal value in Power BI, you can use the following DAX formula. This assumes that your dataset has a column representing the deal value (e.g., Deal Value) and a column for the deal stage (e.g., Deal Stage), where closed deals are marked as "Won".
Avg Closed Deal Value = 
AVERAGEX(
    FILTER(
        'TableName',
        'TableName'[Deal Stage] = "Won"
    ),
    'TableName'[Deal Value]
)
Churned Customers = 
COUNTROWS(
    FILTER(
        sales_pipeline,
        sales_pipeline[Deal Stage] = "Lost"
    )
)
Average Close Days = 
AVERAGEX(
    FILTER(
        sales_pipeline,
        sales_pipeline[Deal Stage] = "Won"
    ),
    DATEDIFF(sales_pipeline[Start Date], sales_pipeline[Close Date], DAY)
)
 calculated column
Account Size = 
SWITCH(
    TRUE(),
    accounts[employees] <= 10, "Micro",
    accounts[employees] >= 11 && accounts[employees] <= 200, "Small",
    accounts[employees] >= 201 && accounts[employees] <= 500, "Medium",
    accounts[employees] >= 501 && accounts[employees] <= 1000, "Large",
    accounts[employees] > 1000, "Enterprise",
    "Unknown"
)
