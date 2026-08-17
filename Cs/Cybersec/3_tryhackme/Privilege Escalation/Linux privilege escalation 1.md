# OS Enumeration:
1. `Hostname`: Returns the name of the host this might give a slight idea what is machine is used for 
2. `uname -a`: will give information about the kernal used by the host
3. `/proc/version`: information about the kernal version and compilers used
4. `/etc/issue`: also about kernal
5. `ps`: process status to see what process is running and by what user
	`ps aux`: a-> All user, u-> user that launched the process, x-> non terminal only
6. `Cron`: Time based job scheduler
	`/etc/crontab`: list contents of `/var/spool/cron` or `/etc/cron.d` jobs and who is running them
	![[Screenshot 2026-07-21 at 1.51.22 AM.png]]
7. `Dpkg`: To know all the installed packages and the use of an exploit in them
	`Dpkg -l` -> lists all installed softwares

# User Enumeration:
About obtaining info on local users using different commands
1. `Id`: Obtain general information of the user
2. `Env`: shows envoirnmental variables, 
	Here path variable may have a compiler or a scripting language to run a code and get elevated privileges
3. `History`: might show old run commands, usfult ot scope
4. `sudo -l`: shows lists of commands your user can run as sudo, thne later used to get elevated privilages
5. `/etc/passwd`: easily find users on the system
	output can be filtered using `cut`
	real users will have a /home directory

# Network Enumeration 
[[Networks]] also read
[[Network Utilities]] also read
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

# File Enumeration 
`2>/dev/null` sends all error messages to void
using `ls -la` we find any simple hidden files in directories 
1. `find`: using find command.       read perm's manual 
	1. `find / -perm -a=x` find executable files in the system
	2. `find / -atime -10` find files that were acessed in last 10 minutes
	3. `find / -type f -perm 0777` find files who have 777 perm i.e read and write by all users
	4. `find / -writable -type d` & `find / -perm -o 2 -type d` : to find directories with world write orders
	5. `find / -perm -o x -type d` finds world executable directories 
	6. `find / -name pass*.txt` this will search for files with name CONTAINING "pass" 
	7. `find / -perm -u=s -type f` find files with SUID bit that is set uid, which makes a file run with sudo perm

## Non exact search of files
`find / -name pass*.txt` this will search for files with name CONTAINING "pass"

## Finding files with SUID bit
`find / -perm -u=s -type f` find files with SUID bit that is set uid, which makes a file run with sudo perm