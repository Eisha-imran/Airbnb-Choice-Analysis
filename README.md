# Airbnb-Choice-Analysis
### Introduction
Airbnb was founded in 2008 and since then it has changed the travel and hospitality industry around the world greatly. Airbnb offers short-term rentals as opposed to traditional hotels by being pocket-friendly for those looking for accommodations and allowing house owners to rent out their properties to guests. In a city like Toronto, which Boyd (2024) estimates will have 8.95 million visitors in 2023, Airbnb is a major influence on the housing market and the visitor experience. Airbnb offers alot of possibilities to tourists and other clients, enabling homeowners to optimize their profits through clever placement of their apartments. Comprehending the elements that impact client happiness and long-term performance is crucial for both visitors wanting exceptional experiences and hosts hoping to maximize their profits. In this project, we are analyzing Toronto Airbnb listings, reviews, and availability data to help Airbnb customers get value for their money and to help Airbnb hosts improve customer experiences, and by inference, maximize profit.

### Motivation
This project's motivation stems from our curiosity about how Airbnb listings in a lively city like Toronto can tell the story of customer experiences, host behaviors, pricing strategies, and the impact of local festivals on the overall demand and pricing of Airbnb.

It has become important to mention that we are not being sponsored by Airbnb for this project.

### Datasets
The datasets for our project were retrieved from Inside Airbnb, a mission-driven initiative that provides data and advocacy about Airbnb's impact on residential communities (Airbnb, n.d.-a). Their data is licensed under a Creative Commons Attribution 4.0 International License (Airbnb, n.d.-b). This License allows others to share, copy, redistribute, adapt, and build upon the material for any purpose, including commercial use, when proper credit is given (Creative Commons, n.d.).

We will analyze multiple datasets to assess the Airbnb market in Toronto, Ontario, Canada. The datasets, generated quarterly over the past 12 months, are in CSV format, making them easy to process using Python. At the time of this proposal, Inside Airbnb last scraped the datasets from the Airbnb website on the 5th of September 2024, compiling listings and reviews as of that date. As a result, we have data on calendar availability and pricing from September 2024 to September 2025.

#### The key datasets for this analysis include:

**Detailed_listings.csv:** Contains information about each Airbnb listing, including amenities, location, property type, et cetera. It has 21,825 rows and 75 columns. Out of 75 columns, we have mainly used columns i.e. id, price, host_acceptance_rate, host_response_rate, amenities, beds, bedrooms, bathrooms, room_types, neighbourhood_cleansed, review_scores_rating

**Detailed_reviews.csv:** Includes guest reviews, review dates, et cetera. It has 573,077 rows and 6 columns which are listing_id, id , date, reviewer_id, reviewer_name, comments.

**Neigbourhoods.csv:** Provides a list of neighborhoods. It has 140 rows and 2 columns i.e. neighbourhood_group, neighbourhood.

**Calendar.csv:** Provides information on Airbnb pricing and availability over one year. It has 7,966,127 rows and 7 columns from which we utilised listing_id, date, available, price, minimum_nights, maximum_nights

**Events.csv:** Provides information on specific dates for each event and how these dates correlate with Airbnb demand and pricing. It has 52 rows and 4 columns i.e. event, date_started, date_ended, comments.

### Guiding Questions
Our guiding questions revolve around:

##### What neighbourhoods in Toronto offer the best value for money in terms of price and review score?

This question is about finding out which neighbourhoods in Toronto offer the best balance between cost and customer ratings. Both price and reviews are very important when people choose Airbnb. According to Inside Airbnb, these factors are key in deciding how happy guests are with their stay (Inside Airbnb, 2023). The answer will help understand which neighbourhood has a better match between price and review scores, providing a valuable suggestion for future customers.

##### What is the trade-off between price, amenities, and customer satisfaction in Airbnb listings?

This question looks at how price, amenities, and customer satisfaction are connected. For Airbnb hosts, it's important to know what amenities make the price worth it. Airbnb’s blog mentions that things like Wi-Fi, parking, and a kitchen can affect how happy guests are (Airbnb News, 2023). For example, if a host wants to charge $200 per night, what amenities should be included? Answering this can help hosts decide how to price their listing and which amenities to offer.

##### Is there a relationship between the number of listings a host has and their reviews?

It helps to identify whether hosts can manage all their listings without affecting service quality, whether the host with more experience may attract more guests, and how scaling up impacts guest satisfaction. It is important as it provides insights into how Airbnb can create a better support system and identify best practices.

##### As a business owner, what attributes do customers value the most, based on reviews?

This question allows hosts to know what amenities customers prefer when looking for an Airbnb. With this, they can invest in a place where they can provide maximum amenities for improved customer experience. This is important as there is high competition in the market with multiple options to choose from.

##### Are there any seasonal trends in the number of customer reviews on Airbnb?

This can help Airbnb understand the best times to encourage customers to write reviews. If we find patterns, Airbnb can use this information to send out reminders to guests to leave a review during the right times. With this answer, Airbnb can choose the best times to invite guests to write reviews, improving the number of reviews on the platform.

##### How do local festivals and events in Toronto impact Airbnb demand and pricing trends?

We will use additional data on annual events in Toronto and compare them with the dates of Airbnb listings and calendar data to see if we can draw any meaningful correlations between demand, pricing or availability around these festivals.

In the course of our exploration, our questions have definitely evolved with interesting findings and a few roadblocks. Each team member worked on cleaning and exploring separate tables in our dataset (listings, reviews, calendar, neighborhood, and events), eventually coming together to discuss results and find connections between our findings. We will discuss these tables consecutively.

### Data Loading
We utilized the following libraries and used gdown.download() to download all the datasets from Google Drive.
```
# import required modules
from nltk.sentiment import SentimentIntensityAnalyzer # for sentiment analysis
from deep_translator import GoogleTranslator # for translation services
from collections import Counter
import matplotlib.pyplot as plt
from wordcloud import WordCloud # for unstructured text visualization
import seaborn as sb
import pandas as pd
import numpy as np
import calendar # for date analysis
import nltk # for unstructured text analysis
import gdown # for downloading data from google drive
import ast # for type conversions
import re # for regex
import os

# download stopwords from nltk to get a list of English stopwords
nltk.download('stopwords')
# download VADER for sentiment analysis
nltk.download('vader_lexicon')

# import stopwords after download
from nltk.corpus import stopwords
```
