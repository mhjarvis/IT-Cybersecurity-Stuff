# <h1 style="text-align:center">Web Requests</h1>

## Introduction
Most internet communications happen through the HTTP protocol on port 80 (443 for HTTPS), though this can be changed to any other port. When a user requests a website (by entering a URL), a request is sent to a DNS server to resolve the domain and get the IP address. All domain names must be resolved this way. 

However, browsers usually look at the local ```/etc/hosts``` file and check if a record of the domain is stored there. The ```/etc/hosts``` file can have records added to it (IP_address:domain_name). 

Once the browser has a IP address, it sends a ```GET``` request to the default HTTP port asking for the root ```/``` path. The web server receives and processes the request. By default, servers are configured to return an index file when ```/``` is requested (index.html). This response from the server also contains a status code (e.g. ```200 OK``` (request was successfully processed)). The web page is then rendered by the browser. 

## ```cURL```
```cURL``` (client URL) is a command-line tool and library that supports HTTP. It allows us to create scripts (and automation) and creating web requests via the CLI. We can send a basic HTTP request to any URL as follows:

    curl inlanefreight.com

This does not render the web page, but instead prints it in raw form. We are mainly interested in the request and response context. We can download a page and save it to a file using:

    curl -O inlanefreight.com/index.html