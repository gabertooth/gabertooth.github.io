---
layout: post
title:      "Sports Modeling Data Obtaining (Part 2)"
date:       2020-02-25 22:02:09 +0000
permalink:  sports_modeling_data_obtaining_part_2
---


Unfortunately, I realized the data I was scraping was only for the current season and the other data I had was for seasons from 2003 to 2016. I have decided to just to do two separate models and create metadata from my betting web scraped data. Then use another web scraping technique to get even more historical data from sports reference website. 

I decided to plan out what exact models I was going to do so this way I have sort of mini goals or sprints if you will. Below is the outline or plan of what I want to model or display visually.  

Betting Data  
•	How often did a team cover the spread?  
•	How often did a team hit the over or under?  
•	This will all be achieved using either decision trees, XGBoost, Logistic Regression, or Random Forest algorithms  

In addition, the metadata I would like to include here is their win loss records or winning streaks. Along with the trend of hitting the under or over and covering the spread. So in total it would be around 3-4 extra columns.  

Historical Data  

Hypothesis Testing:  
•	When a team scores a certain number of points more likely to win  
•	Playing back to back games  
•	Home vs. Away  
•	Attendance and winning  
•	Home vs. Away more points being scored  

Time Series Analysis:  
•	Attendance

