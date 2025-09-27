# Document Digestion
This module has 7 challenges. Here, Documentation is just to figure out how to use all these dang programs, and a specific case of that is figuring out what arguments to specify on the command line. This module will mostly dig into that concept, as a proxy for figuring out how to use the programs in general.

# 1. Learning from Documentation 
For this challenge is /challenge/challenge, and you'll need to invoke it properly. You can do it by passing the argument of `--giveflag`.

## My solution
**Flag:** `pwn.college{wnhSUtmnaXPI_4IU_F5-Ub80jXo.QX0ITO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. I pass the command  `/challenge/challenge --giveflag`, bcz as per question its given that, you need to pass /challenge/challenge with a proper argument, which gave me the flag.
```bash
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{wnhSUtmnaXPI_4IU_F5-Ub80jXo.QX0ITO0wCMxkjNzEzW}
```
## What I learned 
1. The correct usage of programs depends, in a large part, on the proper specification of arguments to them. Like in the case of `ls -a`

## References
-[pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation resource pages 

# 2. Learning Complex Usage 
In this challenge, use `/challenge/challenge --printfile (argument)` to print the flag

## My solution
**Flag:** `pwn.college{QVN71xbVmyDe7yBYgDL_M8yZo-t.QX1ITO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. Connected to the dojo. Now, I executed `/challenge/challenge --printfile /flag` , bcz in this challenge, we are introduced to a new concept of passing argument along with another argumeent 
``` bash
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{QVN71xbVmyDe7yBYgDL_M8yZo-t.QX1ITO0wCMxkjNzEzW}
```

## What I learned 
1. Somewhere on the spectrum between cd and awk are commands that take arguments to their arguments. 
2. find has a -name argument, and the -name argument itself takes an argument specifying the name to search for

## References
-[pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation resource pages

# 3. Reading Modules 
In this challenge has a secret option that, when you use it, will cause the challenge to print the flag. You must learn this option through the man page for challenge.

## My solution
**Flag:** `pwn.college{YVNdAR-sckRBPJqr1SchwaQJ0zx.QX0EDO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. I execute `man challenge` to read the manual of challenge. From the manual, I identify 3 things 
a) we need to execute `/challenge/challenge with arguments`
b) The argument is `--dsckqr NUM`
c) And NUM should be 100 
So I execute `/challenge/challenge --dsckqr 100`, which gave me the flag
```bash
hacker@man~reading-manuals:~$ man challenge
hacker@man~reading-manuals:~$ /challenge/challenge --dsckqr 100
Correct usage! Your flag: pwn.college{YVNdAR-sckRBPJqr1SchwaQJ0zx.QX0EDO0wCMxkjNzEzW}
```

## What I learned 
1. `man` command : man is short for manual, and will display (if available) the manual of the command you pass as an argument.
2. You can scroll around the manpage with your `arrow keys` and PgUp/PgDn. When you're done reading the manpage, you can hit `q` to quit.
3. Manpages are stored in a centralized database and this database lives in the /usr/share/man directory, but you never need to interact with it directly: you just query it using the man command. 

## References
-[pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation resource pages

# 4. Searching Manuals
In this challenge, Find the option that will give you the flag by reading the challenge man page.

## My solution
**Flag:** `pwn.college{s_Z01aMV2jOGYa-LO1KLRCeCT5X.QX1EDO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected . First, I opened the manual page of challenge by running `man challenge`. Then, ran `/flag` to search for the keyword, which in turn is the argument for `/challenge/challenge` , which later on gave me the flag.
```bash
hacker@man~searching-manuals:~$ man challenge
hacker@man~searching-manuals:~$ /challenge/challenge --sde
Initializing...
Correct usage! Your flag: pwn.college{s_Z01aMV2jOGYa-LO1KLRCeCT5X.QX1EDO0wCMxkjNzEzW}
```

## what I learned 
1. You can scroll man pages with the arrow keys (and PgUp/PgDn) and search with /
2. After searching, you can hit n to go to the next result and N to go to the previous result.
3. Instead of /, you can use ? to search backwards

## References
-[pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation resource pages

# 5. Searching for Manuals 
In this challenge, it hides the manpage for the challenge by randomizing its name. To figure out how to search for the right manpage, read the man page manpage by doing: man man!

## My solution
**Flag:** `pwn.college{4O-xmkm8iz9cR9EF0Gq0uGRjLIP.QX2EDO0wCMxkjNzEzW}`

1. Connecting the wsl to the dojo
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I execute the `man man` command. I did a lot of trial and error in solving this question. First, we needed to find the manpage that contains the argumrnt to execute /challenge/challenge.
a) I executed `man -l -Tdvi ./foo.1x.gz > ./foo.1x.dvi`,bcz its description contained "flag" , but it gave me errors 
```bash
hacker@man~searching-for-manuals:~$ man -l -Tdvi ./foo.1x.gz > ./foo.1x.dvi
man: ./foo.1x.gz: No such file or directory
```
3. Then, I returned to man ( ) commands given in the man man page, and started doing trial and error with the commands until `man -K` worked 
```bash
hacker@man~searching-for-manuals:~$ man -l
What manual page do you want?
For example, try 'man man'.
hacker@man~searching-for-manuals:~$ man -K
What manual page do you want?
For example, try 'man man'.
hacker@man~searching-for-manuals:~$ man -k
apropos what?
hacker@man~searching-for-manuals:~$ man man
hacker@man~searching-for-manuals:~$ man -k "/challenge/challenge"
xmkmizcquj (1)       - print the flag!
hacker@man~searching-for-manuals:~$ /challenge/challenge xmkmizcquj (1)
bash: syntax error near unexpected token `('
hacker@man~searching-for-manuals:~$ /challenge/challenge xmkmizcquj
Incorrect usage! Please read the hidden challenge man page!
hacker@man~searching-for-manuals:~$ man -K "/challenge/challenge"
```
4. From man -K "/challenge/challenge", I got the argument for executing /challenge/challenge. On executing it, the shell revealed the flag
Description of man -K : --xmkmiz NUM
              print the flag if NUM is 489
```bash
hacker@man~searching-for-manuals:~$ /challenge/challenge --xmkmiz 489
Correct usage! Your flag: pwn.college{4O-xmkm8iz9cR9EF0Gq0uGRjLIP.QX2EDO0wCMxkjNzEzW}
```

## what I learned 
1. To figure out how to search for the right manpage, read the man page manpage by doing: man man

## References
-[pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation resource pages

# 6. Helpful Programs 
In this challenge, you will practice reading a program's documentation with --help.

## My solution
**Flag:** `pwn.college{EX6IbjfoC3x0AQp2yMJekjY0a9w.QX3IDO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. I ran the command `--help`, to find how to find the flag. I got :
a) Find the secret value by passing the argument with the command like : `/challenge/challenge --print-value`
b) Find the flag by passing another argument with the command, along with the secret value like : `/challenge/challenge --give-the-flag 630`
```bash
hacker@man~helpful-programs:/$ /challenge/challenge --help
usage: a challenge to make you ask for help [-h] [--fortune] [-v] [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to give you the flag
hacker@man~helpful-programs:/$ /challenge/challenge --print-value
The secret value is: 630
hacker@man~helpful-programs:~$ /challenge/challenge --give-the-flag 630
Correct usage! Your flag: pwn.college{EX6IbjfoC3x0AQp2yMJekjY0a9w.QX3IDO0wCMxkjNzEzW}
```

## What I learned
1. Some programs don't have a man page, but might tell you how to run them if invoked with a special argument, which is --help

## References
-[pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation resource pages.

# 7. Help for Builtins
In this challenge, we'll practice using help to look up `help` for builtins. This challenge's challenge command is a shell builtin, rather than a program. Like before, you need to lookup its help to figure out the secret value to pass to it

## My solution
**Flag:** `pwn.college{AEoI2M4Qmq_zUMF2xY9AV2oNn7E.QX0ETO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. First, I ran `help challenge` to get more info on solving the problem. 
```bash
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!

    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "AEoI2M4Q".
```
3. Now is executed `challenge --secret AEoI2M4Q` as specified in the help description, which gave me the flag. 
```bash
hacker@man~help-for-builtins:~$ challenge --secret AEoI2M4Q
Correct! Here is your flag!
pwn.college{AEoI2M4Qmq_zUMF2xY9AV2oNn7E.QX0ETO0wCMxkjNzEzW}
```

## What I learned 
1. Some commands, rather than being programs with man pages and help options, are built into the shell itself. These are called builtins.
2. Builtins are invoked just like commands, but the shell handles them internally instead of launching other programs. You can get a list of shell builtins by running the builtin help.

## References
-[pwn.college](https://pwn.college/linux-luminarium/man/) - Digesting Documentation resource pages.




