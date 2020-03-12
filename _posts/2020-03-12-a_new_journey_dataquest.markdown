---
layout: post
title:      "A New Journey: DataQuest"
date:       2020-03-12 13:10:23 +0000
permalink:  a_new_journey_dataquest
---


This week I have started a new journey, that journey involves another learning platform. I have decided to go through DataQuest online data science self-pace lessons. I think this will bolster my knowledge greatly. Already within learning two different modules I am learning new techniques I did not previously know. The topic I will focus on in this post is the use of frequency charts. 

Frequency charts can be used to essentially create meta data in the form of counts from your existing data. This can be very useful for many reasons. The best use case in my opinion is to be able to show some high-level summary statistics. In addition, it is a great use of dictionaries in Python. The construction of a frequency table is quite easy. 

The first step is to create a empty dictionary. From there you will want to loop through your data that is in a list. When you loop for you will want to check if your value in the for loop happens to be in the actual dictionary already. If it is then you just add one to it. Otherwise you must add the new value as a key in the dictionary. From there you give it a count of 1 due to it being the first time you see it.  All this code looks something like this:


```
dictionary= {}

for x in list:
     if x in list:
		      list[x]+=1
		else:
		     list[x]=1

```
