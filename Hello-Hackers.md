1) # Intro to Commmands
To invoke the hello command to get the flag.

## My solve
**Flag:** `pwn.college{0Cs6uZmpb2os5GCaQlUKXHOPmvy.QX3YjM1wCMxkjNzEzW}`

```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
hacker@hello~intro-to-commands:~$ hello
Success! Here is your flag:
pwn.college{0Cs6uZmpb2os5GCaQlUKXHOPmvy.QX3YjM1wCMxkjNzEzW}
```

## What I learned
Commands in Linux are case sensitive: hello is different from HELLO. Also commands like whoami and hello 

## References 
https://www.youtube.com/watch?list=PL-ymxv0nOtqqRAz1x90vxNbhmSkeYxHVC&v=g_85EVO3IC0


2) # Intro to Arguments 
To implement a command along with arguments.

## My solve
**Flag:** `pwn.college{ADXzCgIUrom3AgzYGGhwKEl0DYZ.QX4YjM1wCMxkjNzEzW}`

```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
hacker@hello~intro-to-arguments:~$ hello hackers
Success! Here is your flag:
pwn.college{ADXzCgIUrom3AgzYGGhwKEl0DYZ.QX4YjM1wCMxkjNzEzW}
```

## What I learned 
When we invoke a command with arguments, additional data is being passed to the command. More than one argument can be passed to the command.
Command learned : echo

## References 
https://www.youtube.com/watch?list=PL-ymxv0nOtqqRAz1x90vxNbhmSkeYxHVC&v=g_85EVO3IC0


3) # Command History
To use the arrow key to scroll through the command history and find the flag.

## My solve
**Flag:** `pwn.college{MZkIV6qu-H18TJraZnogcbdz6hs.0lNzEzNxwCMxkjNzEzW}`

```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
hacker@hello~command-history:~$ the flag is pwn.college{MZkIV6qu-H18TJraZnogcbdz6hs.0lNzEzNxwCMxkjNzEzW}
```

## What I learned 
The shell saves a history of every command you invoke and you can use the up/down arrow keys to scroll through and invoke the command again, instead of typing it all over again.

## References
https://www.youtube.com/watch?list=PL-ymxv0nOtqqRAz1x90vxNbhmSkeYxHVC&v=g_85EVO3IC0