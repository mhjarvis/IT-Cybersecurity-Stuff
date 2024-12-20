<h1 style="text-align:center">Authentication Bypass</h1>

Website authentication can be bypassed, defeated, or broken.

## Username Enumeration

Username enumeration can be used with signup pages. For example, you can enter a username (e.g. `admin`) and attempt a signup. This will invariably tell you that the username is in use. This error message can be used to produce a list of valid usernames.

The `ffuf` tool uses a list of commonly used usernames to check for matches.

https://github.com/ffuf/ffuf

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

## Logic Flaws

Authetication can contain logic flaws. This is when the logical path of authentication is bypassed somehow.

```php
if( url.substr(0,6) === '/admin') {     // can use aDmin to bypass check
    # Code to check user is an admin
} else {
    # View Page
}
```

## Cookie Tampering

Request the target page:

`user@tryhackme$ curl http://10.10.26.219/cookie-test`

Set logged_in cookie set to `true` and admin set to `false`:

`user@tryhackme$ curl -H "Cookie: logged_in=true; admin=false" http://10.10.26.219/cookie-test`

Set logged_in and admin to `true`:

`curl -H "Cookie: logged_in=true; admin=true" http://10.10.26.219/cookie-test`

Cookies can come in the form of hashes.

https://crackstation.net/ - used to check for hashes.
