# Genre_Classification_of_Million_Song_Dataset

## Objective:

**To cluster the data with LDA topic modeling and try to find genres in the music based on lyrics and to build a model that can predict what genre a song has to based on lyric content.**


## Data Source

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

## Metrics I Used:

I used a confusion matrix to see how well I was able to classify and used accuracy as my base statistic for performance.


## Findings:

### **WORK IN PROGRESS**

## Limitations of the project and data

- My model is only looking at the lyric content as of currently. This means that the information in the acoustic metadata that is also available is not accounted for. Doing so may rectify some magnitude of error with classification as it would be even more data to train off of but also give a better view of the music as a whole, such as whether the acoustic data or the language data is more dominating in the relationship of genres or if it about even.
- The lyrics content in the data is pre processed into a bag of words and thus I cannot analyze relationships between words because there are only 1 n-grams and the original corpus of actual lyrics was not supplied for obvious legal reasons.

## My Statistical Methods:

### What I implimented:
----
- I implemented a LDA (Latent Dirichlet Allocation) method to topic model a training set from the lyric data done by MusiXMatch. These topics would represent the genres within my dataset. I would utilize the existing tags given by the MSD dataset and then see what are the dominating features within those tags for each topic. I then made a classification model based on logistic regression that incorporated these topics to predict what tag a song will/would most likely posess based on the lyric content. I used an exisiting tag dataset to set the tags for all the songs and have a train and test set for the evaluation portion.

### Results:
----
**- WORK IN PROGRESS**

### Inference:
----

#### What I can say confidently is: (and say why you're confident, mention some summary statistics here)

#### What I cannot say for sure is: (explain why youre not sure)

## What's Next?
