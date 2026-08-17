[[Linux privilege escalation 1]]
[[Network Utilities]]
# Nmap
we use to check open ports and all the services running on them

## Protocols
1. FTP => File Transfer Protocol
2. SSH => Secure Shell
3. HTTP => Web browsering protocol

## FTP:
	ftp machine_ip
	ls
	get file_name
we use *get file_name* to dwonlaod a file using the ftp protocol 

`pwd` : print working directory 

# Network Enumeration 
Learning about network interface and listening ports
1. `If config`: now is simply known as `ip addr`
2. `Netstat`: add t or u for protocol(UDP/TCP)
	1. `netstat -a`: all listening ports and connections
	2. `netstat -l` show ports in listening mode
	3. `netstat -s` usuage statistics by protocol 
	4. `netstat -tp` connections wih service  name and PID information
		`-l` shows listening port and `-n` shows numerica address
		therefore it is `netstat -tpln`
	5. `netstat -i` : `netstat -ano` shows interface statistics 