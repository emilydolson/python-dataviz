---
title: "Visualizing data with Seaborn"
teaching: 10
exercises: 2
questions:
- "How can I use Seaborn to make more complex data visualizations?"
objectives:
- "Explain how to visualize pandas DataFrames with seaborn."
- "Explain how to rearranged pandas DataFrames."
keypoints:
- "Seaborn has a ton of really pretty visualizations that you can pretty much just drop your DataFrame into"
- "An index is basically a column that includes row names - they're really important in pandas"
- "Pandas provides a lot of tools for re-arranging DataFrames, such as melt()"
---

Pandas has a wealth of plotting features (we haven't even scratched the surface yet), but sometimes you need a slightly more elaborate data visualization. For those times, there's Seaborn (there are a lot of other Python visualization libraries too, but Seaborn is possibly the easiest).

Let's start out by making a heatmap of inflammation over time by patient.

~~~
import seaborn as sns
sns.heaatmap(data, xticklabels=False, yticklabels=False)
~~~
{: .python}

It would be useful to have a plot that shows error around an average trajectory over time. We can accomplish this with Seaborn's `tsplot`, but we need to re-arrange the data a little first. We need to have all of our information about what time point a given inflammation value was taken at in a single column. This will take a few steps:
~~~
data = pandas.concat(frames)
data = data.set_index(pandas.Series([i for i in range(720)]))
data.reset_index(level=0, inplace=True)
data = pandas.melt(data, id_vars=["index"])
data.columns = ["patient", "day", "inflammation"]
~~~
{: .python}

Now we're ready to make the plot:

~~~
sns.tsplot(data=data, time="day", value="inflammation", unit="patient")
~~~
{: .python}


> ## Making a histogram
>
> Seaborn has a function called distplot that makes a histogram. See if you can use the documentation to figure out how to make a histogram of the various inflammation values.
>
> > ## Solution
> >
> > ~~~
> > sns.distplot(data["inflammation"])
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}
