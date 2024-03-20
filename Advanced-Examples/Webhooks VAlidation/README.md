# How to validate webhooks with Loadmill
When testing a system that sends webhooks and triggers other systems, we aim to avoid actual triggering but still want to verify the request sent as the webhook and its validity.
## Notes
A webhook is essentially a regular HTTP request; therefore, Loadmill's webhook service is a regular HTTP server that stores the requests it receives, without triggering any other system as a webhook was intended to do.
### First two requests
The first request demonstrates how to send a webhook request to Loadmill's webhook service. The only important thing here is the host (in this case `https://wh.loadmill.com/${UUID}`); all other details should fit the webhook's structure. For example:

The tested system usually sends a webhook to service Y (which we don't test) after you press a combination of buttons.

The webhook request should be an `HTTP POST` request to `https://service-y.com/api/hooks/trigger-x`. In order to test that without actually triggering service Y, and to check the webhook's validity, we should only replace service Y's address with Loadmill's webhook service address, and all the rest should be the same as it should be in the original webhook, i.e., an `HTTP POST` request to `https://wh.loadmill.com/${UUID}/api/hooks/trigger-x`.


In the second request, the flow queries Loadmill's webhook service, and the latest captured webhook is returned. The distinction between sending a webhook to the service and querying it to retrieve previously sent ones lies in the addition of `requests` before the UUID. That is, the URL format changes to `https://wh.loadmill.com/requests/${UUID}`.

### Requests 3 - 8
Querying a webhook from the service can also include filters to specify the desired webhook. For instance, if multiple webhooks were sent to the service, each with a different value for the header "unique_id," we can easily locate a specific webhook by applying the header filter to the request. This would look like `https://wh.loadmill.com/requests/${UUID}?headers.unique_id=<ID>`.
