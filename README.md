# Walmart Sales Analysis Project

## Overview
This project aims to explore the Walmart Sales data to understand top-performing branches and products, sales trends of different products, and customer behavior. The goal is to study how sales strategies can be improved and optimized. The dataset was obtained from the Kaggle Walmart Sales Forecasting Competition.

> "In this recruiting competition, job-seekers are provided with historical sales data for 45 Walmart stores located in different regions. Each store contains many departments, and participants must project the sales for each department in each store. To add to the challenge, selected holiday markdown events are included in the dataset. These markdowns are known to affect sales, but it is challenging to predict which departments are affected and the extent of the impact."

## Purposes of the Project
The major aim of this project is to gain insights into Walmart's sales data to understand the different factors that affect sales across various branches.

## About the Data
The dataset contains sales transactions from three different branches of Walmart located in Mandalay, Yangon, and Naypyitaw. It includes 17 columns and 1000 rows:

| Column                        | Description                                          | Data Type        |
|-------------------------------|------------------------------------------------------|-------------------|
| invoice_id                    | Invoice of the sales made                             | VARCHAR(30)       |
| branch                        | Branch at which sales were made                       | VARCHAR(5)        |
| city                          | The location of the branch                            | VARCHAR(30)       |
| customer_type                 | The type of the customer                              | VARCHAR(30)       |
| gender                        | Gender of the customer making purchase                | VARCHAR(10)       |
| product_line                  | Product line of the product sold                      | VARCHAR(100)      |
| unit_price                    | The price of each product                             | DECIMAL(10, 2)    |
| quantity                      | The amount of the product sold                        | INT               |
| VAT                           | The amount of tax on the purchase                    | FLOAT(6, 4)       |
| total                         | The total cost of the purchase                        | DECIMAL(10, 2)    |
| date                          | The date on which the purchase was made              | DATE              |
| time                          | The time at which the purchase was made              | TIMESTAMP         |
| payment_method                | The total amount paid                                | DECIMAL(10, 2)    |
| cogs                          | Cost of Goods Sold                                   | DECIMAL(10, 2)    |
| gross_margin_percentage       | Gross margin percentage                               | FLOAT(11, 9)      |
| gross_income                  | Gross Income                                         | DECIMAL(10, 2)    |
| rating                        | Rating                                               | FLOAT(2, 1)       |

## Analysis List
1. **Product Analysis**: 
   - Understand the different product lines, identify top performers, and those needing improvement.
   
2. **Sales Analysis**:
   - Analyze sales trends of products to measure the effectiveness of sales strategies and identify necessary modifications.

3. **Customer Analysis**:
   - Uncover different customer segments, purchase trends, and profitability of each segment.

## Approach Used
1. **Data Wrangling**:
   - Inspection of data to detect NULL and missing values, followed by appropriate replacement methods.

2. **Database Creation**:
   - Create a table and insert the data.
   - Ensure no NULL values are present by setting `NOT NULL` constraints for each field.

3. **Feature Engineering**:
   - Generate new columns from existing ones:
     - `time_of_day`: Indicates sales in Morning, Afternoon, and Evening.
     - `day_name`: Extracted days of the week for sales transactions.
     - `month_name`: Extracted months of the year for sales transactions.

4. **Exploratory Data Analysis (EDA)**:
   - Conduct EDA to answer the project’s key questions.

## Conclusion

### Business Questions to Answer
**Generic Questions**:
- How many unique cities does the data have?
- In which city is each branch?

**Product-Related Questions**:
- How many unique product lines does the data have?
- What is the most common payment method?
- What is the most selling product line?
- What is the total revenue by month?
- What month had the largest COGS?
- What product line had the largest revenue?
- What is the city with the largest revenue?
- What product line had the largest VAT?
- Fetch each product line and categorize as "Good" or "Bad" based on average sales.
- Which branch sold more products than the average?
- What is the most common product line by gender?
- What is the average rating of each product line?

**Sales-Related Questions**:
- Number of sales made at different times of the day per weekday.
- Which customer types bring in the most revenue?
- Which city has the highest tax percent/VAT?
- Which customer type pays the most in VAT?

**Customer-Related Questions**:
- How many unique customer types does the data have?
- How many unique payment methods does the data have?
- What is the most common customer type?
- Which customer type buys the most?
- What is the gender distribution among customers?
- Which time of day do customers give the most ratings?
- Which day of the week has the best average ratings?

## Revenue and Profit Calculations
- **COGS** = unit_price × quantity
- **VAT** = 5% × COGS
- **Total (Gross Sales)** = VAT + COGS
- **Gross Profit (Gross Income)** = Total - COGS
- **Gross Margin** = Gross Profit / Total Revenue

### Example Calculation:
For the first row in the database:
- **Unit Price** = 45.79
- **Quantity** = 7
- **COGS** = 45.79 × 7 = 320.53
- **VAT** = 5% × 320.53 = 16.0265
- **Total** = VAT + COGS = 16.0265 + 320.53 = 336.5565
- **Gross Margin Percentage** = Gross Income / Total Revenue = 16.0265 / 336.5565 ≈ 4.76%

## SQL Code
For the SQL code and queries used in this project, check the `SQL_queries.sql` file.

```sql
-- Create database
CREATE DATABASE IF NOT EXISTS walmartSales;

-- Create table
CREATE TABLE IF NOT EXISTS sales (
    invoice_id VARCHAR(30) NOT NULL PRIMARY KEY,
    branch VARCHAR(5) NOT NULL,
    city VARCHAR(30) NOT NULL,
    customer_type VARCHAR(30) NOT NULL,
    gender VARCHAR(30) NOT NULL,
    product_line VARCHAR(100) NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    quantity INT NOT NULL,
    tax_pct FLOAT(6,4) NOT NULL,
    total DECIMAL(12,4) NOT NULL,
    date DATETIME NOT NULL,
    time TIME NOT NULL,
    payment VARCHAR(15) NOT NULL,
    cogs DECIMAL(10,2) NOT NULL,
    gross_margin_pct FLOAT(11,9),
    gross_income DECIMAL(12,4),
    rating FLOAT(2,1)
);
