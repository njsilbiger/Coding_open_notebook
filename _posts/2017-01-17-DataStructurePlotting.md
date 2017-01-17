---
layout: post
title: Data structure and simple plotting!
categories: R
tags: [Data structure; plotting]
---
This post focuses on proper data structure and some basic plotting techniques.

----------

## work in progress 

**Data structure**   
How you structure your data in excel is very important. Putting your data in a complicated structure can make coding very difficult.  The best way to organize your data is by using a long format. 

*What does it mean to have a long format?*

Lauren Pandori, a grad student in the Sorte Lab, supplied me with some of her data for this lesson.  Let's take a look at how she formatted it.

The first time that she sent me here data it was formatted like this:

![ShortFormat]({{ njsilbiger.github.io }}/images/Week2/ShortFormat.png)

There are two issues with this formatting:
1) It is in short format.  You can see that ever quadrat has its own column.  This is completely fine for analyzing data in excel, but it is not appropriate for R.
2) The names have spaces and non alphanumeric characters in them and they are long. 

Here is an example of this same data, but formatted in a way that is much more amenable to R:

![LongFormat]({{ njsilbiger.github.io }}/images/Week2/LongFormat.png?raw=true =200x200)

You can see now that every row is a unique data point with all the columns listed the different attributes of that data point. 

----------
**Simple Plotting** 

Today we are going to take Lauren's data and make a simple plot. Lauren's data set consists of Mussels counts across 5 different microhabitat types (Tide pools, Unsheltered Solitary, Sheltered Aggregate, and Unsheltered Aggregate) in 3 different tidal zone (Low, Mid, High). She also has 10 replicate quadrats across each tidal zone and microhabitat type. When I asked Lauren how she wanted her data plotted she sent me this picture. :) So, this is what we are going to plot today!

![LaurenDrawing]({{ njsilbiger.github.io }}/images/Week2/LaurenDrawing.jpeg)


----------

**Let's code!**  

First, remember from last week how to properly structure your script. So, let's follow our best practices

```R
#################################################### 
# Script to create plot for Lauren's ocean project #
# Created by Nyssa
# created on 1/16/2017
####################################################

## clear workspace---------
rm(lists=ls())

## set working directory------
setwd(getwd())

# load libraries------------------
library(plyr) #need to summarize data 

## Load Data-------------
Data<-read.csv('Data/PandoriData.csv')

## Data analysis-----------------
```

Before we start any data analysis it is always best to check your dataset and make sure that there are no errors. You can do this by using the head () and tail () function. This shows your the first 6 and last six rows of your data. Then you can see if there is anything weird and you can clean it

```R
# clean the data--------------
# check the data
head(Data)
tail(Data)

## there seems to be an extra row, probably because something was deleted

#remove extra/unwanted column
Data$X<-NULL

```
There is nothing worse than having a messy working directory.  One of the major benefits of coding is to create transparent and reproducible research.  Having a messy directory makes it difficult for outsiders to follow your code/data.

Our data is now in a clean *dataframe* (the name of the data strucutre).  You will notice that there are two different types of data in the dataframe. A *factor* and an *integer*. The factor are discrete data that have levels.  For example, Tide height here is a factor with levels low, mid, and high.  R automatically puts the levels in alphabetical order, but sometimes this does not make sense.  For example, high should go after mid, not before. So now we are going to order the factors a way that makes sense for Lauren's data. 

```R
# order the habitat data by level of environmental filtering:
# 1. Unsheltered solitary (Usol), 2. Unsheltered aggregate (Uagg), 3. Sheltered solitary (Ssol),
# 4. Sheltered aggregate (Sagg), 5. Tidepool (Tide)

Data$Uhab <- ordered(Data$Uhab, levels = c("Usol", "Uagg", "Ssol","Sagg","Tide"))

# check that they are ordered the correct way
unique(Data$Uhab)

#Let's do the same for tide height
Data$TideHt<-ordered(Data$TideHt, levels = c("Low","Mid","High"))
```

Next, we want to take the averages by tide height, life stage, and habitat type to make the figure that she would like.  We are going to have an entire lesson on different ways to summarize data so I am not going to go into detail on different ways to do this.  I really like the *ddply* function from the *plyr* package so that is what I am going to use. 


```R
## take the averages by tide height, juve/adult, and habitat
Data.mean<-ddply(Data, c("TideHt","LifeStage","Uhab"), summarize,
                 Abun.Mean = mean(Abun, na.rm=TRUE), # this is saying to take the mean and ignore missing data if there is any
                 N = sum(!is.na(Abun)), # how many samples do you have (code says what is not a missing value and sum the counts)
                 Abund.SE = sd(Abun)/sqrt(N) # this is the standard erre
                 )

# check the data
Data.mean  #notice that it calculated the means and SE in the order that you specified above
# Low, then Mid, then High, and same for the order for Uhab

```

I now have a new dataframe with the averages and standard error values by each group that I am interested in visualizing. 

Now let's plot the data.
 first let's create a barplot with just the low tide data. Because we have 2 different groupings (Tide height and also Life stage), we need to make the data a matrix with adults on top and juveniles on the bottom. The below code will put the first 5 data points (adults) in one column and then the second 5 in the second column and then I used t to transpose it so that there are 5 columns and 2 rows. 

```R
# I created a matrix for the mean and named it m 
m<-t(matrix(Data.mean$Abun.Mean[Data.mean$TideHt=='Low'],5,2))
# a matrix for the SE and names it mse
mse<- t(matrix(Data.mean$Abund.SE[Data.mean$TideHt=='Low'],5,2))    
```

Now let's create a barplot with this data.

```R
x<-barplot(m) # m is our mussel mean data
        
```
When we run this code we get a really simple plot below with all the defaults.

![simpleplot]({{ njsilbiger.github.io }}/images/Week2/simpleplot.png)


 The default is to stack the data on top of each other.  If this were % cover data it would be fine, but it is not so let's put them next to each other using beside=TRUE. Also, let's customize it a bit so that it is more informative. The names.arg says what we should name the x-axis.  You can also manually put in names to make it prettier. I also set the y axes from 0 to the max abundance across + SE the entire data set and I gave it a title of Low tide and a y-label of mussel density. Look at ?barplot to find all the ways that you can manipulate a barplot.

```R
x<-barplot(m, # m is our mussel mean data
        beside=TRUE, names.arg = unique(Data.mean$Uhab), ylim=c(0, max(Data.mean$Abun.Mean)+ max(Data.mean$Abund.SE)),
        main='Low Tide', ylab="Mussel Density")
```

This code will now create the plot below.

![LowTide1]({{ njsilbiger.github.io }}/images/Week2/LowTide1.png)

Now, let's add error bars. One of the ways to make error bars in the base package with the function *arrows* which essentially adds an arrow from 
 point x to point y in whatever direction that you want. I named the barplot above x. You will notice that now x is a 2 x 5 matrix.  These are the positions of the data (the bars in the figure) along the x-axis.  The first row is the adult and the second are the Juveniles


----------

**Set-up your first script**  

New coders tend to start their code right away with no comments or explanations of what they are doing. But, again, we want to produce transparent and reproducible research. There have been times where I set-up a script poorly and had to go back to it after a year to re-analyze some data (reviewers are always asking to change analyses, aren't they... ;) ). I, the creator of the code, could not figure out for the life of me what I did. It was a painful few days trying to remember why I was doing what I was doing; it definitely could have been avoided by using proper coding etiquette.  

This lesson, I am just going to show you what a properly set-up script looks like. Over the next few weeks we will discuss these different sections in more detail.  

Below, I have divided my script up into 7 different sections:  
 
![CleanScript]({{ njsilbiger.github.io }}/images/Week1/CreatingAScript.jpg?raw=true =300x300) 

Section 1:  Start with a short intro of what your intend to do with your script. Say who you are, the date you created it, and when you last edited it.  

Section 2: Clear the workspace. This section removes everything from your environment.  People have different opinions on this. I always like start with a clean slate so that variables from prior R sessions don't conflict my my new session.  

Section 3:  Load the libraries. Here, I load all the libraries that I need for my code to run.  

Section 4:  Set your working directory.  Luckily, with projects, you will be sent straight to your project working directory.  But, if you have created a sub-directory, like I did here, you will need to navigate to that folder.

Section 5: Functions. If you will be creating your own functions it is best to put them all right up front so that they are available for the whole script.  If I have lots of functions, sometimes I will put them in their own script and then source them in so that it is not so messy.  More on that later.  

Section 6: Load data.  This is where you load all your data files.

Section 7 and beyond: All your analyses, which can also be subset into different sections.

**Probably the most important advice that I can give you is to comment, comment, comment, and comment some more on your code.  You can never give too many details, but you can definitely give too little.**  

For example, look at *section 5* where I wrote a function to calculate the fugosity of CO2 in seawater. I listed all the parameters and what they mean, I commented all the formulas and the units that the output should be in, and I also listed the citation for where the formula came from.  This way, if you share the code with a colleague, they can see what you are trying to do and where it came from, and maybe find any errors.  

OK, now your turn! 
