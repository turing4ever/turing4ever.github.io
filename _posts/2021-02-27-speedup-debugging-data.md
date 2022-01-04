---
title: Speed up data debugging
key: 2021-02-27
tags: 
published: false
---
When you start debugging data issues, you typically: 
1. Form a hypotheis on what's happening and trying to find some evidence to support or refute the hypothesis.
2. Check data values in some table to see if they make sense.
3. Jumping table to table because sometimes you need to translate some values or cross check.
4. You found something, then repeat above three steps until you clear all your doubts. 
It's an iterative process and your speed to solution depends on a lot of factors, such as: 
- Clairity on data definition and contrstraints. 
- Your familarity with the business and how data flows in the system with each business operation. 
- How fast your query runs. 

There are a lot of efforts required to achieve the first two speedups and sometimes it's beyond your control as
an individual engineer. But there are things you can do to speed up your SQL queries during investigation. 
Here are a few tips that I found useful: 
1. Narrow down the scope. 
   Obviously, if you can scope it down, you can deal with less volume of data, therefore you query runs faster. 
   Often, a simple time range can speed your query quite a lot. If you can only deal with one day's data, why bother 
   scan the whole table?
1. Try `random()` in your `where` clause when you are just trying to sample the data set. 
   When exploring values from a large table, especially when you are not quite sure about what you are looking for, 
   sampling with `random()` can help you speed up the query and at the same time get you more represenative samples. 
   On the contrary, if you try `select ... limit 100` instread, it's slower and you might just stare at the same few again and again. 
1. Create temporary tables to speed up joins. 
   Often the query runs slow because there are multiple joins in it. And you can not avoid joins because you need to piece those information together 
   to see a bigger picture. This is when the technique of temporary table can help you. 
   e.g. Narrow down your scope to a month, and create a temporary table from the large table with a few filters. Now join against your much smaller 
   temporary table instread of the large one, your query will spit out resutls much faster. 

Due to the nature of the iterative process, once you can get a few key queries run faster, you can drammatically cut down the time needed for your investigation. 

