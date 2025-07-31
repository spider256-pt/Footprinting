## MySQL

	1. Is an open-source SQL relational database management system
	2. The Database system can quickly process large amount of data with high performance 
	3. Data storage is done in a manner to take up as little space as possible.
	4. Controlled using SQL database language
	5. Works according to client-server principle.
	6. Consists of a MySQL server and one or more MySQL clients
	7. Data is stored in tables with different columns, rows and data types. extension (.sql)
==1. ***Runs on TCP port 3306==***
#### MySQL Clients:
	1. Clients can retrive and edit data using structured queries. 
	2. inserting, deleting, modifying and retriving data is done using the SQL language.
	3. Sql is suitable for managing different database.
	4. Depending on the use of Database, access is possible via an internal network or the public internet.

#### MySQL Databases:
	1. MySQL is ideally suited for application such as dynamic websites.
	2. Efficient syntax and high response speed are essential.
	3. Often combined with {Linux, Apache, MySQL, PHP} LAMP  when used with NGINX it is termed as LEMP.
	4. In a web-hosting with MySQL database with PHP scripts some content is stored they are:
		a. Headers
		b. Texts
		c. Meta Tags
		d. Forms
		e. Customers
		f. Usernames
		g. Administartors
		h. Moderators
		i. Email addresses
		j. user information
		k. Permissions
		l. Passwords
		m. External/Internal links
		n. Links to Files
		o. specific contents
		p. Values

## Dangerous Settings 

	1. user | Sets which user the MySQL servive will run as 

	2. password | Sets the password for the MySQl user
	
	3. admin_address | This sets the IP address to listen for admin TCP/IP network connections.
	
	4. debug | This variable indicates the current debugging settings
	
	5. sql_warnings | This setting shows a message if a one-row insert has a warning.
	
	6. secure_file_priv | This variable is used to limit effect of data import and export operations.

==***The setting user, password and admin_address are security relevant because the entries are made in plain text.==*** 

## Footprinting the Service

#### Scanning MySQL Server:

	1. Nmap:
		
		a. sudo nmap <target> -sV -sC -p3306 --script mysql*
		
			might return false-positve output. {so check mannually}.
#### MySQL Commands 
	1. Interaction with the MySQL Server:
		
		a. mysql -u <user> -h <address> {no pass}
		b. mysql -u <user> -p<password> -h <target>
		c. show database;
		d. use database;
		e. show tables;
		f. show columns from <tables>;
		g. select * from <table>;
		h. select * from <table> where <column> = "<string>";
***==More commands can be use from SQL database Language==***
