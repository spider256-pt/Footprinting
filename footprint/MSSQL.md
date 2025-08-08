1. MSSQL is Microsoft' s SQL-Based relational database management system.
2. Unlike MySQL, MSSQL is closed source and was initially written to run on windows OS.
3. Popular for among database administrators and developer when building applications that run on Microsoft's .NET framework{due to strong support for .NET}
USEs Port ==***1433***==
## MSSQL Clients
1. SQL Server Manager Studio(SSMS) comes pre-install with MSSQL package.
2. Can be installed separately.
3. Commonly installed on the server for initial configuration.
4. Also used for managing database by admins.
5. SSMS is a client side application.
6.  Could come across a vulnerable system with SSMS with saved credentials that allow us to connect to the database.
#### To find if and where the client is located on host:
	Command:
			locate mssqlclient(returns the path is mssql existed)
	
## MSSQL Database
1. Have default system databases that help us to understand the structure of all databases. That may be hosted on a target server.
		
	Default System Database:
	1. master | Tracks all system information for an SQL server instance.
	2. model | Template DB that acts as a structure for every new DB.
	3. msdb | SQL server agents uses this DB to schedule jobs & alerts.
	4. tempdb | stores temporary objects
	5. resource | Read-only database containing system objects included with SQL server
## Default Configuration:

#### MSSQL Default Configuration (Summary)
- **Service Account:** Runs as `NT SERVICE\MSSQLSERVER`
- **Authentication:** Defaults to **Windows Authentication**
- **Encryption:** **Not enforced** by default
- **Auth Source:** Uses **Local SAM** or **Active Directory**
- **Risk:** Compromised AD accounts can lead to **privilege escalation** and **lateral movement**
## Dangerous Settings

- MSSQL clients not using encryption to connect the MSSQL server.
- The use of self-signed cert when encryption is being used.  It is possible to spoof self-signed certificates.
- The use of named pipes.
- Weak & default `sa` credentials.

## Footprinting the Service:

	1. NMAP MSSQL Script Scan:

		nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 <target>


	2. MSSQL Ping in Metasploit:

		use scanner/mssql/mssql_ping
		set RHOSTS <target>
		run
		
	3. Connecting with Mssqlclient.py
			Only works when credential are already guessed.
			Connects to MSSQL remotely.
			
		python3 mssqlclient.py Administrator@10.129.201.248 -windows-auth
