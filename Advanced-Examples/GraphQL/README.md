# How to use Graphql API in Loadmill?
Note! This page does not provide information about what GraphQL is but on how to use GraphQL API requests within Loadmill.
## Notes
- The requests in this flow are sent to a free GraphQL API providing information about SpaceX (an arbitrary example out of these [8 free GraphQL APIs](https://www.apollographql.com/blog/)8-free-to-use-graphql-apis-for-your-projects-and-demos)
- In order to send a GraphQL request over HTTP, json-body structure should look like this:
```json
{
    "query": " string of the query ",
    "variables": { json of the variables }
}
```
- The "string of the query" should be in one line. e.g.

The query:
```graphql
query ExampleQuery {
  rockets {
    active
    country
    company
  }
}
```
The query inside the request's json-body:
```json
{
    "query": "query ExampleQuery { rockets { active country company } }",
}
```