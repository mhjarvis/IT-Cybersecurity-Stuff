# Terms

## Web

- `Load Balancers` - give high traffic websites the ability to handle large amounts of traffic and provide a failover if a server becomes unresponsive.

  - Can use different algorithms such as `round-robin` (sends requests to each server in turn) or `weighted` (checks how many requests a server is currently dealing with).
  - Load Balancers will perform `health checks` to ensure a server is running correctly.

- `CDN (Content Delivery Networks)` - allows for the hosting of static files to a website across numerous servers and sends requests to whatever server is closest to the requestor.

- `WAF (Web Application Firewall)` - sits between web request and web server; will stop common attack techniques and can drop potential requests.

## Web Servers

Web servers listen for incoming connections. Common ones being:

- `Nginx` and `Apache (Linux-based)` - serve files from `/var/www/html/`.
- `IIS (Windows-based)` - serve files from `C:\inetpub\wwwroot\`.

- `Virtual Hosts` - allows web servers to host multiple websites by checking the hostname being requested from the HTTP header and matches it against a virtual host (e.g. /var/www/website_one, /var/www/website_two, etc.).

- `Static Content` - content that never changes (e.g. pictures, js, css, etc.).
- `Dynamic Conent` - content that can change with requests (e.g. blogs).
