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

![LaurenDrawing]({{ njsilbiger.github.io }}/images/Week2/LaurenDrawing.jpg)


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


There is nothing worse than having a messy working directory.  One of the major benefits of coding is to create transparent and reproducible research.  Having a messy directory makes it difficult for outsiders to follow your code/data.

For example, here is *what not to do*.  


![BadDirectory]({{ njsilbiger.github.io }}/images/Week1/BadDirectory.png?raw=true =100x100)  

Ah! My eyes! You can see that I have all sorts of data files, script files, and images all in the same folder and unless you are me, you can not tell what is what. So, let's set-up our new *RCodingClass* project so that it does not look like a crazy jumble.  

I typically create a minimum of two subfolders in my project directory: one for all my data files (e.g., .csv, etc.) and one for my output files (e.g., saved images). If I am writing a lot of functions, I will sometimes also have a subfolder for my functions and source them into my script. Some people like to also have a subfolder for all of their scripts, but that is personal preference and we will touch more on that later.    
 
A clean working directory looks something like this:  
![CleanDirectory]({{ njsilbiger.github.io }}/images/Week1/CleanDirectory.png?raw=true =100x100)  

Much better... Now it is time to set-up your script  

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
