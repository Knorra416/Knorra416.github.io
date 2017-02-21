---
title: "Python Unstructured Learning - Building a Book Recommender Engine"
author: "Alex Knorr"
published: true
output:
  html_document:
    fig_height: 4
    highlight: pygments
    theme: spacelab
  pdf_document: default
status: publish
---
 
## Description
Through an invitation with Datacamp I was able to take and review their Python course on [Unstructured learning]("https://www.datacamp.com/courses/unsupervised-learning-in-python"). From this I have created an example of how to build a recommender engine. In this example we will be using a list of books from the Gutenberg library and look for the top books similar to Moby Dick. The first thing we have to do is load all our necessary libraries. This includes numpy, pandas, some functions from sklearn, and of course the Gutenberg library and associated functions. I am on a Windows machine, so this was quite a difficult process. The Gutenberg library depends on a Berkly DB connection, this required a wheel install for windows instead of the usual "pip install". I had some problems with the meta data connection to the Gutenberg library, so I pulled a random list of ten books. These are an individual text string for each book and will be the data to work with. Finally, I created a list of the books and a list of the associated titles. 
 

{% highlight python %}
import numpy as np
import pandas as pd
from sklearn.decomposition import NMF
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.preprocessing import normalize
 
from gutenberg.acquire import load_etext
from gutenberg.cleanup import strip_headers
from gutenberg.query import get_etexts
from gutenberg.query import get_metadata
 
#Load books from Gutenberg project#
MD = strip_headers(load_etext(2701).strip())
VK = strip_headers(load_etext(2400).strip())
ARG = strip_headers(load_etext(2703).strip())
LO = strip_headers(load_etext(2730).strip())
DT = strip_headers(load_etext(1001).strip())
HEN = strip_headers(load_etext(1100).strip())
DO = strip_headers(load_etext(501).strip())
SH = strip_headers(load_etext(41).strip())
MET = strip_headers(load_etext(5421).strip())
BER = strip_headers(load_etext(12016).strip())
 
#Create a list of the text
books = [MD, VK, ARG, LO, DT, HEN, DO, SH, MET, BER]
 
#Create a list of the book titles
title = ['Moby Dick','Vikram and the Vampire', 'The Argonauts of North Liberty', 'Long Odds', 'The Divine comedy of Dante Alighieri',
         'The First Part of Henry the Sixth', 'The Story of Doctor Dolittle',
         'The Legend of Sleepy Hollow', 'The Metropolis', 'The Merchant of Berlin']
 
{% endhighlight %}
 
## NMF Engine Method
For this engine we will be leveraging a Non-negative Matrix Factorization. NMF is a dimension reduction technique similar to PCA, but has a much more interpretible output. These reduced dimensions with respect to books, will be the common themes. To leverage the NMF method we first have to create a CSR matrix of the word frequency in each book. The below code creates a TFIDF matrix where the columns are words used in the book and the rows are the books. The data is then the frequency of each word in each book.
 
Next we apply the word frequency matrix to an NMF model. NMF requires a set number of components, in this case I chose 6. In an ideal world, I would be comparing the entire Gutenberg library of 53,000 books. There are 21 sub categories of books, so in that case I would choose 21 components. Once the NMF model is fit to the data we can extract the feature set.The feature matrix will be built based on the number of components set. 
 

{% highlight python %}
#Convert to CSR matrix (needs to be list)#
tfidf = TfidfVectorizer()
csr_mat = tfidf.fit_transform(books)
print(csr_mat.toarray())
 
words = tfidf.get_feature_names()
print(words[0:10])
 
#Create NMF features#
model = NMF(n_components=4)
#arbitray number of components, but based on 4 books in 2000s, 2 books in 1000s, 2 books less than 1000, and 2 books greater than 5000 (ids)
model.fit(csr_mat)
nmf_features = model.transform(csr_mat)
print(nmf_features[0:10])
 
{% endhighlight %}
 

{% highlight text %}
## [[ 0.00220866  0.          0.00038646 ...,  0.00012991  0.          0.        ]
##  [ 0.00140888  0.00066293  0.0012326  ...,  0.          0.          0.        ]
##  [ 0.          0.          0.         ...,  0.          0.          0.        ]
##  ..., 
##  [ 0.          0.          0.         ...,  0.          0.          0.        ]
##  [ 0.          0.          0.         ...,  0.          0.          0.        ]
##  [ 0.          0.          0.00016869 ...,  0.          0.          0.        ]]
## ['000', '000l', '10', '100', '101', '102', '103', '104', '105', '106']
## [[ 0.63451992  0.03682026  0.          0.16784476]
##  [ 0.55995244  0.04338835  0.1169237   0.15690176]
##  [ 0.07277913  0.          0.906831    0.        ]
##  [ 0.43319966  0.          0.29025667  0.17250588]
##  [ 0.32949563  0.30299528  0.01500623  0.41801439]
##  [ 0.          1.20324253  0.          0.        ]
##  [ 0.02686749  0.          0.          1.24758635]
##  [ 0.74750811  0.          0.          0.        ]
##  [ 0.03162562  0.          0.84505837  0.15445836]
##  [ 0.10503363  0.14098317  0.74667685  0.02519439]]
{% endhighlight %}
 
## Recommending Similar Books
Now we have a set of NMF Features which represent the themes of the books in our list. Now we need a way to compare the features of articles. This is done using Cosine similarity. The basics of Cosine similarity comparison plots lines for each books themes and measures the angle between them as a measure of similarity. A higher value is a closer book similarity. 
 
First, we normalize the features. Then we create a pandas DataFrame using these normalized features and the titles of the books. Finally we need a comparison for the cosine similarity. By setting article equal to Moby Dick we have a book which we want recommendations for. Finally the .dot method on our pandas DataFrame computes the cosine similarity. We can view the 5 books most similar to Moby Dick, and the fisrt is obviously itset, but second closes is Vikram and the Vampire
 

{% highlight python %}
 
#Convert features set and look for cosine similarities#
norm_features = normalize(nmf_features)
books_df = pd.DataFrame(norm_features, index = title)
article = books_df.loc['Moby Dick']
similarities = books_df.dot(article)
 
print(similarities.nlargest())
 
{% endhighlight %}
 

{% highlight text %}
## Moby Dick                               1.000000
## Vikram and the Vampire                  0.980214
## The Legend of Sleepy Hollow             0.965231
## Long Odds                               0.841489
## The Divine comedy of Dante Alighieri    0.721037
## dtype: float64
{% endhighlight %}
 
## Conclusion
So, how good is the engine created? It says that the book in our list most similar to Moby Dick is Vikram and the Vampire. From wikipedia this book is an ancient indian tale about a King named Vikram who vows to capture a vampire. Each time he tries to capture the vampire it escapes. This seems like a decent comparison to Moby Dick of a main character chasing after a mythical creature. 
 
This is just one example where NMF can be used to create a recommender engine. Any array that contains non-negative values is suitable for NMF. This could also be used for image recognition, or lists of ecommerce purchases.
