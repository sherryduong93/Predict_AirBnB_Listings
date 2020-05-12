# Predicting Airbnb Daily Listing Prices
![image](https://moneymorning.com/wp-content/blogs.dir/1/files/2019/04/shutterstock_712018732-1280x720.jpg)

## Motivations & Goals
Airbnb has grown widely in the past five years due to increased interest in travel across the world.

Meanwhile, in the Bay Area/San Francisco in particular, the cost of owning a home has continued to increase substantially year over year due to low supply. 

My goal is this project is to predict daily airbnb listing prices, and understanding the most impactful features for determining listing prices

## The Datasets

### 52 Datasets Comprised of information for every Airbnb listing available in that month, for 52 months from Sep 2015 to April 2020
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
## EDA Feature Importances
### Overview of the Data from 2015-2018 (Train Data)
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/Daily_rate_over_time.png)
<br>-There is clear seasonality between months. Spike in Airbnb Rentals in 2017 were strongly linked to rent increases in some of the largest US metro areas.
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/Distribution_Daily_Prices.png)
<br>-Distribution of the daily listings do not follow a normal distribution, so we will take the log and remove the outliers
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/Log_DailyRates.png)
<br>-Now that the dependent variable follows a normal distribution, this will likely help with our predictions.
### Numeric Features: (Based on Correlation plot with correlation over 1%)
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/numeric_corr.png)
<br>-Accommodates, bathrooms, bedrooms, beds, cleaning_fee, security_deposit, review_scores_rating, review_scores_cleanliness, review_scores_location,   review_scores_accuracy, review_scores_communication, review_scores_checkin, review_scores_value, extra_people, month, year, number_of_reviews
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/price_vs_accom.png)
-There is a trend, the more rooms/accomodations available will increase the listing price until a certain threshold, where it appears it no longer matters and does not affect price. Likely due to the fact that places with that much space have difficulties filling.
### Categorical Features
<br>-Features that seem to have an impact: neighbourhood_cleansed, property_type, room_type
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/neighborhood_dist.png)
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/propertytype_dist.png)
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/roomtype_dist.png)

## Methodology & Baseline Model
<br>**Methodology:** 
<br>-Test-Split Option 1: Train Data will be from 2015 - 2018. Test data from 2019-2020.
<br>-Test-Split Option 2: Randomized Test Size of 30% with all available data
<br><br> **Baseline Models: No model tuning or feature engineering besides converting price to log. Will only be used for the model selection for tuning.** 
<br>Features selected for Baseline Model (based on EDA): 'accommodates','bathrooms','bed_type','bedrooms', 'beds','cleaning_fee','extra_people', 'host_response_time', 'neighbourhood_cleansed','property_type','review_scores_cleanliness', 'review_scores_rating', 'room_type', 'security_deposit', 'year','month','day_of_week'
<br>Data Processing: Converted Categorical Data to Dummies.
<br><br>**Baseline Model Performance**
<br>-Between both Test-Split Options, the performance of the models were the same.
<br>-Linear Regression: Cross-Val R2: 0.61, RMSE: 1.20
<br>-Decision Tree Regressor: Cross-Val R2: 0.81, RMSE: 1.09
<br>-Random Forest Regressor: Cross-Val R2: 0.86, RMSE: 1.06
<br>-Gradient Boosting Regressor: Cross-Val R2: 0.65, RMSE: 1.17
<br>**Will proceed with Random Forest Estimator for future iterations.**
<br><br>**Feature Importance from Baseline Model**
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/Feature_imp_BaseModel_RF.png)
<br>Most important feature: Number of Bedrooms
<br>Second: Whether or not the Airbnb was access to an entire home/apartment, with the 8th most important feature capturing whether or not the Airbnb was a shared room or not. Seems to highlight that travellers have a preference on privacy.
<br>Fees also seem to be important, with all 3 fee categories in the top 20
<br>Review ratings overall & cleanliness rating contributed to the price, which makes sense.
<br>Year: Interestingly, year made it into the top 20, but not month. This could be due to the fact that 2017 was vastly different from any other year.
<br>Property type: Whether or not the property was a house/apartment was also important.
<br>Appears that neighborhood may not be as important as suspected, though it appears neighborhoods downtown rank higher overall in the feature rankings.
![image](ADD)
<br><br>
### Feature Engineering
<br>**Converting The Fee Columns to "0/1" based on whether or not they had the fee**
<br>-Cross-Validation R2 for Random Forest dropped to 0.82
<br>-Next Step: Keep columns as is
<br><br>**Count Of Amenities**
<br>-ADD
<br><br>**Categorical Feature for Accomodations/beds/bedrooms/bathrooms**
<br>Is it above a threshold? Otherwise, price could be lower
<br><br>**Neighborhoods**
<br>After converting the price density into a heatmap on top of San Francisco, it is apparently that the highest listing prices are concentrated in the center of San Francisco.
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/scatter_heatmap_neighborhoods.png)
![image](https://github.com/sherryduong93/Predict_AirBnB_Listings/blob/working/Graphs/all_listings_sf.png)
<br>From this insight, I created a new feature to capture whether or not the listing was in the city center, which I determined as 1 if neighborhood within list: [X,X,X], and 0 if not.
<br><br>**If time permits NLP text vectorization of columns**
<br>-ADD
![image](ADD)
<br><br>



## Conclusion: 



## Assumptions Made & Caveats....
<br>-Data Source: InsideAirbnb.com. Listing Prices are set by the host and may not reflect the final price paid by the tenant.

## Goals for future Analysis:


