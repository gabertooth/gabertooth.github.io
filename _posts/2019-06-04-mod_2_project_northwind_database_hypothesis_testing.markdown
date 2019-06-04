---
layout: post
title:      "Mod 2 Project: Northwind Database Hypothesis Testing"
date:       2019-06-04 19:42:46 +0000
permalink:  mod_2_project_northwind_database_hypothesis_testing
---


The module two project was a huge step in my data science career. It cemented many data analysis techniques we learned in Module 1. In addition, I furthered my understanding of SQL and hypothesis testing. All in all, I am extremely happy with the outcome of my Module 2 project and cannot wait to continue my data science journey.

The module two project consistent of querying a mocked data base (Northwind) using SQL. With the data, I was tasked with answering one required question while coming up with three questions of my own. The freedom to choose your own question was a challenging surprise. I loved the idea of being able to formulate my own hypothesis questions to disprove but did not realize how much time and effort this would take. I think this is the exact reason I liked the module two project so much. I decided to use the ORM sqlalchemy to easily query the SQL database and specifically used the following Pandas method pd.read_sql_query() to put all of my data queries into usable pandas data frames. From there I formulated three different questions. Below are the questions my Jupyter notebook answers about the Northwind database:

1.	Do discounts have a statistically significant effect on the number of products customers order? If so, at what level(s) of discount?

2.	Is there a statistically significant difference in having the top product vs. having a product in the top 5 bestselling products?

3.	Is there a statistically significant difference between the supplier’s total profit and quantity ordered by customers?

4.	Does the price of the product change based on region?

The findings were as follows:

1.	There is significant statistical difference between the quantity of products ordered for discount vs. non-discounted items.
           a.	In addition, products that are discounted at the 5%, 10%, 15%, 20%, and 25% rates generally will have higher order quantities than products with no discount. 

2.	There is no statistical difference between the top five best selling products. This means it does not matter if your product is in the top five best selling or the overall number one selling product.  The product on average will sell relatively the same. 

3.	There is a statistical difference between the Total Profit of the supplier and their corresponding shipment quantity. The suppliers that had the highest profit generally will have the most products ordered. Mass quantities will rake in more money (i.e. it was not just one product that brought a supplier a lot of money, it was the combination of many products.)

4.	There is a statistically significance difference between the region and the price of the product. Obviously, products will be priced differently in the areas of business based off the region market the product is selling in.


This was such a great learning experience and tremendously progressed my Data Science Career.  I look forward to many more challenges like this in my Data Science horizon. 



