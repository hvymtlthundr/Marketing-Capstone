# Marketing-Capstone
Real-world use of Google Analytics


---
title: "Untitled Campaign Analysis"
author: "Armand Culpepper"
date: "`r Sys.Date()`"
output: html_document
---

## Marketing Case-study Analysis
 The stakeholders at Studio ND., INC. need to know their overall performance relative to their marketing objectives.They needed clarity on best marketing strategy to implement, and executed a variety of approaches while documenting the process. The dataset contains campaigns that have been launched to improve engagement with their audience and further exposure for their brand, from June 2022 to Oct 2022.


##### (The Stakeholder's Concerns): "What was the prior engagement rate and how can it be improved?"

We need:

```{r loading packages, include=FALSE}
library(ggplot2)
```

```{r Defining X, include=FALSE}
x <- read.csv("TikTok Campaign - Studio ND.csv") #Total Campaigns dataset
```

```{r Defining Y, include=FALSE}
y <- na.omit(x$Follows) 
```

* View:Like ratio as %  

```{r echo=TRUE}
r <- na.omit(x$Initial.Views/x$Likes)
r  # the lower, the better for likes; the higher the better for views
# For our purposes, lower results are more desirable 
```

* View:Follow ratio as %
```{r echo=TRUE}
t <- na.omit(x$Initial.Views/x$Follows)
t  # the lower, the better for follows; the higher the better for views
# For our purposes, lower results are more desirable  
```
* Followers:Duration ratio as %

*Note:* Duration is defined by individual campaigns.
```{r}
boxplot(Follows ~ Duration, x) #shows relationship between following engagement and campaign length
```

We also collected data to identify KPIs, including but not limited to:
```{r echo=TRUE}
#total views
tv <-sum(na.omit(x$Initial.Views))
tv
```

```{r echo=TRUE}
sum(na.omit(x$Cost)) # total dollar cost
```


```{r echo=TRUE}
boxplot(x$Cost ~ x$Initial.Views)
```

Here's the same data in a scatter plot, to further see the potential of a correlation
```{r warning=FALSE}
ggplot(data=x) +    #shows correlation $ amount spent and initial view reached
  geom_point(mapping=aes(x$Initial.Views, y=x$Cost))
```

As it turns out, there may very well exist a correlation.
```{r echo=TRUE, warning=FALSE}
ggplot(data=x) +
  geom_line(mapping=aes(x=x$Follows,y=x$Cost))
```

### Reccomendation:

* Duration 
```{r}
boxplot(Follows ~ Duration, x) #shows relationship between following engagement and campaign length
### Using Bayesian logic, the current implication indicates a greater ROI for longer campaigns on average, while factoring in use of resources.
```

* Budget
There appeared three price ranges, >50, >=100, and <200. While there was noticeable growth within the >=100 range, there appears a trend of steadily growing engagement within the >50.Therefore, Studio ND has clear incentive towards improving targeted demographic outreach within these two areas
