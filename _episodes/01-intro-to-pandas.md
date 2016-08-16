---
title: "Intro to Pandas"
teaching: 10
exercises: 2
questions:
- "How can I neatly wrangle data in Python?"
objectives:
- "Explain how to use Pandas to import, plot, and manipulate data."
keypoints:
- "A DataFrame is like an array that gives you more control of your data"
---

You've already seen numpy's `loadtxt` function, which is a great way to quickly import data. When you're going to be doing heavy-duty data-wrangling, though, you often want a tool with a little more power, even if it comes at the cost of additional complexity. By far the most popular such tool is Pandas.

Pandas provides a new type of object called a DataFrame. DataFrames are objects, just like lists, NumPy arrays, and everything else in Python, but they're a little more complicated (and in return make a lot of things way easier!). If you've ever used R before, pandas DataFrames will probably feel really similar to R DataFrames.

First, we need to import our libraries. We'll import pandas. Plotting in pandas is built on maplotlib, so in order to specify how we want our graphs to look, we'll import matplotlib and give it a style to use. We're also adding the magic command `%matplotlib inline` which will make our graphs show up in the Jupyter notebook.

~~~
import pandas
import matplotlib.pyplot as plt
%matplotlib inline
plt.style.use("seaborn-ticks")
~~~
{: .python}


We can load a single comma-separated value file into pandas with `pandas.read_csv()`. We need to set the `header` parameter to `None`, or pandas will think the first row is a header.

~~~
data = pandas.read_csv("../data/inflmmation-01.csv", header=None)
~~~
{: .python}

Pandas DataFrames are built on top of NumPy arrays, so most of the features you've already seen carry over, albeit with slightly different syntax. For instance, if we want to take row or column means, we can:


~~~
data.mean(axis=0)
~~~
{: .python}

Pandas has built-in plotting commands, so we can quickly see what our data looks like:

~~~
data.mean(axis=0).plot()
~~~
{: .python}

It's good to see what the mean is, but the mean often doesn't tell the whole story. Let's plot all of the patients' values over time! By default, pandas' `plot` function plots columns, rather than rows (since usually each column represents a different variable). To plot columns, we'll access the transposed version of the DataFrame with `.T`:

~~~
data.T.plot(legend=False)
~~~
{: .python}

That's a lot of data! We can get a summary of our variables with:

~~~
data.describe()
~~~
{: .python}

If we want to grab a subset of variables to look at in depth, we can index into our DataFrame. Again, the syntax is similar, but here we need to specify that we're asking the DataFrame for the data by location:

~~~
data.iloc[1:5, 2:4]
~~~
{: .python}

Adding `.iloc` may seem like an arbitrary and cumbersome step, but there's a good reason for it: pandas lets you select data in a lot of other ways too! We're not going to go into all of them right now, but here's on example. Pandas lets you grab a subset of a DataFrame based on a boolean condition. Let's see that we want to look at the set of patients who has same amount of inflammation on day 1 of the experiment:

~~~
data[data[1] > 0]
~~~
{: .python}

We've only imported one of our data files! We could type out all of their names individually to import them, but there's a better way: the `glob` library. As strange a name as it has, the glob library is incredibly useful for grabbing lists of files that match a pattern:

~~~
data[data[1] > 0]
~~~
{: .python}



> ## Line plot
>
> Make a line plot of the inflammation values for the first 5 patients over the course of the experiment.
>
> > ## Solution
> >
> > ~~~
> > data.iloc[0:5, 1:60].T.plot()
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}
