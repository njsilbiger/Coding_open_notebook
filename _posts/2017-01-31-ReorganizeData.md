---
layout: post
title: Reorganize Data from wide to long format
categories: R
tags: [Data structure, plotting]
---
This post focuses on how to reorganize your data from a wide to a long format

----------

**Reorganize data** 

My friend, Krissy, contacted me with a common coding problem.  She said:


"I have ʻplate mapsʻ made up of sample names laid out spatially in a 96 well plate (row names are A-H, column names 1-12) 

I'd like to "stack" these so that we have 3 columns-Row Name, Column Name, & Sample Name

I need to keep track of the original "location" of each of these sample names...

For those of us that this means something to: The ultimate goal will be to match these plate maps with the primer plates I used to build 16S libraries."

Here is what a 96-well plate looks like:

![WellPlate]({{ njsilbiger.github.io }}/images/Week4/WellPlate.png?raw=true =200x200)

Here is what her data looks like:

![KrissyData]({{ njsilbiger.github.io }}/images/Week4/KrissyData.png?raw=true =200x200)

To do this, I used the function gather in the tidyr package like so:

```R
df<-read.csv('KRPlate.csv') # read in the data

library('tidyr') # load the library

# dataframe name, tell it what the new columns names are (column, SampleName), then say what columns you are gathering (X1:X12), and that you want the data to be a factor.

df.melt<-gather(df, column, SampleName, X1:X12, factor_key=TRUE)
colnames(df.melt)[1]<-'Row' # rename the first column as Row
```

Here is what the output looks like:

![KrissyResults]({{ njsilbiger.github.io }}/images/Week4/KrissyResults.png?raw=true =200x200)
