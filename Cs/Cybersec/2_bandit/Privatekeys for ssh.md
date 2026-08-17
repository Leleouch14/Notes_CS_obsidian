[[Index_bandit]]
## Lvl13-14
we can use a privatekey to log via ssh just as we do using normal passwords. 
but for this we need to ensure the private key is in the same directory as the terminal(windows powershell in my case).

1. we need to download the key from the other machine on to my own computer 
	  `scp -P 2220 bandit14@bandit.labs.overthewire.orgs:/home/bandit13/sshkey.private .`
		here `scp` is used to download something from remote server
		we also need to specify where exactly is our file. we can use `realpath` for this
		`.` means that we r downloading the key to exactly where our terminal is already installed 
2. now we need to log into the bandit14 
	`ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`
		here we need to specify `-i key_name` that we are using a private key to log into the user bandit14
		
