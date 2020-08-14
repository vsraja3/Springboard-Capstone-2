# Springboard-Capstone-2

*This is the repository for all Capstone Project 2 files pertaining to Spotify Genre Prediction & Lyrical Analysis. This README contains the overall project report with a summary of each section. The headers contain links to the associated Jupyter Notebook with code and annotations - please see these for more in depth analysis and associated visualization.*

## Introduction
The field of data science is constantly growing with limitless applications in different industries. As an amateur musician and avid listener, I am particularly enthusiastic about the potential applications of data science to benefit the music streaming industry. Spotify is well known today as one of the first services that popularized music streaming as an alternative to purchasing individual songs. As one of the first movers in the industry, they have done an impressive job of enhancing their services beyond a simple streaming service to one that curates playlists and creates recommendations for each of it’s listeners on a daily basis while also providing annual insights into a users listening history, ultimately improving the listening experience for all subscribers by introducing them to new songs and artists they may not otherwise be exposed to while at the same time promoting lesser known artists allowing them to get more plays and income as a result as well the potential to win over new fans. 

One of the primary ways in which Spotify builds all of its additional features beyond streaming is to use the data it gathers from users’ listening preferences along with the data it generates by performing an audio analysis of each of the songs it holds to discover commonalities. As someone who has made Spotify one of the staples of my daily routine, I have benefited from using their services and catered playlists to stream music for all different types of daily occasions including commuting to work, studying or working, showering and brushing, and even sleeping. After taking advantage of their services to find music for various circumstances to keep my life music filled, I became particularly interested in researching what types of data Spotify stores and uses in order to facilitate their services. With some quick research I discovered that Spotify does indeed have an API that can be accessed for free in order for developers to utilize their platform to build applications around as well as gain insights into their data. Their developer website provided additional insights into the type of data that each track stores which includes the standard categorical information regarding a track’s name, artist, and album but beyond that also an array of musical attributes that are measured numerically and were apparently generated using an audio analysis tool. While we cannot gain access to Spotify’s particular tools for audio analysis given they may be proprietary, what we can do is to retrieve the data of any set of tracks we wish to analyze and explore that data to gain further insights into what similarities songs may have that contribute to their recommender systems as well as create our own projects using it.

After spending some time researching the data Spotify houses and brainstorming potential applications for it, I determined that there are endless possibilities and that I could spend years digging into musical data. However, for the sake of narrowing down my options down to one clear-cut choice that could be pursued for the time being, I decided that the best option for the moment would be to explore what features help determine the musical genre of a particular song or artist. This came to mind after listening to a variety of music during my additional time spent at home during quarantine where I broadened my musical tastes beyond what I’m used to (most commonly Indie and Alternative Rock) and listened to artists in different genres as well as some artists that seem to blend genres amongst all of their songs. Beyond this, I also became intrigued by the occasional contrast between the musical and instrumental components of certain songs in opposition to the lyrics that are sung. I listened to several songs that seemingly sounded happy and cheerful based on the way it is sung as well as the positive instrumental notes being largely in keys that are in a Major mode, while the lyrics are actually quite dark (ex. Pumped Up Kicks by Foster the People). As a result, I decided to build a project using Spotify musical attributes as well as the respective lyrics of each song in my dataset, as generated by the popular website Genius, and explore both to determine how they each contribute to the classification of a particular song or artists into a standard genre. 

## Spotify Data Acquisition
This experiment was done by first acquiring the data using both the Spotify API in order to extract 10 thousand songs across 5 of the most recognizable genres in today’s music (Rock, Pop, Hip-Hop, Country, Electronic/Dance) that also I gauged would be more distinguishable from one another rather than having considerable overlap in efforts to simplify the process. One unfortunate limitation of the Spotify API was that they do not have a way to search for tracks by genre on their back end, but strangely enough they do on their front end although it appears to be limited artist level rather than track level. As such, I went ahead and generated playlists using my Spotify account that were created by searching on their front end the first 2000 songs in each genre and storing them in a playlist, which I was then able to access on the back end to create my dataset.

## Genius Lyrics Data Acquisition
The next step was to acquire the lyrics for each of the songs in the dataset generated from the five Spotify playlists which contained songs for each genre. There are several databases for lyrics online, but we chose to use the site Genius as it is amongst the most popular sites for finding lyrics as well as interpretations of the meaning of lyrics. Moreover, there are several Spotify artists and tracks where they specifically have an interface with Genius to display the lyrics of a particular song while also sharing a brief background on the song in a segment called “Behind the Music”. Given this connection, it stands to reason that there may be an API out there for their site that makes it possible for Spotify to connect to it. Some quick research revealed that there indeed does exist a custom Python wrapper created by developer John Miller that streamlines the search for songs on Genius website and directly scrapes the HTML content to pull the lyrics via BeautifulSoup. We used this wrapper to iterate through the dataframe and search for each song by track name and artist to pull the lyrics into the Pandas dataframe.

## Data Wrangling and NLP Pre-Processing
After we completed the data acquisition process using the two API’s for Spotify and Genius lyrics, there remained the step to use Natural Language Processing to clean the text data that the lyrics were presented in. We transformed the lyrics through a number of pre-processing steps in order to make the lyrics more digestible and interpretable when applied to data visualizations in our EDA section as well as to improve the performance of our eventual goal of applying the lyrics to a machine learning algorithm to predict genre. Some of the steps that were taken include removing HTML markers, song section text, punctuation, stop words, as well as finding the root words through lemmatization. We also generated some numerical metrics in hopes of combining them to our Spotify attributes when training a machine learning classifier. These metrics include the total count of words and the count of unique words in the raw text as well as the counts of words after pre-processing.

## Exploratory Data Analysis
With the data prepared, we began some EDA (exploratory data analysis) in order to answer some high level questions about our data, identify trends and relationships between variables, hypothesize potential features that will contribute to the predictability of a genre when we train and test our machine learning algorithms, as well as discover trends in our text data to discover potential topics or subgenres. Among these findings were the distribution of each of the numerical features and which genres trended higher across each of these features, with some high level takeaways including higher levels of instrumentalness in EDM songs, higher levels of speechiness and word count in Hip-Hop, and higher duration of songs amongst Rock songs. We additionally confirmed that the majority of the numerical variables are independent of one another by plotting a heatmap and observing low correlations between features, which helps support assumptions needed for machine learning models. Lastly, we generated word clouds to find frequently used words across genres and also used LDA (Latent Dirichlet Allocation), an unsupervised learning technique for text data, to find some potential subgenres and topics hidden within the lyrics.

## Machine Learning Modeling
The last component of the project involved training and testing a variety of different machine learning algorithms with the goal of creating a classifier that can identify the genre of any new song data that is input based on the numerical attributes housed by Spotify as well the lyrics. The models that were tested include a Random Forest Classifier model and a gradient boosting tree with XGBoost to predict genre using the numerical data, as well as a Multinomial Naive Bayes model along with a transformation using Count Vectorizer and TFIDF (term frequency inverse document frequency). All of the models yielded modest to positive results based on their accuracy scores, with the numerical feature based models being overall more accurate. The confusion matrices generated to show the number of tracks correctly and incorrectly classified into each genre also helped reveal similarities between genres as well as potential instances where a song may have attributes more similar to it’s predicted genre whereas it’s genre label, which is artist based, has it classified into another genre. 

## Conclusion & Next Steps
Overall, this project was a very intriguing and exciting one to undertake and provided us some very interesting insights into what numerical features and lyrical features lead to a song’s identification into a particular genre. The data acquisition process using the two APIs proved to be a challenging but excellent exercise for building a unique dataset from scratch and cleaning it for analysis as opposed to downloading an already prepared dataset that often does not need much more wrangling. An additional step to explore in a future project or building upon this would be to include songs of even more genres and include some that are very similar (such as Alternative and Rock, or R&B and Pop) and attempt to find distinctions in the lyrics and attributes of those. 

Likewise, the exploratory data analysis section helped to visualize at a high level the attributes that are more pronounced in each genre. The unsupervised text analysis using LDA for topic modeling was particularly interesting in terms of getting a gauge of some of the most frequently used words and subjects included in the lyrics to music. One additional area of exploration here would be to expand on our topic analysis by using PyLDAvis to visualize the clusters of words that were generated by the LDA modeling in order to get a better idea of the similarities between clusters and potentially identify some subgenres.

Lastly, the machine learning models that were built and tested were done at a very basic level with regards to skipping certain steps such as dimensionality reduction, regularization, and feature selection. These are a few additional steps that could be made to tune our models better for greater accuracy. In addition, it could potentially be interesting to build an ensemble model using both the text classifier using Multinomial Bayes as well as the numerical classifiers using a Random Forest. This may provide the potential for a more unique genre prediction system that accounts for all of the components in a song together. Moreover, it would be highly intriguing to compare text and numerical predictors in their predicted labels against one another to highlight differences between the mood of a song lyrically and musically. With the constant evolution of music and diversity of artists blending elements from various styles of music and genres, there is an endless amount of exploration that can be done in such a complex and creative field.
