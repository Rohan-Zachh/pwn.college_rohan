# Pondering Paths 
How does the shell know how to check for commands like ls, cat, etc ? In this module, we will find the answer to that question.

# 1. The PATH Variable
In this level, you will disrupt the operation of the /challenge/run program. This program will DELETE the flag file using the rm command. However, if it can't find the rm command, the flag will not be deleted, and the challenge will give it to you! Thus, you must make it so that /challenge/run also can't find the rm command

## My solution
**Flag:** `pwn.college{0sTHmGcSSP0u0k7bhqnENW4vFk6.QX2cDM1wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As said in question, we need to prevent the /challenge/run file from being deleted. In order to prevent that, we can use the PATH variable (as mentioned in what I learned section), in doing so, I run the command, `/challenge/run`, which reveals the flag.
```bash
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ rm
bash: rm: No such file or directory
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{0sTHmGcSSP0u0k7bhqnENW4vFk6.QX2cDM1wCMxkjNzEzW}
```

## What I learned
1. There is a special shell variable, called PATH, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands.
2. Without a PATH, bash cannot find the ls command.
3. So things break when you blank out PATH, ie the shell cannot find the command like it used to. `MAIN CONCEPT OF THIS QUESTION`
Syntax: `PATH=""`

## References
-[pwn.college](https://pwn.college/linux-luminarium/path/) -  Pondering Paths manual pages 

# 2. Setting Path
This level's /challenge/run will run the win command via its bare name, but this command exists in the /challenge/more_commands/ directory, which is not initially in the PATH. The win command is the only thing that /challenge/run needs, so you can just overwrite PATH with that one directory.

## My solution
**Flag:** `pwn.college{YyU2pQKp7VaxsTZ1OneSFdHJH3o.QX1cjM1wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. This question just follows what is being explained in the question, ie, Just add `/challenge/more_commands/` to the PATH variable and then run `/challenge/run`, which runs the file `win`, which is in `/challenge/more_commands/` directory, to reveal the flag!!
```bash
hacker@path~setting-path:~$ PATH=/challenge/more_commands/
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{YyU2pQKp7VaxsTZ1OneSFdHJH3o.QX1cjM1wCMxkjNzEzW}
```

## What I learned
1. If a file/commands are in nonstandard places, which is not initially in the PATH, they cannot be invoked simply by calling their names. But, sometimes, in crucial moments, it would be better if we could just get the file / execute the command, just by calling its name. If you wanna do it, you must add it to the PATH variable, as given below

2. SYNTAX: (for example) - `PATH=/home/hacker/scripts` , now all the files in scripts can be accessed, just by calling its name.

## References
-[pwn.college](https://pwn.college/linux-luminarium/path/) -  Pondering Paths manual pages 

# 3. Finding Commands
In this challenge, we added a win command somewhere in your $PATH, but it won't give you the flag. Instead, it's in the same directory as a flag file that we made readable by you! You must find win (with the which command), and cat the flag out of that directory

## My solution
**Flag:** `pwn.college{UDgGM-3UcnHjyBr6Yx4oyXjMedd.01NzEzNxwCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As the `win` command is in the same directory as the flag file, I use `which` command to find its directory.
```bash
hacker@path~finding-commands:~$ which win
/challenge/paths/5130/win
```

3. On getting the directory address, I just execute `cat /challenge/paths/5130/flag`, which outputs the flag!!
```bash
hacker@path~finding-commands:~$ cat /challenge/paths/5130/flag
pwn.college{UDgGM-3UcnHjyBr6Yx4oyXjMedd.01NzEzNxwCMxkjNzEzW}
```

## What I learned 
1. which command :  `which` looks at each directory in $PATH in order and prints the first file it finds whose name matches the argument you passed.

## References
-[pwn.college](https://pwn.college/linux-luminarium/path/) -  Pondering Paths manual pages 

# 4. Adding Commands
Previously, the win command that /challenge/run executed was stored in /challenge/more_commands. This time, win does not exist! Recall the final level of Chaining Commands, and make a shell script called win, add its location to the PATH, and enable /challenge/run to find the flag.

## My solution
**Flag:** `pwn.college{Yn9rM-b3-mFgvP1DQbPGsBh8RhG.QX2cjM1wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. By question, first, I created shell script called win as shown
```bash
hacker@path~adding-commands:~$ cat > win <<'EOF'
> #!/bin/bash
> /bin/cat /flag
> EOF
```
3. Then, as learnt before, I checked the shell script's permission, whether if its executable or not. It wasn't executable, so I made it executable using chmod command 
```bash
hacker@path~adding-commands:~$ ls -l win
-rw-r--r-- 1 hacker hacker 27 Oct  9 18:27 win
hacker@path~adding-commands:~$ chmod ugo+x win
hacker@path~adding-commands:~$ ls -l win
-rwxr-xr-x 1 hacker hacker 27 Oct  9 18:27 win
```
4. As the program run by invoking /challenge/run needs win file to be executable by just referring by its name. For that, I use PATH variable. 
```bash
hacker@path~adding-commands:~$ PATH=/home/hacker
```
5. Then, I run `/challenge/run`, which refers to win file, whose execution reveals the flag
```bash
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{Yn9rM-b3-mFgvP1DQbPGsBh8RhG.QX2cjM1wCMxkjNzEzW}
```

## What I learned
1. I learned how to use knowledge from different modules, in solving a single question, which is a practice for what we need to do in real ctf challenges.

## References
-[pwn.college](https://pwn.college/linux-luminarium/path/) -  Pondering Paths manual pages 

# 5. Hijacking Commands
This challenge is almost the same as the first challenge in this module. Again, this challenge will delete the flag using the rm command. But unlike before, it will not print anything out for you. How can you solve this? You know that rm is searched for in the directories listed in the PATH variable. You have experience creating the win command when the previous challenge needed it. What else can you create?

## My solution
**Flag:** `pwn.college{kqIY-qNKnFBanlyOWq0VU_vf8nC.QX3cjM1wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. In this question, we can't use PATH="", bcz its blocks our only way of making the process run by /challenge/run for detecting rm file name, as secretly mentioned in the question. Therefore, the only way is to make the shell detect our fake rm file before the real rm command, to prevent the deletion of the flag.

So, I make a new directory and make a shell script `rm` as shown 
```bash
hacker@path~hijacking-commands:~$ mkdir -p /home/hacker/mal
hacker@path~hijacking-commands:~$ cat > /home/hacker/mal/rm <<'EOF'
> #!/bin/bash
> /bin/cat /flag
> EOF
```
3. Then, as learnt before, I checked the shell script's permission, whether if its executable or not. It wasn't executable, so I made it executable using chmod command 
```bash
hacker@path~hijacking-commands:~$ ls -l /home/hacker/mal/rm
-rw-r--r-- 1 hacker hacker 27 Oct  9 18:54 /home/hacker/mal/rm
hacker@path~hijacking-commands:~$ chmod ugo+x /home/hacker/mal/rm
hacker@path~hijacking-commands:~$ ls -l /home/hacker/mal/rm
-rwxr-xr-x 1 hacker hacker 27 Oct  9 18:54 /home/hacker/mal/rm
```
4. As the program run by invoking /challenge/run needs win file to be executable by just referring by its name. For that, I use PATH variable. 
```bash
hacker@path~hijacking-commands:~$ PATH=/home/hacker/mal
```
5. Now, I run `/challenge/run`, whose execution reveals the flag
```bash
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
pwn.college{kqIY-qNKnFBanlyOWq0VU_vf8nC.QX3cjM1wCMxkjNzEzW}
```

## What I learned
1. Learned to combine all the lessons learnt in this module into solving this challenge.

## References
-[pwn.college](https://pwn.college/linux-luminarium/path/) -  Pondering Paths manual pages 

