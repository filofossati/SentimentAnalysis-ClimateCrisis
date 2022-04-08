# A Sentiment Analysis on Environmentalism 


## Problem Statement 

Extreme weather events such as wildfires and hurricanes have been already intensifying at a pace that scientists did not predict. The Intergovernmental Panel of Climate Change (IPCC) in its 2021 [climate science report](https://www.ipcc.ch/report/ar6/wg1/) clearly articulates that: 1)it is virtually likely that human activities are the main cause of global warming and thus the exacerbation of extreme weather events; 2) the world is getting closer to irreversible tipping points and thus heading in a world that goes beyond 1.5 degree of warming. 

It is interesting to notice how the perception of this climate crisis has changed in the majority of the world population in the recent years. In fact, recent studies suggest that the younger generation has been developing a climate anxiety about their future. For instance, on September 2021, [Nature](https://www.nature.com/articles/d41586-021-02582-8) published a survey of 10,000 young people showing that "negative feelings about climate change can cause psycological distress". 27% and 32 % of interviewees were respectively extremely worried and very worried about climate change. Only 5% were not worried. The most common words utilized in the same survey were said, afraid, anxious, angry, powerless, guilty, optimistic and indifferent.

An American non-profit organization wanted to have  a better picture of the general sentiment that people have when talking about environmental-related topics. More specifically, they wanted to understand whether by talking about climate change in more broaden context such as sustainability, the overall sentiment could become more propositional and less catastrophic. 
Serving as a data scientist in this organization, I decided to apply a Sentiment Analysis - an area of natural language processing that classifies text as having either positive or negative emotion - over two different subreddits: sustainability and climatechange. Because the sustainability subreddit is more focus on the solution side of the environmental crisis, the hypothesis is that its overall sentiment score should be more positive than the one for climate change; and I am expecting that this difference should improve model's predictions.


### Data Dictionary

The data dictionary reports the only features that I use throughout the whole project. Thus, there will be the descriptions of features that I used for poly trasformation, and the ones I used for fitting the regression model. 

|Feature|Type|Dataset|Description|
|---|---|---|---|
|title|object|reddits.csv| the title of the post |
|selftext|object|reddits.csv| the content of the post | 
|subreddit|object|reddits.csv| the group the post is coming from |
|subreddit|int|reddits_cleaned_sentiment.csv| the group the post is coming from, binarized |
|title_selftext|object|reddits_cleaned_sentiment.csv| the union of the title and the content of a post|
|sentiment_score|float|reddits_cleaned_sentiment.csv| the compound score coming from the Sentiment Analysis|



## Summary of the Analysis

To answer to the problem statement I needed to find first two separate online groups that were talking about respectively climate change and sustainability. To do that, I decided to pull about ~19000 posts from two separate groups on reddits: [sustainability](https://www.reddit.com/r/sustainability/) and [climatechange](https://www.reddit.com/r/climatechange/). After taking a look at the posts and making some data cleaning I ended up utilizing ~4000 posts for each subreddit. Successively, I built two separate Logistic Regression classification models that could analyze the posts and predict from which group the text was coming from. The sentiment compound score coming from the Sentiment Analysis was added as additional feature only to the second logistic model. If there was a difference in the compound score between the two groups, the classification model could detect this signal and improve its predictions. Lastly,I repeated the with and without sentiment analysis with a Random Forest classification model. 


## Conclusions

The non-profit organization was interested to understand whether by talking about climate change in a more broaden context such as sustainability, the overall sentiment that people have when talking about environmental-related topics could become more propositional and less catastrophic.  

As shown in Part 2 of this project, the sustainability group tends to present a more positive distribution of its sentiment scores with a median value of 0.25 against 0.00 for climate change. Moreover, in part 3, we have seen how the word **anxiety** is within the 10 best  predictors for the class climate change. This seems to confirm the original hypothesis where I was expecting to detect a more positive sentiment in the sustainability group as people tend to be  more focus on the solution side of the environemntal crisis. 

The difference of the compound between the two groups was great enough to create a signal that the logistic model classifier could detect to sharpen its predictions. Infact, thanks to the Sentiment Analysis, the overall accuracy of the Logistic Regression increased from .815 up to .821. We can also see improvement in its precision and specificity metrics. The only score that experienced a drop is the sensitivity. 

This with and without analyis has been replicated with a Random Forest Classifier. However, the predictions of both models were less accurate than the ones obtained through the Logistic Regression Classifiers. 
A summary of the different scores for all models is provided below



|Model|Sensitivity|Specificity|Accuracy|Precision|
|---|---|---|---|---|
|Logistic Regression |0.844|0.788| 0.815|0.799 |
|Logistic Regression with Sentiment Analaysis |0.838 |0.804| 0.821 | 0.810|
|Random Forest|0.847|0.785| 0.816 |0.802|
|Random Forest with Sentiment Analaysis|0.870|0.751| 0.811 |0.783|






