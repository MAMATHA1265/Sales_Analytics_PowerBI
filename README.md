# Sales_Analytics_PowerBI
##Project Overview
This project contains my Power BI sales analytics assignment and DAX practice.
##DAX Questions and Formulas
## create columns
1.Total sales=sale_data[Quantity]*sales_data[Unit_price]

2.Discount Amount=sales_data[Total sales]*sales_data[Discount]

3.Final Sales=sales_data[Total sales]-sales_data[Discount Amount]

4.Profit=sales_data[Final Sales]-sales_data[Unit_Cost]

## Basic DAX Measures
1.calculate total sales
total_sales=sum(sales_data[Sales_Amount])

2.Calculate total quantity sold.
total_quantity_sold = sum(sales_data[Quantity_Sold])

3.Calculate total profit.
total_profit = sum(sales_data[Profit])

4.Calculate average sales.
avg_sales = AVERAGE(sales_data[Sales_Amount])

5.Calculate average product price.
avg_price = AVERAGE(sales_data[Unit_Price])

6.Find the maximum sales value.
max_sales = MAX(sales_data[Sales_Amount])

7.Find the minimum sales value.
min_sales = MIN(sales_data[Sales_Amount]) 

8.Count total orders.
total_orders = COUNT(sales_data[Product_ID])

9.Count unique customers.
unique_customer = DISTINCTCOUNT(sales_data[Customer_Type])

10.Count unique products.
unique_products = DISTINCTCOUNT(sales_data[Product_Category]) 

## CALCULATE Practice
Create measures for:
1.Calculate total sales for the Electronics category.
total_sales_electronics = CALCULATE([total_sales],sales_data[Product_Category]="Electronics") 

2.Calculate total profit for the Furniture category.
total_profit_furniture = CALCULATE([total_profit],sales_data[Product_Category]="Furniture")

3.Calculate sales for the Online payment mode.
sales_online = CALCULATE([total_sales],sales_data[Sales_Channel]="Online")

4.Calculate sales for the North region.
sales_North = CALCULATE([total_sales],sales_data[Region]="North") 

5.Calculate total sales where quantity is greater than 5.
total_sales_qty>5 = CALCULATE([total_sales],sales_data[Quantity_Sold]>5)

6.Calculate total profit where discount is less than 20%.
total_profit_discount<20% = CALCULATE([total_profit],sales_data[Discount]<20/100)

7.Calculate total sales for a particular salesperson.
total_sales_rep = CALCULATE([total_sales],sales_data[Sales_Rep]="David")
## FILTER + CALCULATE
1.Calculate sales for products where sales are greater than ₹10,000.
filter+calculate(sales_products) = CALCULATE([total_sales],FILTER(sales_data,sales_data[Total sales]>10000))

2.Calculate profit from orders where quantity is greater than 10.
filter+calculate(profit_quantity) = CALCULATE([total_profit],FILTER(sales_data,sales_data[Quantity_Sold]>10))

3.Calculate sales where discount is greater than 10%.
filter+calculate(sales_discount) = CALCULATE([total_sales],FILTER(sales_data,sales_data[Discount]>10/100) )

4.Calculate total sales for products belonging to Electronics or Furniture.
filter+calculate(sales_products(electronics or furniture) = CALCULATE([total_sales],FILTER(sales_data,sales_data[Product_Category]="Electronics"||sales_data[Product_Category]="Furniture"))

5.Calculate total profit for orders having Final Sales greater than ₹5,000.
filter+calculate(profit_final sales>5000) = CALCULATE([total_profit],FILTER(sales_data,sales_data[Final sales]>5000))
## SUMMARIZE Practice
1.Create a table showing Category-wise Total Sales.
category_wise total sales = SUMMARIZE(sales_data,sales_data[Product_Category],"total sales",sum(sales_data[Total sales]))

2.Create a table showing Product-wise Total Quantity.
product_wise total quantity = SUMMARIZE(sales_data,sales_data[Product_Category],"total quantity",sum(sales_data[Quantity_Sold]))

3.Create a table showing Region-wise Total Profit.
Region_wise total profit = SUMMARIZE(sales_data,sales_data[Region],"total profit",[total_profit])

4.Create a table showing Salesperson-wise Total Sales.
Sales_Rep_Sales = SUMMARIZE(sales_data,sales_data[Sales_Rep],"total sales",[total_sales])

5.Create a table showing:
Region| Total Sales | Total Profit
Region_sales_profit = SUMMARIZE(sales_data,sales_data[Region],"total sales",[total_sales],"total profit",[total_profit])

6.Create a table showing:
Category | Total Sales | Total Quantity | Total Profit
category_total sales_total qty_total profit = SUMMARIZE(sales_data,sales_data[Product_Category],"total sales",[total_sales],"total quantity",[total_quantity],"total profit",[total_profit])

7.Create a table showing:
Salesperson | Sales | Profit | Orders
Sales_Rep_sales_profit_orders = SUMMARIZE(sales_data,sales_data[Sales_Rep],"total sales",[total_sales],"total profit",[total_profit],"total orders",[total_orders])
## TOPN Practice
1.Find the Top 5 Products by Sales.
Top5_products_sales = TOPN(5,SUMMARIZE(sales_data,sales_data[Product_Category],"total sales",[total_sales]),[total_sales],DESC)

2.Find the Top 3 Regions by Sales.
Top3 Regions_sales = TOPN(3,SUMMARIZE(sales_data,sales_data[Product_ID],"total sales",[total_sales]),[total_sales],DESC)

3.Find the Top 3 Sales_Rep by Profit.
Top3_sales_Rep_profit = TOPN(3,SUMMARIZE(sales_data,sales_data[Sales_Rep],"total_profit", [total_profit]),[total_profit],desc)


4.Find the Top 3 Categories by Quantity Sold.
Top3_category_quantity_sold = TOPN(3,SUMMARIZE(sales_data,sales_data[Product_Category],"total quantity",[total_quantity]),[total quantity],DESC)

5.Find the Top 3 Product_Category by Sales.
Top3 products_category = TOPN(3,SUMMARIZE(sales_data,sales_data[Product_Category],"total sales",[total_sales]),[total sales],DESC)

6.Find the Bottom 5 Products by Sales.
Bottom5_product_sales = TOPN(5,SUMMARIZE(sales_data,sales_data[Product_ID],"total sales",[total_sales]),[total_sales],ASC)

## Advanced DAX
1.Calculate each product's percentage contribution to total sales.
product_sales % = DIVIDE([total_sales], CALCULATE([total_sales],ALL(sales_data[Product_Category])))*100

2.Calculate average order value.
Average_order_value = DIVIDE([total_sales],DISTINCTCOUNT(sales_data[Product_ID]))

3.Calculate profit margin %.
profit margin % = DIVIDE([total_profit],[total_profit],0)

4.Calculate discount percentage.
discount % = DIVIDE([total discount],[total_sales],0) 

5.Find the highest-selling product.
highest_selling_product = CALCULATE(SELECTEDVALUE(sales_data[Product_ID]),TOPN(1,sales_data,[max_sales],desc))


6.Create a measure for Top 5 Product Sales.
Top5_product_sales = CALCULATE([total_sales],TOPN(5,sales_data,[total_sales],DESC)

7.Calculate sales excluding the selected category.
sales_excluding_selected_category = CALCULATE([total_sales],ALLSELECTED(sales_data[Product_Category]))

8.Create a dynamic measure that changes according to the selected category.
Dynamic_sales = VAR SelectedCategory=SELECTEDVALUE(sales_data[Product_Category])RETURN CALCULATE([total_sales],sales_data[Product_Category]=SelectedCategory)
       (or)
Dynamic_sales = [total_sales]
## DAX Challenge Questions
1.Calculate cumulative sales by date.
Cumulative_Sales = CALCULATE([total_sales],FILTER(ALL(sales_data[Sale_Date]),sales_data[Sale_Date]<=MAX(sales_data[Sale_Date])))

2.Calculate cumulative profit by date.
Cumulative_Profits = CALCULATE([total_profit],FILTER(ALL(sales_data[Sale_Date]),sales_data[Sale_Date]<=MAX(sales_data[Sale_Date])))

3.Find products whose sales are above the average product sales.
Products_Above_Average = IF([total_sales]>[avg_sales],[total_sales],BLANK())

4.Calculate the difference between a product's sales and the category's average sales.
Product sales vs Category avg = CALCULATE([total_sales],ALLEXCEPT(sales_data,sales_data[Product_Category]))

5.Calculate the rank of products according to sales.
Product Sales Rank = RANKX(ALL(sales_data[Product_ID]),[total_sales],,DESC,Dense)

6.Calculate the rank of salespersons according to profit.
Salesperson Profit Rank = RANKX(ALL(sales_data[Sales_Rep]),[total_profit],,DESC,Dense) 

7.Create a measure that displays:
High Sales → Sales > ₹1,00,000
Medium Sales → ₹50,000–₹1,00,000
Low Sales → Sales < ₹50,000
Sales_Category = SWITCH(TRUE(),[total_sales]>100000,"High Sales",[total_sales]>=50000&&[total_sales]<=100000,"Medium Sales",[total_sales]<50000,"Low Sales")
## KPI Cards
Create cards for:
1.Total Sales
total_sales = sum(sales_data[Sales_Amount])

2.Total Profit
total_profit = sum(sales_data[Profit])

3.Total Orders
total_orders = COUNT(sales_data[Product_ID]) 

4.Total Quantity
total_quantity = sum(sales_data[Quantity_Sold])

5.Average Order Value
Average_order_value = DIVIDE([total_sales],DISTINCTCOUNT(sales_data[Product_ID]))

6.Profit Margin %
profit margin % = DIVIDE([total_profit],[total_profit],0)
## Charts and Visualizations
1. Sales by Region
Chart: Bar Chart

2. Monthly Sales Trend
Chart: Line Chart

3. Category Sales
Chart: Column Chart

4. Region-wise Profit
Chart: Bar Chart

5. Top 5 Products
Chart: Bar Chart

6. Sales-Rep Performance
Chart: Column Chart

7. Payment Mode Analysis
Chart: Donut Chart

9. Sales vs Profit
Chart: Scatter Chart

10. City + Category Analysis
Chart: Stacked Column Chart

## Dashboard Slicers
1.Sales_Rep
2.Region
3.Product_Category
4.Year
