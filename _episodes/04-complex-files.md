---
title: "Files with multiple variables"
teaching: 10
exercises: 2
questions:
- "How can I use Seaborn to visualizae more complex data?"
objectives:
- "Explain how to use more complex Seaborn visualizations."
keypoints:
- "Seaborn has a ton of really pretty visualizations that you can pretty much just drop your DataFrame into"
---
So far, we've only been using a fraction of pandas' abilities. One of the coolest things that it can do is deal nicely with column names. So lets load in a dataset that takes advantage of that.

~~~
gapminder = pandas.read_csv("gapminder_all.csv", index_col="country")
~~~
{: .python}

This is a lot of data. We can select a subset of the columns to play with, using their names:

~~~
gapminder_recent = gapminder[["gdpPercap_2007", "pop_2007", "lifeExp_2007"]]
~~~
{: .python}

There are a lot of things you want to see when you first load in a new dataset - the distribution of each of the variables, relationships between those variables, and so on. Seaborn lets you make a grid containing all of those things.

~~~
g = sns.PairGrid(gapminder_recent, diag_sharey=False)
g.map_lower(sns.kdeplot)
g.map_upper(plt.scatter)
g.map_diag(sns.kdeplot, lw=3)
~~~
{: .python}

Looks like there are roughly two clusters for gdp, and they seem to have a relationship with life expectancy. Let's explore that further with a violin plot. A violin plot allows you to look at the distributions of a variable across various subgroups. Let's make one looking at life expectancy by continent.

~~~
sns.violinplot(data=gapminder_recent, x="continent", y="lifeExp_2007")
~~~
{: .python}

It would be interesting to see how gdp relates. Seaborn allows you to create split violin plots, to compare two subgroups per group that you're looking at. Let's make a column with a boolean value, indicating whether a country is in the high gdp cluster or not, and use that to make a split violin plot.

~~~
high_gdp = gapminder_recent["gdpPercap_2007"] > 20000
gapminder_recent.append({"high_gdp": high_gdp}, ignore_index=True)
sns.violinplot(data=gapminder_recent, x="continent", y="lifeExp_2007", split=True, hue="high_gdp")
~~~
{: .python}

> ## Exploring plots
>
> Seaborn has a ridiculous number of data visualizations for you to use, and so does pandas. Browse the galleries (https://stanford.edu/~mwaskom/software/seaborn/examples/index.html and http://pandas.pydata.org/pandas-docs/stable/visualization.html#plotting-tools) and pick out a graph to try out.
{: .challenge}
