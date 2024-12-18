# Web Applications

## Robots.txt

The `robots.txt` file is a document that tells search engines which pages they are and are not allowed to show in their results. This can be a intial place to find information on website paths.

## Favicon

The favicon can give clues as to the framework being used if the image is left over from development. You can download and get the md5 has by:

```bash
// Bash
curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum
```

```powershell
// PowerShell
curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico -UseBasicParsing -o favicon.ico

Get-FileHash .\favicon.ico -Algorithm MD5
```

The hash can then be compared to frameworks via: https://wiki.owasp.org/index.php/OWASP_favicon_database

## Sitemap.xml

The `sitemap.xml' file gives a list of every file the website owner wishes to be listed on a search engine. It can list old websites that are still accessable.

## HTTP Headers

Site headers can give additional infomration such as the programming/scripting language used.

```bash
curl http://ip-address -v               // -v is verbose mode
```

## OSINT Websites

https://www.wappalyzer.com/ - can be used to determine technologies used on a website.

https://archive.org/web/ - wayback machine to determine older archives of websites.

github.com

s3 buckets - amazon

## Automated Discovery

Automated discovery uses wordlists to discover directory and filenames. Common wordlists can be found at:

https://github.com/danielmiessler/SecLists

Popular tools to use with wordlists:

ffuf

```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -u http://10.10.182.59/FUZZ
```

dirb

```bash
dirb http://10.10.182.59/ /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```

Gobuster

```bash
gobuster dir --url http://10.10.182.59/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```
