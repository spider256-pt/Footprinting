
Integral Part of the Internet.
Used to resolve computers name into Ip address, and does not have the central database.


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


***DNS records*** are used for the DNS queries

	1. A | Returns an IPv4 add of the requested domain
	2. AAAA | Returns an IPv6 add of the requested domain
	3. Mx | Returns the responsible mail server
	4. NS | Returns the DNS server(nameservers) of the domain
	5. TXT | This record can contain various information
	6. CNAME | This serves as an alias for another domain name
	7. PTR | It converts ip add into valid domain name
	8. SOA | Provides information about the corresponding DNS zone and email add of the administrative contact
	9. CH | It asks the local DNS server for its version using CHAOS class

**==FQDN - hostname + domain + top-level domain + root (.)==**
**==dot(.) is replaced by an at sign (@) in the email add.==** 


## Default Configuration
	All DNS servers work with three different types of configuration Files:
		1. local DNS configuration files
		2. zone files
		3. reverse name resolution files
		
	Bind9 is very often used for Linux-based distribution.
		- named.conf.local
		- named.conf.options
		- named.conf.log
	
	The named.conf is divided into several options that control the behaviour of  the name server.
	  - global options - affect all zones.
	  - zone options - only affect the zone to which it is assigned.
	  - Options not listed in named.conf have defaul values.


==Bind file - Bind file format is the industry-preferred zone file format and is now well establish in DNS server software.== 

There must be precisely one ***SOA***{usually located at the beginning of a zone file.} and at least one ***NS*** record.

## Dangerous Settings
	1. allow-query | Defines which hosts are allowed to send requests to the DNS server
	2. allow-recursion | Defines which hosts are allowed to send recursive requests to the DNS server.
	3. allow-transfer | Defines which hosts are allowed to receieve zone transfer from the DNS server 
	4. zone-statisstics | collects statistical data of zones.

## Footprinting The Service
	DIG - NS Query:
		  dig ns <nameserver> @<target>
	DIG - Version Query:
		 dig CH TXT @<target> version.bind
	DIG - Any Query:
		 dig any <nameserver> @<target>
	Dig - AXFR Zone Transfer {DNS zone transfer on -p 53}
		 dig axfr <nameserver> @<target>
		 dig axfr internal.<nameserver> @<target> {for internal zone transfer}


## SubDomain Brute forcing 
	
	1. for sub in $(cat /opt/useful/seclists/Discovery/DNS/subdomains-top1million-110000.txt);do dig $sub.<nameserver> @<target> | grep -v ';\|SOA' | sed -r '/^\s*$/d' | grep $sub | tee -a subdomains.txt;done

	2. DNSenum:
		 dnsenum --dnsserver <target> --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/seclists/Discovery/DNS/subdomains-top1million-110000.txt <nameserver>


[[Nmap Basics]]
[[Footprinting important commands]]
