


A protocol for sending emails in an IP network.

May combined with the IMAP or POP3 protocols which can fetch emails and send emails.
It use client-server-based protocol. =={Can also be used between 2 SMTP serves}{In this case, a server effectively acts as a client.==}

==***Default port to accept requests on port 25 {also uses TCP port 587}***==
for encrypted connection SMTP may use other ports like 467.
### STARTTLS Encryption:
	- Begins with plaintext Connection.
	- Uses STARTTLS command to switch to encrypted communications
	- Protects authentication credential(username/password) from being exposed.
	
## For prevention of Spam
	TO prevent spamming in the smtp server. it Uses the authenticstion mechanisms that allow only authorized users to send emails.
	So mordern SMTP server uses protocol extension like ESMTP with SMTP-Auth.

## SMTP agents
		1.MUA: Mail User Agent | Client 
		2. MSA: Mail Submission Agent | submission Agent
		3. MTA: Mail Tansfer Agent | Open Relay
		4. MDA: Mail Delivery Agent | Delivery Agent
		
==MUA->MSA->MTA->MDA->POP3/IMAP==
## Default Configuration

	1. AUTH PLAIN | Service extension used to authenticate the client
	2. HELO | clients logs in its computer name and thus starts the session.
	3. MAIL FROM | client names the email sender
	4. RCPT TO | Client name the email recipient.
	5. DATA | clients initiates the transmission of the email.
	6. RSET | abort the transmission but keeps the connection between client and server.
	7. VRFY | clients checks if a mailbox is available for transfer.
	8. EXPN | checks the mailbox is available for messaging with this command.
	9. NOOP | requests a response from the server to prevent disconnection due to time-out.
	10. QUIT | clients terminates the session.

## Dangerous Settings

To avoid emails being marked as spam, senders often use **trusted SMTP relay servers**, which usually require **authentication**. However, due to poor configuration or lack of IP control, administrators sometimes allow **all IPs** to access the SMTP server. This misconfiguration is common and can expose the server to abuse, especially during **external or internal penetration tests**.
#### Open relay Configuration:
	mynetwork = 0.0.0.0/0
	
	With this setting, this SMTP server can send fake emails and thus initialize communication between multiple parties. Another attack possibility would be to spoof the email and read it.

## Footprinting the Service 

Default Nmap scripts include smtp-commands , which uses the EHLO command to list all possible commands that can be executed on the target SMTP server.

	I. nmap <target> -sC -sV -p25
	II. nmap <target> -p25 --script smtp-open-relay -v
	
	{we can uses the smtp-open-relay NSE scripts to identify the target server as an open relay using 16 diff tests. Also prints the output in details} 

## Ennumeration on the SMTP:

TOOLS that is used for ennumerate the username in the server is {smtp-user-enum}

	smtp-user-enum -M VRFY -U /home/spider/Downloads/footprinting-		wordlist.txt -t <target> -p 25 -w <time in seconds>


[[Footprinting important commands]]
[[Nmap Basics]]
