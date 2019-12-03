---
layout: post
title:      "WSJ NLP S&P 500 Market Predictor"
date:       2019-12-02 21:35:55 -0500
permalink:  wsj_nlp_s_and_p_500_market_predictor
---


I have finally made it! The end of my Flatiron education. To finish it off a capstone related to two of my favorite things, the WSJ and the economy. I am very proud of my capstone and believe it encompasses a multitude of the python capabilities I possess. This last project cemented my Python understanding. Now for all of the details surrounding my capstone project. 

Originally the idea was to create a classification model for newspaper/media websites to decide whether the articles or headlines were right or left leaning.   

With my interest in the financial markets/economy I decided to tweak the project a bit. Two things changed, first only one newspaper was selected to predict data. Second, the classification of the text data was changed. The object that was classified changed from the political spectrum to the direction of the S&P 500 market.  

The project can be summarized as using NLP to analyze text data scraped from the WSJ homepage to predict the following days direction of the S&P 500. 

Framework:

A OSEMN framework was followed for this project:

Obtain: the data from the relevant resources and stakeholders  
Scrub: Cleaning the data into formats that can be digested in Python packages such as Sklearn or NLTK. Remember the “Garbage in, garbage out” principle  
Explore: Using statistical methods and data analytic techniques explore the data to find significant patterns or trends  
Model: Construct models to predict and forecast the data. Here we focus on our target variable of the direction of the   S&P 500!  
Interpret: Take the results of the analysis and model and create meaningful visualizations or presentations  

I am only going to touch on the new techniques I used for this project, that stood out the most to me. The two different lessons learned were webscraping and creating neural networks.
 
__Text Data Web Scraping__
I was very intimidated by this exercise, as I did not fully grasp NLP or webscraping (BeautifulSoup) when we first learned these lessons in the Flatiron curriculum. I can proudly say I fully understand these concepts now and am not afraid to use my python powers! 

First I will touch on using Beautiful soup and the automated web driver Selenium. With these two packages I was able to automate the webscraping of all of the WSJ text data. BeautifulSoup was intimidating at first, but once I buckled down and figured out what html tags I really needed to look for, it was not hard at all! This also can be attributed to selenium, which enabled me to individually navigate to each days WSJ homepage. This allowed me to target the html tags from each web page. From there Beautiful soup was used to only pull the text data from the headlines, subheadings, and bullets on the front page.

There was one small hiccup. For some reason the html tags that housed the headlines changed format in the month of June. My guess is a new coder joined the team or just a new layout was instituted at the WSJ. This just required a quick addition of a line of code which is below:

```
date=[] #List created for dates
headline_blurb_data= [] #Headline and subheading list
for link in feb: 
    driver.get(str(link)) #Selenium getting the links from the provided month
    my_html= driver.page_source
    soup= BeautifulSoup(my_html, 'html.parser')
    for div in soup.findAll('a', {'class': 'wsj-headline-link'}): #Obtaining the headings from each link's html
        headline_blurb_data.append(div.contents[0])
        date.append(str(link)[29:37])
    for div in soup.findAll('p', {'class':'wsj-summary'}): #Getting all the sub-headings
        headline_blurb_data.append(div.text)
        date.append(str(link)[29:37])
df_wsj=pd.DataFrame({'Date':date,'Text':headline_blurb_data}) #Creating a dataframe
df_wsj.Date= pd.to_datetime(df_wsj.Date) #Changing the date to a date time object
df_feb=df_wsj.merge(sp_500,how='left') #Merging into one dataframe
```



__Neural Networks__
Lastly, I will touch on building my first neural network. To obtain a baseline model, I used vectorization from sklearn for a basic logistic regression model. I obtained a accuracy of around 50-60 percent depending on the level of data cleaning/strategy of manipulation of the text data.

Neural networks were another intimidating factor as I did not fully grasp the concept until the latter half of the capstone project. After countless YouTube videos, I am proud to say I have a rudimentary understanding! I decided to start with just a basic neural network with one to two layers.

``` 
model = Sequential()
model.add(Embedding(MAX_NB_WORDS, EMBEDDING_DIM, input_length=X.shape[1]))
model.add(LSTM(100, dropout=0.2, recurrent_dropout=0.2))
model.add(Dense(2, activation='sigmoid'))
model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])
print(model.summary())
```

From there, I decided to add a LSTM model as this seemed practical due to the nature of classification. The previous day's direction of the S&P 500 could help predict the following day. Along with this I added multiple dense layers going in factors of 8 per best practices. 

```model = Sequential()
model.add(Embedding(MAX_NB_WORDS, EMBEDDING_DIM, input_length=X.shape[1]))
model.add(LSTM(120, dropout=0.2, recurrent_dropout=0.2))
model.add(Dense(24, activation='sigmoid'))
model.add(Dense(16, activation='sigmoid'))
model.add(Dense(8, activation='sigmoid'))
model.add(Dense(2, activation='sigmoid'))
model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])
print(model.summary())
```

The one problem I ran into was the fact that you really do not know what the neural network is actually doing within the different layers. This is where the black box saying comes into play. Unfortunately, I only was able to increase my accuracy from 62.8% to 65.1%. The real win was decreasing the loss function from .744 to .650. All in all this was a great experience and I am very pleased with the results of my capstone and the Data Science Journey I have just finished. Although as they say every ending has a new beginning and I can not wait!  

