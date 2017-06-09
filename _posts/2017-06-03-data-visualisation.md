---
layout: post
title:  "Data Visualisation"
date:   2017-06-03 20:10:39 +0530
subtitle: Ranking Indian cities with best and worst sex ratios.
categories: personal
---
### Reddit is awesome.
While I was browsing Reddit, I came across some posts from the subreddit **[/r/Dataisbeautiful](https://www.reddit.com/r/dataisbeautiful/)**. So, I decided to make use of data sets available online to visualise it into something meaningful.

Then after some search, I found this site: [Kaggle Datasets](https://www.kaggle.com/datasets). This site contains open datasets on everything from government, health, and science to popular games and dating trends. After this, finding a relevant data set wasn't much difficult, and I settled on this particular one: [Top 500 Indian Cities](https://www.kaggle.com/zed9941/top-500-indian-cities). It contains population data for top 500 Indian cities, including male/female population, literacy rate, sex ratio, total graduates, etc.

### So I wrote a program using Python and Matplotlib.

{% highlight python %}
import csv
import matplotlib.pyplot as plt
import numpy as np

x = np.array([0,1,2,3,4,5,6,7,8,9])
sex_ratio_improvement = []
cities_name = []

with open('cities.csv', newline='') as cities:
	cities_data = csv.reader(cities, delimiter=',', quotechar='|')
	for row in cities_data:
		if row[14] != str or row[14] !=list:
			sex_ratio_improvement.append(int(row[14])-int(row[13]))
		cities_name.append(row[0])

neww = list(zip(cities_name, sex_ratio_improvement))
sorted_by_second = sorted(neww, key=lambda tup: tup[1], reverse=True)

sorted_by_second = sorted_by_second[:10]
cities_10, ratio_10 = zip(*sorted_by_second)

cities_10 = list(cities_10)
ratio_10 = list(ratio_10)

plt.xticks(x, cities_10)

plt.bar(x,ratio_10, color="#e74c3c")
plt.xlabel('Top 10 Cities with improving sex ratio in India')
plt.ylabel('Child Sex Ratio - Overall Sex Ratio')
plt.title('Cities with improving sex ratio.')
plt.show()
{% endhighlight %}

There was a column named "child_sex_ratio" for age group 0-6.

**So, I decided to go ahead and rank top 10 cities which were showing an improvement in sex ratio.** 

I grabbed the CSV file and stripped the required information using Python. Calculated the difference between **child sex ratio** and **overall sex ratio** for all 500 cities, ranked them and plotted top 10 on a bar graph.

### This was the result. 

#### ***Higher is better**

<p data-height="450" data-theme-id="light" data-slug-hash="NgGJjX" data-default-tab="result" data-user="sachinverma" data-embed-version="2" data-pen-title="Sex ratio #1" class="codepen">See the Pen <a href="https://codepen.io/sachinverma/pen/NgGJjX/">Sex ratio #1</a> by Sachin Verma (<a href="https://codepen.io/sachinverma">@sachinverma</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

My own city "Shimla" ranks 9th on this list, which is no doubt a good sign. The sex ratio of children aged 0-6 is 890 whereas overall sex ratio is 818, which is an increase of 8.8%.

Bally city from West Bengal ranked #1 on this list, with an increase of 37.31% (863 to 1185).

**Some facts:**
Two out of 10 of these cities are from Maharashtra, and two are from Assam.

### Now it was the time to see ten cities with worst sex ratios.

{% highlight python %}
import csv
import matplotlib.pyplot as plt
import numpy as np

x = np.array([0,1,2,3,4,5,6,7,8,9])
sex_ratio_improvement = []
cities_name = []

with open('cities.csv', newline='') as cities:
	cities_data = csv.reader(cities, delimiter=',', quotechar='|')
	for row in cities_data:
		if row[14] != str or row[14] !=list:
			sex_ratio_improvement.append(int(row[14])-int(row[13]))
		cities_name.append(row[0])

neww = list(zip(cities_name, sex_ratio_improvement))
sorted_by_second = sorted(neww, key=lambda tup: tup[1])

sorted_by_second = sorted_by_second[:10]
cities_10, ratio_10 = zip(*sorted_by_second)

cities_10 = list(cities_10)
ratio_10 = list(ratio_10)

plt.xticks(x, cities_10)

plt.bar(x,ratio_10, color="#e74c3c")
plt.xlabel('Top 10 Cities with improving sex ratio in India')
plt.ylabel('Child Sex Ratio - Overall Sex Ratio')
plt.title('Cities with improving sex ratio.')
plt.show()
{% endhighlight %}

### Results

#### ***Value closer to 0 is better**

<p data-height="450" data-theme-id="light" data-slug-hash="XgmGYL" data-default-tab="result" data-user="sachinverma" data-embed-version="2" data-pen-title="Sex ratio #1" class="codepen">See the Pen <a href="https://codepen.io/sachinverma/pen/XgmGYL/">Sex ratio #1</a> by Sachin Verma (<a href="https://codepen.io/sachinverma">@sachinverma</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

Kozhikode from Kerala topped this list with a percentage decrease of 12.17% (1093 to 960).

**Some facts:**
Four out of 10 of these cities are from Kerala.
Two are from Maharashtra

This was my first go at data visualisation using Python. Technically I am not ranking cities purely on the basis of sex ratio, but on the basis of improvement and decline in the ratios. It's not a proper metric to conclude anything, but it was fun doing this.

I am still in the learning phase of Python, which I will continue after my semester exams. The program I wrote was in no way optimised and written perfectly, so feel free to criticise and suggest some improvements.