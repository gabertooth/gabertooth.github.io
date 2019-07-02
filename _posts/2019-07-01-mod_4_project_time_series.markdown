---
layout: post
title:      "Mod 4 Project: Time Series"
date:       2019-07-02 01:15:53 +0000
permalink:  mod_4_project_time_series
---


What are the best zip codes to invest in? Answering such an ambiguous question was the biggest challenge of the project. I do have quite the finance background, so I immediately thought of a couple of options to answer this question. The different measurements I came up with were ROI, historical average price, standard deviation of the historical prices, current market value, and weighted average return.

The decision to choose just one or two metrics was very difficult. I decided to go with the ROI and the average price of the houses in each zip code. I decided on these metrics because I felt like together this would paint the best financial picture for housing prices in each zip.  The ROI is a basic, but very reliable and successful investment strategy. For those who are not familiar, this is taking the current price of a asset and subtracting what you paid for it. Then, dividing the result by the original price. This showed the zip codes that had the biggest increase in their value as a whole over the 20 so years.  Furthermore, the average price was used as a check to make sure we were not investing in any of the most expensive housing markets. Finally, to address the risk we decided to spread our investments across multiple cities/regions.  With this all in mind, our goal was to get the biggest return and pay the least amount of money (biggest bang for our buck). 

Using the above methodology, I came up with the following 5 zip codes:

11211 NY, NY (King County)

11930 NY, NY (Suffolk County)

80449 Hartsel, CO (Park County)

20001 Washington, DC (District of Colombia)

7320 Jersey City, NJ (Hudson County)

To get the above data from a csv file that was in wide format was also a challenging new experience.  Using the melt method and the code below, I was able to manipulate the data into a long format which then could be transformed into a time series for each zip code. 

``df_melted=pd.melt(df, id_vars=['RegionName', 'City', 'Metro','AvgHomePrice', 'ROI'], value_vars=df.iloc[:,7:-3], var_name='Date', value_name='Price')``

From there one must check for stationarity of the data.  Obviously since all the zip codes had extremely high ROI’s, we knew there would be a trend in the data. This had to be removed before we can do any sort of modeling.  I found the best method to detrend the data was to use a rolling mean subtracted from logged original data. Then I differenced the data with periods equal to 10 (this is the recommended period when dealing with financial data). To see whether or not a zip code was stationary after transformation, I used a created stationarity check function below (one for graphing and one for the Dicky Fuller test):

``def stationarity_check_graph(orig_df, window, zipcode): #function for stationarity through graphing a rolling mean and rolling std.
    rolling_mean= orig_df[zipcode].rolling(window=window, center= False).mean() #rolling mean
    rolling_std= orig_df[zipcode].rolling(window=window, center= False).std() #rolling std. 
    
    fig = plt.figure(figsize=(15,6))
    orig = plt.plot(orig_df[zipcode], color='blue',label='Original') #graph original data
    mean = plt.plot(rolling_mean, color='red', label='Rolling Mean') #graph rolling mean
    std = plt.plot(rolling_std, color= 'green', label= 'Rolling Std') #graph rolling std
    plt.ylabel('Price')
    plt.legend(loc='best')
    plt.title(zipcode)
    
def stationarity_check_test(orig_df, zipcode): #Dicky Fuller test to check p-value for stationarity
    dftest = adfuller(orig_df[zipcode])
    print ('Results of Dickey-Fuller Test:')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic','p-value','#Lags Used','Number of Observations Used'])
    for key,value in dftest[4].items():
        dfoutput['Critical Value (%s)'%key] = value
    print (dfoutput)``

With this function I was able to use the Dicky Fuller test’s p-value to confirm stationarity. As one would expect with all the transformations, each zip code had a very low p-value indicating strong stationarity. Thus, we are now ready to model!

To be honest the modeling was the easiest part. Using my googling techniques and after a few ARIMA model Youtube videos, I was ready to model my five zip codes. The models predicted the future price using the past historical data. I decided on a 1,1,0 as my order for the models. I believed this would be best, considering I got a error of around 2.1%. After confirming my model was accurate, I made the following observations. 

1. All of the zip codes selected have around a 40 percent ROI after 10 years which is very good.  
2. Weirdly all of the zip codes have a sort of down turn or bad couple months between 100 (8.3 years) and 150 (12.5 years) which could mean maybe there is going to be a recession. 
3. 11211 had the highest return coming in around 50 percent ROI after 10 years. This is expected the Williamsburg housing market is jumping currently and will not be slowing down anytime soon. 
4. The most expensive zip code is the Suffolk, NY County due to it being in a prime beach/general location for New Yorkers.
5. The least expensive zip code is Hartsel, Colorado and saw the second highest ROI. 

In conclusion, I would recommend investing in all of the selected zip codes. Further analysis could be done to bring in factors like crime rate, education/school ratings, real estate taxes, and population growth over the 20 year time period. I believe the already very accurate model would become even more precise with the added features. There will of course be a recession or downward turn in the stock market over the next 10 years as we are due in the cycle. I would advise to invest in all zips for five years and see where the market is. From there re-balance the portfolio for the next 5 years as this is a normal financial protocol. 

