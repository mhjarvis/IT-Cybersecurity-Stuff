<h1 style="text-align:center">IDOR</h1>

Insecure Direct Object Reference is a type of access control vulnerability.

A simple example is changing the order number in a url to another one and then seeing another customer's order and information.

## IDORs in Encoded IDs

When data is passed from a webpage by post data, query strings, or cookies, raw data will often be encoded. It changes binary data into ASCII strings. Base64 is the most common encoding. You can use websites to decode a string and then re-encode it, then resubmit the web request to see if there is a change in response.

https://www.base64decode.org/ - decode

https://www.base64encode.org/ - encode

## Hashed IDs

Hashed IDs may follow a predictable pattern, such as being the hashed value of a integer value. Check any discovered hashes at crackstation.net.

## Unpredictable IDs

If the Id cannot be detected using the above methods, an excellent method of IDOR detection is to create two accounts and swap the Id numbers between them. If you can view the other users' content using their Id number while still being logged in with a different account (or not logged in at all), you've found a valid IDOR vulnerability.

## Where are IDORs Located?

The vulnerable endpoint you're targeting may not always be something you see in the address bar. It could be content your browser loads in via an AJAX request or something that you find referenced in a JavaScript file.

Sometimes endpoints could have an unreferenced parameter that may have been of some use during development and got pushed to production. For example, you may notice a call to /user/details displaying your user information (authenticated through your session). But through an attack known as parameter mining, you discover a parameter called user_id that you can use to display other users' information, for example, /user/details?user_id=123.
