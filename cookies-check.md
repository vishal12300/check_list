
# Cookie 

Identify the required session cookie by removing them one by one. Send a request (that includes user data in the response) to the Repeater, remove each cookie individually, and observe which one breaks authentication. Also review and clean up unnecessary headers.

Once you identify the session cookie, use Burp's search feature to find where it was first assigned. Search for the cookie value across requests to locate its origin. 
Then, send that request to Repeater and verify whether the session cookie value remains the same. Next, analyze the GET/POST parameters or request headers to determine which input is responsible for generating the session cookie.
