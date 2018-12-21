---
title: Parsing JSON with JQ
key: 20181220 
tags: jq JSON 
---

[jq](https://stedolan.github.io/jq/) is a command line tool for querying and manipulating JSON. This article will use
an example to demonstrate how to use it to parse JSON. 

Suppose you have a few EC2 instances running in AWS and you would like to get an overview of how many instances are there for each type. How would you approach it?

First of all, you run the `aws` command from cli and get a JSON file from AWS. 
```bash
aws ec2 describe-instances > ec2.json 2>&1
```    
Now, you have this `ec2.json` file with all the information about your EC2 instances. 
You need to figure out a way to parse the JSON file and do some aggregation. Like using a SQL query, you need to group the instances by type and count them. 

Luckily, AWS is kind enough to output the JSON file in a pretty format, meaning every key-value pair is in its own line. This makes it easy to use `Bash` tools to parse it. 
```Bash
cat ec2.json | grep InstanceType | sort | uniq -c
```
Quick and easy. 

However, what if the JSON is not in a pretty format? What if the output still has to be in JSON format?
In that case, you need `jq`. 

Same solution using `jq`: 
```Bash
map({Type: ..|objects|select(has("InstanceType")).InstanceType})
| group_by(.Type)
| map({key: .[0].Type, value: length})
| sort_by(-.value)
| from_entries
```
You can do it in a one liner but I prefer to save it into a script (`cnt.jq`) and run the script: 
```Bash
jq -f cnt.jq ec2.json
```
Then you will get the results in a JSON format 
````JSON
{
  "r4.xlarge": 143,
  "t3.small": 6,
  "t2.2xlarge": 4,
  ...
  "c4.8xlarge": 1,
  "t3.nano": 1,
  "c3.xlarge": 1
}
````
`jq` is a very powerful tool that can make wonders happen to JSON. I will write more notes on it.   