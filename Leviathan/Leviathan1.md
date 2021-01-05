Leviathan1

# Leviathan1 05/01/2021 07:22

# Login with ssh
`ssh leviathan1@leviathan.labs.overthewire.org -p 2223`
password: `rioGegei8m`

By default, ssh tries to connect to port ``22``.

# Enumeration
running `ls -la`
>total 28
drwxr-xr-x  2 root       root       4096 Aug 26  2019 .
drwxr-xr-x 10 root       root       4096 Aug 26  2019 ..
-rw-r--r--  1 root       root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root       root       3526 May 15  2017 .bashrc
-r-sr-x---  1 leviathan2 leviathan1 7452 Aug 26  2019 check
-rw-r--r--  1 root       root        675 May 15  2017 .profile

`check` file has SETUID bit set for users that belong to group `leviathan1`.

running `file ./check`
>check: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=c735f6f3a3a94adcad8407cc0fda40496fd765dd, not stripped

`./check` asks for a password.
>leviathan1@leviathan:~$ ./check 
password: foobarbaz
Wrong password, Good Bye ...

# Use `strings` utility
Using `strings ./check` to output the readable characters, we can see somewhere in the program.

>puts                                           
setreuid                               
printf                                   
getchar                                    
system                                    
geteuid                                    
strcmp
password:                                   
/bin/sh
main
PTRhp
...
...
...
QVh;                                         
secrf                                      
love                                      
UWVS                                       
t$,U                                       
[^_]

From the looks of it, the program prompts a `/bin/sh` shell if the password is correct. The words like `love` hints that password might `love`? ... after trying it, nope its not.

# There are several ways you can approach this level.

## Way 1 - Bruteforce
Let's bruteforce our way through, we'll use English dictionary for this challenge.

## Way 2 - Reverse Engineering with `radare2`
Reading Materials 

https://www.youtube.com/watch?v=LAkYW5ixvhg

https://www.loginsoft.com/blog/2018/09/11/introduction-to-reverse-engineering-and-radare2/

# Shell
running `id`
>uid=12002(leviathan2) gid=12001(leviathan1) groups=12001(leviathan1)

Notice how our `GID` does not change, only the `UID`. It's because SETUID binaries only sets our UID to the effective UID, and in contrast SETGID binaries sets our GID to the effective GID.

Seems like we're in! Remember you can look at `/etc/leviathan_pass` for the various level passwords.

`cat /etc/leviathan_pass/leviathan2`
>ougahZi8Ta

### Password for `leviathan2`: ougahZi8Ta
