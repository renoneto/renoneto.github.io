---
layout: post
title:      "Understand the Q-Q Plot"
date:       2021-03-04 13:49:12 +0000
permalink:  understand_the_q-q_plot
---

The Quantile-Quantile Plot is a scatterplot that helps to assess whether a variable is normally distributed. However, because it's a graphical tool, it's prone to error. Another benefit of the plot is to quickly show deviation in the data (skewness/tailedness).

## How does it work?
Let's say we have a data set, and we would like to check if the samples follow a normal distribution.

Using the Q-Q Plot, we can quickly answer that question. 

First, we need to calculate the **quantile of each Sample**.

### What are Quantiles?
Quantiles represent the Percentage of the Data Set below a certain Data Point. For example, let's say we have the following samples:

> Samples: 4,5,6,1,2,3,7,8,9,13,14,15,10,11,12.

To calculate quantiles, we take the quantile value (**q**) and multiply by the no. of samples plus one (**n + 1**), the result will be the sample location after ordering all samples from smallest to largest.

> Ordered samples: 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15.

**The calculation of the 0.5 quantile is the following then:**
- 0.5 x (15 + 1) = 8 > The 8th sample. Which in this case is **8**. 
    - **Group Below:** 1, 2, 3, 4, 5, 6, 7 >> 7 elements
        - (7 + 1) / (15 + 1) = 0.5 >> 50% of the elements are below 8.
    - **Group Above:** 9, 10, 11, 12, 13, 14, 15 >> 7 elements.

**Therefore, using the same calculation we can also get to the 0.25 quantile:**
- 0.25 x (15 + 1) = **4** is the 0.25 quantile (25% of the data set is below **4**).
    - **Group Below:** 1, 2, 3 >> 3 elements.
        - (3 + 1) / (15 + 1) = 0.25 >> 25% of the elements are below 4.
    - **Group Above:** 5, 6, 7, 8, 9,10,11,12,13,14,15 >> 11 elements.

## Analyzing the Q-Q Plot
Now that we understand Quantiles, the rest is very straightforward. Because all the plot does is to compare Quantiles of a Normal Distribution vs. the Sample's. 

The way it works, the chart will calculate each element's quantile from your data set and do the same using a normal data set (with the same No. of Elements from the data set). Then it will plot them side-by-side, following the same order (from smallest to largest).

If the Sample is normally distributed, the plot will form a straight line. Otherwise, we will see something else:

![](https://miro.medium.com/max/1024/1*_wuWDNGs3hB2K0_kgpoc1A.jpeg)

[Source: Polymatheia](http://sherrytowers.com/2013/08/29/aml-610-fall-2013-module-ii-review-of-probability-distributions/qqplot_examples/)

Look how easy it's to spot a non-normal distributed data set. With that information, data scientists can fine-tune their models or scale/normalize features.

> Notice that, like many things in statistics and machine learning, having more data points will make the plot more reliable.
