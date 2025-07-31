#SNMP 
	1. Created to monitor network devices.
	2. This protocol can also be used to handle configuration tasks and change settings remotely.
	3. SNMP-enabled hardware includes routers, switches, servers IoT devices and many other devices. 
***==SNMPv3 increases the security of SNMP==***
	4. SNMP also transmit control commands using agents over ==UDP port 161==
	5. SNMP  also enables the use of so-called==trap over UDP port 162.==
## MIB {Management Information Base}
	1. It ensures that SNMP works across manufacturers and with diff client-server combinations.
	2. An independent format of storing device information.
	3. MIB is a text file in which all queryable SNMP objects of a device are listed in standard hierarchy tree 
	4. It contains atleast one OID{Object identifier}

## OID{Object Identifier}
	1. A node in a hierarchical namespace.
	2. Longer the chain more specific the information
		e.g. .1.3.6.1.2.1.1.3.0 
	3. Many nodes doesnt conatian anything except the refernces to those below them.

## SNMP Versions
### SNMPv1
	1. Purpose: basic network monitoring and mangement
	2. Security
		a. No Authentication
		b. No Encryption -- all data sent in plain text
	3. Still used in small and simple networks
### SNMPv2c
	1. Imporvements: Performance and additional features
	2. Security:
		a. Community-based access, but still plain text
		b. no real improvement over SNMPv1 in terms of security

### SNMPv3
	1. Major Improvements:
		1. Authentication(username/password)
		2. Encryption(data confidentiallity)
	2. Security:
		a. Strongest among all version
	3. Drawback: More complex configuration
#### SNMPv3 Security levels:
	a. NoauthNopriv: userbased access on the sever without encryption and authorizarion
	b. authNopriv: authorized but no encryption over the server.
	c. authprive: authorized with encrypytion over the server
## Community Strings
	Community Strings can be seen as password that are used to determine whether the requested informationn can be viewed or not.
#### Drawback:
		1. Organization widely use SNMPv2 and SNMPv3
		 as v3 is more complex so v2 is used widly but its not encrypted which can leads to interception over the network.

## Dangerous Settings 
#### Commands of SNMP:

	1. rwuser noauth | Provides access to the full OID tree without authentication.
	
	2. rwcommunity <community string> <ipv4 target> | Provides access to the full OID tree regardless  of where the requests were sent from.	
	
	3. rwcommunity <community string> <ipv6 target> | same access as with rwcommunity with the difference of using IPv6.

## Footprinting the SNMP Service
#### Tools used:
	1. snmpwalk | used to query the OIDs with their informations

		*snmpwalk -v2c -c public <target>
	
	2. onesixtyone | used to brute-force the name of the community strings{password}

		
		onesixtyone -c <path>/seclists/Discovery/SNMP/snmp.txt <target>
		 

	3. braa | used to brute-force individual OIDs and enumerate the information behind them.

		can be used after knowing the community string.

		braa <community-string>@<target>:<Oid range>