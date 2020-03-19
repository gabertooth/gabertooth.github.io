---
layout: post
title:      "Dataquest Project"
date:       2020-03-19 19:31:29 +0000
permalink:  dataquest_project
---


I have reached the end of another module in Dataquest. As with FlatIron this means a project to demonstrate what you learned. This blogpost will go over the different code techniques and details surround this project. The project title is Exploring Hacker News.  

Background:  

Hacker News is a site started by the start-up incubator Y Combinator, where user-submitted stories (known as "posts") are voted and commented upon, similar to reddit. Hacker News is extremely popular in technology and start-up circles, and posts that make it to the top of Hacker News' listings can get hundreds of thousands of visitors as a result.
Below are descriptions of the columns:  
      •	id: The unique identifier from Hacker News for the post  
      • title: The title of the post  
      •	url: The URL that the posts links to, if it the post has a URL  
      •	num_points: The number of points the post acquired, calculated as the total number of upvotes minus the total number of downvotes  
      •	num_comments: The number of comments that were made on the post  
      •	author: The username of the person who submitted the post  
      •	created_at: The date and time at which the post was submitted  
			
The first part to the project was just getting the list of lists set up. From there we divided the list of list into separate lists for different kinds of posts. There are three categories: asks, show, and other posts. Then we calculated the average number of comments for each kind of post.  

The main lesson from this project is working with date time objects. This next part covers that. The below code takes in the comments by hour and then the counts by hour and uses the date time object to do this. See below for code: 

```
import datetime as dt

result_list = []

for post in ask_posts:
    result_list.append(
        [post[6], int(post[4])]
    )

comments_by_hour = {}
counts_by_hour = {}
date_format = "%m/%d/%Y %H:%M"

for each_row in result_list:
    date = each_row[0]
    comment = each_row[1]
    time = dt.datetime.strptime(date, date_format).strftime("%H")
    if time in counts_by_hour:
        comments_by_hour[time] += comment
        counts_by_hour[time] += 1
    else:
        comments_by_hour[time] = comment
        counts_by_hour[time] = 1

comments_by_hour
```

From here we are able to deduce the average number of comments by hour. This was the whole purpose of the exercise! Thank you for tuning in. 
