---
layout: post
title: Drawing a Conclusion Between Movie Length and Its IMDB Rating
date: '2017-06-03 20:10:39 +0530'
subtitle: Ranking Indian cities with best and worst sex ratios.
categories: personal
published: true
---
I got my hands dirty with another dataset from Kaggle, **[IMDB 5000 Movie Dataset](https://www.kaggle.com/deepmatrix/imdb-5000-movie-dataset)**. So, I decided to relate movie length to its IMDB ratings.

Kaggle datasets are mostly in CSV file format, the CSV module in Python makes it easy to read CSV data.

### Program that I wrote in Python
*Please ignore bad coding habits and useless sorting of data. As the data didn't take a long time to process, I didn't find it necessary to optimised the code.*

{% highlight python %}
import csv
import numpy as np 

file = open('movies.csv', newline='')
reader = csv.reader(file)

header = next(reader)

movie_length = []
movie_rating = []

for row in reader:
	movie_length.append(row[3])
	movie_rating.append(row[25])

neww = list(zip(movie_rating, movie_length))
sorted_by_second = sorted(neww, key=lambda tup: tup[1], reverse=False)

movie_rating, movie_length = zip(*sorted_by_second)

movie_length = movie_length[:5015]
movie_rating = movie_rating[:5015]
movie_length = movie_length[15:]
movie_rating = movie_rating[15:]
for length in movie_length:
	movie_length = [int(length) for length in movie_length]
#print(movie_length)
movie_length = np.array(movie_length)
movie_rating = np.array(movie_rating).astype(np.float)

movie_rating = np.mean(movie_rating.reshape(-1, 50), axis=1)
movie_length = np.mean(movie_length.reshape(-1, 50), axis=1)

neww = list(zip(movie_rating, movie_length))
sorted_by_second = sorted(neww, key=lambda tup: tup[1], reverse=False)

movie_rating, movie_length = zip(*sorted_by_second)
print(movie_length)
print(movie_rating)
rating_file = open('rating.txt', 'w')

for rating in movie_rating:
  rating_file.write("%s," % rating)

length_file = open('length.txt', 'w')

for length in movie_length:
  length_file.write("%s," % length)
{% endhighlight %}


### The result. 

#### *Movie Length VS IMDB Rating*

<p data-height="470" data-theme-id="light" data-slug-hash="EXPwze" data-default-tab="result" data-user="sachinverma" data-embed-version="2" data-pen-title="Movie Length VS IMDB Rating" class="codepen">See the Pen <a href="https://codepen.io/sachinverma/pen/EXPwze/">Movie Length VS IMDB Rating</a> by Sachin Verma (<a href="https://codepen.io/sachinverma">@sachinverma</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

### Conclusion

This data was gathered from a set of 5000 movies. After sorting the data, an average of 50 consecutive values was used to draw a smooth graph. *Data may be slightly skewed.*

So, in the final graph if we ignore some outliers, it is evident that the length of a movie is directly proportional to its IMDB rating.
