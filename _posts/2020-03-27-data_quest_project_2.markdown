---
layout: post
title:      "Data Quest Project #2"
date:       2020-03-27 19:00:28 +0000
permalink:  data_quest_project_2
---


I have been whizzing through the dataquest projects and have come to their second project. The second module focuses all on data visualization. Something I think is fairly easy, but I did learn a thing or two! For starters I realized the difference between calling the method on our object say a dataframe vs. on a series. Below I explain and demonstrate the differences:

```
df[XX:XX].plot.bar(x='dummy x', y='dummy y') 

df.plot(kind='dummy graph type')
```

Where XX is the range of your data and x and y variables are the columns you want to select. This is different from calling a datarame and then the plot method. We use Series.plot() to plot a specific column and DataFrame.plot() to generate plots that use values from multiple columns.

Un addition there are advantages to say calling the histogram method on a dataframe as this allows for more customization. For example, for histograms there is a way to customize the bins and range which is not available in the series.plot().

The second thing I learned that was very useful and I gained full clarity on was subplots. I am not very comfortable with creating a figure (aka space for your graph to go) then adding subplots to the figure space. The method add_subplot() is used for this. Below I demonstrate my understanding of this concept.

```
.add_subplot(X,Y,Z)

fig= plt.figure()
ax1= fig.add_subplot(2,1,1)
ax2= fig.add_subplot(2,1,2)
```

X= Row of the number of graphs
Y= Column of the number of the graphs
Z= Position or order of graphs aka a label

So the above example would be a figure that shows two graphs stacked on top of each other because there is one column with two rows. The ax1 would be the first graph followed by ax2, the second graph.








