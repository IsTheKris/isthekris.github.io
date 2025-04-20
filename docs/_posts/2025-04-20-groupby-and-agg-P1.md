---
layout: post
title: "Pandas: groupby and agg"
date: 2025-04-20
categories: [blog]
---
For some, `groupby()` and `agg()` can be a bit confusing in the beginning. The syntax may look strange, especially when they are chained together 
as `groupby().agg()`. But learning how to use them properly is very important. These are powerful functions in pandas that help you group data 
and then apply functions like `sum()`, `mean()`, or even custom functions to each group. Using this we can create new summarized DataFrames. 

The `agg()` function is commonly used alongside `groupby()` in pandas. When you group data using `groupby()`, you often need to perform one or more 
operations on each group. This is where `agg()` becomes useful. It allows you to compute summary statistics such as `totals`, `averages`, `counts`, or 
even apply `multiple functions` at the same time, making it a powerful tool for data analysis.

Let's discuss this concept in more detail using an example. I’ve created a dataset that tracks my monthly expenses from January 1, 2025, to April 15, 2025. 
Go through the Jupyter Notebook linked below for a step by step explanation.

