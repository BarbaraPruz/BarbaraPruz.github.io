---
layout: post
title:      "fetch() and handling errors"
date:       2018-11-10 21:14:40 -0500
permalink:  fetch_and_handling_errors
---


With fetch(), how do you handle unexpected errors like server or authentication failures?  The error information is provided through the HTTP status code.  

Here is how sample code often handles errors:

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

But does this really prevent the app from trying to process a response with an HTTP error/non-success status code?   Is it necessary to check the response ok flag before working with the response? 

I decided to experiment and wrote a small test app. You can find it here: [github.com/BarbaraPruz/fetchit](https://github.com/BarbaraPruz/fetchit).  

![](https://drive.google.com/uc?id=10u2isxAfaGW8mUsGVgzaYs-o4WxjzFFu)

To setup a test, select an HTTP status code and specify if the fetch handling should check the response ok flag.  An additional option to use an invalid route is also provided.

The app has a Rails backend and if the route is valid, the controller will generate a simple JSON response (message string describing request) and send it with the specified status code.  The app's fetch response handling has statements tracing its execution and these are shown on the UI.

So what happens?  As expected, for a successful response code (200), the end results are perfect – the response is  converted to JSON and then handled.   But what about response codes like 400 and 500?   In these cases, there is a difference with OK checking!

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
app because even with the bad status, there is a valid JSON payload.   But for an actual issue, like an HTTP 500, there is no JSON payload.  The code to process the response will need to check for undefined.  In the app, you can see this by selecting the invalid route option.

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

To detect HTTP error status codes in the fetch response handling, it is necessary to check the response ok flag.   Here is an example of a general implementation – this code catches errors for HTTP error codes as well as network errors (detected by fetch).  If checking for specific status codes, response.status contains the integer value.

```
fetch(uri)    
    .then(response => {
        if (!response.ok) {
            throw Error(response.statusText);
        return response;   
    })                               
    .then(response => response.json())
    .then(response =>{
        handleReponse(response); // app code to process reponse payload
    })
    .catch(function(error) {
        console.log(error);
    })       
```

Hope you have a 200 sort of day!
