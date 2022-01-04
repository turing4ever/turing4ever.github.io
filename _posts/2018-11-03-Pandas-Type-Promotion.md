---
title: Pandas Type Promotion
key: 20181017 
tags: 
published: false
---
If you are dealing with data in pandas, sooner or later you will run into some surprises: type promotion.

**What is type promotion?**  
Unlike Numpy, Pandas promises to handle heterogeneous arrays, meaning data of different types can co-exist within the same column. 
Just like what you would expect in an excel sheet. This feature gives you more flexibility when facing messy data. However, under the hood, all pandas
data is stored in a continuous memory space with a constant unit. This is because pandas wants to keep the performance of accessing the array randomly. 
Here comes the conflicting interests: on one hand, more tolerant element type leads to variant element size. On the other hand, high performance memory access demands unified element size. 
The trade-off made to resolve the conflicts is type promotion. When one column contains data with mixed types, the type is `promoted` from the type with low memory size to type with the highest memory size.
In this way, the `column` can `contain` all the possible data with the type with highest memory size.  
   

**What triggers type promotion?**
1. New elements with higher type is added. 
    ```python
    s = pd.Series([1, 2, 3, 4, 5], index=list('abcde'))
    print(s.dtype) #int64
    s['f'] = 9.9
    print(s.dtype) #float64 
    ```
2. Missing data `NaN` or `NaT` mixed with `int` elements.  
    ```python
    s = pd.Series([1, 2, 3, 4, 5], index=list('abcde'))
    print(s.dtype) #int64
    s['a'] = None
    print(s.dtype) #float64 
    ```
3. Mixed type columns from SQL query.   
    When pd.read_sql() is called against a database, type promotion can happen if column contains `NULL` values.
 

**What's the impact?**  
It will cause some type sensitive functions to fail. For example, if you are inserting data into tables in postgres database, 
data with wrong type will get rejected by the database. 

**Remedy**  
The flexibility of mixed type data is a blessing when doing manual data analysis, but a curse when building data pipelines. When some data type mutated, due to either missing data or wrong data, your once working data pipeline all of sudden breaks down. Therefore, you would prefer to suppress the automatic type promotion by:  
* Force type casting. (Especially in SQL query)
* Assign default value to missing data.
  
I wonder if this is the down side of using Pandas for building data pipelines. Numpy's homogeneous array might be better suited for building reliable data pipelines.  
