# WeRateDog_Data_Wrangling_Project


## Data Wrangling of 'WeRateDog' Twitter Dataset
Data in its raw form is not useful for analysis and predictions. Data wrangling is the processing of transforming raw data to useable data for data analysis and machine learning predictions. If data wrangling is not properly carried out, it will lead to false conlusion which will affect the decisions and insights drawn from it.

This project was carried out to demonstrate data wrangling process on 'WeRateDog' twitter dataset. The data wrangling procedure was divided into three stages; gathering, assessing and cleaning.

## Data Gathering
The data used for this project was collected from three different sources. The first data (twitter_archive.csv) was provided in the working environment. The twitter_archive_csv was read to dataframe using the pandas pd.read_csv() method.

The link to the second dataset (image_prediction.tsv) was provided which the request library was used to get the file, the os library was used to store the data into the working environment and pandas read method was used to load the data into dataframe.

The last dataset (tweet_json.txt) for the project was supposed to be downloaded by querying the Twitter API using the tweepy library but I used the provided file since I could not obtain the Twitter developers' account. I extracted the needed information (tweet_id, retweet_count and favorite_count) from the json file using the json library and the data was loaded to dataframe using the pandas read method.

## Data Assessment
Once all the required data have been successfully loaded, data assessment was performed on the each dataframe to inspect how messy or dirty the data is. Both visual and programmatic assesment was carried out each dataset to uncovery any quality or tidiness issue in the dataframe. Although the amount of quality and tidiness issue in the datasets are many, only eight (8) quality issues and two (2) tidiness issue were recorded for cleaning.

### Quality issues
#### twitter_archive table
- Missing values in some columns (in_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp)

- Improper names in the name column ('a', 'actually', 'all', 'an', 'by', 'getting', 'his', 'incredibly', 'infuriating', 'just', 'my', 'not', 'None', 'officially', 'one', 'quite', 'space', 'such', 'the', 'this', 'unacceptable', 'very')

- timestamp is string not datetime

- tweet_id should be in string not int

- original ratings only with no retweets that have images

- source column should be category not object

- source column contain url

#### image_prediction table
-Mixed uppercase and lowercase value in columns p1, p2, and p3

### Tidiness issues
- One column (dog_stage) spread in four columns ('doggo', 'floofer', 'pupper', 'puppo')

- twitter_api_df should part of tweet_archive_df

## Data cleaning
All the documented tidness and quality issues discovered during the data assessment stage were cleaned. First, retweet values present in the twitter_archive_df were removed since we only need the original tweet for analysis. Next, the column with large missing values were dropped from the dataframe using the pandas drop() method.

After the missing values issues were addressed, the two tidiness issues were taken care of. The pd.melt() function was used to collapse four columns ('doggo', 'floofer', 'pupper', 'puppo') into two ('stage', 'dog_stage'). Subsequently, the 'stage' column was dropped and the duplicate values were removed from the dataframe. Then, two dataframes (twitter_archive_df and tweet_count_df) were merged into one dataframe (twitter_archive_count_df) since two tables contains information about tweets.

Once the tidiness issues have been addressed, the remaining quality issues were resolved. The source values were extracted from in the 'source' column using the str.extract() method. Improper names present in the name column were replaced with 'NaN' value and wrong datatypes were changed to their correct datatypes.
