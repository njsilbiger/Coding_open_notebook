---
layout: post
title: Let's get started!
categories: R
tags: [Getting started]
---
##post in progress##

This post focuses on how to start a project, properly set up a script, manage a clean working directory, and importing simple data.

----------

**What is a project**   
A project is a great way to keep all your different coding projects organized.  Each *project* has its own working directory, workspace, history, and documents. 

Here is how you create a project:  


1) Open R Studio  
2) Notice the Projects icon in the right hand corner 
 
![WhereIsProjects]({{ njsilbiger.github.io }}/images/Week1/WhereIsProjects.jpg?raw=true =200x200)
  
3)  Click on the drop down menu and then click on *New Project*...    
Notice how I have a bunch of random names (i.e. MASCOT, BioerosionCommunity, CarbonateChemistry).  These are the names of my current projects.
  
![NewProjects]({{ njsilbiger.github.io }}/images/Week1/ClickNewProject.png?raw=true =100x100)  

4) Once you click *New Project...*, you will be directed to this interface. Click *New Directory*.  Note this will create a project in your default working directory. If you want to put your project in a different directory, like dropbox, my documents, or your local GitHub folder, then click *Existing Directory* and navigate to where you want.  

![CreateNewProjects]({{ njsilbiger.github.io }}/images/Week1/CreateNewProject.png?raw=true =100x100)  

5) Next, click on *Empty Project*

![EmptyProjects]({{ njsilbiger.github.io }}/images/Week1/EmptyProject.jpg?raw=true =100x100)  

6) Then name your project whatever you would like (I named this one *RCodingClass*) and click *Create Project*.  

![NameProject]({{ njsilbiger.github.io }}/images/Week1/NameProject.jpg?raw=true =100x100)  

7) You will now be directed to your new project directory and you will notice that it now says *RCodingClass* in the top right-hand corner.  


![ProjectCreated]({{ njsilbiger.github.io }}/images/Week1/ProjectCreated.jpg?raw=true =100x100)  

8) Now, when you click on the drop down menu, you will not notice that *RCodingClass* has been added to the list of projects.   

![ProjectComplete]({{ njsilbiger.github.io }}/images/Week1/ProjectComplete.jpg?raw=true =100x100)  

9) When you have multiple projects, you can click on the project name to navigate between each and pick up right where you left off.

----------

**Setting up your working directory**  

There is nothing worse than having a messy working directory.  One of the major benefits of coding is to create transparent and reproducible research.  Having a messy directory makes it difficult for outsiders to follow your code/data.

For example, here is *what not to do*.  


![BadDirectory]({{ njsilbiger.github.io }}/images/Week1/BadDirectory.jpg?raw=true =100x100)  

Ah! My eyes! You can see that I have all sorts of data files, script files, and images all in the same folder and unless you are me, you can not tell what is what. So, let's set-up our new *RCodingClass* project so that it does not look like a crazy jumble.  

I typically create a minimum of two subfolders in my project directory: one for all my data files (e.g., .csv, etc.) and one for my output files (e.g., saved images). If I am writing a lot of functions, I will sometimes also have a subfolder for my functions and source them into my script. Some people like to also have a subfolder for all of their scripts, but that is personal preference and we will touch more on that later.    
 
A clean working directory looks something like this:  
![CleanDirectory]({{ njsilbiger.github.io }}/images/Week1/CleanDirectory.jpg?raw=true =100x100)  

Much better... Now it is time to set-up your script 
```R
# Let's get to coding! 
me<-c('excited','to','code')
```
