[[Index_bandit]]

Immediately after starting the system a file called *bash.rc* starts
rc is runcommand. its the basic things our terminal does once we start

# Lvl 18 
our bash.rc was rigged against us. it logs us out immediately. after we log in 

so we bypass it during ssh 
	`ssh -pssh bandit18@bandit.labs.overthewire.org -p 2220 "bash --norc --noprofile"`
	here we log in with no runcommnd and no profile 
then we get a *readme* file and we got our pass for lvl19

# Lvl 19 Privilege upgrade
here a file called *bandit20-do*
it is a file with setuid privileges due to which it operates as bandt20
	here we can use `ls -l bandit20-do`
		`-rwsr-xr-x` lowercase s means it has setuid enabled and execute privileges
		`-rwSr-xr-x` uppercase S means it has setuid enabled but does not have execute privileges 
	now all we need to do is 
	`bandit20-do cd /etc/bandit_pass`
	`cat bandit20` and get the passwrod of bandit20


