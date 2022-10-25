# Pratilipi Predictor
#### Aryamaan Singh

Pratilipi Predictor is a KNN algorithm based simple technique of predicting which N number of books a user is going to read based on his past preferences.

## Pre-requisites
```sh
pip install ipynb
```
```sh
pip install pandas
```

## How it works

- First loads up the user data and the metadata
- Cleans them up, sorts them according to a specified datetime column.
- Merges them on 'pratilipi_id'.
- Further prunes this merged data based on a category threshold,
- Splits this into 75% training and 25% testing data.
- Uses this clean data to pivot onto a new table.
- Uses this pivot table to create a sparse matrix.
- Fits this matrix into KNN model.
- Uses the test data to conduct predictions, analysis on a per user basis.
- If for some reason we are not able to find any nearest neighbors, we simply suggest the most popular pratilipis based on the category the users have read before.
- We calculate category match percentage, pratilipi match percentage.
- We add these as a column in the test data to be able to find what factors might or might not fluctuate the end result.


## Why I chose KNN
As I was researching reccomendation and prediction engines, I came across two types of filteration strategies:
- Content-based filtering.
- Collaborative filtering.

![Alt text](https://labelyourdata.com/img/article-illustrations/content-based_vs_collaborative_dark.png "a title")

I learnt that almost all the reccomendations we receive on any platform is a combination of the two, but for this project I chose to tackle the first part i.e the Content Based Filteriing.
KNN would prove to be the best way for me to find similar pratilipis to the ones the user had already read. I could use the 'category_name' column, encode it to be numerical, use that as the value for my pivot table and then find the K nearest neighbors to that category.

## Improvements to this approach
This is an extremely naive approach, without collaborative filtering, the entire reccomendation process might become stale as the algorithm keeps on reccomending books that you have always read, and nothing new that you might be excited about.
My approach is not memory efficient either as I have called a dataframe time and again redundantly where I can through some hardwork be able to reduce the number of times I have to load these humongous dataframes. My approach does not play well with RAM either as 16GB of it was not sufficient to pivot such a table and caused bottlenecks. 
Other than that I would love to work on clustering the categories further as my approach in its current state will either predict a category that is the same as the one the user has read or something completely random. We can all agree that the category 'romance' is closer to 'comedy' than 'horror'. My current approach fails to take this into account. As I am new to this, I believe I could leverage NLP to my benefit but I am stepping into unknown territory here so I will need to research a bit more.

