# Genre_Classification_of_Million_Song_Dataset
---
## Objective:
---
### **To cluster the data with LDA topic modeling and try to find genres in the music based on lyrics and to build a model that can predict what topic a song belongs to based on lyric/tag content.**
---

## Data Source
---
**The data set is not included here and it is given in the form of a direct download or it can be mounted using a snapshot id to an AWS EC2 instance on an EBS volume. More information on this here:** 
[Getting The Dataset](https://labrosa.ee.columbia.edu/millionsong/pages/getting-dataset "Million Song Dataset")

I am using the Million Song Dataset, the lyrics dataset done in collaboration with MusixMatch, and the genre annotations dataset done by Tagtraum Industries


Citation for Million Song Dataset and Lyrics dataset:

*Thierry Bertin-Mahieux, Daniel P.W. Ellis, Brian Whitman, and Paul Lamere.*
*The Million Song Dataset. In Proceedings of the 12th International Society*
*for Music Information Retrieval Conference (ISMIR 2011), 2011.*


Citation for Genre Annotations dataset:

*Hendrik Schreiber.*
*Improving Genre Annotations for the Million Song Dataset.*
*In Proceedings of the 16th International Society for Music Information*
*Retrieval Conference (ISMIR), pages 241-247, Málaga, Spain, Oct. 2015.*

The million song dataset is quite large and holds a lot of good features that can be explored. I was particularly interested in genres and lyric content. As you can see below, there are quite a few words in the lyrical content (the top 5000 of which are in the data set that was given by the MSD admins).

![cloud](./wordcloud/words.png)

## Metrics I Used:
---
I used accuracy to see how well I was able to classify. I also looked at the value counts of tags to see how the topics were distributed.

 
## Limitations of the project and data
---
- My model is only looking at the lyric content as of currently. This means that the information in the acoustic metadata that is also available is not accounted for. Doing so may rectify some magnitude of error with classification as it would be even more data to train off of but also give a better view of the music as a whole, such as whether the acoustic data or the language data is more dominating in the relationship of genres or if it about even.
- The lyrics content in the data is pre processed into a bag of words and thus I cannot analyze relationships between words because there are only 1 n-grams and the original corpus of actual lyrics was not supplied for obvious legal reasons.

## My Statistical Methods:
----
 - I implemented a LDA (Latent Dirichlet Allocation) method to topic model a training set from the lyric data done by MusiXMatch. These topics would represent the genres within my dataset. I would utilize the existing tags given by the MSD dataset and then see what are the dominating features within those tags for each topic. 
 - I then made a classification model based on logistic regression, random forest, and gradient boosting (of which the highest scoring was chosen for the final model) that incorporated these topics to predict what genre a song will/would most likely posess based on the lyric content and tags. I used an exisiting tag dataset to set the tags for all the songs and have a train and test set for the evaluation portion.

## Findings:
---
 - I found that utilizing LDA methods that I was able to find the best number of topics to use for the data. I came to the conclusion that **10 topics** is ideal. This can be seen in the Coherence Model plot I generated. (see below)
![plot]('./model_plot.png')
 - If too few topics were used (2-5) there wasn't much to be noticed in terms of meaningful classification. It was easier to classify because there were fewer classes, but the classes themselves were not very representative of the symbolic genres I was going for.
 - The exact genre each topic represents is a more difficult problem, because of the semantics of what a genre is. By definition a genre is a grouping of subcategories of some medium of art. The easy way to recognize genres would be to look at the most common tag within the different topics. The problem, however is that pop/rock was by far the most dominating class. This brings in some amount of bias if that simple method is used. Further analysis is needed and will be looked into.
 - The model itself performed fairly well (utilizing the gradient boosting method) with an accuracy of 65% on the training set and 61% on the test set. These numbers are on the subset data, and I will go forward with the full dataset once I have made my code more efficient and tried to avoid memory bottlenecks and leaks because a ~100000 by 5000 matrix is an enormous amount of data and to work with that I need to move efficiently and intelligently.

### Inference:
----
 - What I can infer from my findings is that:
 ⋅⋅⋅⋅ * Music/lyrical data is incredibly complex, especially when you take into account dialects, slang, and different languages. From my study I think that the best methodology for music data is one that takes the route of dimensional reduction and feature extraction, because dealing with the full data is incredibly computationally expensive. There are methods such as the [joblib](https://joblib.readthedocs.io/en/latest/) library that can help with larger datasets like this, but overall it is best to try and trim the fat where you can.
 ⋅⋅⋅⋅ * I believe that an important thing to understand is the unbalanced nature of this set when it comes to genre. Pop/rock are 2 of the most popular music genres available for listening. Looking at the top 20 lists for past years show how popular those 2 genres are. Because of this having them in this set may not be the right approach. I hypothesize that trying to cluster the pop/rock genre seperate from all the other genres may be a better route. Another alternative would be to undersample and sample from the larger classes to match the size of some of the smaller ones. This is what I believe should be done as there is a lot of data, so it may still be enough for an adequate model.

## What's Next?
---
 - Working on the larger dataset
 - Adding in the acoustic data
 - Potentially undersampling the data to decrease the dominance of the pop/rock tag
