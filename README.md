# Wrangling WeRateDogs Twitter Dataset

### Introduction
WeRateDogs is a Twitter account that rates user submitted photos, usually with humorous content. It has a unique rating system that comprises of a numerator and denominator. The numerator is usually greater than that the denominator. The main object of this project will be gather, wrangle and retrieve some insights of the WeRateDogs account that will be retrieved from different sources.

<p>
    Data for this project was retrieved from three different source. The first batch was retrieved from a CSV file
    (twitter-archive-enhanced.csv). This file was downloaded and loaded into dataframe called archives_df using the
    pandas read_csv method. The second batch was downloaded pragmatically using the requests library and written into a
    predictions.tsv file that was stored in the project’s root folder. The Pandas’ read_csv method was subsequently used
    to read the data from the file that it was saved into predictions_df dataFrame. The last batch of data was retrieved
    from a text file that contained JSON data. I used the glob module to find text files in my working directory, then
    used a For Loop together with the Python readline() method to read each line of the file. I then converted what was
    read using the readline method into a json Object that I later parsed into a Python dictionary object.
</p>

<p>
    After testing and ensuring that I had loaded all the datasets correctly into their respective dataframes, I
    proceeded with assessing the 1st data from the archives CSV file both visually and programmatically. I used the
    pandas.DataFrame.sample method to get a visual representation of how the rows were populated. I noticed that some
    columns had populated almost entirely by NULL values.
</p>

<h5> List of Data Quality isssues that were noted in the datasets </h5>
<h6>archive_df Table</h6>
<ol>
    <li>duplicate tweets inform of retweets</li>
    <li>tweet_id is an integer instead of a string object</li>
    <li>timestamp is a string object</li>
    <li>in_reply_to_user_id, in_reply_to_status_id, retweeted_status_timestamp, retweeted_status_id and
        retweeted_status_user_id columns have null values</li>
    <li>The source of the tweet is embedded in html tags in the source column</li>
    <li>missing names represented as None</li>
    <li>names extracted incorrectly in some cases i.e 'a', 'the', 'an' among many others</li>
    <li>rating_denominator is greater than or less than 10 in some cases</li>
</ol>

<h6>additional_tweet_df Table </h6>
<ol>
    <li>created_at column in the additional_tweets_df is a duplicated of the timestamp column in archives_df</li>
    <li>tweet_id is an integer instead of a string object</li>
</ol>
<h6>predictions_df Table </h6>
<ol>
    <li>tweet_id is an integer instead of a string object</li>
</ol>

<h5>Tidiness Issues</h5>
<ol>
    <li>The doggo, floofer, pupper and puppo identifiers should unpivoted into a single column</li>
    <li>The three tables should be merged into a single unit.</li>
</ol>


## Summary of Findings

###### Insight 1:
The day with the most number of tweets is Monday
The first insight that was produced from the data was in relation to the frequency at which the WeRate Dogs twitter account sent out tweets. We found that most of the tweets were sent out on Monday and the day with the least tweets was Sunday. In order to arrive to arrive at these findings, we first identified the timestamp as the column that we were going to base our calculations on. Then, the second step was to retrieve the days of the week from the datetime object using the .dt accessor and the day_name() function.

###### Insight 2.
Tweets sent out between 12:01PM and 11:59PM were favorited more than tweets sent out in the morning. 
The second insight was retrieved from the timestamp and favorite_count columns.  We found that most of the favourited   tweets were sent out in the afternoon than those that were sent out in the morning. To arrive at this insight, we first select favorite_count column and the group it using the timestamp column [morning/afternoon] categories. 

###### Insight 3:

The series object returned by the value_counts method indicates that the two items with the highest count were the unnamed dogs under the `no_name` and `incorrect_name` categories. The most common names after this category  were `Charlie` and `Lucy` which had a count of 11.
The third insight was on the most common name of dogs in the dataset. In this case, this finding can be retrieved by using the value_counts method to obtain the count of unique names. The highest portion of the name column was occupied by both unnamed and misnamed entries. The most common names were Charlie and Lucy with a count of 11 followed closely by Oliver and Cooper whose count stood at 10. 
