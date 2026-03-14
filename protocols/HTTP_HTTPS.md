# Hypertext Transfer Protocol
Used whenever you visit a website. A set of rules for transmitting of webpage data, like HTML, Images, Videos, etc.<br>

# Hypertext Transfer Protocol Secure
A secure version of HTTP, where HTTP data is encrypted such that no one can see the data that you are sending and receiving, and also gives assurance that the web server you are talking to is legit and not someone impersonating it. <br>

# Uniform Resource Locator (URL)
An instruction on how to access a resource on the internet.<br>

<img width="960" height="258" alt="image" src="https://github.com/user-attachments/assets/e1463b6b-72d1-43c6-9d3e-2943b736edd3" />

Query String: Extra bits of information that can be sent to the requested path. For example, /blog?id=1 would tell the blog path that you wish to receive the blog article with the id of 1.<br>

Fragment: This is a reference to a location on the actual page requested. This is commonly used for pages with long content and can have a certain part of the page directly linked to it, so it is viewable to the user as soon as they access the page.<br>

## Making a request
You can make a request to a web server with just one line: `GET /HTTP/1.1`. However, for better web experience, we need to send headers too, which are extra information to give the web server you are communicating with.<br>
```
GET / HTTP/1.1

Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```
Line 1 is showing that the request is sending the GET method, requesting for the home page (/) and telling the web server that we are using HTTP version 1.1.<br>

Line 2 tells the web server that we are trying to access the website "tryhackme.com" <br>

Line 3 tells the web server that we are using Firefox version 87 <br>

Line 4 tells the web server that "https://tryhackme.com/" referred us to this one <br>

Line 5 is empty to show that the request has finished.<br>

### The response
```
HTTP/1.1 200 OK

Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98


<html>
  <head>
      <title>TryHackMe</title>
  </head>
  <body>
      Welcome To TryHackMe.com
  </body>
</html>
```

Line 1 shows that the web server is using HTTP version 1.1, followed by status code 200 OK, which means successful retrieval.<br>

Line 2 shows the web server software and the version number<br>

Line 3 shows the client what kind of content is going to be sent, in this case, text/html<br>

Line 4 shows the length of the response, where we can confirm no data is missing<br>

Line 5 is empty to show end of response, followed by the web page that we requested in HTML<br>

# HTTP methods
### GET
For getting information out of the web server

### POST
For submitting data to the web server and maybe create new records (Like creating an account)

### PUT
Used for submitting data for updating purposes.

### DELETE
Used for deleting information/records from the web server

# HTTP Status Codes
<img width="960" height="754" alt="image" src="https://github.com/user-attachments/assets/3f8427cf-d3cd-40e7-8a82-12c2fec41110" /> <br>

[http.cat](https://http.cat/) resource is a great place to study status codes

# Cookies
<img width="950" height="951" alt="image" src="https://github.com/user-attachments/assets/1c14779d-3b87-4ebe-9d65-26d8fef81f6a" /> <br>

Commonly used for website authentication. The cookie value is not a plain text, but a token.
