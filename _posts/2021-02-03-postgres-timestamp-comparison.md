---
title: Postgres SQL Timestamp Comparison Puzzle
key: 2021-02-03
tags: postgres SQL 
---
I ran into a weird puzzle today when comparing two timestamps in postgres. 
Take a look at following queries: 
```sql
select sum(metric)
from table_name
where lower(dt_range) < '2021-01-06 00:00:00+00'
and lower(dt_range) >= '2021-01-05 00:00:00+00' 
;
```
and 
```sql
select sum(metric)
from table_name
where lower(dt_range) < '2021-01-06 00:00:00+00'
and lower(dt_range) >= '2021-01-05 00:00:00+00' 
;
```
-- here lower(dt_range) is timestamptz type and in eastern timezone. 

Those two queries produce different results. Why?   


The culprit here is the timezone in implicit type conversion.   

First of all, when postgres compares two values they should be the same type, 
postgres sometimes will implicitly convert one type into another to facilitate comparison. 
In our example here, timestamp strings will be implicitly converted into timestamptz.
Secondly, the '+00' in '2021-01-06 00:00:00+00' will be treated as explicitly setting timezone to UTC. 
The string '2021-01-06' will be treated as a sting of timestamp without timezone and then the actual conversion happens in two steps: 
- Append default timezone to the timestamp.
- Convert to eastern time. 

Maybe it will look more obvious in following queries: 
```console
=# set timezone to 'America/New_York';
=# select timestamptz('2021-01-06');
      timestamptz
------------------------
 2021-01-06 00:00:00-05

=# set timezone to 'America/Los_Angeles';
=# select timestamptz('2021-01-06');
      timestamptz
------------------------
 2021-01-06 00:00:00-08

=# select timestamptz('2021-01-06 00:00:00+00');
      timestamptz
------------------------
 2021-01-05 16:00:00-08
```
