# What is Content Discovery (Web application)?

Its about discovery of a file, video, picture. backup, website feature that isn't immediately obvious on the website.<br>

Things like pages or portals that are intended only for the staff or administration.

## 3 ways of content discovery: *Manually*, *Automated*, *OSINT*

# MANUALLY
* [Robots.txt](#robotstxt)
* [Sitemap.xml](#sitemapxml)
* [Favicon](#favicon)
* [Framework stack](#framework-stack)
* [HTTP Headers](#http-headers)

<a name="robotstxt"></a>
## Robots.txt
Robots.txt is a document that clearly lists the pages that are allowed or not allowed to show by search engines, or even completely ban search engines from showing the website altogether.<br>
These pages can be administration portals or files meant for website owners.<br>

This is a great piece of information, because it holds information about the locations of the website the owners don't want people to be peeking into.<br>

To access this document, simply tag the end of the url with the file `/robots.txt`.

<a name="sitemapxml"></a>
## Sitemap.xml
Similar to `robots.txt`, but the `sitemap.xml` gives a list of EVERY file the website owner wishes to be listed on a search engine.<br>

This allows us to discover old webpages or areas of the website that are a bit obscure, but works behind the scenes.<br>

You can access the file by tagging the url with the file `/sitemap.xml`.

<a name="favicon"></a>
## Favicon
Favicons are a small icon that is display in the browser's address tab to brand a website.

<img width="996" height="65" alt="image" src="https://github.com/user-attachments/assets/3c905286-cd20-4dd3-9956-301ae65640d4" />

Sometimes when frameworks are used to build a website, the favicon that is part of the installation isn't changed by the website creator. This gives us a clue as to what framework was used.<br>

With this information, pentesters can acquire the md5 hash value of the favicon icon and do a lookup on the https://wiki.owasp.org/index.php/OWASP_favicon_database. After knowing the exact framework that was used to build the website, pentesters can look to find any vulnerabilities within the framework that can be exploited.<br>

<a name="framework-stack"></a>
## Framework Stack
Upon establishing the framework of a stack, either via Favicon or via comments, copyright notices or credits in the page source, we can locate the framework's website.<br>

Learning about the software and other information could possibly reveal a vulnerability that we can exploit.

<img width="1152" height="290" alt="image" src="https://github.com/user-attachments/assets/6bff7811-27c0-4a1c-b589-0663bcfbb090" />

<img width="1232" height="561" alt="image" src="https://github.com/user-attachments/assets/eb3a1fc4-6873-466b-b880-79b3a77c1b9c" />

<a name="http-headers"></a>
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
* [Google Hacking/Dorking](#google-hacking-dorking)
* [Wappalyzer](#wappalyzer)
* [Wayback Machine](#wayback-machine)
* [GitHub](#github)
* [S3 Buckets](#s3-buckets)

<a name="google-hacking-dorking"></a>
## Google Hacking/Dorking
A hacker technique that performs a normal Google Search but with filter words to locate specific websites or information that are evidence of vulnerabilities, like specific versions of vulnerable Web applications.

<img width="969" height="576" alt="image" src="https://github.com/user-attachments/assets/7af9d9df-8388-4d9d-945e-2505f4eeb513" />


<a name="wappalyzer"></a>
## Wappalyzer
Wappalyzer (https://www.wappalyzer.com/) is an online tool and browser extension that helps identify what technologies a website uses, such as frameworks, Content Management Systems (CMS), payment processors and much more, and it can even find version numbers as well.

<a name="wayback-machine"></a>
## Wayback Machine
The Wayback Machine (https://archive.org/web/) is an archive storing the websites that date all the way back in the 90s. You can search a domain name, and it will show you all the times the service scraped the web page and saved the contents. This service can help uncover old pages that may still be active on the current website.


<a name="github"></a>
## Github
A hosted version of Git on the internet. It is a version control system, which allows team members to work on a project easier. Use GitHub to search for company names or website names and you may uncover the source code or some information that was not available before.

<a name="s3-buckets"></a>
## S3 Buckets
S3 Buckets is a storage service hosted by Amazon Web Services (AWS) that allows users to store files or static web content in the cloud, accessible over HTTP or HTTPS. Users can set it as private, public or even writable. The s3 bucket looks like this format ` http(s)://{name}.s3.amazonaws.com`. S3 buckets can be discovered in many ways, such as finding the URLs in the website's page source, GitHub repositories, or even automating the process. One common automation method is by using the company name followed by common terms such as {name}-assets, {name}-www, {name}-public, {name}-private, etc.

# Automated Discovery
Using automation tools like dirb and Gobuster to go through a wordlist containing a list of common names for files and directories to find hidden file and directories of a website. Basically bruteforcing. 
