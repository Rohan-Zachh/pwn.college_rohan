# SHELL VARIABLES 
Because the command line interface is colloquially referred to as a "shell", programs written in this language are referred to as "shell scripts". When you're using the command line, you are basically writing a shell script line by line!
Like most programming languages, the shell supports variables. This module will get you familiar with setting, printing, and using these variables!

# 1. Printing Variables 
In this challenge, have your shell print out the FLAG variable and solve this challenge!

## My solution
**Flag:** `pwn.college{UUl5dVm5lst6vcyhGW8--AUJBEn.QX3UTN0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. Following the syntax for printing out a variable, I printout the variable FLAG, using echo and on execution, I got the flag
```bash
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{UUl5dVm5lst6vcyhGW8--AUJBEn.QX3UTN0wCMxkjNzEzW}
```

## What I learned 
1. Command : echo - This command just prints stuff
2. You can also print out variables with echo, by prepending the variable name with a $

## References
-[pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables resource pages 

# 2. Setting Variables
In this level, you must set the PWN variable to the value COLLEGE.

## My solution
**Flag:** `pwn.college{Y96heaPftcBZ_IpOZNvuqKQCoea.QX5UTN0wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. This question is a straight-foward question, like just assign PWN variable with COLLEGE. So, on executing command `PWN=COLLEGE`, I got the flag
```bash
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{Y96heaPftcBZ_IpOZNvuqKQCoea.QX5UTN0wCMxkjNzEzW}
```

## what I learned 
1. you can write values to variables, same as with many other languages, using =. 
2. Note that there are no spaces around the =!

## References
-[pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables resource pages 

# 3. Multi-word Variable 
In this level, you'll need to set the variable PWN to COLLEGE YEAH.

## My solution
**Flag:** `pwn.college{k1pNc_jnDQm3jcews771eqLQdLj.QXwYTN0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. Inoder to incorporate more than one components into a variable, we use quoting mechanism. So, I run ` PWN="COLLEGE YEAH"` command, which gave the flag as the output 
```bash
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{k1pNc_jnDQm3jcews771eqLQdLj.QXwYTN0wCMxkjNzEzW}
```

## What I learned 
1. In this level, I learned about quoting 
2. Spaces have special significance in the shell, and there are places where you can't use them spuriously.
3. When the shell sees a space, it ends the variable assignment and interprets the next word (SAUCE in this case) as a command. example : hacker@dojo:~$ VAR=1337 SAUCE

## References
-[pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables resource pages 

# 4. Exporting Variables 
In this challenge, you must invoke /challenge/run with the PWN variable exported and set to the value COLLEGE, and the COLLEGE variable set to the value PWN but not exported

## My solution
**Flag:** `pwn.college{sNvjkeLv5ovi8EPSSKsAVnBur0s.QXyYTN0wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I exported the variable PWN and set to value COLLEGE 
```bash
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
```
3. The, I set the variable COLLEGE with value PWN, but not exported.
```bash
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```
4. Then, I ran `/challenge/run PWN`, whose execution gave the flag
```bash
hacker@variables~exporting-variables:~$ /challenge/run PWN
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great
job! Here is your flag:
pwn.college{sNvjkeLv5ovi8EPSSKsAVnBur0s.QXyYTN0wCMxkjNzEzW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```

## What I learned 
1. By default, variables that you set in a shell session are local to that shell process.
2. When you export your variables, they are passed into the environment variables of child processes.

## References
-[pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables resource pages 

# 5. Printing exported variables 
In this challenge, Try the env command: it'll print out every exported variable set in your shell, and you can look through that output to find the FLAG variable!

## My solution
**Flag:** `pwn.college{kM3MQB3o9FUwCsthMDbc00n6LSI.QX4UTN0wCMxkjNzEzW}`
1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. This is a very straightfoward question, to make us familiar with env command. Here, I just executed the env command then inspected the variables, among which I found the FLAG variable, which contained the flag, which is the flag we needed to find.
```bash
hacker@variables~printing-exported-variables:~$ env
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
MANPATH=/run/dojo/share/man:
DOJO_AUTH_TOKEN=ca67b3b38a79bc3588bdd4ff4194805b4a21cff3067d0995f96d2e06bcb9aa09
HOME=/home/hacker
LANG=C.UTF-8
FLAG=pwn.college{kM3MQB3o9FUwCsthMDbc00n6LSI.QX4UTN0wCMxkjNzEzW} ---> FLAG!!!!
TERMINFO=/run/dojo/share/terminfo
TERM=xterm-256color
SHLVL=2
LC_CTYPE=C.UTF-8
SSL_CERT_FILE=/run/dojo/etc/ssl/certs/ca-bundle.crt
PATH=/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
DEBIAN_FRONTEND=noninteractive
_=/run/dojo/bin/env
```

## What I learned 
1. the env command: it'll print out every exported variable set in your shell

## References
-[pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables resource pages 

# 6. Storing command output 
In this challenge, read the output of the /challenge/run command directly into a variable called PWN, and it will contain the flag!

## My solution
**Flag:** `pwn.college{gYPR97PE3_oHlXgs-WvA8ZWw8v8.QX1cDN1wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. By question, you need to first pass the output of /challenge/run to the variable PWD. For that I execute the command ` PWN=$(/challenge/run )`
```bash
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run )
Congratulations! You have read the flag into the PWN variable. Now print it out
and submit it!
```
3. Now, as per the message, I execute PWD to get the flag. 
```bash
hacker@variables~storing-command-output:~$ echo "$PWN"
pwn.college{gYPR97PE3_oHlXgs-WvA8ZWw8v8.QX1cDN1wCMxkjNzEzW}
```

## What I learned 
1. If you want to store the output of some command into a variable, use command substitution ie use $() while passing the value to the variable 

## References
-[pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables resource pages 

# 7. Reading Input 
In this challenge, your job is to use read to set the PWN variable to the value COLLEGE.

## My solution
**Flag:** `pwn.college{441B6e0jrHE9tgaAeLVoxZk7SY-.QX4cTN0wCMxkjNzEzW}`
1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, inorder to set the value of PWN as COLLEGE, I follow the syntax of read command, and I execute the command `read -p "INPUT: " PWN`, whose execution displayed the flag in the shell
```bash
hacker@variables~reading-input:~$ read -p "INPUT: " PWN
INPUT: COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{441B6e0jrHE9tgaAeLVoxZk7SY-.QX4cTN0wCMxkjNzEzW}
```

## What I learned 
1. For reading input, The syntax is read -p "INPUT: " variable

## References
-[pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables resource pages 

# 8. Reading Files 
In this challenge, use < to read /challenge/read_me into the PWN environment variable, and we'll give you the flag! The /challenge/read_me will keep changing, so you'll need to read it right into the PWN variable with one command.

## My solution
**Flag:** `pwn.college{MgClVm-RZtDtCA_9sRzlvDzTZHe.QXwIDO0wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, I need to read the info of /challenge/read_me into the variable PWN. So, I executed the command `read PWN < /challenge/read_me`, whose execution, outputted the flag.
```bash
hacker@variables~reading-files:~$ read PWN < /challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{MgClVm-RZtDtCA_9sRzlvDzTZHe.QXwIDO0wCMxkjNzEzW}
```

## What I learned 
1. Instead of running another program inorder to read the info of a file like using cat,etc , we can use < to read the info of a file into a variable

## References
-[pwn.college](https://pwn.college/linux-luminarium/variables/) - Shell Variables resource pages 

