# Natural-Language-Processing-NLP-on-TechCrunch-Blogs
Used Spark to conduct NLP analysis on writing style, topic modeling and sentiment analysis on Techcrunch's blogs
## Executive Summary

TechCrunch is one of the most popular technology media property in the U.S. It not only has a high exposure, but also owns valuable readership. Our project aims to apply Natural Language Processing (NLP) to help TechCrunch transform its valuable readership into value. More specifically, we want to help it identify what writing styles and topics are related with higher influence and better reader’s reaction. As a result, it could attract more advertiser and content sponsor and generate more revenue.

We first applied writing style and topic modeling on TechCrunch posts and then applied sentiment analysis on its comments. Finally, we did exploratory data analysis and developed regression models. It is showed that Topics relates to new product announcement, social networks, and devices are most popular. TechCrunch could partner with advertisers and content sponsors to promote their devices and social networks products. Additionally, readers prefer blogs with longer words but shorter sentences as well as blogs with higher vocabulary richness and readability. TechCrunch could train its bloggers to focus on these features and write more attractive blogs. 
## Business Objective and Initiative

TechCrunch is a leading technology media property, who is dedicated to obsessively profiling startups, reviewing new Internet products, and breaking tech news. It has 13 million followers that generate 26 million monthly page views. More importantly, it owns valuable readership, with 19% considering themselves influential and 44% earn an annual household income of $110K+. However, the problem is how can we transform the valuable readership into value. 

Like all the media property, TechCrunch’s revenue is mainly driven by the advertisement and the sponsored content in the blogs. Advertisers are concerned with the influence of the blog, and content sponsors are interested in both the influence of the blog and the reader’s reaction. We aim to apply Natural Language Processing (NLP) to identify what factors will affect the influence and reader’s reaction and to provide TechCrunch with insights to attract more advertisers and content providers to generate more value.


How can we measure if we successfully transformed the valuable readership into value? We use both direct and indirect metrics. The direct metric is the revenue generated by the advertisement and the sponsored content. It is straightforward, but it might take a long time to measure. The indirect metrics will be what drive the revenue, which are the price and volume of the advertisement, which are related to the influence of the blog and the reader’s reaction. The former one could be measured by the page views and the number of comments and shares, and the latter one could be measured by the sentiment analysis of the comment, and we strongly recommend TechCrunch to add a like/unlike feature to better capture the reader’s reaction. Additionally, we could measure user acquisition by the number of registration and subscription as well as user engagement by the number of their pageviews, comments, and shares.
Think through the Analytics
Data

To comprehensively capture the factors related to the bloggers and blogs, we applied analysis on a series of datasets with multiple metrics. The author dataset contains 107 bloggers of TechCrunch, with computed influence index, MEIBI, which relates to the number of the blog post’s inlinks and its comments, as well as MEIBIX, which relates both the number and age of inlinks and comments. The post dataset contains 19464 posts by those bloggers and the comment dataset contains the 746561 comments which were submitted by the readers of those posts. We will try to identify writing styles and topics for post dataset, and sentiments for comment dataset. For further model development and measurement, the data could be collected from the TechCrunch database.



## Types of Analytics

The analytics is mainly prescriptive, we hope to identify what contributes to the influence and reader’s reaction, then provide suggestions to improve these aspects accordingly. We applied Explanatory Data Analysis (EDA) and regression to identify the factors and wanted to further test our findings by experiments such as A/B testing.

### Executing the Analytics

The data analytics team will be responsible for data collection, data analytics. Additionally, they need to closely cooperate with marketing and financial team to test the success of the project.  Here are some key steps on how we execute the analytics, including writing styles identification, topic modeling, sentiment analysis, and regression.
### Writing Styles Identification

First, we tried to identify the writing styles for the posts. Writing styles could be complex, and we broke it down into three aspects with multiple metrics. The first aspect is lexical features, which are the most basic features that tell us about the structure of the text. The second aspect is vocabulary richness features. Richness refers to the diversity of the vocabulary, for example, posts with low richness have limited vocabulary repeated over and over again. The final aspect is the readability scores. Readability stems from the field of linguistics and researchers have frequently used linguistics’ laws to determine the metrics.

In short, the first aspect differentiates the complexity of the text, the second one differentiates the diversity of the vocabulary, and the final one differentiates the understandability. We processed the text and calculated more than twenty metrics for further modelling.

The Features of the Writing Styles
Aspects	Features
Lexical Features	Average Word Length, Average Sentence Length By Word, Average Sentence Length By Character, Average Syllable per Word, Functional Words Count, Punctuation Count, Special Character Count
Vocabulary Richness Features	Hapax Legomenon, Hapax DisLegemena, Honores Measure, Brunets Measure, Yules Characteristic, Shannon Entropy*, Simpson’s Index*
Readability Scores	Flesch Reading Ease, Flesch-Kincaid Grade Level, Gunning Fog Index, Dale Chall Readability Formula, Shannon Entropy*, Simpson's Index*

* Shannon Entropy and Simpson's Index are both Vocabulary Richness Features and Readability Scores
### Topic Modeling

Secondly, we tried to extract the topics for the posts with topic modeling. It is challenging to extract high-quality topics that are clear, segregated, and meaningful, for we need to consider the quality of text processing and the algorithm of modeling. In this report, we applied a popular topic modeling algorithm called Latent Dirichlet Allocation(LDA). LDA considers each post as a collection of topics and each topic as a collection of keywords, and it rearranges the topics and keywords distribution when the number of topics is given. 

The mechanism of Latent Dirichlet Allocation
 

Firstly, we cleaned up and tokenized the posts. Secondly, we created bigrams and trigrams models and lemmatized. Bigrams refer to two words frequently occurring together in the post, and trigrams refer to three words. Lemmatization refers to grouping inflected or variant forms of the same word. Then, we created two main inputs to the LDA topic model, the dictionary and the corpus. Finally, we developed the LDA model and optimized the number of topics by the coherence score.

The Optimization of the Number of Topics
 

As the graph is shown, we chose 20 different topics. With the LDA model, each topic has a combination of keywords and each keyword contributes a certain weightage to the topic.
For example, topic 16 has the summarized keywords of “event”, “startup”, “launch”, “conference”, so the posts labeled as this topic are related to the announcement of a new product.

 

Let’s look into the relationship between topics and influence. It is showed that the most frequent as well as most influential topics in TechCrunch are 16 (new product announcement), 18(social network), and 13(device). 

The Frequency Distribution of Topics
 
The Relationship between Topics and MEIBI
 
### Sentiment Analysis

Then, we tried to determine readers attitude towards the posts with sentiment analysis. Sentiment analysis studies the subjective information in an expression, that is, the opinions, emotions, or attitudes towards a topic. We assigned a sentiment score to each comment, with 1 indicating positive, -1 indicating negative, and 0 indicating neutral. Then, we calculated the average sentiment score for each post.

Sentiment Score for Each Comment
 
 Sentiment Score for Each Post
 
### Regression

Finally, we developed multiple regression models with the influence index average sentiment score as the dependent variable and the features we created with writing styles identification, topic modeling, and sentiment analysis as independent variables. We first explored the correlation between the independent variables and dependent variables and excluded some variables to improve the performance of the model. 

Then we built linear regression, tree regression as well as gradient boosted tree regression model. By looking into RMSE to measure the goodness of fit, it is shown that gradient boosted tree regression slightly outperformed the other two regressions. Thus, we chose the gradient boosted tree regression as the regression model and test the relationship between sentiment score and other independent variables.

The RMSE of Regression Models
Model	RMSE
Linear Regression	0.0806914
Tree Regression	0.0802835
Gradient Boost Tree Regression	0.0801473


 As a result, we developed the importance of different features to the posts and those significant features will be used to select future influential blogs. We set 0.05 as our threshold and therefore we derived 12 important variables. For example, the number of comments and retrieved links and MEIBI are the most important variables to identify the influence as they represent the popularity of the posts. For topics, readers have positive reactions for topic 1, which relates to “product”, “service”, “application”. For writings styles, Lexical features (Average Word Length, Average Sentence Length By Character, Punctuation count), vocabulary richness features (Hapax Legomenon, Hapax DisLegemena) and readability features (Dale Chall Readability, Simpson's Inde) features in writing styles play an important role in comment’s sentiment. It shows that user prefer blogs with relatively longer words and shorter sentences as well as blogs with higher vocabulary richness and readability. 

Feature Importance of the Model
Feature	Importance
Number of comments	0.11065
Number of retrieved inlinks	0.08365
MEIBI score	0.08333
topic_0	0.07735
Post Length (#words)	0.07583
dihapax ( Hapax DisLegemena(Sichel’s Measure))	0.06864
meanwl (Average Word Length)	0.06770
meansl (Average Sentence Length By Character)	0.06214
D (Dale Chall Readability)	0.06178
S (Simpson's Index)	0.05941
p (Punctuation Count)	0.05757
TTratio (Hapax Legomenon)	0.05397

## Implementing the Analytics

In order to identify influential blogs to increase the revenue for advertising and sponsored content, we first used natural language processing to identify the writing style and topics of posts, and sentiment analysis of comments.  After that, we built a gradient boosted tree regression to test the relationship between the sentiment score and other features of the posts such as writing styles, topics, number of links and other influential indexes. 
Here are two recommendations that could be implemented. First, topics relates to new product announcement, social networks, and devices are most popular. The data analytics and marketing team could work together on partner with advertisers and content sponsors to promote their devices and social networks products. Additionally, readers prefer blogs with longer words but shorter sentences as well as blogs with higher vocabulary richness and readability. The data analytics team could provide info sessions and workshops to train its bloggers to focus on these features and write more attractive blogs.

## Scaling Up

We tried to identify potential barriers to the implementation of our model — and think about some strategies to cope with these scenarios to make sure a better realization of our goals.
First, we used several perspectives in the model development, which involves stylometry features and different NLP techniques. Thus, a lack of understanding of the logic and the method we employed in our model might make it hard for the company to adopt our model and solution to the business problem.
Our method to deal with this potential obstacle includes adding enough and clear comments in the code, writing this report which goes through our methods used in developing the model, and making presentations to illustrate the impact our project can bring about.
Second, since the application of the model is directly associated with the revenue of the company, they might tend to be cautious in taking radical changes in how they match and put advertising contents on the website. Thus, our model needs to be examined first, the adoption will take some time and there can be some necessary further improvement of the model.
A strategy we can think about is suggesting the company to try out our approach by A/B experiment. By assigning the new advertising method to a group of users and the old way to another group, we can clearly tell how our approach works, and try to identify any improvements we need to do with our model.

