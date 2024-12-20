<h1 style="text-align:center">fuff</h1>

`ffuf` (Fuzz Faster U Fool) is a tool primarily used for web fuzzing and brute-forcing.

https://github.com/ffuf/ffuf

## Username Enumeration

```bash
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.26.219/customers/signup -mr "username already exists"
```

The `-w` argument selects the wordlist on the computer. The `-X` argument specifies the request method (a GET request by default), but a POST request in this example. The `-d` argument specifies the data that is being sent. The username is set to `FUZZ`, which is a keyword signifying there the wordlist will enter its requests. The `-H` argument is used for adding additional headers to the request. `Content-Type` is being set so the web server knows we are sending a form. The `-u` argument specifies the URL we are making a request to. The `-mr` argument is the text on the page we are looking for to validate we have found a valid username.

## Brute Force

Using `ffuf` and making sure you are in the same directory as the file of usernames that were found on the target system:

```bash
ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.26.219/customers/login -fc 200
```

In this command we are using multiple wordlists. We are using `W1` for the list of valid usernames stored by us based on what was found during enumeration. And we are using `W2` for the list of passwords we will try (also from a wordlist). Multiple wordlists are specified using the `-w` option, seperated by commas. To determin if we find a positive match, we can use the `-fc` argument to check for a HTTP status code of 200.

## Logic Flaw
