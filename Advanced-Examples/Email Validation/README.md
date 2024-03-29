# How to Work with Loadmill's Email Validation Service?
### A guide with a real life example on Slack.
When we perform a signup/login flow we sometimes have to confront with a One Time Password which is sent to the email we use for the test. 

In Loadmill we offer a service hosted in `https://loadmill.com/open-api/emails/{uuid}` which gets every email fitting the next pattern:
> `<STRING>+<UUID>@test.loadmill.com**`
> 
> e.g. `test+dabd64d9-d3dc-4dd1-888c-d536ecb923ae@test.loadmill.com`

The service returns the RAW BODY of the email (sometimes it might be a raw html page for example), there is no analyzation on the body, therefore the OTP extraction should happen within the test flow (check out the example).
### Ok, how to use it in a flow?
Basically, it is possible to open the email service in the browser inside the **same tab** that is used to record the flow.

Thus, ones the OTP was seen, and put back in the app thats waiting, Loadmill's test composer will do it's magic and find the correlations, since it was recording also the email-checking. 

NOTE! quite often the app that is waiting for the OTP requires to stay on it's page, i.e opening a different page in the same tab will stop the recorded procedure. The solution for this is to add it manually in Loadmill's test editor.
### Deleting an email inbox
Sending an `HTTP DELETE` request to Loadmill's email service empties the inbox for the given UUID. This is helpful, for example, at the beginning of a flow, to ensure that the UUID's inbox is empty. Check out the first request (the flow is unlikely to fail the test since the expected HTTP response is ANY. Therefore, if there is something to delete, it will be deleted. Otherwise, nothing will happen.)

### Real life example on Slack - Notes
- The test email is generated every test using Loadmill's function `__random_uuid()`
- It seems like Slacks API returns 200 HTTP status code on every request, and the json body contains the actual status. So it requires a bit more work in order to determine whether or not the request is valid. For that reason, there is an assertion that checks if a certain JSON is returned, and if not, the test fails. (In Slack's case, the json should return:
```json
{
    "ok": true
}
```

Try this yourself!