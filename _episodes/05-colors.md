---
title: "Pretty colors"
teaching: 10
exercises: 2
questions:
- "How can I choose colors responsibly?"
objectives:
- "Explain things to consider when choosing color palettes and how Seaborn can help."
keypoints:
- "Cubehelix pallettes are great, because they are both color-blind friendly and play nicely with non-color printers"
- "Some color palettes (such as the standard rainbow one) can be deceptive to the eye"
- "When choosing colors, consider your goals"
---

If you find the right corner of the internet, people have some very strong opinions about color. While you may not care to get as impassioned as them, it's still good to be familiar with their high-level points:
1. Color is the most popular way for conveying information about a third dimension in your data - when done right, it is both aesthetically pleasing and effective.
2. 8% of men are color-blind - that's a sizeable portion of your audience, so you should pay attention to making figures that are comprehensible to them
3. Of those people who do have perfect color-vision, a large number will print your graph out in black and white.
4. When converted to greyscale, many popular color palettes are at best hard to see and at worst misleading (this is also true to some extent of those same palettes when not converted to greyscale)

Seaborn has color palettes designed to solve all of these problems. The most versatile is the Cubehelix palette, which you can play with by entering the following command into your Jupyter Notebook:

~~~
sns.choose_cubehelix_palette()
~~~
{: .python}

It's also important to consider what information you're trying to convey. Is your data on a continuous scale? Then you probably want a continuously changing color palette. Is is indicating completely unrelated categories? Then you probably want a categorical palette, like `color_brewer`. Much more detail is available on the Seaborn documentation: https://stanford.edu/~mwaskom/software/seaborn/tutorial/color_palettes.html.

In general, color palettes can be passed to any seaborn graphic to control what colors it uses.

> ## Using color palettes
>
> Choose a color palette that you like and apply it to a visualization that you like.
{: .challenge}
