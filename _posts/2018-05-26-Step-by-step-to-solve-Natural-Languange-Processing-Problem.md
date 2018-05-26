# How to solve 90% of NLP problems: a step-by-step guide
Using Machine Learning to understand and leverage text.

Text data is everywhere
Whether you are an established company or working to launch a new service, you can always leverage text data to validate, improve, and expand the functionalities of your product. The science of extracting meaning and learning from text data is an active topic of research called Natural Language Processing (NLP).

NLP produces new and exciting results on a daily basis, and is a very large field. However, having worked with hundreds of companies, the Insight team has seen a few key practical applications come up much more frequently than any other:

- Identifying different cohorts of users/customers (e.g. predicting churn, lifetime value, product preferences)
- Accurately detecting and extracting different categories of feedback (positive and negative reviews/opinions, mentions of particular attributes such as clothing size/fit…)
- Classifying text according to intent (e.g. request for basic help, urgent problem)

While many NLP papers and tutorials exist online, we have found it hard to find guidelines and tips on how to approach these problems efficiently from the ground up.

# How this article can help
After leading hundreds of projects a year and gaining advice from top teams all over the United States, we wrote this post to explain how to build Machine Learning solutions to solve problems like the ones mentioned above. We’ll begin with the simplest method that could work, and then move on to more nuanced solutions, such as feature engineering, word vectors, and deep learning.

After reading this article, you’ll know how to:

- Gather, prepare and inspect data
- Build simple models to start, and transition to deep learning if necessary
- Interpret and understand your models, to make sure you are actually capturing information and not noise

> We wrote this post as a step-by-step guide; it can also serve as a high level overview of highly effective standard approaches. (https://github.com/hundredblocks/concrete_NLP_tutorial/blob/master/NLP_notebook.ipynb)

This post is accompanied by an interactive notebook demonstrating and applying all these techniques. Feel free to run the code and follow along!

# Step 1: Gather your data
## Example data sources
Every Machine Learning problem starts with data, such as a list of emails, posts, or tweets. Common sources of textual information include:

- Product reviews (on Amazon, Yelp, and various App Stores)
- User-generated content (Tweets, Facebook posts, StackOverflow questions)
- Troubleshooting (customer requests, support tickets, chat logs)

## “Disasters on Social Media” dataset

For this post, we will use a dataset generously provided by CrowdFlower (https://www.crowdflower.com/data-for-everyone/), called “Disasters on Social Media”, where:

> Contributors looked at over 10,000 tweets culled with a variety of searches like “ablaze”, “quarantine”, and “pandemonium”, then noted whether the tweet referred to a disaster event (as opposed to a joke with the word or a movie review or something non-disastrous).

Our task will be to detect which tweets are about a disastrous event as opposed to an irrelevant topic such as a movie. Why? A potential application would be to exclusively notify law enforcement officials about urgent emergencies while ignoring reviews of the most recent Adam Sandler film. A particular challenge with this task is that both classes contain the same search terms used to find the tweets, so we will have to use subtler differences to distinguish between them.

In the rest of this post, we will refer to tweets that are about disasters as “disaster”, and tweets about anything else as “irrelevant”.

# Labels
We have labeled data and so we know which tweets belong to which categories. As Richard Socher outlines below, it is usually faster, simpler, and cheaper to find and label enough data to train a model on, rather than trying to optimize a complex unsupervised method.

![](https://cdn-images-1.medium.com/max/1600/1*CdnxyA_fMXxEcEQ1kUTFRg.png)

# Step 2: Clean your data
> The number one rule we follow is: “Your model will only ever be as good as your data.”

One of the key skills of a data scientist is knowing whether the next step should be working on the model or the data. A good rule of thumb is to look at the data first and then clean it up. **A clean dataset will allow a model to learn meaningful features and not overfit on irrelevant noise.**

Here is a checklist to use to clean your data: (see the code (https://github.com/hundredblocks/concrete_NLP_tutorial/blob/master/NLP_notebook.ipynb) for more details):

1. Remove all irrelevant characters such as any non alphanumeric characters
2. Tokenize (https://nlp.stanford.edu/IR-book/html/htmledition/tokenization-1.html) your text by separating it into individual words
3. Remove words that are not relevant, such as “@” twitter mentions or urls
4. Convert all characters to lowercase, in order to treat words such as “hello”, “Hello”, and “HELLO” the same
5. Consider combining misspelled or alternately spelled words to a single representation (e.g. “cool”/”kewl”/”cooool”)
6. Consider lemmatization (https://nlp.stanford.edu/IR-book/html/htmledition/stemming-and-lemmatization-1.html) (reduce words such as “am”, “are”, and “is” to a common form such as “be”)

After following these steps and checking for additional errors, we can start using the clean, labelled data to train models!

# Step 3: Find a good data representation
Machine Learning models take numerical values as input. Models working on images, for example, take in a matrix representing the intensity of each pixel in each color channel.

![](https://cdn-images-1.medium.com/max/1600/1*6pW5mPAxYhYBZxkc-hKf0A.png)

Our dataset is a list of sentences, so in order for our algorithm to extract patterns from the data, we first need to find a way to represent it in a way that our algorithm can understand, i.e. as a list of numbers.

# One-hot encoding (Bag of Words)
A natural way to represent text for computers is to encode each character individually as a number (ASCII for example). If we were to feed this simple representation into a classifier, it would have to learn the structure of words from scratch based only on our data, which is impossible for most datasets. We need to use a higher level approach.

For example, we can build a vocabulary of all the unique words in our dataset, and associate a unique index to each word in the vocabulary. Each sentence is then represented as a list that is as long as the number of distinct words in our vocabulary. At each index in this list, we mark how many times the given word appears in our sentence. This is called a Bag of Words model, since it is a representation that completely ignores the order of words in our sentence. This is illustrated below.

![](https://cdn-images-1.medium.com/max/1600/1*oQ3suk0Ayc8z8i1QIl5Big.png)

# Visualizing the embeddings
We have around 20,000 words in our vocabulary in the “Disasters of Social Media” example, which means that every sentence will be represented as a vector of length 20,000. The vector will contain mostly 0s because each sentence contains only a very small subset of our vocabulary.

In order to see whether our embeddings are capturing information that is relevant to our problem (i.e. whether the tweets are about disasters or not), it is a good idea to visualize them and see if the classes look well separated. Since vocabularies are usually very large and visualizing data in 20,000 dimensions is impossible, techniques like PCA will help project the data down to two dimensions. This is plotted below.

![](https://cdn-images-1.medium.com/max/1600/1*ikis3EFujlrmVk_JEQMvzQ.png)

The two classes do not look very well separated, which could be a feature of our embeddings or simply of our dimensionality reduction. In order to see whether the Bag of Words features are of any use, we can train a classifier based on them.

# Step 4: Classification
When first approaching a problem, a general best practice is to start with the simplest tool that could solve the job. Whenever it comes to classifying data, a common favorite for its versatility and explainability is Logistic Regression. It is very simple to train and the results are interpretable as you can easily extract the most important coefficients from the model.

We split our data in to a training set used to fit our model and a test set to see how well it generalizes to unseen data. After training, we get an accuracy of 75.4%. Not too shabby! Guessing the most frequent class (“irrelevant”) would give us only 57%. However, even if 75% precision was good enough for our needs, we should never ship a model without trying to understand it.

...CONTINUE 