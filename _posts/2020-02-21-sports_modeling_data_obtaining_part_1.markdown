---
layout: post
title:      "Sports Modeling (Data Obtaining Part 1)"
date:       2020-02-21 21:28:19 +0000
permalink:  sports_modeling_data_obtaining_part_1
---


As my last post touched on I decided to switch my efforts to a new sports modelling project. The first hurdle of this project was obtaining the data. I decided to google around for college basketball historical data and sure enough got lucky. I found a pretty cleaned and comprehensive data set on Kaggle. The data can be accessed using Big Query from Google.

Unfortunately, I ran into some issues connecting through Big Query and my jupyter python notebook. I decided to just download data into a csv and then directly access it through my github repo. This ended up being ok as I was able to download data from 2001 to 2016. I ended up running into even more issues when trying to obtain betting odds and over under statistics. 

Finally, I found a website called oddshark and was able to create a for loop that uses selenium and pandas to web scrape html tables that had current gambling odds. The only problem is my Big Query Google data does not go to present day. Thus, I plan to do two separate analyses on this data both EDA and modelling. 
Below is the code I have been using to web scrape around 823 teams gambling data into csv files. In addition, I have included a sample table! Cheers until next week!

Code:

```exceptions=[]
for x in college[650:700]: #STOPPED HERE next up is 700 to 750
    browser.get('https://www.oddsshark.com/ncaab/database')
    browser.find_element_by_xpath('//*[@id="team-search-h2h"]').click()
    browser.find_element_by_xpath('//*[@id="team-search-h2h"]').send_keys(str(x))
    browser.find_element_by_xpath('//*[@id="frm-h2h"]/table/tbody/tr[3]/td/div/div[3]/label').click()
    browser.find_element_by_xpath('//*[@id="chalk-select-game-type-h2h"]/option[4]').click()
    browser.find_element_by_xpath('//*[@id="frm-h2h"]/table/tbody/tr[6]/td/div/div[1]/label').click()
    browser.find_element_by_xpath('//*[@id="chalk-select-odds-h2h"]/option[5]').click()
    browser.find_element_by_xpath('//*[@id="submit-h2h"]').click()
    time.sleep(1)
    try:
        df=pd.read_html(browser.page_source)
        df[1].to_csv(str(x)+'.csv')
    except: 

```

Table: 


