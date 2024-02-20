# Notes
### Parameters accessability
> Postscript variables (`var`s, `let`s and `const`s) are indeed accessible from other request in the same flow, although they are not shown under 'user parameters' after the flow is executed.
### Logs & Debugging
> Logs are allowed in postscripts (`console.log()`) - powerful for debugging
### Possible warning
> More particularly - **<param> doesn't have a default value** error.
> If a previously-defined-by-postscript parameter is used **not** in a postscript in the next requests, the above-mentioned error might occur.

> You can either initialize it outside of a postscript and then only modify it in it (unlike creating it in the script) or Ignore it if you know this is the case