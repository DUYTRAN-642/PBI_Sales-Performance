# 📊 Project Title: Superstore Sales Analysis

A comprehensive analysis of Superstore's global sales data. This project explores sales trends, profitability, and return rates across regions and product categories to inform strategic market expansion and product selections.

Author: DUY TRAN

Date: 2025-03-28

Tools Used: Power BI

---

# Table of Contents

📌 Background & Overview

📂 Dataset Description & Data Structure

🧠 Design Thinking Process

⚒️ Main Process

📊 Key Insights & Visualizations

🔎 Final Conclusion and Future Enhancements

---

# 📌 Background & Overview

## 📖 What is this project about?

✔️ This project analyzes sales performance data of an E-commerce business **Superstore** to provide insights into key business metrics and trends. The analysis covers sales, profit, order information, and return analysis across various categories, markets, and customer segments. 

✔️ The goal is to understand factors influencing sales performance and identify areas for improvement.

## 👤 Who is this project for?

✔️ Sales and Marketing Teams: use the insights to target strategies, refine campaigns, and improve performance.

✔️ Business Executives and Managers: can leverage the insights to make informed decisions about business strategies, resource allocation, and growth opportunities

✔️ Business Analysts and Data Analysts: need to interpret data and identify trends, patterns, and areas for improvement in business performance.

---

# ❓ Key Objectives/Business Questions:

## **Situation**

👉🏻 **Growth Potential vs. Concerns:**  
  The sales data indicates significant growth potential alongside issues such as profitability pressures and high product return rates.

👉🏻 **Management Needs:** Senior management requires data-driven insights to refine market strategies.

👉🏻 **Category-Specific Clues:** Despite lower sales volumes, categories like *Office Supplies* are experiencing high return rates.

## **Task**

🎯 **Data Analysis:** Dissect the sales data to uncover trends affecting overall performance, including sales trends, profitability metrics, and return rates.
 
🎯 **Strategic Planning:** Formulate strategies to boost sales, enhance profitability, and expand market share.
 
🎯 **Actionable Recommendations:** Provide detailed, data-driven insights based on the analysis.

# 📂 Dataset Description & Data Structure

## 📌 Data Source

Source: Superstore sample dataset

Size: This project has 3 tables of orders (over 51k rows and 20 columns), return (1172 rows and 2 columns) and sales person (13 rows & 2 columns)

Format: .csv

## 📊 Data Structure & Relationships

1️⃣ Table Schema

<details>
<summary>👉🏻 Fact Table 1: Orders</summary>
<br>

| Column Name        | Data Type        | Description                                               |
| :----------------- | :--------------- | :-------------------------------------------------------- |
| Order ID           | int              | A unique identifier for each order.                        |
| Order Date         | datetime         | The date when the order was placed.                        |
| Ship Date          | datetime         | The date when the order was shipped.                       |
| Ship Mode          | varchar(50)      | The method or mode of shipping used for the order.         |
| Customer           | nvarchar(50)     | The name or identifier of the customer who placed the order. |
| Customer Segment   | nvarchar(50)     | The segment or category to which the customer belongs.     |
| City               | nvarchar(50)     | The city where the customer is located.                    |
| State              | nvarchar(50)     | The state where the customer is located.                   |
| Country            | nvarchar(50)     | The country where the customer is located.                 |
| Postal Code        | varchar(20)      | The postal code of the customer's location.               |
| Market             | nvarchar(50)     | The market or region where the order was placed.            |
| Region             | nvarchar(50)     | The specific region within the market where the order was placed. |
| Product ID         | int              | A unique identifier for each product in the order.         |
| Category           | nvarchar(50)     | The category to which the product belongs.                |
| Sub-Category       | nvarchar(50)     | The sub-category to which the product belongs.            |
| Product Name       | nvarchar(100)    | The name of the product.                                 |
| Sales              | money            | The total sales amount for the order.                     |
| Quantity           | int              | The quantity of products ordered.                        |
| Profit             | money            | The profit earned from the order.                         |
| Person             | Nvarchar         | The name of the sales person.                             |
| Count of Order ID  | Int              | The number of order id.                                  |
| Sum of Sales       | money            | The sum of sales amount for the order.                     |
| Order Processing Time (Days) | Float      | The number of days taken to process an order.           |
| Orders Returned    | Int              | Total orders returned.                                   |
| Total Returns      | Money            | Total returns value.                                     |
| Returns per 1000 Orders | Float      | Returns per 1000 orders.                               |
| Returns per 1000 Customers | Float   | Returns per 1000 customers.                              |
| Total Orders Return per Orders | Float | Total orders return per order.   

</details>

<details>
<summary>👉🏻 Fact Table 2: Returns</summary>
<br>

| Column Name   | Data Type |
| :------------ | :-------- |
| Order ID      | int       |
| Returned      | bit       |

 </details>

 <details>
<summary>👉🏻 Dim Table: People</summary>
<br>

| Column Name | Data Type   |
| :---------- | :------------ |
| Person      | nvarchar(255) |
| Region      | nvarchar(255) |

</details>

2️⃣ Data Relationships:

![image](https://github.com/user-attachments/assets/66b76429-5d45-4025-a6fb-a447646fe02d)

# ⚒️ Main Process

The main process involved:

1.  **Data Exploration and Cleaning:** Analyzing the dataset to understand its structure, identify missing values, and ensure data quality.
2.  **Sales Analysis:** Analyzing sales data to identify trends, patterns, and key performance indicators (KPIs) such as total sales, total revenue, total profit, and profit margin.
   DAX was applied to calculate the new columns of `Processing Time` and `Profit Margin` to support for the analysis

                ```DAX
               Processing Time = Orders[Ship Date] - Orders[Order Date]
               ```
               
               ```DAX
               Profit Margin = Orders[Profit] / Orders[Sales]
               ```

4.  **Market and Segment Analysis:** Examining sales performance across different markets and customer segments to identify high-performing and underperforming areas.
5.  **Category and Sub-Category Analysis:** Analyzing sales and profitability by product category and sub-category to identify profitable products and areas for improvement.
6.  **Return Analysis:** Analyzing return data to understand the reasons for returns, identify products with high return rates, and calculate return metrics.
   * Values of each returned order was calculated by using DAX

              ```DAX
              values = SUMX(
                  FILTER(Orders, Orders[Order ID] = Returns[Order ID]),
                  Orders[Sales]
              )
              ```
     * 2 measures was also deployed to show on KPI card `Returns per 1000 Orders` and  `Returns per 1000 customers`
       
8.  **Order Processing Time Analysis:** Calculating and analyzing the average order processing time.
9.  **Visualization and Reporting:** Creating visualizations and reports to communicate key findings and insights to stakeholders.

---

# 📊 Key Insights & Visualizations

### 📌 Page 1: Sales Overview

![image](https://github.com/user-attachments/assets/1d06cdbd-d862-428a-b979-fcbb7dfd07ee)

* **Overall Performance:** The business generated 13M in revenue with 1.5M in profit from 25,035 orders.
* **Market Analysis:**
    * APAC is the strongest market, contributing the most to sales (4.3M).
    * Africa is the weakest market in terms of sales (0.4M). 
* **Category Analysis:**
    * Technology products lead in sales (4M), followed by Furniture (4M) and Office Supplies (2M). 
* **Segment Analysis:**
    * The Consumer segment is the primary sales driver (7M). 
* **Profitability:**
    * Copiers are a high-profit sub-category. 
* **Efficiency:**
    * The average order processing time is 3.97 days. 

### 📌 Page 2: Sales Analysis

![image](https://github.com/user-attachments/assets/063b140d-792d-4bb9-b860-6072ae13d411)

* **Profitability by Product:**
    * Profit margins vary significantly across sub-categories. 
    * Tables have negative profit margins (-24.2%), indicating potential issues. 
* **Order Processing:**
    * Average order processing time is consistently around 3.97 days. 
* **Sales Performance by Individual:**
    * Sales performance varies considerably between salespersons, with some generating significantly higher sales than others (e.g., Anna Andreadi with 2,822,303). [cite: 10]

### 📌 Page 3: Return Analysis

* **Return Volume and Value:**
    * There were 1172 orders returned, totaling $819,020 in returns. [cite: 12]
* **Return Rate:**
    * The return rate is 46.81 per 1000 orders. [cite: 12]
* **Returns by Salesperson:**
    * Return rates differ substantially across salespersons (e.g., Shirley Daniels with 13.8%). [cite: 13]
* **Returns by Customer Segment:**
    * The Consumer segment also leads in the number of returns (606). [cite: 14]
* **Returns by Product Category:**
    * Office Supplies have the highest return volume. [cite: 14]
---

## Skills Improvement

This project significantly enhanced my skills in:

* **Data Visualization:**  
  * Mastering the selection of the right chart types (*bar*, *pie*, *line*) to present data effectively.
  * Creating clear visualizations that tell a compelling data story.
* **Data Analysis:**  
  * Identifying key metrics for assessing sales performance, profitability, and returns.
  * Performing deep-dive analysis to uncover trends and anomalies.
  * Structuring insights using the STAR method for clarity and focus.
* **Strategic Thinking:**  
  * Balancing quantitative analysis with strategic recommendations.
  * Enhancing insights through targeted investigations (e.g., return spikes during Q4).

---

## Recommendations

* **Product Focus:**  
  * Capitalize on the performance of *Technology* products.
  * Address persistent issues with high return rates in *Office Supplies*.
* **Profitability Enhancements:**  
  * Implement strategies to drive profitability across all categories.
* **Internal Synergy:**  
  * Leverage insights from top-performing salespeople.
* **Market Targeting:**  
  * Prioritize expansion in the EU and APAC regions based on current trends.

---

## Next Steps

* **Office Supplies Analysis:**  
  Initiate a detailed investigation into the reasons behind high *Office Supplies* returns.
* **Customer Segmentation:**  
  Analyze customer data to tailor targeted marketing strategies.
* **Seasonal Trends:**  
  Investigate the cause of the Q4 return spike to optimize seasonal strategies.
---
