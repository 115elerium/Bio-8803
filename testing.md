# Building Shiny apps

**Tyrone Lee**

**June 14 2018**

## Table of contents

1. [Prerequisites](#prerequisites)
2. [What is Shiny?](#what-is-shiny)
3. [Create an empty Shiny app](#Create-an-empty-Shiny-app)
4. [Load the dataset](#load-the-dataset)
5. [Build the basic UI](#build-the-basic-ui)
6. [Add inputs to the UI](#add-inputs-to-the-ui)
7. [Add placeholders for outputs](#add-placeholders-for-outputs)
8. [Checkpoint: what our app looks like after implementing the UI](#checkpoint-what-our-app-looks-like-after-implementing-the-ui)
9. [Implement server logic to create outputs](#implement-server-logic-to-create-outputs)
10. [Reactivity 101](#reactivity-101)
11. [Using uiOutput() to create UI elements dynamically](#using-uioutput-to-create-ui-elements-dynamically)
12. [Final Shiny app code](#final-shiny-app-code)
13. [Share your app with the world](#share-your-app-with-the-world)
14. [References & Resources](#references-&-resources)


## 1. Prerequisites

Before coming to this talk you would need a laptop and a fresh installation of R and Rstudio


[R base](http://mirrors.nics.utk.edu/cran/)


[RStudio](https://www.rstudio.com/products/rstudio/download/#download)

Once installed, open R studio and install the `shiny` package.


```r
install.packages("shiny")
```
If you are on windows and having issues, there is a known bug in the latest version. Instead, try installing an earlier version of `shiny`.

```r
install.packages("devtools")
require(devtools)
install_version("shiny", version = "1.0.5", repos = "http://cran.us.r-project.org")

```

To ensure you successfully installed Shiny, try running one of the demo apps.


```r
library(shiny)
runExample("01_hello")
```

If the example app is running, press *Escape* to close the app. 
We will also need some other packages to build the final resulting app in this tutorial, after verifying
shiny works, try to install the other packages we will need.

```r
install.packages("dplyr")
install.packages("ggplot2")
```

# 2. What is shiny?


Shiny is a package from RStudio that can be used to build interactive web pages with R. While that may sound scary because of the words "web pages", it's geared to R users who have 0 experience with web development, and you do not need to know any HTML/CSS/JavaScript.

You can do quite a lot with Shiny: think of it as an easy way to make an interactive web page, and that web page can seamlessly interact with R and display R objects (plots, tables, of anything else you do in R).

This tutorial is a hands-on activity complement to today's Lunch and Learn. In this activity, we'll walk through all the steps of building a simple shiny app that reads a stored dataset and displays a histogram that can be created dynamically by changing inputs in the app. Copy and paste the code into a fresh R script and follow along with the presentation. 

This tutorial should take approximately an hour to complete. Any activity deemed as an exercise throughout this tutorial is not mandatory for building our app, but they are good for getting more practice with Shiny. We will also not be covering reactivity in section 10, we in the interest of time will be stopping at section 9 which covers most of the basic user interface and server interactions.  The final app also includes a few extra features that are left as exercises for the reader.

If you want even more practice, another great tutorial is the [official Shiny tutorial](http://shiny.rstudio.com/tutorial/). RStudio also provides a [handy cheatsheet](https://www.rstudio.com/resources/cheatsheets/) to remember all the little details after you already learned the basics. I would also strongly encourage those willing to invest time into learning shiny to cover reactivity as it is a core feature of the package.
