---
title: Hello World in GraphQL
key: 2021-03-15
tags: 
---
When you are learning a new programming language, you want to try out the simplest thing first.   
In programming languages such as C or Python, you print out a stirng "hello world".   
In SQL, you are probably running a query like `select now()`.   
In another word, you are looking for the simplest statement of the language, actionable, but at the same time, OS agnostic, library agnostic and configuration agnostic.  
Once you issue this statement and see it coming back with easily recognizable results, you know that your local dev environment is all set. 


What is such a `hello world` statement in GraphQL? What I found is this introspection query: 
```graphql
{
    __schema{
        tyeps{
            name
        }
    }
}
```
Simple, minimal and schema agnostic. 


For exmaple, if you are trying out a python gql libary, you might run into several potential issues: 
- autentication
- query syntax error
- library or configuration issue


Facing those uncertainties, you should not start with a complicated yet useful GQL query. 
Instead, you should try this query first. 

```python
from gql import Client, gql
from gql.transport.requests import RequestsHTTPTransport

reqHeaders = {
    'Content-Type' : 'application/json',
    'Authorization' : 'ApiKey YOUR_ACTUAL_API_KEY',
}
transport = RequestsHTTPTransport(
    url="https://YOUR_API_SERVER/api/graphql",
    headers = reqHeaders,
    use_json=True,
)
client = Client(transport=transport, fetch_schema_from_transport=True)

query = gql(
        """
        {
        __schema{
            types{
                name
            }
        }
        }
 """
)

result = client.execute(query)
print(result)
```
Once you see a list of type names printed, you know you see your `hello world` in GraphQL. 
