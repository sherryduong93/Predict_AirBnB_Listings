# Predicting Airbnb Daily Listing Prices
![image](https://moneymorning.com/wp-content/blogs.dir/1/files/2019/04/shutterstock_712018732-1280x720.jpg)

## Motivations & Goals
Airbnb has grown widely in the past five years due to increased interest in travel across the world.

Meanwhile, in the Bay Area/San Francisco in particular, the cost of owning a home has continued to increase substantially year over year due to low supply. 

My goal is this project is to predict daily airbnb listing prices, and understanding the most impactful features for determining listing prices

## Datasets & Exploratory Analysis

### 52 Data Sets Comprised of information for every Airbnb listing available in that month, for 52 months from Sep 2015 to April 2020
<pre>-Data: 395,202 entries, 92 columns
<br>-Null Values: 2842171 
<br>-Missing Monthly Data: 
<br>-2015 only had Sep, Nov, and Dec data
<br>-2016 missing Jan and Mar data
<br>-2018 missing June data</pre>
<br>**Data Cleaning**
<pre>-Removed all columns with more that 70% of data being null
<br>-Converted the "Last Scraped" date to date format, and created additional date features to indicate year, month-year, month, dayofweek, and day
<br>-Converted columns related to currency (price, extra_people, security_deposit and cleaning_fee] from string to float, removed '$'
<br>- ADD</pre>
<br>**EDA Feature Importances**
<br>Numeric Features: (Based on Correlation plot)
<br>-Accommodates, bathrooms, bedrooms, beds, cleaning_fee, security_deposit
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/numeric_corr.png)
ADD
![image](ADD)
ADD
![image](ADD)


## Methodology & Baseline Model
<br>**Methodology:** 
<br>-To simulate real life data, I will use all data up to 2019 (2015 - 2018) to train and validate my model. Then, after all model tuning, will use 2019-2020 data for the final model evaluation.
<br> **Baseline Models: No model tuning or feature engineering besides converting price to log. Will only be used for the model selection for tuning.** 
<br>Features selected for Baseline Model (based on EDA): 'accommodates','bathrooms','bed_type','bedrooms', 'beds','cleaning_fee','extra_people', 'host_response_time', 'neighbourhood_cleansed','property_type','review_scores_cleanliness', 'review_scores_rating', 'room_type', 'security_deposit', 'month-year','month','day_of_week'
<br>Data Processing: Converted Categorical Data to Dummies.
<br>**Baseline Model Performance**
<br>-Linear Regression: R2: 0.61, RMSE: 1.20
<br>-Decision Tree Regressor: R2: 0.81, RMSE: 1.09
<br>-Random Forest Regressor: R2: 0.86, RMSE: 1.06
<br>-Gradient Boosting Regressor: R2: 0.65, RMSE: 1.17
<br><br>**Will proceed to tuning Random Forest Regressor**
![image](ADD)
![image](ADD)
<br><br>
### Results: ADD
**ADD
<br>ADD**
<br>-ADD
<br>-ADD
<br>**ADD**
![image](ADD)
<br><br>


## Conclusion: 



## Assumptions Made & Caveats....
<br>-Data Source: InsideAirbnb.com. Listing Prices are set by the host and may not reflect the final price paid by the tenant.

## Goals for future Analysis:


