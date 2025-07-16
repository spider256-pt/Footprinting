
Integral Part of the Internet.
Used to resolve computers name into Ip address, and does not have the central database.



![[ChatGPT Image Jul 16, 2025, 01_09_13 PM.png]]
1. There are several types of DNS servers that are used World Wide.

	- ***DNS root server*** | Top-level DNS servers that direct queries to TLDs; managed by ICANN with 13 global instances.
		
	- ***Authoritative name server*** |Holds official records for a DNS zone and provides final answers to queries in its domain
		
	- ***Non-authoritative name server*** | Retrieves DNS info via recursion/iteration but isn't responsible for the zone
		
	- ***Caching server*** |Temporarily stores DNS query results to speed up future lookups.
		
	- ***Forwarding server*** | Sends DNS queries to another DNS server for resolution.
		
	- ***Resolver*** | Local component (in OS/router) that initiates and manages DNS lookups

IT security Professionals apply 
- DOT - DNS over TLS
- DOH - DNS over HTTPS
- DNSCrypt- encrypts the traffic between the computes and the name server.

![[tooldev-dns.webp]]

***DNS records*** are used for the DNS queries

	1. A | Returns an IPv4 add of the requested domain
	2. AAAA | Returns an IPv6 add of the requested domain
	3. Mx | Returns the responsible mail server
	4. NS | Returns the DNS server(nameservers) of the domain
	5. TXT | This record can contain various information
	6. CNAME | This serves as an alias for another domain name
	7. PTR | It converts ip add into valid domain name
	8. SOA | Provides information about the corresponding DNS zone and email add of the administrative contact






[[Nmap Basics]]
[[Footprinting important commands]]