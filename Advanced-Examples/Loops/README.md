# How to Implement a Loop with Loadmill
The flow demonstrates a workaround for a `for` loop in Loadmill's editor.
## 1st request
### Fetching the countries array + initializing parameters
#### TLDR
- Items of an array must be surrounded by double quotes -> `["foo"]`
- This request sends the array so it'll get it back as a response, but in the actual test we'll replace the request to be the one that actually returns the necessary array.
#### Further explanation
- The items inside the array must have double quotes around them in order to be treated as an array and not String. i.e ["israel"] and not ['israel']
- In this example, we send an array as a `plain/text` content type to a sort of an echo server, that returns our exact input but in a json under the key "data". In the actual test we'll replace the request with a one that really returns the necessary array.
- Inside the extractions we initialize the index (the counter for the loop), and the state (the first country in this example)

## 2nd request
### Requesting in a loop for every array item
#### TLDR
We put an arbitrary large number in the 'max iter.' box so the loop won't run indefinitely no matter what.

#### Further explanation
- Here is a flow explaining what happens there: 
1. The request is sent (In the first request we already have the `state` parameter from the first request's extraction).
2. The index is increased
3. The next state is calculated
4. The 'Flow control' checks whether or not the index reached the list length. And if so, the loop stops.
5. And back to stage 1