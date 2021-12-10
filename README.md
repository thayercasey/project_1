# project_1

Project Title: Gas Price Inflation by region in America

Team Members: Juan Estrella, Casey Thayer, Dick Brown, Fatih Ezgin

Project Description/Outline: An in depth analysis per region of the rise in gas prices over the last 5 years.

Research Questions to Answer: You are the HR executive of a large corporation. Your workforce switched to hybrid working model with two days office and three days wfh as a result of the pandemic.  Work from home created opportunities for savings for your associates but the inflation also went up. You are trying to figure out the impact of workfrom home given that gas prices have increased but average commute has decreased. In this project we will try to figure out the impact of inflation on gas prices along with reduction on commute for the next round of salary increase. We will make assumptions on average commute distance and make calculations on past and future commute costs. 


Datasets to be Used: https://download.bls.gov/pub/time.series/ap/ap.data.2.Gasoline

Rough Breakdown of Tasks: 

-create 3 scripts: 
    -extracting the data from the bls api (Primary Juan, Reviewer Fatih)
    -putting data in to a data frame and analyzing it (Primary Fatih, Reviewer Casey)
    -visualization of data (Primary Casey, Reviewer Dick)
    
-design of how data should be presented in powerpoint (Primary Dick, Reviewer Juan)

Script #1- Extraction 
-----------------------------------------------------------
```
#####Download prices and seriesID s
# Imports for json, requests, 
import requests
import json
import prettytable
headers = {'Content-type': 'application/json'}
data = json.dumps({"seriesid": ['CUUR0000SA0','SUUR0000SA0'],"startyear":"2011", "endyear":"2014"})
p = requests.post('https://api.bls.gov/publicAPI/v2/timeseries/data/', data=data, headers=headers)
json_data = json.loads(p.text)
for series in json_data['Results']['series']:
    x=prettytable.PrettyTable(["series id","year","period","value","footnotes"])
    seriesId = series['seriesID']
    for item in series['data']:
        year = item['year']
        period = item['period']
        value = item['value']
        footnotes=""
        for footnote in item['footnotes']:
            if footnote:
                footnotes = footnotes + footnote['text'] + ','
        if 'M01' <= period <= 'M12':
            x.add_row([seriesId,year,period,value,footnotes[0:-1]])
    output = open(seriesId + '.csv','w')
    output.write (x.get_string())
    output.close()

#### above code will download the gasoline prices / series ids and periods with years into the local machine. 
Other tables and data will either be manually downloaded from the BLS.gov or hard coded directly in the code (if small)
```


**-Download series description tables and periods. Manual download 
**-Upload everything back into into a dataframe.  
**-Use pandas read_csv method to read all three tables into its dataframes 
**-Join three tables into Gas_prices_df

Gas_prices_df will look like this:

SeriesID|Price|Description of the series ID| Months/Periods|Area COde|Area Description|Latitude|Lontgt|


Script #2 - Data Analysis 
-------------------------------------

SeriesID|Price|Description of the series ID| Months/Periods|Area COde|Area Description|Latitude|Lontgt|


1- Calculate pct change month to month
2- Cumulative change over time 
3- Average commute is 30 miles/day

Script #3 - Visualization
------------------------------------
Gas_prices_df analysis using line chart, geoviz, geoJSON, along with average commute data


PowerPoint 
-------------
Page 1 - Introduction+ What the project is about = What are we solving = HR Executive is trying to figure out gas inflation on salary increases 
Page 2 - The data set - where we pulled it from ( BLS_) , how we pulled it,  
Page 3-  Approach to the development :
 -Data extraction (manual or automated) 
 -Data transformation ( creating dataframes,joining tables) 
 -Analysis 
 -Visulizations 
Page 4 - Results - Given that the prices increased but average commute per month/year decreased, the gas inflation has ...... impact on the salary increases. .


 
















