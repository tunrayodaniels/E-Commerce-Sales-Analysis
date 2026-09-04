# E-Commerce Sales Performance Analysis

## From Messy Transactional Data to Business Insights

## Project Overview

This project analyzes an e-commerce transactional dataset to understand sales performance, identify products and categories contributing to sales, examine sales patterns, and develop data-driven recommendations.

The dataset was obtained from Kaggle and initially contained 103 records across 11 columns.

I used this dataset as a portfolio project to practice an end-to-end data analysis process, from identifying data-quality issues to cleaning, validating, analyzing, visualizing, and interpreting the results.

### The Four question framework 
I approached these project using four questions:

1. What is the problem?
2. What metrics matter?
3. What recommendations can be made?
4. What could be the potential business impact?
   
This helped me to move beyond simple describing the dataset and focus in the business meaning behind the numbers 

## 1. What Is the Problem?

Before analyzing sales performance, I needed to make sure the underlying data was reliable.
The dataset contained several inconsistencies and data-quality issues, including:

▪︎ Duplicate transaction records
▪︎ Inconsistent category names and capitalization
▪︎ Incorrect product-category assignments
▪︎ Missing values
▪︎ Invalid quantity entries
▪︎ Negative quantities
▪︎ Invalid price entries
▪︎ Negative price values
▪︎ Missing or inconsistent values
▪︎ Invalid dates

This meant that simply importing the dataset into Power BI and building visuals could have produced misleading results.
My first step was therefore to understand what was wrong with the data and determine what could be corrected reliably.


## 2. Data Cleaning & Transformation

I used Power Query in Power BI to clean and transform the dataset.

My general approach was:

**Inspect —> Identify —> Validate —> Correct —> Recalculate —> Verify**

One principle I followed throughout the cleaning process was:

**"Don't guess your data into being clean."**

If I could confidently determine the correct value, I corrected it. If I could not determine the intended value reliably, I left it as "null" instead of making an assumption.


## Duplicate Records

The original dataset contained 103 records.
During the initial investigation, I found repeated transaction records involving IDs 142, 146, and 175.

I did not immediately remove the repeated IDs. Instead, I compared the records to determine whether they were genuine duplicates and whether any of the values needed to be corrected first.

**ID 142**: The two records contained the same transaction information but had different "Total" values.
I checked the Total using:

Total = Quantity × Price

5 × ₦645.26 = ₦3,226.30

The incorrect Total was corrected before the duplicate was removed.

**ID 146**: The two records were completely identical across the available fields, so I treated one as a duplicate and removed it.

**ID 175**: The two records contained the same transaction information but had different "Total" values.
I validated the correct value:

1 × ₦111.36 = ₦111.36

The inconsistent value was corrected before the duplicate was removed. After resolving the identified duplicates, the dataset went from **103** records to **100** records.

This was important because I wanted to correct inconsistent records before removing duplicates rather than simply deleting repeated IDs without investigating them.


## Category Standardization & Product/Category Validation

The Category column contained several naming and capitalization inconsistencies, including:

▪︎ Sports vs sports
▪︎ Electronics vs electronic, electronics, ELECTRONICS, Electronicss, Electronic

I standardized these variations.

I also found products that had been assigned to categories that did not match the product. I reviewed the product-category relationships and corrected the classifications before carrying out the category analysis.

The final product-category mapping was:

Category| Products

Books| Science, Biography, Comics, Fiction
Clothing| Shoes, T-shirt, Jacket, Jean
Electronics| Smartphone, Laptop, Headphones, Smartwatch
Home| Blender, Vacuum, Lamp, Microwave
Sports| Tennis Racket, Basketball, Football, Yoga Mat

This gave me a consistent category structure for the analysis.



## Quantity Cleaning

The Quantity column contained missing values, negative values, and invalid text.

For example, "4a" could not reliably be interpreted as a quantity, so I treated it as missing rather than guessing what the value should have been.

After cleaning:

▪︎ 92% valid
▪︎ 8% null/empty
▪︎ 0% errors


## Price Cleaning

The Price column contained several invalid or questionable values, including:

▪︎ "abd"
▪︎ "four hundred"
▪︎ "-100"

Where the intended value was clear, I corrected it.

For example:

"four hundred" => "400"

Values that could not be reliably determined were converted to "null".

After cleaning:

▪︎ 92% valid
▪︎ 8% null/empty
▪︎ 0% errors


## Total Calculation & Validation

The original Total column contained missing and inconsistent values.

I validated the transaction value using:

Total = Quantity × Price

Where both Quantity and Price were available, I used them to validate or recalculate Total.

Where either value was unavailable, I left the calculated Total as "null" rather than creating a value without sufficient evidence.

After cleaning:

▪︎ 85% valid
▪︎ 15% null/empty
▪︎ 0% errors


## Date Cleaning

The Order Date column contained an invalid value ("abc"), which I converted to "null".

I also standardized the valid dates and created additional fields for analysis:

▪︎ Month
▪︎ Month Name
▪︎ Year


## 3. What Metrics Matter?

After cleaning the data, I used Power BI and DAX to analyze sales performance.

Key Metrics

Metric| Result
Gross Sales Value| ₦133.94K
Estimated Realized Revenue| ₦68.51K
Total Orders| 100
Total Units Sold| 3,357
Gross Average Order Value| ₦1.34K

## Gross Sales Value vs Estimated Realized Revenue

The ₦133.94K Gross Sales Value represents the total recorded value of transactions in the cleaned dataset, including transactions with different order statuses.

This means it includes orders that were:

▪︎ Delivered
▪︎ Shipped
▪︎ Processing
▪︎ Returned
▪︎ Cancelled

Because cancelled and returned orders may not represent revenue ultimately retained by the business, I calculated an additional metric:

Estimated Realized Revenue = Gross Sales Value − Returned Value − Cancelled Value»

This resulted in an **Estimated Realized Revenue of ₦68.51K**

I use the word estimated because the dataset does not contain detailed refund or payment-settlement information. The calculation assumes that returned and cancelled orders generated no revenue retained by the business.

Gross Average Order Value

I calculated Gross AOV as:

Gross AOV = Gross Sales Value ÷ Total Orders

₦133.94K ÷ 100 ≈ ₦1.34K
The **Gross Average Order is ₦1.34K**

Other areas I analyzed included:

▪︎ Sales by Category
▪︎ Sales by Product
▪︎ Monthly Sales
▪︎ Units Sold by Category
▪︎ Sales by Order Status
▪︎ Sales by Payment Method
▪︎ Top 5 Products by Sales Value

  
## 4. Key Insights

Category Performance

Category| Recorded Sales Value
Books| ₦40K
Home| ₦31K
Clothing| ₦28K
Sports| ₦23K
Electronics| ₦12K

Books recorded the highest sales value among the five categories, while Electronics recorded the lowest.

However, I did not treat sales value alone as enough evidence to make inventory decisions. Units sold, pricing, and product-level performance would also need to be considered.


### Top 5 Products by Sales Value

The five products with the highest recorded sales value were:

1. Shoes
2. Comics
3. Lamp
4. Blender
5. Science

These products could be useful starting points for further analysis of demand, pricing, inventory availability, and promotional performance.


### Monthly Sales

I analyzed monthly sales to identify periods with relatively higher and lower recorded sales.

These patterns could be related to factors such as:

▪︎ Product demand
▪︎ Number of orders
▪︎ Product mix
▪︎ Pricing
▪︎ Promotions

However, the dataset does not contain enough information to determine the exact reasons for the monthly changes, so I treated these as observations rather than causal conclusions.


### Order Status

Order Status| Recorded Sales Value

Returned| ₦38K
Shipped| ₦30K
Cancelled| ₦27K
Processing| ₦25K
Delivered| ₦13K

One of the most important observations was the relatively high recorded value associated with Returned and Cancelled orders.
This also reinforced why I separated Gross Sales Value from Estimated Realized Revenue.
The ₦133.94K recorded sales value should not automatically be interpreted as ₦133.94K retained by the business.


### Payment Method

Payment Method| Recorded Sales Value

Cash on Delivery| ₦44K
Bank Transfer| ₦42K
PayPal| ₦25K
Credit Card| ₦23K

Cash on Delivery recorded the highest sales value, followed by Bank Transfer.

This could be useful when looking at customer payment preferences and the checkout experience.


## 5. What Recommendations Can Be Made?

Based on the patterns in the cleaned dataset, I would recommend:

1. Maintain focus on high-performing categories and products
Books recorded the highest category sales value, while Shoes and Comics were among the highest-performing products.
The business could prioritize the availability of strong-performing products while monitoring whether their performance is sustained over time.

2. Review Electronics at the product level
Electronics recorded the lowest category sales value.
Rather than immediately reducing the category's inventory, I would review individual Electronics products, their units sold, prices, and demand to understand what is driving the lower performance.

3. Investigate returns and cancellations
The high recorded value associated with Returned and Cancelled transactions deserves attention.
The business should investigate the reasons behind these transactions and identify whether there are recurring issues that could be reduced.
Reducing avoidable returns and cancellations could increase the proportion of recorded sales that becomes realized revenue.

4. Consider payment preferences
Cash on Delivery recorded the highest sales value among the payment methods.
The business could consider this pattern when reviewing its payment options and checkout experience.

5. Continue monitoring monthly performance
Monthly sales should be monitored over a longer period to determine whether the stronger and weaker periods observed in this dataset are recurring patterns.

This could eventually support better inventory and promotional planning.


## 6. What Could Be the Business Impact?

If these findings were validated using larger and more complete business data, they could potentially help the business:

▪︎ Improve inventory allocation
▪︎ Identify underperforming products
▪︎ Reduce avoidable returns and cancellations
▪︎ Improve understanding of customer payment preferences
▪︎ Plan promotions more effectively
▪︎ Improve sales and inventory planning
▪︎ Make better data-informed decisions

To make these recommendations actionable, additional information would be needed, such as profit margins, inventory levels, customer behavior, return reasons, cancellation reasons, marketing activity, discounts, and longer-term sales data.


## Dashboard

The final Power BI dashboard provides a one-page view of the sales performance analyzed in this project.

Dashboard Includes

▪︎ Gross Sales Value
▪︎ Estimated Realized Revenue
▪︎ Gross Average Order Value
▪︎ Total Units Sold
▪︎ Total Orders
▪︎ Sales by Category
▪︎ Monthly Sales
▪︎ Units Sold by Category
▪︎ Top 5 Products by Sales Value
▪︎ Sales by Order Status
▪︎ Sales by Payment Method

"E-Commerce Sales Dashboard" (ecommerce-sales-dashboard.png)


## Tools Used

▪︎ **Kagggle**: Data source 
▪︎ **Power Query**: Data cleaning and transformation
▪︎ **Power BI**: Data modeling, analysis, and visualization
▪︎ **DAX**: Measures and calculations
▪︎ **GitHub**: Project documentation and version control


## Project Workflow

Raw Data => Data Quality Assessment => Cleaning => Validation => Data Modeling => Analysis => Visualization => Insights => Recommendations


## Limitations

This is a portfolio project using a relatively small Kaggle dataset, rather than live business data.
The main limitations are:

▪︎ The dataset contains only 103 raw records.
▪︎ Some values were missing or invalid and had to be retained as "null" where they could not be reliably determined.
▪︎ Gross Sales Value includes transactions across different order statuses.
▪︎ Estimated Realized Revenue assumes that Returned and Cancelled transactions generated no retained revenue.
▪︎ Actual refund amounts and payment settlement information were not available.
▪︎ The analysis is descriptive and does not establish causation.
▪︎ The dataset is too limited to support reliable forecasting or long-term trend analysis.

The recommendations should therefore be treated as initial business hypotheses that would require validation with larger and more complete business data.


## Project Files

▪︎ README.md: Project documentation
▪︎ E-Commerce-Sales-Analysis.pbix: Power BI project file
▪︎ ecommerce-sales-dashboard.png: Dashboard preview


## Conclusion

This project gave me practical experience working through a messy dataset rather than starting with clean, analysis-ready data.
The main lesson was that building a dashboard is only one part of the analysis. Understanding the quality of the data, validating questionable values, defining the right metrics, and interpreting the results are just as important.

