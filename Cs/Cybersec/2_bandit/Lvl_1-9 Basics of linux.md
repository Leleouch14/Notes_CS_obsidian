# Level 1 -> 4 basics 

[[Index_bandit]]
## lvl1 to open a file with name "-"
	cat ./- 
as - is a special file name in linux 
## lvl2 file named --file--
	cat "./--file--"
## lvl3 change directory 
	cd directory_name
## lvl4 find a text file
in the directory with files we run
	`find . -type f -exec file {} +`
		here -exec -> means execute another command i.e. **file**
		**+** means that run it all at once

---
# level 5 -> 9 search and finds
## lvl5 find a file among multiple sub-directories
we know the file size is 1033 bytes and is non *executable*
	`find . -type f -size 1033c ! -executable`
		c -> means bytes 
## lvl6 find a file across all the directories and sub
		`find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null`
			/ ensures we search across all directories and sub directories
			here we use -user to find the files owned by bandit7
			and -group to also ensure its owned by group bandit6
			2>/dev/null return any perm denied error into void to keep clean
## lvl7 search for the word millionth 
	`grep -i millionth data.txt`
		-i makes it case insensitive 
## lvl8 search in a file for a line occurring only once 
in a file with multiple lines 
	`sort data.txt | uniq -u ` or `uniq -c`
	here *-u* ensures it prints out only the unique line and *-c* ensures it prints out all the lines once and counts their reoccurrence
## lvl9 find strings in a file
we used `strings - data.txt` to find all the human readable strings.
now we gotta sort the only ones which r proceeded by multiple " === " so i used grep
`strings - data.txt | grep "^===`" as itll print only those strings which have at least 3 == in start.