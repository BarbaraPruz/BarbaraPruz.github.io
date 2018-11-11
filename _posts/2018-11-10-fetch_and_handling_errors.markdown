---
layout: post
title:      "fetch() and handling errors"
date:       2018-11-11 02:14:39 +0000
permalink:  fetch_and_handling_errors
---


With fetch(), how do you handle unexpected problems, like server or authentication errors?  This information is provided through the HTTP status code.  Looking around at sample code, it is often something like  

```
fetch(uri)                              
    .then(response => response.json())
    .then(response =>{
        handleReponse(response); // app code to process reponse payload
    })
    .catch(function(error) {
        console.log(error);
    })   
```

But does this really prevent the app from trying to process a response on an HTTP error?   Is it necessary to check the response ok flag before working with the response? I decided to try some experiments.  I wrote a small test app and you can find it here [https://github.com/BarbaraPruz/fetchit](http://).  See readme for instruction on running. 

To setup a test, use the app UI to

* select an HTTP status code
* specify if the fetch handling should check the response ok flag 
* additional option to see behavior if the route is invalid

The app has a Rails backend and if the route is valid, the controller will generate a simple JSON response (message string describing request) and send it with the specified status code.  The app's fetch response handling has statements tracing its execution and these are shown on the UI.

So what happens?  As expected, for a successful response code (200), the end results are the same – the response is successfully converted to JSON and then handled.   But what about response codes like 400 and 500?   In these cases, there is a difference!  

    ------------------
    Test Start for /api/test/500 with response ok check
    Going to Fetch
    Check HTTP status check
    Response not OK!
    Detected Fetch Error - Error: Internal Server Error
    ------------------
    Test Start for /api/test/500 with no response ok check
    Going to Fetch
    Converted Response to JSON
    Completed Response Processing, Payload: Responding to HTTP Get with status code 500
		
Without the ok flag check, the response is converted to JSON and then handled.  This is no real problem for the test
app because even with the bad status, there is a valid JSON payload.   But for an actual issue, like an HTTP 500, there would be no JSON payload.  The code to process the response will need to check for undefined.  In the app, you can see this by selecting the undefined route option.

    ------------------
    Test Start for /api/invalid/400 with response ok check
    Going to Fetch
    Check HTTP status check
    Response not OK!
    Detected Fetch Error - Error: Not Found
    ------------------
    Test Start for /api/invalid/400 with no response ok check
    Going to Fetch
    Converted Response to JSON
    Completed Response Processing, Payload: undefined

To detect HTTP error status codes in the fetch response handling, it is necessary to check the response ok flag.   Here is an example of some general code that can be used – this code will catch errors for HTTP error codes as well as general network errors (detected by fetch).

```
fetch(uri)    
    .then(res => {
        if (!res.ok) {
            throw Error(res.statusText);
        return res;   
    })                               
    .then(response => response.json())
    .then(response =>{
        handleReponse(response); // app code to process reponse payload
    })
    .catch(function(error) {
        console.log(error);
    })       
```

Heres hoping you have a 200 sort of day!
