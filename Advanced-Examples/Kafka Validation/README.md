# Kafka Testing with Loadmill
To get more familiar with the idea behind testing Kafka in Loadmill, please refer to the [Kafka Testing documentation](https://docs.loadmill.com/integrations/kafka-testing).

## IMPORTANT REQUIREMENTS TO RUN THIS SPECIFIC FLOW
- The test uses a locally-running container with the loadmill-kafka-relay service. That is why the `url` field is `localhost:3000`. The command executed before the test **on the same machine** is `docker run -p 3000:3000 loadmill/kafka-relay`.
- Since the kafka-relay runs locally, the loadmill-agent should also be local since it should send the requests to the local kafka-relay container. (Check out [how to setup a private loadmill agent](https://docs.loadmill.com/integrations/testing-localhost-application))

## Notes about this example
- The Kafka service that is used here is [Upstash](https://upstash.com). It acts kind of like a Kafka-db server. It stores the produced messages, and does nothing but keeping them.
- The kafka service on Upstash is already pre-configured and contains the topic 'first-topic'
## About the requests
- Second request - produce. The produce request sends a message where the value contains the test execution timestamp! It was added in order to filter the message later when consuming it.
- Third request - consume. The consume request can take a regex filter as an url param (`filter=.*${test_timestamp}.*` -> thus, every message whose value contains the variable `test_timestamp`).
- The response once found, is returned inside a JSON response, so its extracted using JSONPath.
- To verify that the correct response was returned, an assertion is also made at the end, that verifies the existence of the `test_timestamp` inside the response value.