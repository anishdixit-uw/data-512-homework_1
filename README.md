# data-512-homework_1
Anish Dixit code and submissions for DATA 512 Assignment 1

# Goal of the Project

In this project, I try to acquire data relating to Wikipedia article searches for some popular Academy Award winning movies. I also try to visualize some important metrics corresponding to the timeseries data. The aim is to understand the popularity of movies across different eras or years and how it waned or waxed across time.

# Source Data: 

2 columns: Name of the Movie, and link to the Wikipedia Page.

https://docs.google.com/spreadsheets/d/1A1h_7KAo7KXaVxdScJmIVPTvjb3IuY9oZhNV4ZHxrxw/edit#gid=1229854301

# Important Considerations for the Data

The data is largely consistent, with no outliers or missing data. Most of the articles are handled in the standard fashion, but **one of the articles : "Victor/Victoria" cannot be handled in the normal format by urllib.parse.quote, and needs an additional parameter(safe="" "") to be handled**.

# Licensing

1. Wikimedia Foundation REST API terms of use : https://www.mediawiki.org/wiki/API:REST_API#Terms_and_conditions

2. Creative Commons License: https://creativecommons.org/licenses/by/4.0/

# Helpful API Documentation

1. Wikimedia REST API: https://wikimedia.org/api/rest_v1/#/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end

2. Analytics/AQS/Pageviews: https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews

3. Article Page Views API Example: https://colab.research.google.com/drive/1XjFhd3eXx704tcdfQ4Q1OQn0LWKCRNJm

# Coding process followed:

1. Python Notebook (**DATA_512_A1_Data_Acquisition.ipynb**) is used. Initially we import the required libraries, setup constant params relating to Wikipedia Pageviews API used. Article titles were obtained by importing the CSV data given, and fed into the API call URL.

2. Starting with desktop-access, total monthly page view counts for given movies is acquired by running the **request_pageviews_per_article function** and stored into **academy_monthly_desktop_201507-202309.json**, after removing the 'access' field as required.

3. Moving onto mobile accesses, we have mobile-app & mobile-web, both are called one by one. **Remember to change the "access" param in the ARTICLE_PAGEVIEWS_PARAMS_TEMPLATE and rerun the request_pageviews_per_article function**. The data acquired for these 2 access methods are stored into **academy_monthly_mobile_web_201507-202309.json** and **academy_monthly_mobile_app_201507-202309.json**.

4. We then load in data from these 2 JSON files into Pandas dataframes, carry out simple manipulations to **add the pageview counts** from both sources and save it into a final JSON called **academy_monthly_mobile_201507-202309.json**.

5. Moving onto Python Notebook (**DATA_512_A1_Data_Analysis.ipynb**). For the first question asked, we need to identify the movie titles with the maximum and minimum average monthly page views for both desktop and mobile accesses and visualize the same.

6. First, we group data by article, calculate mean views for each article. Then find the articles with the min and the max values from the same. Filter the dataframes to only include these specific articles, and plot the timeseries data (timestamp -> x axis, log(views) -> y axis) ensuring explainability and readability. Save the graph generated into **Max & Min Average.png**

7. The second question, To get top 10 articles for each access types with highest monthly page view values and visualize the same.

8. We group the dataframe by article and select the month with maximum pageview value for each movie. Then sort these in a descending order and select top 10 articles. Filter the dataframes to only include these specific articles, and plot the timeseries data (timestamp -> x axis, log(views) -> y axis) ensuring explainability and readability. Combine desktop and mobile data but ensure they are separably visual. Save the graph generated into **Top 10 movies with highest average views.png**

9. The third question, To get top 10 articles for each access type with least amount of data available.

10. We group the dataframes by articles, and count the total number of occurrences of each article. Then sort the articles in ascending order of number of counts and select top 10 articles. Filter the dataframes to only include these specific articles, and plot the timeseries data (timestamp -> x axis, log(views) -> y axis) ensuring explainability and readability. Combine desktop and mobile data but ensure they are separably visual. Add labels, legends and well separated lines whereever possible. Save the graph generated into **Top 10 movies with least amount of data.png**.

