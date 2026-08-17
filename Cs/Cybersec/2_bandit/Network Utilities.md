[[Index_bandit]]
[[Linux privilege escalation 1]]
[[Networks]]
# Lvl 14: Nc
Learning about nc protocol 
	`nc localhost 30000`
we get the password as return 
	here we open a connection between our machine(bandit14) and other. 
	we send over the current password and it verifies it and sends back the password of bandit15

# Lvl 15 : ncat 
ncat is the more secure and updated version of nc
here we used --ssl to secure our connection and encrypt our data as we send it over the port 
	`ncat --ssl 30001`
after thi we get our password for level16

# Lvl20

