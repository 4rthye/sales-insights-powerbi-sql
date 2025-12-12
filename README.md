# Sales Insights Dashboard - Power BI & SQL 💼

End-to-end sales analytics project combining MySQL data extraction with Power BI visualization to deliver actionable business insights.

## 🔗 Project Files
- 📊 [Power BI Dashboard (.pbix)]([sales_dashboard.pbix](https://app.powerbi.com/groups/me/reports/80f5babe-6d02-4332-9405-b77278083760?ctid=6e5a6b5e-3c8f-4821-81c5-28885a52597c&pbi_source=linkShare))
- 📄 [Dashboard PDF] [Sales_Insights_POWER _BI.pdf](https://github.com/user-attachments/files/24136315/Sales_Insights_POWER._BI.pdf)
- 💾 [SQL Queries]

## 📸 Dashboard Preview
![Sales Dashboard]<img width="1421" height="792" alt="image" src="https://github.com/user-attachments/assets/e7296a8e-8259-45e3-b849-56986d63327d" />


## 🎯 Project Overview
Built a comprehensive sales analytics solution to help stakeholders:
- Track revenue and sales trends across time periods
- Identify top-performing customers and products
- Analyze regional sales performance
- Make data-driven business decisions

**Tech Stack:** MySQL + Power BI + DAX + Power Query

## 📁 Dataset
- **Source**: Company sales database (MySQL)
- **Tables**: Sales transactions, customers, products, markets, date
- **Geographic Coverage**: Multiple regions in India

## 🔍 SQL Analysis

### Data Extraction & Exploration
Performed initial analysis using MySQL to understand data structure and quality:
```sql
-- Total revenue calculation
SELECT SUM(sales_amount) as total_revenue 
FROM sales_transactions;

-- Revenue by market
SELECT 
    m.markets_name,
    SUM(s.sales_amount) as revenue
FROM sales_transactions s
JOIN sales_markets m ON s.market_code = m.markets_code
GROUP BY m.markets_name
ORDER BY revenue DESC;

-- Top 5 customers by revenue
SELECT 
    c.customer_name,
    SUM(s.sales_amount) as total_revenue
FROM sales_transactions s
JOIN sales_customers c ON s.customer_code = c.customer_code
GROUP BY c.customer_name
ORDER BY total_revenue DESC
LIMIT 5;

SELECT * FROM sales.customers;
SELECT count(*) From sales.transactions;
SELECT * FROM sales.transaction limit 5;
SELECT * FROM sales.transactions where market_code="Mark001";
SELECT count(*) FROM sales.transactions where market_code="Mark001";


-- to check how many usd currency:--
SELECT * FROM sales.transactions where currency="USD";

-- Show transactions in 2020 join by date table (.* means print all columns)
SELECT sales.transactions.*, sales.date.* FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020;

-- Show total revenue in year 2020
SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date where sales.date.year="2020";

-- Show total revenue in year 2020 in Chennai
SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN sales.date ON sales.transactions.order_date=sales.date.date 
where sales.date.year="2020" and sales.transactions.market_code="Mark001"; 


-- distinct product sold in chennai
SELECT distinct sales.transactions.product_code FROM sales.transactions where market_code="Mark001";

SELECT SUM(sales.transactions.sales_amount) FROM sales.transactions INNER JOIN date ON sales.transactions.order_date=sales.date.date where sales.date.year=2020 and and sales.date.month_name="January" 
and (sales.transactions.currency="INR" or sales.transactions.currency="USD");
```

## 🧹 Data Cleaning & Transformation

### Power Query Transformations:

1. **Geographic Filtering**
   - Removed Paris and New York records (outliers in India-focused dataset)
   - Focused analysis on Indian markets for consistency

2. **Data Quality**
   - Filtered out negative sales values (data entry errors)
   - Removed zero-value transactions
   - Eliminated duplicate entries

3. **Currency Normalization**
   - Created `norm_amount` column to standardize currency
   - Converted USD transactions to INR using exchange rate
   - Applied conditional logic: IF USD THEN amount * 75 ELSE amount
   - Filtered out duplicate currency entries

4. **Data Model**
   - Built star schema with fact and dimension tables
   - Created relationships between sales, customers, products, and markets
   - Optimized for performance

## 📊 Dashboard Features

### Key Metrics (DAX Measures):
```dax
// Total Revenue
Revenue = SUM(sales_transactions[norm_amount])

// Total Sales Quantity
Sales Qty = SUM(sales_transactions[sales_qty])

// Revenue Last Year
Revenue LY = CALCULATE([Revenue], SAMEPERIODLASTYEAR(sales_date[date]))

// Revenue Growth %
Revenue Growth = DIVIDE([Revenue] - [Revenue LY], [Revenue LY], 0)
```

### Visualizations:

**Performance Overview:**
- 💰 Total Revenue (KPI card)
- 📦 Total Sales Quantity (KPI card)
- 📈 Revenue Growth % (KPI card)

**Customer Analysis:**
- 👥 Revenue by Customer Name (Bar chart)
- 🏆 Top 5 Customers by Revenue (Table)

**Product Analysis:**
- 📦 Sales Quantity by Product (Bar chart)
- 🌟 Top 5 Products by Revenue (Table)

**Time Analysis:**
- 📅 Revenue by Year (Line chart)
- 📊 Revenue by Month (Column chart)
- 🔄 Revenue by Day of Week (Bar chart)

## 🛠️ Technical Implementation

### SQL Skills Demonstrated:
- Complex JOIN operations
- Aggregate functions (SUM, COUNT, AVG)
- GROUP BY and ORDER BY
- Subqueries and CTEs
- WHERE clause filtering
- Date functions

### Power BI Skills:
- **Power Query (M)**: Data transformation and cleaning
- **DAX**: Calculated columns and measures
- **Data Modeling**: Star schema implementation
- **Visualization**: Multiple chart types and layouts
- **UX Design**: User-friendly dashboard layout

### Data Cleaning Approach:
```
1. Identify Issues (SQL) → 
2. Remove Outliers (Power Query) → 
3. Normalize Data (Conditional Columns) → 
4. Build Model (Relationships) → 
5. Create Measures (DAX) → 
6. Visualize (Power BI)
```

## 👤 Author
**Your Name**
- GitHub: [@your_username](https://github.com/4rthye)
- LinkedIn: [Your Profile](https://linkedin.com/in/arthyesridharan)

## 📄 License
This project is open source and available under the MIT License.

---

## 🏆 Project Highlights
✅ Full ETL pipeline from SQL to visualization  
✅ Complex data cleaning and transformation  
✅ Advanced DAX calculations  
✅ Professional dashboard design  
✅ Real business insights  
```
business-intelligence
sales-analytics
data-cleaning
