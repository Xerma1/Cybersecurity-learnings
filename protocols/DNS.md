# Domain Name System (DNS) protocol
Translates human-readable website names (like academy.networkchuck.com) into an IP address that web browsers use to connect to the website. It is a vital system that, if broken, causes the internet to stop functioning. The domain name to IP address mapping is stored in a DNS server. 

# The DNS Query Process (www.academy.networkchuck.com)
- Stub Resolver: Your computer checks its local DNS cache for the IP address.
- Recursive DNS Server: If not found locally, the request goes to a public recursive DNS server (like Google's `8.8.8.8`).
- Root Servers: The recursive DNS server queries the "Mafia Bosses" of the internet, which are the root servers. There are 13 of them. The root server will direct the request to a TLD server that is in charge of `.com`
- TLD Servers:  Direct the query to the specific server authoritative for the second-level domain under the `.com` domain (e.g., networkchuck.com).
- Authoritative Server: Holds the Zone file and returns the final IP address.

# DNS Security 
The Risk: Default DNS queries use UDP Port 53, which is plain text and vulnerable to sniffing and DNS spoofing. <br>

The Solution: DNS over HTTPS (DoH) encrypts DNS traffic, making it look like regular website traffic. 

# Types of DNS Records
- A Records: Map domain names to IPv4 addresses.
- AAAA Records: Map domain names to IPv6 addresses.
- NS Records: Identify the authoritative Name Servers for a domain.
- MX Records: Identify the Mail Exchanger servers responsible for handling email for a domain.
- PTR Records: Used for reverse DNS to map an IP address back to a domain name.
- CNAME Records: Canonical Name records, which act as an alias to point one domain to another (e.g., www.networkchuck.com points to networkchuck.com).
- TXT Records: Text records used for metadata, specifically for security protocols like SPF, DKIM, and DMARC to verify email legitimacy.
