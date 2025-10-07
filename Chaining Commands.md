# Chaining Commands
Sometimes, you might want to run several commands in quick succession to achieve some cumulative effect. This module will cover a few ways, aside from piping, that commands can be chained.

# 1. Chaining with Semicolons 
 In this level, you must run /challenge/pwn and then /challenge/college, chaining them with a semicolon.

## My solution
**Flag:** `pwn.college{Uty7Bld7ppLmg948DDWhsPcSk2f.QX1UDO0wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. This is a straight-foward challenge. We just need to run /challenge/pwn, followed by /challenge/college, using semicolon, whose execution outputted the flag.
```bash
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{Uty7Bld7ppLmg948DDWhsPcSk2f.QX1UDO0wCMxkjNzEzW}
```
## what I learned 
1. The easiest way to chain commands is ; . In most contexts, ; separates commands in a similar way to how Enter separates lines.

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 

# 2. Building on Success
In this challenge, you need to chain the programs /challenge/first-success and /challenge/second using the && operator.

## My solution
**Flag:** `pwn.college{4Pc9qpr_T-nShMIcbfm0abYORlo.0lM0MDOxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, as per question, I ran the commands individually to see what would happen. 
```bash
hacker@chaining~building-on-success:~$ /challenge/first-success
hacker@chaining~building-on-success:~$ /challenge/second
Error: /challenge/first-success must be successfully chained with
/challenge/second using &&
```
3. Now, I ran both the commands utilising && operator, whose output gave me the flag 
```bash
hacker@chaining~building-on-success:~$ /challenge/first-success && /challenge/second
Nice chaining! Flag: pwn.college{4Pc9qpr_T-nShMIcbfm0abYORlo.0lM0MDOxwCMxkjNzEzW}
```

## What I learned 
1. The && operator allows you to run a second command only if the first command succeeds (in Linux convention, this means it exited with code 0).
2. This is called the "AND" operator because both conditions must be true: the first command must succeed AND then the second command will run. That's super useful for complex commandline workflows where certain actions depend on the success of other actions.

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 

# 3. Handling Failure 
In this challenge, you need to chain /challenge/first-failure and /challenge/second using the || operator.

## My solution
**Flag:** `pwn.college{4tvKiAfeXJgQj4IjCBBBoovysAh.01M0MDOxwCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. This challenge is very straught-foward. By question, you just need to chain /challenge/first-failure and /challenge/second using the || operator, whose execution gave me the flag!!
```bash
hacker@chaining~handling-failure:~$ /challenge/first-failure || /challenge/second
Nice chaining! Flag: pwn.college{4tvKiAfeXJgQj4IjCBBBoovysAh.01M0MDOxwCMxkjNzEzW}
```

## What I learned 
1. the || operator allows you to run a second command only if the first command fails.
2. This is called the "OR" operator because either the first command succeeds OR the second command will run.
3. The || operator is super useful for providing fallback commands or error handling!

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 

# 4. Your First Shell Script 
In this challenge, run /challenge/pwn and then /challenge/college, but this time in a shell script called x.sh, then run it with bash!

## My solution
**Flag:** `pwn.college{4Y6u2OojECzvX2_s_RsB9GDbvAo.QXxcDO0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per qquestion, inorder to write the commands in a shell script, we gotta make one. For that, I run the command `cat > x.sh <<'EOF'` and then enter the commands as shown:
```bash
hacker@chaining~your-first-shell-script:~$ cat > x.sh <<'EOF'
> /challenge/pwn
> /challenge/college
> EOF
```
3. Now, Inorder to execute the shell script, I execute `bash x.sh`, whose execution outputs the flag!!
```bash
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{4Y6u2OojECzvX2_s_RsB9GDbvAo.QXxcDO0wCMxkjNzEzW}
```

## What I Learned 
1. As you combine more and more commands to achieve complex effects, the length of the combined prompt quickly gets really annoying to deal with. When this happens, you can put these commands in a file, called a shell script, and run them by executing the file!
2. We can create a shell script called pwn.sh (by convention, shell scripts are frequently named with a sh suffix).
3. Syntax : bash filename.sh

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 

# 5. Redirecting Script Output 
In this level, we will practice piping (|) from your script to another program. Like before, you need to create a script that calls the /challenge/pwn command followed by the /challenge/college command, and pipe the output of the script into a single invocation of the /challenge/solve command!

## My solution
**Flag:** `pwn.college{M20ir84YVVz1rBKzX_uew2nqWtr.QX4ETO0wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, first I made a shell script named x.sh as shown:
```bash
hacker@chaining~redirecting-script-output:~$ cat > x.sh <<'EOF'
> /challenge/pwn
> /challenge/c
chio.py  college
> /challenge/college
> EOF
```
3. Now, I piped the shell script to the command, as required, by executing the command `bash x.sh | /challenge/solve`, whose execution revealed the flag!!
```bash
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{M20ir84YVVz1rBKzX_uew2nqWtr.QX4ETO0wCMxkjNzEzW}
```

## what I learned 
1. Inorder to send the output of several programs to one command, we use the concept of shell script. 
2. As far as the shell is concerned, your script is just another command. That means you can redirect its input and output just like you did previously!!

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 

# 6. Executable Shell Scripts 
In this level, Make a shellscript that will invoke /challenge/solve, make it executable, and run it without explicitly invoking bash!

## My solution
**Flag:** `pwn.college{gFmSk0d4h8rynnfAHa5JJD4Dxzb.QX0cjM1wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I made a shell script that invokes `/challenge/solve` and I make it executable using chmod, as shown below:
```bash
hacker@chaining~executable-shell-scripts:~$ cat > x.sh <<'EOF'
> /challenge/solve
> EOF
hacker@chaining~executable-shell-scripts:~$ chmod ugo+x x.sh
hacker@chaining~executable-shell-scripts:~$ ls -l x.sh
-rwxr-xr-x 1 hacker hacker 18 Oct  7 14:46 x.sh
```
3. As I am in the `/home/hacker` directory, I execute my shell script, whose execution outputted the flag!!
```bash
hacker@chaining~executable-shell-scripts:~$ pwd
/home/hacker
hacker@chaining~executable-shell-scripts:~$ ./x.sh
Congratulations on your shell script execution! Your flag:
pwn.college{gFmSk0d4h8rynnfAHa5JJD4Dxzb.QX0cjM1wCMxkjNzEzW}
```

## What I learned 
1. When you invoke bash script.sh, you are, of course launching the bash command with the script.sh argument. This tells bash to read its commands from script.sh instead of standard input, and thus your shell script is executed.
2. It turns out that you can avoid the need to manually invoke bash. If your shell script file is executable (recall File Permissions), you can simply invoke it via its relative or absolute path!

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 

# 7. Understanding Shebangs
For this challenge, create a script at /home/hacker/solve.sh that has a proper shebang and outputs "hack the planet". Remember to make it executable, then run /challenge/run to verify your script works correctly!

## My solution
**Flag:** `pwn.college{E3kaVLsyfPGWzf8fXaGZJrKaFFp.0VOzMDOxwCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I make a shell script that has a proper shebang and outputs "hack the planet", as required by the question.
```bash
hacker@chaining~understanding-shebangs:~$ cat > solve.sh <<'EOF'
> #!/bin/bash
> echo "hack the planet"
> EOF
```
3. Then, I checked if the shell script was executable or not. It wasn't!! So, I made it executable using the chmod command.
```bash
hacker@chaining~understanding-shebangs:~$ chmod ugo+x solve.sh
```
4. As required, I ran the `/challenge/run` command, whose execution gave me the flag!!
```bash
hacker@chaining~understanding-shebangs:~$ /challenge/run
Testing your script...
Perfect! Your flag:
Flag: pwn.college{E3kaVLsyfPGWzf8fXaGZJrKaFFp.0VOzMDOxwCMxkjNzEzW}
```

## WHAT I LEARNED 
1. Like in the previous level (because you were invoking your script from the bash shell), but they won't work if your script was being invoked by, say, a program written in Python (or any other language).
2. When a program is invoked in Linux, the Linux kernel first inspects the file to determine how it should be run. This does NOT use the extension (which is why you don't have to name your shell scripts with a .sh extension, or your Python scripts with a .py extension, or so on). Rather, Linux looks at the first few bytes of the file for this information.
3. There are a bunch of different types of programs, but if the program file starts with the characters `#!` (often termed a "shebang"), Linux treats the file as an interpreted program, and the contents of the rest of the line as the path to the interpreter. It then invokes the interpreter with the path to the program file as its only argument.
4. Common shebangs :
a) #!/bin/bash for bash scripts
b) #!/usr/bin/python3 for Python scripts
c) #!/bin/sh for POSIX shell scripts --- this is a more primitive predecessor to bash with fewer features, but more compatibility to non-Linux systems!

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 

# 8. Scripting with arguments 
For this challenge, you need to write a script at /home/hacker/solve.sh that:

a) Takes two arguments
b) Outputs them in REVERSE order (second argument first, then the first argument)

## My solution
**Flag:** `pwn.college{I3LEb0pluoMd0sAaSp7J5ZD-hSr.0VNzMDOxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I create a shell script following the requirements as given in the question and I test whether the conditions are followed or not 
```bash
hacker@chaining~scripting-with-arguments:~$ cat > solve.sh <<'EOF'
> #!/bin/bash
> echo "$2 $1"
> EOF
hacker@chaining~scripting-with-arguments:~$ bash solve.sh pwn college
college pwn
```
3. Then, I run `/challenge/run`, whose execution outputs the flag
```bash
hacker@chaining~scripting-with-arguments:~$ /challenge/run
Correct! Your script properly reversed the arguments.
Here's your flag:
pwn.college{I3LEb0pluoMd0sAaSp7J5ZD-hSr.0VNzMDOxwCMxkjNzEzW}
```

## What I learned 
1. Scripts become much more powerful when they can accept arguments!
2. This might look like: bash (shell script) argument.
3. The script can access these arguments using special variables:
    $1 contains the first argument 
    $2 contains the second argument 

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 

# 9. Scripting with Conditionals
For this challenge, write a script at /home/hacker/solve.sh that:

a) Takes one argument
b) If the argument is "pwn", output "college"
c) For any other input, output nothing
Once your script works correctly, run /challenge/run to get your flag

## My solution
**Flag:** `pwn.college{QNbI4zFw0abOtBwmolHfoy0uYmY.0lNzMDOxwCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. I create a shell script as per the conditions given in the question and run it, to check if its working as required 
```bash
hacker@chaining~scripting-with-conditionals:~$ cat > solve.sh <<'EOF'
> if [ "$1" == "pwn" ]
> then
>   echo "college"
> fi
> EOF
hacker@chaining~scripting-with-conditionals:~$ bash /home/hacker/solve.sh pwn
college
```
3. Then, I run `/challenge/run` , which outputs the flag
```bash
hacker@chaining~scripting-with-conditionals:~$ /challenge/run
Correct! Your script properly handles all the conditions.
Here's your flag:
pwn.college{QNbI4zFw0abOtBwmolHfoy0uYmY.0lNzMDOxwCMxkjNzEzW}
```

## What I learned 
1. In bash, you can use if statements to make decisions.
2. Some things you need to remember :
a) you must have spaces after if, after [ and before ] .
b) if, then, and fi must all be on different lines (or separated by semicolons)
c) the terminator of the if statement is fi (if backwards).

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 

# 10. Scripting with Default Cases
For this challenge, write a script at /home/hacker/solve.sh that:

a) Takes one argument
b) If the argument is "pwn", output "college"
c) For any other input, output "nope"
Once your script works correctly, run /challenge/run to get your flag

## My solution
**Flag:** `pwn.college{Yj993nAedIPT_hR7GYbmucISP28.01NzMDOxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I create a shell script that follows all the requirements given in the question and I test it with multiple inputs
```bash
hacker@chaining~scripting-with-default-cases:~$ cat > solve.sh <<'EOF'
> if [ "$1" == "pwn" ]
> then
> echo "college"
> else
> echo "nope"
> fi
> EOF
hacker@chaining~scripting-with-default-cases:~$ bash solve.sh pwn
college
hacker@chaining~scripting-with-default-cases:~$ bash solve.sh hack
nope
```
3. Then, I executed the `/challenge/run`, which outputted the flag
```bash
hacker@chaining~scripting-with-default-cases:~$ /challenge/run
Correct! Your script properly handles the if/else conditions.
Here's your flag:
pwn.college{Yj993nAedIPT_hR7GYbmucISP28.01NzMDOxwCMxkjNzEzW}
```

## What I learned 
1. The else clause executes when the if condition is false.
2. Note that the else doesn't have a condition --- it catches everything that didn't match previously. It also doesn't have a then statement.

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 

# 11. Scripting with Multiple conditions 
For this challenge, write a script at /home/hacker/solve.sh that:

a) Takes one argument
b) If the argument is "hack", output "the planet"
c) If the argument is "pwn", output "college"
d) If the argument is "learn", output "linux"
e) For any other input, output "unknown"
Once your script works correctly, run /challenge/run to get your flag.

## My solution
**Flag:** `pwn.college{YoWUtOnEBIVbGFXlDQbwaEYRsjS.0FOzMDOxwCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I create a shell script that follows all the requirements given in the question and I test it with multiple inputs, as shown
```bash
hacker@chaining~scripting-with-multiple-conditions:~$ cat > solve.sh << 'EOF'
> if [ "$1" == "hack" ]
> then
> echo "the planet"
> elif [ "$1" == "pwn" ]
> then
> echo "college"
> elif [ "$1" == "learn" ]
> then
> echo "linux"
> else
> echo "unknown"
> fi
> EOF
hacker@chaining~scripting-with-multiple-conditions:~$ bash solve.sh hack
the planet
hacker@chaining~scripting-with-multiple-conditions:~$ bash solve.sh pwn
college
hacker@chaining~scripting-with-multiple-conditions:~$ bash solve.sh learn
linux
hacker@chaining~scripting-with-multiple-conditions:~$ bash solve.sh bet
unknown
```
3. Now, I run the command `/challenge/run`, which reveals the flag as the output 
```bash
hacker@chaining~scripting-with-multiple-conditions:~$ /challenge/run
Correct! Your script properly handles all the conditions with elif.
Here's your flag:
pwn.college{YoWUtOnEBIVbGFXlDQbwaEYRsjS.0FOzMDOxwCMxkjNzEzW}
```

## What I learned 
1. To check multiple conditions, You can use elif (short for else if).
2. Note that you do need a then after the elif, just like the if.
3. Unlike many other languages, bash requires the [ and the ] to be separated from other characters by spaces, otherwise it cannot parse the condition.

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 

# 12. Reading Shell Scripts 
In this level, we will learn to read shell scripts. /challenge/run is a shell script that requires you to put in a secret password, but that password is hardcoded into the script iself! Read the script (using, say, cat), figure out the password, and get the flag!

## My solution
**Flag:** `pwn.college{YR6SApR7XX3I4ZRckcYhbyD15VL.0lMwgDOxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I open /challenge/run, to see what is the password that I need to guess, inorder to get the flag
```bash
hacker@chaining~reading-shell-scripts:~$ cat /challenge/run
#!/opt/pwn.college/bash

read GUESS
if [ "$GUESS" == "hack the PLANET" ]
then
        echo "CORRECT! Your flag:"
        cat /flag
else
        echo "Read the /challenge/run file to figure out the correct password!"
fi
```
3. I was able to find that the string "hack the PLANET" is the password. So, I pass it into /challenge/run, whose execution revealed the flag!!!
```bash
hacker@chaining~reading-shell-scripts:~$ echo "hack the PLANET" | /challenge/run
CORRECT! Your flag:
pwn.college{YR6SApR7XX3I4ZRckcYhbyD15VL.0lMwgDOxwCMxkjNzEzW}
```

## what I learned
1. I learned it is necessary to read a lot of shell scripts and thus, we can incorporate those new ideas into my script.
2. Learned to use multiple concepts in solving one question.

## References
-[pwn.college](https://pwn.college/linux-luminarium/chaining/) -  Chaining Commands manual pages 