IMAP stands for Internet Message Access Protocol.
POP3 stands for Post Office Protocol. 
Both the protocols are used for Email services.
***Client establish the connection on port 143(Plaintext) alternative port 993 For IMAP***
***Client establish the connection on port 110(Plaintext)alternative port 995 for POP3***

## IMAP 
	1. Imap allows online management of emails directly on the server supportd folder structure. {Onl used for online management of emails on a remote server.}
	2. Client-server based.
	3. Allows Scynchronizarion of local email client with the mail box on the server.
	4. Can create folders and folder structure in the mail-box.
	5. Unencrypted and trtansmits commands, emails or username and passwords in plain text.
## POP3 
	 1. POP3 onl provides Listing, retriving and deleting emails as function at email servers.
	 
	a. Clients access these structures online and can create local copies.
		even for several clients, this results in uniform database. 

	b. The client establish the connection to the server via port 143.
	c. For communication it uses text-based commands in ASCII format.
	d. The autentication done by using username & passwords.

## Default Configuration
	The default configuration are set in dovecot-imapd and dovecot-pp3d using apt.

## IMAP Commands

	1. 1 LOGIN username password | User's login
	2. 1 LIST "" "*" | List all directories
	3. 1 CREATE "Inbox" | Creats a mailbox with a specified name
	4. 1 DELETE "Inbox" | Deletes a mailbox
	5. 1 RENAME "ToRead" "Important" | Renames a mailbox
	6. 1 LSUB "" * | returns a subset name from the set of names that user has declared as beign active ir subscribed.
	7. 1 SELECT INBOX |  select a mailbox so that message in the mailbox can be accessed 
	8. 1 UNSELECT INBOX | Exits the selected mailbox
	9. 1 FETCH <ID> all | retrives data associated with a message in the mailbox 
	10. 1 CLOSE | Removes all message with the Deleted flag set
	11. 1 LOGOUT | Closes the connection with the IMAP server.


## POP3 Commands

	1. USER username | Identifies the user 
	2. PASS password | Authentication of the user using password
	3. STAT | Request the saved emails from the server
	4. LIST | Request the number and size of all emails from server.
	5. RETR id | Request the server to deliver the requested email by ID
	6. DELE id | Request theb server to delete the requested email by ID
	7. CAPA | Request the server to display the server capabilities
	8. RSET | Request the server to reset the transmitted inforamtion
	9. QUIT | closes the connection with the POP3 server

## Dangerous Settings

	1. auth_debug | enables all authentication debug logging
	2. auth_debug_passwords | This setting adjusts log vebosity, the submitted passwords, and the scheme gets logged.  
	3. auth_verbose | Logs unsuccessful authentication attempts and their reason
	4. auth_verbose_passwords | Password used for authentication are logged and can be truncated 
	5. auth_anonymous_username | This specifies the username to be used when logging in with the ANONYMOUS SASL mechanism  
	
## Footprinting Service

==By default  ports 110 and 995 are used by POP3==
==Ports 143 and 993 are used by IMAP==

high ports(993 and 995) use TLS/SSL to encrypt the communication between client and sever. 

#### service
	
	1. Nmap 
		nmap 10.129.14.128 -sV -p110,143,993,995 -sC
	
	2. cURL
		curl -k 'imaps://<target>' --user user:p4ssw0rd

## OpenSSL - TLS Encrypted Interaction IMAP/POP3 
	1. To interact with the IMAP or POP3 server over SSL, we can use `openssl`, as well as `ncat`:
	I. For POP3:
		openssl s_client -connect <target>:pop3s
	II. For IMAP:
		openssl s_client -connect <target>:imaps
## Signing in the server:
	Use telnet to sign in the server using the taget address and the port number 

 	1. telnet <address> <port>

[[Nmap Basics]]
[[Footprinting important commands]]
