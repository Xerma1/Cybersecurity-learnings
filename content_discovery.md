# What is Content Discovery (Web application)?

Its about discovery of a file, video, picture. backup, website feature that isn't immediately obvious on the website.<br>

Things like pages or portals that are intended only for the staff or administration.

## 3 ways of content discovery: *Manually*, *Automated*, *OSINT*

# MANUALLY
* [Robots.txt](robotstxt)
* [Sitemap.xml](sitemapxml)
* Favicon
* Framework stack
* HTTP Headers

## Robots.txt
Robots.txt is a document that clearly lists the pages that are allowed or not allowed to show by search engines, or even completely ban search engines from showing the website altogether.<br>
These pages can be administration portals or files meant for website owners.<br>

This is a great piece of information, because it holds information about the locations of the website the owners don't want people to be peeking into.<br>

To access this document, simply tag the end of the url with the file `/robots.txt`.

## Sitemap.xml
Similar to `robots.txt`, but the `sitemap.xml` gives a list of EVERY file the website owner wishes to be listed on a search engine.<br>

This allows us to discover old webpages or areas of the website that are a bit obscure, but works behind the scenes.<br>

You can access the file by tagging the url with the file `/sitemap.xml`.

## Favicon
Favicons are a small icon that is display in the browser's address tab to brand a website.

<img width="996" height="65" alt="image" src="https://github.com/user-attachments/assets/3c905286-cd20-4dd3-9956-301ae65640d4" />

Sometimes when frameworks are used to build a website, the favicon that is part of the installation isn't changed by the website creator. This gives us a clue as to what framework was used.<br>

With this information, pentesters can acquire the md5 hash value of the favicon icon and do a lookup on the https://wiki.owasp.org/index.php/OWASP_favicon_database. After knowing the exact framework that was used to build the website, pentesters can look to find any vulnerabilities within the framework that can be exploited.<br>

## Framework Stack
Upon establishing the framework of a stack, either via Favicon or via comments, copyright notices or credits in the page source, we can locate the framework's website.<br>

Learning about the software and other information could possibly reveal a vulnerability that we can exploit.

<img width="1152" height="290" alt="image" src="https://github.com/user-attachments/assets/6bff7811-27c0-4a1c-b589-0663bcfbb090" />

<img width="1232" height="561" alt="image" src="https://github.com/user-attachments/assets/eb3a1fc4-6873-466b-b880-79b3a77c1b9c" />


## HTTP Headers
When making requests to the web server, the server returns various HTTP headers. This headers can contain useful information such as the webserver software and the programming/scripting language in use.<br>
```
user@machine$ curl http://10.48.177.32 -v
*   Trying 10.48.177.32:80...
* TCP_NODELAY set
* Connected to 10.48.177.32 (10.48.177.32) port 80 (#0)
> GET / HTTP/1.1
> Host: 10.48.177.32
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Server: nginx/1.18.0 (Ubuntu)
< X-Powered-By: PHP/7.4.3
< Date: Mon, 19 Jul 2021 14:39:09 GMT
< Content-Type: text/html; charset=UTF-8
< Transfer-Encoding: chunked
< Connection: keep-alive
```
In this HTTP header, we can see that the webserver is `nginx.1.18.0` and runs `PHP version 7.4.3`. Using this, we can identify when a webserver is using outdated and vulnerable software for us to exploit.<br>

You can get this header via `curl [URL] -v`

# OSINT
* [Google Hacking/Dorking](#google-hacking/dorking)
* Wappalyzer
* Wayback Machine
* GitHub
* S3 Buckets

## Google Hacking/Dorking

# Automated Discovery
