# FILE GLOBBING
This module has 10 challenges. 
Even just a few levels in, you might already be tired of typing out all these file paths. Luckily, the shell has a solution: globbing! That's what we'll learn in this module.
Before executing commands that you enter, the shell first performs expansions on them, and one of these expansions is globbing. 
Globbing lets you reference files without typing them all out, or typing out their full paths.

# 1. Matching with *
In this challenge, You must start from your home directory. Then, change your directory to /challenge, but use globbing to keep the argument you pass to cd to at most four characters! Once you're there, run /challenge/run for the flag

## My solution
**Flag:** `pwn.college{gRiLycLsBH6idlkQh9vOaJ_Qrfh.QXxIDO0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. I felt that, to change directory using cd along with an argument with at most four characters, the command must be something like `cd /ch*`, to incorporate * with this as well, to reduce the length of the argument, that resembles /challenge. Running this command, I got the flag!!
```bash
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{gRiLycLsBH6idlkQh9vOaJ_Qrfh.QXxIDO0wCMxkjNzEzW}
```


## What I learned 
1. When the shell encounters a * character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern.
2. Usually, only one file is bring matched with the argument * 
3. When zero files are matched, by default, the shell leaves the glob unchanged
4. The * matches any part of the filename except for / or a leading . character

## References
-[pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing resource pages 

# 2. Matching with ?
In this challenge, Starting from your home directory, change your directory to /challenge, but use the ? character instead of c and l in the argument to cd! Once you're there, run /challenge/run for the flag

## My solution
**Flag:** `pwn.college{8kLDJtTyKXFc0wjvKMsm7sZ3ofv.QXyIDO0wCMxkjNzEzW}`

1. Connected the wsl to the dojo 
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. To implement ? , as per question, we need to use the argument `?ha??enge` along with cd. So, on doing it, I entered the /challenge directory, where I executed `/challenge/run` , which gave me the flag.
```bash
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{8kLDJtTyKXFc0wjvKMsm7sZ3ofv.QXyIDO0wCMxkjNzEzW}
```

## What I learned
1. When the shell encounters a ? character in any argument, the shell will treat it as a single-character wildcard. This works like *, but only matches one character for each ?

## References
-[pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing resource pages 

# 3. Matching with []
In this challenge, Change your working directory to /challenge/files and run /challenge/run with a single argument that bracket-globs into file_b, file_a, file_s, and file_h!

## My solution
**Flag:** `pwn.college{YrAbG0DnF6wZmmSnsWiSq7M1wxY.QXzIDO0wCMxkjNzEzW}`

1. First, Connecting to the dojo, using ssh command
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, First, I changed my cwd to /challenge/files using `cd`. Then, I ran /challenge/run with argument `file[bash]`, as per the syntax of [] wildcard, which gave the flag on execution.
```bash
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{YrAbG0DnF6wZmmSnsWiSq7M1wxY.QXzIDO0wCMxkjNzEzW}
```

## What I learned 
1. The square brackets are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets.

## References
-[pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing resource pages 

# 4. Matching paths with []
Starting from your home directory, run /challenge/run with a single argument that bracket-globs into the absolute paths to the file_b, file_a, file_s, and file_h files.

## My solution
**Flag:** `pwn.college{4c3Gk-BpGBjYUUN-k1559RWrN1v.QX0IDO0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```

2. First I ran `/challenge/run file_[bash]` which gave the message as given below :
```bash
hacker@globbing~matching-paths-with-:~$ /challenge/run file_[bash]
Error: you will need to specify the path to the files as part of your glob
argument, since they are in a different directory than your current working
directory!
```
3. Now, I understood that we needed to pass the absolute path as argument. So, I executed the command ` /challenge/run /challenge/files/file_[bash]`, which gave the flag as output
```bash
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{4c3Gk-BpGBjYUUN-k1559RWrN1v.QX0IDO0wCMxkjNzEzW}
```

## What I learned
1. Globbing happens on a path basis, so you can expand entire paths with your globbed arguments

## References
-[pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing resource pages 

# 5. Multiple Globs 
In this challenge, Go cd to /challenge/files directory and run /challenge/run, providing a single argument: a short (3 characters or less) globbed word with two * globs in it that covers every word that contains the letter p.

## My solution
**Flag:** `pwn.college{wpkCth5pMKbZTn7l1Z80AEPwL12.0lM3kjNxwCMxkjNzEzW}`

1. Connected the wsl to the dojo 
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I changed my cwd to /challenge/files. Reading the question, I understood the argument's name is gonna be like *p*. So on executing `/challenge/run *p*`, I got the flag
```bash
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{wpkCth5pMKbZTn7l1Z80AEPwL12.0lM3kjNxwCMxkjNzEzW}
```

## What I learned 
1. Bash supports the expansion of multiple globs in a single word.

## References
-[pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing resource pages 

# 6. Mixing globs 
In this challenge, using the previous knowledge on file globbing, write a single, short (6 characters or less) glob that (when passed as an argument to /challenge/run) will match the files "challenging", "educational", and "pwning".

## My solution
**Flag:** `pwn.college{E9toFla-BuDOYz1GXMAmeembjIG.QX1IDO0wCMxkjNzEzW}`

1. First, Connecting to the dojo, using ssh command
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I changed my cwd to `/challenge/files`, as per question. Here, I encountered some errors, some of them are:
```bash
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run /challenge/files[in]
Error: your argument is too long! It must be 6 characters or less.
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run /c*/f*[in]
Error: your argument is too long! It must be 6 characters or less.
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run f*[in]
Your expansion did not expand to the requested files (challenging, educational,
pwning). Instead, it expanded to:
f*[in]
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [in]
Your expansion did not expand to the requested files (challenging, educational,
pwning). Instead, it expanded to:
[in]
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]
Your expansion did not expand to the requested files (challenging, educational,
pwning). Instead, it expanded to:
[cep]
```
3. After all these errors, I narrowed down to the idea that, the argument must contain [] glob and * glob . This time, I used the starting letters of the files in [] glob + * glob adding to the extension in the rest of the name of the file. On executing it, I got the flag.
```bash
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{E9toFla-BuDOYz1GXMAmeembjIG.QX1IDO0wCMxkjNzEzW}
```

## What I learned 
1. I learned how to glob multiple globbing functions to solve a question

## References
-[pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing resource pages 

# 7. Exclusionary globbing 
For this challenge, go forth to /challenge/files and run /challenge/run with all files that don't start with p, w, or n!

## My solution
**Flag:** `pwn.college{wqPEbWnCR_5aDbxYAxVhNOPc1Yq.QX2IDO0wCMxkjNzEzW}`

1. Connected the wsl to the dojo 
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As required, I moved into /challenge/files directory. By question, I ran `/challenge/run` with the argument `[!pwn]*`, which follows the same logic as qn 6.
```bash
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{wqPEbWnCR_5aDbxYAxVhNOPc1Yq.QX2IDO0wCMxkjNzEzW}
```

## What I learned
1. In bash, you can filter out the files in a glob. [] helps you do just this, ie if you use ! or ^ in the beginning of [] glob, you will be able to filter out the files as you wish

## References
-[pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing resource pages 

# 8. Tab Completion
This challenge has copied the flag into /challenge/pwncollege, and you can freely cat that file. But you can't type the filename: we used some serious trickery to make sure that you must tab-complete it.

## My solution
**Flag:** `pwn.college{EGMEbqSzK83mY2FFb0qllWjisAs.0FN0EzNxwCMxkjNzEzW}`

1. Connect to the dojo
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. This question is so straightfoward. Just type the initial part of each section of the command and then hit tab to complete the command. On executing this process for the command `cat /challenge/pwncollege` , the shell gave the flag
```bash
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​
pwn.college{EGMEbqSzK83mY2FFb0qllWjisAs.0FN0EzNxwCMxkjNzEzW}
```

## What I learned 
1. Your * glob might expand to unintended files, and you might not spot it until the rm command is already running! No one is safe from this style of error.
2. A safer alternative when you are trying to specify a specific target is tab completion. If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it.


## References
-[pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing resource pages 

# 9. Multiple options for tab completion
This challenge has a /challenge/files directory with a bunch of files starting with pwncollege. Tab-complete from /challenge/files/p or so, and make your way to the flag!

## My solution
**Flag:** `pwn.college{UfT8FCRvUd8KpoNB_ghUkxIiWS3.0lN0EzNxwCMxkjNzEzW}`

1. First, Connecting to the dojo, using ssh command
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, as per question, I used the tab keys to type in the first part of the command `/challenge/files/pwncollege`, as per question. I got these options
```bash
hacker@globbing~multiple-options-for-tab-completion:~$ /challenge/files/pwncollege-
pwncollege-family      pwncollege-flamingo    pwncollege-flyswatter  pwncollege-hacking
```
3. I ran some of all of these commands simply (trial and error), to try and get the flag. But I didn't get it. Like : 
```bash
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-family
No flag in this file!
```
4. Then I hit double tab after this command as well to try and see if another file is there in this directory. There were files inside this directory, and on execution they even gave a flag. But on submitting it in pwn.college, it appeared as an incorrect flag. So, after several tries, I understood, there is a decoy flag, other than the actual flag.
```bash
hacker@globbing~multiple-options-for-tab-completion:~$ /challenge/files/pwncollege-family
.bash_history  .config/       .lesshst       f              foo.1x.dvi     foo.1x.flag    not-the-flag
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-family f
No flag in this file!
pwn.college{I1mGZAL17zuQdizT2mGgI2Uoybb.QXzMDO0wCMxkjNzEzW}  --> Decoy flag 
```

5. Then a thought arose that why not put f after the - in the command to try and make the obvious word flag. And I was right!!!. There was a file called `pwncollege-flag`
```bash
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-f
pwncollege-family      pwncollege-flag        pwncollege-flamingo    pwncollege-flyswatter
```
6. So, I ran the command `cat /challenge/files/pwncollege-flag` and on execution, the shell revealed the flag
```bash
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-flag
pwn.college{UfT8FCRvUd8KpoNB_ghUkxIiWS3.0lN0EzNxwCMxkjNzEzW}
```

## What I learned
1. When there are multiple options, what happens by default is, bash will auto-expand until the first point when there are multiple options (in this case, fl). When you hit tab a second time, it'll print out those options.
2. Other shells and configurations, instead, will cycle through the options.

## References
-[pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing resource pages

# 10. Tab Completion on commands
This level has a command that starts with pwncollege, and it'll give you the flag. Type pwncollege and hit the tab key to auto-complete it!

## My solution
**Flag:** `pwn.college{QOWRVGaDc7MWKGZJFOUld4MIuQG.0VN0EzNxwCMxkjNzEzW}`

1. 1. Connected the wsl to the dojo 
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. According to question, just type the command `pwncollege` and then hit tab and then execute that command. On doing so, the shell revealed the flag for me 
```bash
hacker@globbing~tab-completion-on-commands:~$ pwncollege-30941
Correct! Here is your flag:
pwn.college{QOWRVGaDc7MWKGZJFOUld4MIuQG.0VN0EzNxwCMxkjNzEzW}
```

## what I learned 
1. Tab completion is for more than files. You can also tab-complete commands.

## References
-[pwn.college](https://pwn.college/linux-luminarium/globbing/) - File Globbing resource pages
