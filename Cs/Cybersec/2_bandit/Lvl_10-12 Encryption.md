[[Index_bandit]]
## Lvl 10 base 64
to decode a file which is encrypted in base64 we use base64
it is an encrypting method used for binary-to-text encryption. 
we have a file called data.txt so we use 
`base64 -d data.txt` here we use -d to decode

## Lvl 11 Rot13
Rot13 is an encryption method where we rotate any letter to its succeeding 13th letter. 
very primitive but it works. we use tr in linux
`tr "A-Za-z" "N-ZA-Mn-za-m`

## Lvl 12 Multiple decryption 
>random: we use `cp` and directory name to copy files there.
>we have a data.txt file -> try.txt
>`xxd -r try.txt > myfile` this makes it a binary file 
>>`file myfile` this checks the type of compression : `gzip`
>>>`gunzip -c myfile > myfile2`
>>`file my file2` : `bzip2`
>>>`bzip2 -d myfile2 > myfile3` 
>>>new file name is *myfile2.out* 
>>`file myfile2.out` : `gzip`
>>>`gunzip -c myfile2.out > myfile4
>>another new file is added now we `file myfile4`: `Posix tar archive`
>>> `tar -xf myfile4` a new file is silently added. check with ls -la
>>> 	it may be data5.bin
>repeat until you get the password 

# Gzip 
> `gunzip -c filename`: `-c` for decryption and `-d` for encryption
# bzip2
> `bzip2 -d filename`
# Posix tar archive
>used for tapes and archives. hence we need to specify we r using it on a file 
>`tar -xf filename` : here `-xf` was used to specify its being used on a file 

 




