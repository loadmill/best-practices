# How to Test Databases with Loadmill?
### This example shows how to interact with Loadmill's db-relay service in order to test your DB
A flow in Loadmill is made out of HTTP/WebSocket requests. Usually databases don't support these protocols, but they use their own query protocol/language.
> Good to know - Why do databases not use HTTP? In databases, data integrity is critical, and any loss or corruption of data can have severe consequences. HTTP, is a stateless protocol designed for web communication and does not inherently provide the same level of reliability and ordering as TCP.

Loadmill tests are based on API calls. It avoids direct interaction with the underlying databases due to the stateful nature of database protocols, which differ from the typical request-response paradigm observed in API testing.

Therefore, in order to test data in a database within a test flow in Loadmill, it should be possible to query the DB over a supported API protocol such as HTTP. Meet **Loadmill db-relay-service**:
- Serves various databases querying over HTTP
- Accessible in Docker for local run or under the domain `https://db-relay-service.loadmill.com/api/`.

In this example, we have a Postgres DB running on AWS, and we access it within the db-relay-service, adding the SQL query inside the request body. The value `book_id` is extracted from the response as it is one of the keys returned from the query. 

More information and API reference is available in [github](https://github.com/loadmill/loadmill-db-relay-service/blob/master/README.md), and in [Loadmill's documentation](https://docs.loadmill.com/integrations/database-testing)