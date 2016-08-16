---
title: "Reading in data from multiple files"
teaching: 10
exercises: 2
questions:
- "How can I read in data from multiple files?"
- "How can I check for inconsistencies between files?"
objectives:
- "Explain how to use Pandas to import and clean data."
keypoints:
- "You can use glob.glob() to get a list of files matching a pattern"
- "You can create a list of DataFrames and concatenate them into one big frame."
- "We can use plots to check for potential issues with the data."
---

Pandas has a ton of cool features, but lets not get too distracted! We've only imported one of our data files! We could individually call `read_csv` on each file in the directory, but that would be a pain. Instead, we're going to use a strangely named but highly useful library called `glob.`

Using the `glob` function in the `glob` library, we can get a list of all files that match a given pattern:

~~~
import glob
file_list = glob.glob("../data/inflammation*.csv")
~~~
{: .python}

Now that we have a list of our files, we want to load them into a pandas DataFrame. We can achieve this by looping over each file in the list, loading it, and then glueing them all together with `pandas.concat()`

~~~
frames = []
for filename in file_list:
    frames.append(pandas.read_csv(filename, header=None))
data = pandas.concat(frames)
~~~
{: .python}

That's all well and good, but before we proceed, we should probably take a look at our data and make sure that there aren't any inconsistencies across the files (they were probably all recorded at different times).

~~~
for i,df in enumerate(frames):
    df.min(axis=0).plot()
    df.mean(axis=0).plot()
    df.max(axis=0).plot()
    plt.title(file_list[i])
    plt.legend(["min", "mean", "max"])
    plt.xlabel("Day")
    plt.show()
~~~
{: .python}

Hmm, looks like there are some patients who consistently have 0 inflammation. We might want to exclude them as outliers.

~~~
data = data[(data.T!=0).any()]
~~~
{: .python}



~~~
> ## Challenge Title
>
> There are three data files that we haven't played with yet - the three small ones. Let's pretend that we are only interested in the ones that don't start with 0s. Read them all into a single DataFrame (assume that each of them have the same three columns), remove the rows that start with 0s, and make a line plot showing the average value across the three columns.
>
> > ## Solution
> >
> > ~~~
> > file_list = glob.glob("data/small*.csv")
> > frames = []
> > for fname in file_list:
> > > frames.append(pandas.read_csv(fname))
> > data = pandas.concat(frames)
> > data = data[data.T[0]!=0]
> > data.mean(axis=0).plot()
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}
~~~
{: .source}
