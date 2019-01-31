# WeRateDogs - Data Wrangling & Analysis
#### by Ernest Rowe
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/iRowebot/Wrangling-Analysis-Visualization-WeRateDogs-Tweets/master?filepath=wrangle_act.ipynb)

## Introduction

The dataset for this project is the tweet archive of Twitter user [@dog_rates](https://twitter.com/dog_rates), also known as [WeRateDogs](https://en.wikipedia.org/wiki/WeRateDogs). WeRateDogs is a Twitter account that rates people's dogs with a humorous comment about the dog. These ratings almost always have a denominator of 10. The numerators, though? Almost always greater than 10. 11/10, 12/10, 13/10, etc. Why? Because "[they're good dogs Brent.](http://knowyourmeme.com/memes/theyre-good-dogs-brent)" WeRateDogs has over 4 million followers and has received international media coverage.

Data was gathered in different formats from a variety of sources using Python and its libraries. The data was then assessed for quality and tidiness issues and subsequently cleaned of those errors. Once cleaning was complete, visualization and analysis were performed and presented as an internal document.  

## Gathering

Data for this project consisted of the 3 sources:

- The WeRateDogs Twitter archive. This file was downloaded manually by clicking the following link: [twitter_archive_enhanced.csv](https://d17h27t6h515a5.cloudfront.net/topher/2017/August/59a4e958_twitter-archive-enhanced/twitter-archive-enhanced.csv)
- The tweet image predictions, i.e., what breed of dog (or other object, animal, etc.) is present in each tweet according to a neural network. This file (image_predictions.tsv) hosted on Udacity's servers was downloaded programmatically using the Requests library on the following URL: https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv
- Each tweet's retweet count, favorite (i.e. "like") count and tweet length. Using the tweet IDs in the WeRateDogs Twitter archive, the Tweepy library was used to query Twitter's API for each tweet's JSON data. Each tweet's entire set of JSON data was then stored in a file called tweet_json.txt file, with each tweet's JSON data stored on its own line.


## Assessing

After gathering and loading each of the above sources of data, they were assessed visually and programmatically for quality and tidiness issues. The following issues were discovered:

### Tidiness
* All DataFrames should be inner joined on `tweet_id`.
* `doggo`, `floofer`, `pupper` & `puppo` columns should be a single `dogscription` column.

### Quality
#### `df_twitter_archive`
* 183 of the tweets are retweets.
* Retweet related columns can be removed after retweet records are removed.
* `rating_numerator` and `rating_denominator` are sometimes wrong.
* Remove ratings for non-dog tweets and correct numerators that have errors.
* `in_reply_to_status_id`, `in_reply_to_user_id`, `retweeted_status_id` & `retweeted_status_user_id` should be formatted as strings to fix scientific notation.
* `timestamp` is formatted as strings.
* 109 misidentified names & 745 "None" string values in `name` column. "O" should be "O'Malley". "None" strings should be None type.
* `source` column contains HTML tags.
* Only 2075 `tweet_id`'s had records in `df_image_predictions`. The 281 missing from `df_image_predictions` should be dropped.
* Make `timestamp` display in Eastern Time since that's where the account owner lives.

#### `df_image_predictions`
* Images with 'False' values for all 3 of `p1_dog`, `p2_dog` & `p3_dog` are unlikely to contain images of dogs.
* Multi-word predictions in columns `p1`, `p2` & `p3` use '_' instead of spaces.

## Cleaning
Each of the issues identified in the assessment stage were cleaned using the process of Define, Code, and Test. The Define step outlined what needed to be done, then Code was written to fix the issue either programatically or manually, and Tested to confirm that the Code achieved what it needed to.

##### Resources:
https://classroom.udacity.com  
https://stackoverflow.com/  
https://stackexchange.com/  
http://seaborn.pydata.org  
http://youtube.com  
https://twitter.com  
http://www.tweepy.org/  
https://media.readthedocs.org/pdf/tweepy/latest/tweepy.pdf  
https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv
