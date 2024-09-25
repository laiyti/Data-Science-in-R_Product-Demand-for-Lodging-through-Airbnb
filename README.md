## Project Background

  Airbnb has revolutionized the hospitality industry by providing a platform for homeowners to rent out their properties and travelers to find unique accommodation options. As the platform continues to grow, hosts face increasing competition, making it crucial for them to optimize their listings to attract guests and maximize their booking rates.

  This data science project aims to answer the question: How do guests book on Airbnb? What's the secret behind properties with such high booking rates? It seeks to address this challenge by developing a predictive model to identify properties with a high booking rate on Airbnb. By leveraging a diverse array of features ranging from property attributes to host characteristics, our model will provide actionable insights to empower hosts in enhancing their rental business performance.

  For the final report, please check [here](https://drive.google.com/file/d/1ak_LzncgwwJsaY078Mlb0c7nb968e3Um/view?usp=sharing).

## TargetAudience
Our predictive model is tailored for Airbnb hosts seeking to improve their rental property's booking rate and overall profitability. Additionally, property management companies, real estate investors, and Airbnb itself can benefit from the insights generated by our model to inform decision-making processes and drive business growth.

## Data Understanding

| ID | Feature Name | Description |
| --- | --- | --- |
| 1 | accommodates | the number of people can be accomodated
| 2 | availability_rate_30 | how many days out of the next 30 the listing is available for divided by 30
| 3 | availability_rate_60 | how many days out of the next 60 the listing is available for divided by 60
| 4 | availability_rate_90 | how many days out of the next 90 the listing is available for divided by 90
| 5 | availability_365 | how many days out of the next 365 the listing is available for divided by 365
| 6 | bathrooms | number of bathrooms in the listing
| 7 | bed_type | description of the bed
| 8 | bedrooms | number of bedrooms in the listing
| 9 | beds | number of beds in the listing
| 10 | cancellation_policy | description of how strict the 72 cancellation policy is
| 11 | has_security_deposit | 1 means has, 0 means no
| 12 | has_cleanning_fee | 1 means has,0 means no
| 13 | host_total_listings_count | how many total listings the host has ever had
| 14 | price | price to rent the listing for one night
| 15 | ppp_ind | ppp_ind is 1 if the price_per_person is greater than the median for the property_category, and 0 otherwise
| 16 | property_category | group property type into 4 groups
| 17 | bed_category | group bed type into bed, real bed and other
| 18 | bathrooms | number of bathrooms in the listing
| 19 | charges_for_extra | the value "YES" if extra_people > 0 and "NO" if extra_people is 0 or NA
| 20 | host_acceptance | percent of stay requests the host accepts
| 21 | host_response | percent of stay requests the host accepts
| 22 | has_min_nights | "YES" if minimum_nights > 1, and "NO" otherwise
| 23 | market | Airbnb's definition of the market that the listing competes in
| 24 | max_nights_group | group maximum night into 3 groups. short-term, medium-term, long-term, very long-term and no limit
| 25 | requires the host to have a license or not | requires the host to have a license or not
| 26 | host_year | assume the data is in 2020, calculate how many years that the host operates the airbnb using variable "host_since". NA treated as 0
| 27 | positive_score | In, "summary", (count of positive words - count of negative words) / max(count of positive words - count of negative words)
| 28 | transit_score | In "transit", (count of positive words - count of negative words) / groupby(market) %>% max(count of positive words - count of negative words)
| 29 | super_host | super host or not
| 30 | has_profile_pic | host has profile pic or not
| 31 | identity_verified | host identify verified or not
| 32 | location_exact | host provide exact location or not
| 33 | instant_bookable | can it book instant or not
| 34 | requires_license | requires the host to have a license or not
| 35 | guest)profile_pic_required | require guest profile pic or not
| 36 | guest_phone_verification_required | require guest phone verification or not
| 37 | interaction_score | In "interaction", (count of positive words - count of negative words) / groupby(market) %>% max(count of positive words - count of negative words)
| 38 | space_score | In "space", (count of positive words - count of negative words) / groupby(market) %>% max(count of positive words - count of negative words)
| 39 | nearby_airport | Combine a dataset of airport codes in the USA with Airbnb listings to calculate the proximity of each listing to the nearest airport. Define listings within 30km of an airport as near_airport
| 40 | nearby_attractions | whether the listing is near the famous attractions in that country
| 41 | jurisdiction_category | further group jurisdiction into 6 groups
| 42 | has_weekly_discount | calculate the expected weekly price and compare with the listing price to see if it has a discount.
| 43 | has_monthly_discount | calculate the expected monthly price and compare with the listing price to see if it has a discount.

## Interest Insight In Features

### Text Mining: Natural Language Processing (NLP) And Sentiment Analysis
The original dataset comprises various customer review texts. We applied NLP techniques and sentiment analysis to transform these texts into scores, reflecting customer satisfaction with specific aspects of the property and its management. Additionally, we engineered new features such as positive_score, transit_score, interaction_score, and space_score to quantify satisfaction across different categories.

### Amenities
We used K-Means to cluster amenities into 10 groups to analyze their impact on availability. Across most markets,listings with amenities from cluster 2 tend to be booked more frequently. Notably, hosts in Seattle favor amenities from cluster 7, indicating strategic preferences for boosting bookings.

<img width="708" alt="Screenshot 2024-09-25 at 3 13 49 PM" src="https://github.com/user-attachments/assets/b190efc5-0063-4a59-baa8-814ffa7a902e">

### Distance To Airport
With our domain knowledge, we hypothesize that distance from the airport significantly affects Airbnb
listing booking rates. From the violin plot, we observe that the median distance for both high and low
booking rate listings is similar. However, the distribution of the violin area suggests that listings farther from the airport are more likely to have lower booking rates.

<img width="699" alt="Screenshot 2024-09-25 at 3 16 07 PM" src="https://github.com/user-attachments/assets/ef9f5c99-b81b-4b00-840a-85193985aab2">

## Evaluation and Modeling
### Model Overview
Our team created 6 models, including Logistic, Ridge, Lasso, XGBoost, Boosting, and Random Forest. Discussing splitting the data in detail, we separated into training, testing, and validation data. Then we took the training data to train our model and predict our model on the validation data to get the AUC value. After running all the models, we plotted the models’ AUC curves on the same plot and chose the top 3 winning models with the best AUC then trained the whole data to receive the models’ probability. Finally, we averaged these models’ probability for the final prediction.

We selected three winning models based on their performance evaluated through the average model evaluation performance (AUC) on cross-validation. Our final winning models are: ***random forest, XGboost, boosting***. Subsequently, we further validated their performance using a small held-out dataset, which was utilized only once. This final validation step with the small dataset aims to mitigate the risk of overfitting on the validation data.

### Model Performance
| Model Name | AUC |
| --- | --- |
| Random Forest | 0.88 |
| Boosting | 0.88 |
| XGBoosting | 0.86 |
| Logistic | 0.84 |
| Ridge | 0.84 |
| Lasso | 0.84 |
<img width="403" alt="Screenshot 2024-09-25 at 3 19 50 PM" src="https://github.com/user-attachments/assets/017c7956-7e15-4824-921c-b1d04de88a59">

### Feature Importance
The plot below uses the random forest to generate a features importance chart and see which variables are more important to the model in two aspects, giving us some insight.

<img width="534" alt="Screenshot 2024-09-25 at 3 56 53 PM" src="https://github.com/user-attachments/assets/e475bac5-5826-4246-8258-b59854ba15da">

