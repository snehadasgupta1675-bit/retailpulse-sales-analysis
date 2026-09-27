# RETAILPULSE

## Sales Performance & Customer Insights Analytics System

### Data Analysis with Python — Project Report

---

# 1. Executive Overview

RETAILPULSE is a retail sales performance and customer insights analytics project developed using Python and its major data-analysis libraries.

The purpose of this project is to transform raw retail transaction data into meaningful business information that can help a business understand its sales performance, profitability, products, regions, customers, and sales trends over time.

The project follows a complete business data-analysis workflow:

**DATA → CLEAN → ANALYZE → VISUALIZE → INTERPRET → RECOMMEND**

The analysis was performed using Python in Google Colab with Pandas, NumPy, Matplotlib, and Seaborn.

The project covers sales performance, category performance, product performance, regional performance, customer performance, monthly sales trends, business questions, key insights, recommendations, Pareto analysis, and an executive summary.

---

# 2. Project Background

A retail business generates a large amount of transaction data through customer orders. Although the raw data contains valuable information, the information is not immediately useful for management until it is properly cleaned, analyzed, visualized, and interpreted.

The RETAILPULSE project was designed to answer practical business questions such as:

* Which products generate the most sales?
* Which categories perform best?
* Which categories generate the most profit?
* Which regions generate the most revenue?
* Which regions have weaker profitability?
* Which customers contribute the most revenue?
* When are sales highest?
* Are the highest-sales categories also the highest-profit categories?
* Where are the major business opportunities?
* What areas should management investigate further?

The project therefore focuses not only on writing Python code, but on using Python to answer real business questions.

---

# 3. Project Objectives

The major objectives of RETAILPULSE are:

1. Understand the structure and quality of the retail dataset.
2. Clean and validate the available transaction data.
3. Calculate total sales and total profit.
4. Analyze sales performance by category.
5. Analyze profit performance by category.
6. Analyze sales performance by region.
7. Identify regions with weaker profitability.
8. Identify the top products by sales.
9. Identify the highest-value customers by revenue.
10. Analyze monthly sales trends.
11. Answer ten defined business questions.
12. Identify important business patterns.
13. Perform additional Pareto analysis.
14. Create meaningful visualizations.
15. Develop practical business recommendations.
16. Produce an executive-level summary of the analysis.

---

# 4. Tools and Technologies

The project was developed using the following tools and technologies.

## Python

Python was used as the primary programming language for data loading, cleaning, transformation, analysis, calculations, and visualization.

## Pandas

Pandas was used for:

* Loading the CSV dataset
* Inspecting the data
* Cleaning data
* Grouping records
* Calculating totals
* Ranking products and customers
* Performing time-based analysis
* Creating summary tables

## NumPy

NumPy was imported as a supporting numerical-analysis library.

## Matplotlib

Matplotlib was used to create visualizations including:

* Revenue by category
* Profit by category
* Revenue by region
* Profit by region
* Top products
* Top customers
* Monthly sales trends

## Seaborn

Seaborn was included as a visualization library and can be used to extend the analytical visualizations.

## Google Colab

Google Colab was used as the development environment for the complete Python notebook.

---

# 5. Dataset Overview

The RETAILPULSE analysis was performed using a synthetic practice retail-sales dataset.

The dataset contains:

* **5,000 transaction records**
* **14 columns**

The dataset contains information about orders, customers, products, regions, quantities, sales, discounts, profit, and payment methods.

The columns are:

| Column        | Description             |
| ------------- | ----------------------- |
| Order_ID      | Unique order identifier |
| Order_Date    | Date of the order       |
| Customer_ID   | Customer identifier     |
| Customer_Name | Customer name           |
| Category      | Main product category   |
| Sub_Category  | Product sub-category    |
| Product       | Product name            |
| Region        | Sales region            |
| City          | Customer/order city     |
| Quantity      | Quantity purchased      |
| Sales         | Sales/revenue value     |
| Discount      | Discount applied        |
| Profit        | Profit generated        |
| Payment_Mode  | Payment method          |

The dataset provides enough information to analyze sales, profit, products, customers, regions, and time-based performance.

---

# 6. Dataset Loading

The dataset was loaded into a Pandas DataFrame using:

```python
df = pd.read_csv('/content/RETAILPULSE_sales_dataset.csv')
```

After loading the dataset, the first records were inspected using:

```python
df.head()
```

This allowed the structure and sample values of the dataset to be examined before beginning the analysis.

---

# 7. Dataset Structure

The shape of the dataset was examined using:

```python
df.shape
```

The dataset contains:

* 5,000 rows
* 14 columns

The column names were examined using:

```python
df.columns
```

The data types and non-null counts were examined using:

```python
df.info()
```

This helped identify numeric columns, categorical columns, and date-related information.

---

# 8. Data Cleaning and Validation

Data cleaning is an important part of the RETAILPULSE workflow.

Before performing business analysis, the dataset was checked for missing values, duplicate records, incorrect data types, and invalid values.

## 8.1 Missing Values

Missing values were checked using:

```python
df.isnull().sum()
```

This ensured that missing information could be identified before performing calculations.

## 8.2 Duplicate Records

Duplicate rows were checked using:

```python
df.duplicated().sum()
```

The dataset did not contain duplicate records requiring removal.

## 8.3 Date Conversion

The Order_Date column was converted into a proper datetime format:

```python
df['Order_Date'] = pd.to_datetime(df['Order_Date'])
```

This was necessary for monthly and time-series analysis.

## 8.4 Numeric Validation

The main numeric columns were examined using:

```python
df[['Quantity', 'Sales', 'Profit', 'Discount']].describe()
```

This provided descriptive statistics including count, mean, standard deviation, minimum, maximum, and quartile values.

## 8.5 Negative Sales and Quantity Checks

Potentially invalid negative sales and quantity values were checked using:

```python
(df['Sales'] < 0).sum(), (df['Quantity'] < 0).sum()
```

The analysis confirmed that there were no negative Sales or Quantity values.

## 8.6 Discount Validation

The minimum and maximum discount values were examined using:

```python
df['Discount'].min(), df['Discount'].max()
```

This helped verify that discount values were within the expected range.

---

# 9. Exploratory Data Analysis

After data cleaning, exploratory data analysis was performed to understand the overall characteristics of the dataset.

Descriptive statistics were generated using:

```python
df.describe()
```

The analysis examined:

* Quantity
* Sales
* Discount
* Profit

Categorical distributions were also examined.

For example:

```python
df['Category'].value_counts()
```

```python
df['Region'].value_counts()
```

```python
df['Payment_Mode'].value_counts()
```

The number of unique customers was calculated using:

```python
df['Customer_ID'].nunique()
```

The date range of the dataset was also examined:

```python
df['Order_Date'].min(), df['Order_Date'].max()
```

This exploratory stage provided the foundation for the business analysis.

---

# 10. Sales Performance Analysis

Sales performance was analyzed using total revenue and total profit.

## 10.1 Total Revenue

Total revenue was calculated using:

```python
total_revenue = df['Sales'].sum()
```

This represents the total sales value contained in the dataset.

## 10.2 Total Profit

Total profit was calculated using:

```python
total_profit = df['Profit'].sum()
```

This represents the total profit generated across the analyzed transactions.

These two metrics form the foundation of the business-performance analysis.

---

# 11. Revenue by Category

Revenue was grouped by category:

```python
category_revenue = df.groupby('Category')['Sales'].sum().sort_values(ascending=False)
```

This calculation ranks categories according to their total sales.

The category at the top of this ranking represents the category generating the highest revenue in the dataset.

This analysis helps management understand which broad product categories contribute most strongly to sales.

---

# 12. Profit by Category

Profit was analyzed separately:

```python
category_profit = df.groupby('Category')['Profit'].sum().sort_values(ascending=False)
```

This identifies the category generating the highest total profit.

Analyzing revenue and profit separately is important because a category can generate substantial sales without necessarily generating the highest profit.

---

# 13. Revenue and Profit Category Comparison

A combined category comparison table was created:

```python
category_comparison = pd.DataFrame({
    'Total Revenue': category_revenue,
    'Total Profit': category_profit
})
```

This makes it possible to compare sales performance and profitability together.

The analysis also directly compared the highest-revenue category with the highest-profit category.

```python
highest_revenue_category = category_revenue.idxmax()
highest_profit_category = category_profit.idxmax()

print("Highest Revenue Category:", highest_revenue_category)
print("Highest Profit Category:", highest_profit_category)
print("Same Category:", highest_revenue_category == highest_profit_category)
```

This directly answers whether the category with the highest sales is also the category with the highest profit.

---

# 14. Regional Analysis

Regional performance was analyzed to determine where revenue is strongest and where profitability may require further investigation.

## 14.1 Revenue by Region

```python
region_revenue = df.groupby('Region')['Sales'].sum().sort_values(ascending=False)
```

This identifies the region generating the highest total revenue.

## 14.2 Profit by Region

```python
region_profit = df.groupby('Region')['Profit'].sum().sort_values()
```

Sorting profit in ascending order makes it easy to identify the weakest-profit region.

Regional analysis is useful because strong revenue does not automatically mean strong profitability.

---

# 15. Product Analysis

Products were ranked according to total sales.

```python
top_10_products = df.groupby('Product')['Sales'].sum().sort_values(ascending=False).head(10)
```

This produces the top 10 products by sales.

Product analysis helps identify products that contribute significantly to total revenue and may therefore deserve additional attention in areas such as:

* Inventory planning
* Product availability
* Promotions
* Customer targeting
* Sales strategy

---

# 16. Customer Analysis

Customer revenue contribution was analyzed by grouping sales by customer.

```python
top_10_customers = df.groupby('Customer_Name')['Sales'].sum().sort_values(ascending=False).head(10)
```

This produces the top 10 customers by revenue.

High-value customers can be important for customer-retention strategies and relationship management.

---

# 17. Time-Series Analysis

Time-based analysis was performed to understand monthly sales behavior.

A month field was created:

```python
df['Month'] = df['Order_Date'].dt.month_name()
```

Monthly sales were then calculated:

```python
monthly_sales = df.groupby('Month')['Sales'].sum().sort_values(ascending=False)
```

For chronological analysis, monthly sales were also grouped by year-month:

```python
monthly_sales_time = df.groupby(
    df['Order_Date'].dt.to_period('M')
)['Sales'].sum()
```

The month with the highest sales was identified using:

```python
monthly_sales_time.idxmax()
```

This analysis provides insight into sales patterns over time.

---

# 18. Data Visualization

Visualization was used to make the analytical results easier to understand.

## Revenue by Category

A bar chart was created to compare category revenue.

```python
category_revenue.plot(kind='bar', figsize=(8, 5))
plt.title('Revenue by Category')
plt.xlabel('Category')
plt.ylabel('Total Revenue')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

## Profit by Category

A corresponding chart was created to compare category profitability.

## Revenue by Region

Regional revenue was visualized to identify the strongest revenue-generating region.

## Profit by Region

Regional profit was visualized to highlight differences in profitability.

## Top 10 Products

The top 10 products were visualized using a bar chart.

## Top 10 Customers

The top 10 customers by revenue were visualized.

## Monthly Sales Trend

A line chart was created to show sales movement over time.

The project therefore combines numerical analysis with visual interpretation.

---

# 19. Business Questions

The project was specifically designed to answer ten major business questions.

## Q1. What is the total revenue?

The total revenue is calculated by summing the Sales column.

```python
total_revenue = df['Sales'].sum()
```

The exact result is presented in the RETAILPULSE notebook's Business Snapshot and Executive Summary.

---

## Q2. What is the total profit?

Total profit is calculated by summing the Profit column.

```python
total_profit = df['Profit'].sum()
```

The exact result is included in the notebook's Executive Summary.

---

## Q3. Which category generates the most revenue?

The category revenue ranking is:

```python
category_revenue = df.groupby('Category')['Sales'].sum().sort_values(ascending=False)
```

The first category in this ranking is the highest-revenue category.

---

## Q4. Which category generates the most profit?

Profit was grouped by category:

```python
category_profit = df.groupby('Category')['Profit'].sum().sort_values(ascending=False)
```

The first category in this ranking is the highest-profit category.

---

## Q5. Which region generates the most revenue?

Regional revenue was calculated using:

```python
region_revenue = df.groupby('Region')['Sales'].sum().sort_values(ascending=False)
```

The first region in the ranking is the highest-revenue region.

---

## Q6. Which region has the weakest profit performance?

Regional profit was sorted in ascending order:

```python
region_profit = df.groupby('Region')['Profit'].sum().sort_values()
```

The first region represents the weakest total-profit performance.

This does not necessarily mean the region is unsuccessful overall; it identifies the region requiring further profitability investigation.

---

## Q7. What are the top 10 products by sales?

The top products were calculated using:

```python
top_10_products = df.groupby('Product')['Sales'].sum().sort_values(ascending=False).head(10)
```

The notebook contains the complete ranked list.

---

## Q8. Who are the top 10 customers by revenue?

The top customers were calculated using:

```python
top_10_customers = df.groupby('Customer_Name')['Sales'].sum().sort_values(ascending=False).head(10)
```

The notebook contains the complete ranked list.

---

## Q9. Which month had the highest sales?

Monthly sales were calculated using the transaction dates.

```python
monthly_sales_time = df.groupby(
    df['Order_Date'].dt.to_period('M')
)['Sales'].sum()
```

The highest-sales period was identified using:

```python
monthly_sales_time.idxmax()
```

---

## Q10. Does the highest-sales category also have the highest profit?

The project directly compares:

```python
highest_revenue_category = category_revenue.idxmax()
highest_profit_category = category_profit.idxmax()

highest_revenue_category == highest_profit_category
```

This provides a direct answer to the relationship between sales leadership and profit leadership.

---

# 20. Key Insights

The analysis produced several important business insights.

## Insight 1 — Overall Business Performance

Total sales and total profit provide the overall picture of the dataset's financial performance.

The project also calculates:

* Number of orders
* Number of customers
* Average Order Value
* Profit Margin

These metrics are presented together in the Executive Summary.

---

## Insight 2 — Category Performance

Category-level analysis shows that revenue leadership and profit leadership should be examined separately.

The highest-sales category is identified independently from the highest-profit category.

This prevents the assumption that higher revenue automatically means higher profitability.

---

## Insight 3 — Regional Performance

Regional analysis highlights the region generating the most revenue and separately identifies the weakest total-profit region.

This creates an opportunity for further investigation into factors such as:

* Product mix
* Discounting
* Costs
* Customer behavior
* Sales strategy

---

## Insight 4 — Product Performance

The top 10 products represent the products contributing the most sales.

These products can be monitored for:

* Demand
* Availability
* Inventory planning
* Promotions
* Customer targeting

---

## Insight 5 — Customer Performance

The top 10 customers contribute significant revenue and therefore represent an important group for customer-retention analysis.

---

## Insight 6 — Monthly Sales

The time-series analysis identifies the period with the highest sales and provides a visual view of monthly performance.

Monthly trends can support:

* Inventory planning
* Staffing
* Promotions
* Sales planning
* Business forecasting

---

# 21. Pareto Analysis

An additional Pareto analysis was performed as an advanced analytical challenge.

The analysis calculates the proportion of total revenue generated by the top 20% of products.

The code used was:

```python
product_sales = df.groupby('Product')['Sales'].sum().sort_values(ascending=False)

top_20_percent_count = int(len(product_sales) * 0.20)

top_20_products = product_sales.head(top_20_percent_count)

top_20_revenue_share = (
    top_20_products.sum() / product_sales.sum()
) * 100

print("Number of Products:", len(product_sales))
print("Top 20% Product Count:", top_20_percent_count)
print("Revenue Share of Top 20% Products:", top_20_revenue_share)
```

The purpose of this analysis is to understand whether a relatively small group of products contributes a large proportion of total revenue.

This can help management identify products that may deserve particular attention.

---

# 22. Business Snapshot

The RETAILPULSE Executive Summary contains the following business metrics:

### Total Sales

Calculated as the sum of all Sales values.

### Total Profit

Calculated as the sum of all Profit values.

### Orders

Calculated as the number of unique Order_ID values.

```python
orders = df['Order_ID'].nunique()
```

### Customers

Calculated as the number of unique Customer_ID values.

```python
customers = df['Customer_ID'].nunique()
```

### Average Order Value

Calculated as:

```python
average_order_value = total_revenue / orders
```

### Profit Margin

Calculated as:

```python
profit_margin = (total_profit / total_revenue) * 100
```

These six metrics provide a concise overview of business performance.

---

# 23. Recommendations

Based on the analysis, the following recommendations were developed.

## Recommendation 1 — Focus on the Highest-Revenue Category

The highest-revenue category should be monitored closely because it contributes strongly to overall sales.

Management can investigate:

* Product availability
* Customer demand
* Pricing
* Promotions
* Inventory levels

---

## Recommendation 2 — Investigate the Weakest-Profit Region

The region with the weakest total profit should receive additional analysis.

Possible areas for investigation include:

* Discount levels
* Product mix
* Operating costs
* Pricing
* Sales volume
* Customer behavior

The purpose is not simply to increase revenue but to understand how profitability can be improved.

---

## Recommendation 3 — Strengthen the Highest-Profit Category

The highest-profit category should be analyzed to understand what factors contribute to its profitability.

These factors could potentially provide useful lessons for other categories.

---

## Recommendation 4 — Monitor Top-Selling Products

The top-selling products should be monitored for:

* Inventory availability
* Customer demand
* Sales consistency
* Promotional opportunities

Maintaining availability of high-performing products can help protect sales performance.

---

## Recommendation 5 — Retain High-Value Customers

The top customers by revenue should be considered for customer-retention strategies.

Potential actions include:

* Personalized offers
* Loyalty programs
* Targeted communication
* Repeat-purchase incentives

---

## Recommendation 6 — Use Monthly Trends for Planning

The monthly sales trend should be used to support planning decisions.

Management can use the identified high-sales periods to plan:

* Inventory
* Staffing
* Promotions
* Marketing
* Sales resources

---

# 24. Visual Dashboard

A visual dashboard was added as a portfolio enhancement.

The dashboard summarizes:

* Total Sales
* Total Profit
* Total Orders
* Total Customers
* Average Order Value
* Profit Margin
* Revenue by Category
* Profit by Category
* Revenue by Region
* Profit by Region
* Top 10 Products
* Top 10 Customers
* Monthly Sales Trend

The dashboard provides a quick visual overview of the major analytical findings.

---

# 25. Dashboard Interpretation

The dashboard is designed to allow a manager to quickly understand:

1. Overall business performance.
2. Which category generates the most revenue.
3. Which category generates the most profit.
4. Which region generates the most revenue.
5. Which region has weaker profit performance.
6. Which products generate the most sales.
7. Which customers contribute the most revenue.
8. When sales are highest.

The dashboard therefore acts as a visual summary of the detailed analysis performed in the notebook.

---

# 26. Project Workflow

The complete RETAILPULSE workflow can be summarized as follows:

### DATA

Load the retail transaction dataset into Pandas.

### CLEAN

Check missing values, duplicates, data types, invalid values, and data quality.

### ANALYZE

Calculate revenue, profit, category performance, regional performance, product performance, customer performance, and monthly sales.

### VISUALIZE

Create charts that communicate the most important patterns.

### INTERPRET

Convert numerical results into business insights.

### RECOMMEND

Provide practical areas for management to investigate.

This workflow demonstrates how data analysis can move beyond programming and support business understanding.

---

# 27. Project Structure

The final project is organized into the following components:

```text
RETAILPULSE-Sales-Analysis/
│
├── README.md
├── RETAILPULSE.ipynb
├── requirements.txt
│
├── dataset/
│   └── RETAILPULSE_sales_dataset.csv
│
└── report/
    └── Project_Report.pdf
```

The main notebook contains the complete Python analysis.

The dataset folder contains the CSV used for the analysis.

The report folder contains the project report.

The requirements file identifies the main Python libraries required for the project.

---

# 28. Conclusion

The RETAILPULSE project demonstrates a complete beginner-to-intermediate data-analysis workflow using Python.

The project begins with raw retail transaction data and progresses through:

**DATA → CLEAN → ANALYZE → VISUALIZE → INTERPRET → RECOMMEND**

The analysis covers sales, profit, categories, products, regions, customers, and time-based performance.

The project also answers ten business questions and extends the analysis through Pareto analysis and a visual dashboard.

The most important outcome is that the project does not stop at calculating numbers. It translates the analytical results into business-focused findings and recommendations.

RETAILPULSE therefore demonstrates how Python, Pandas, NumPy, Matplotlib, and Seaborn can be used to transform transaction-level data into information that can support business investigation and decision-making.

---

# 29. Final Executive Summary

RETAILPULSE provides a consolidated analytical view of retail sales performance and customer behavior.

The project calculates the major business performance indicators:

* Total Sales
* Total Profit
* Orders
* Customers
* Average Order Value
* Profit Margin

It identifies the leading revenue category, leading profit category, highest-revenue region, weakest-profit region, top-selling products, highest-value customers, and highest-sales period.

The analysis also compares revenue and profit performance to identify situations where sales leadership and profit leadership differ.

The Pareto analysis provides an additional perspective on revenue concentration among products.

The visual dashboard provides management with a quick overview of the major results.

The project concludes with recommendations focused on category performance, regional profitability, high-performing products, high-value customers, and monthly sales planning.

Overall, RETAILPULSE demonstrates the ability to use Python for practical business data analysis and convert raw transaction data into structured insights, visualizations, and actionable areas for further investigation.

---

## End of Report

**RETAILPULSE — Sales Performance & Customer Insights Analytics System**

**Data Analysis with Python**
