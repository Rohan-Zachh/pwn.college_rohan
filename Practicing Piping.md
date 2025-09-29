# Practicing Piping
This module will teach you about input and output redirection. Simply put, every process in Linux has three initial, standard channels of communication:
1. Standard Input is the channel through which the process takes input. For example, your shell uses Standard Input to read the commands that you input.
2. Standard Output is the channel through which processes output normal data, such as the flag when it is printed to you in previous challenges or the output of utilities such as ls.
3. Standard Error is the channel through which processes output error details. For example, if you mistype a command, the shell will output, over standard error, that this command does not exist.

Because these three channels are used so frequently in Linux, they are known by shorter names: `stdin, stdout, stderr`. This module will teach you how to redirect, chain, block, and otherwise mess with these channels.

# 1. Redirecting Output
In this challenge, you must use this output redirection to write the word PWN (all uppercase) to the filename COLLEGE (all uppercase).

## My solution
**Flag:** `pwn.college{09QR3c9oQ1zf9toz02q9_kvzZL7.QX0YTN0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, I wrote the word PWN to the filename COLLEGE, using the command `echo PWN > COLLEGE`, following the syntax of `>` function, which on execution, gave the flag
```bash
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your
flag:
pwn.college{09QR3c9oQ1zf9toz02q9_kvzZL7.QX0YTN0wCMxkjNzEzW}
```

## What I learned
1. You can accomplish redirecting stdout to files with the `>` character. 
2. For command, `echo hi > asdf`, This will redirect the output of echo hi (which will be hi) to the file asdf.

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages 

# 2. Redirecting more input 
In this level, /challenge/run will once more give you a flag, but only if you redirect its output to the file myflag.

## My solution
**Flag:** `pwn.college{Q6QpCa4wXJ2F8zAFTvWWwIyafx_.QX1YTN0wCMxkjNzEzW} `

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. From the challenge's module, I was able to understand that we don't necessarily need echo/extra commands to do stdout. Instead, we can do it directly. So as per question, I redirected the message from `/challenge/run` to the file `myflag`, and then, executing myflag file using `cat` command, the shell revealed the flag.
```bash
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{Q6QpCa4wXJ2F8zAFTvWWwIyafx_.QX1YTN0wCMxkjNzEzW}
```

## What I learned
1. Every program can send output to stdout (normal output) and stderr (error or instructions).
2. The /challenge/run program prints the flag to stdout, but instructions and messages go to stderr.
3. If you redirect stdout to a file (like myflag), the flag will go into that file.

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 3. Appending Output
In this challenge, run /challenge/run with an append-mode redirect of the output to the file /home/hacker/the-flag. The challenge will write the first half of the flag to the file, and the second half to stdout if stdout is redirected to the file.

## My solution
**Flag:** `pwn.college{IIf2akK-oSf5Mu1W-h18UiHYku6.QX3ATO0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. I ran the command `/challenge/run > /home/hacker/the-flag` to get the first part of the flag, as per question. 
```bash
hacker@piping~appending-output:~$ /challenge/run > /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do
the first write directly to the file, and the second write, I'll do to stdout
(if it's pointing at the file). If you redirect the output in append mode, the
second write will append to (rather than overwrite) the first write, and you'll
get the whole flag!
```

3.  Then inorder to get the 2nd part, we need to redirect the output to /home/hacker/the-flag without erasing the first part. For that we use >> and I ran `/challenge/run >> /home/hacker/the-flag`
```bash
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do
the first write directly to the file, and the second write, I'll do to stdout
(if it's pointing at the file). If you redirect the output in append mode, the
second write will append to (rather than overwrite) the first write, and you'll
get the whole flag!
```

4. Now I ran `cat /home/hacker/the-flag`, which gave me the complete flag.
```bash
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
 |
\|/ This is the first half:
 v
pwn.college{IIf2akK-oSf5Mu1W-h18UiHYku6.QX3ATO0wCMxkjNzEzW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>)
rather than *append* mode (>>), and so the write of the second half to stdout
overwrote the initial write of the first half directly to the file. Try append
mode!
```

## What I learned 
1. A common use-case of output redirection is to save off some command results for later analysis
2. > will create a new output file every time, deleting the old contents, which is not beneficial if you want all the output to keep appending to the same file.
3. In such a case, You can redirect input in append mode using >> instead of >.

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 4. Redirecting errors
In this challenge, you will need to redirect the output of /challenge/run, like before, to myflag, and the "errors" (in our case, the instructions) to instructions. You'll notice that nothing will be printed to the terminal, because you have redirected everything! You can find the instructions/feedback in instructions and the flag in myflag when you successfully pull this off.

## My solution
**Flag:** `pwn.college{onboMLakwwLt0LcnETNkkl0vBFf.QX3YTN0wCMxkjNzEzW}`

1. First, connect to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per the question required, I redirected the output and error respectively, by executing the command `/challenge/run > myflag 2> instructions`, which, as given in the question, gave no output. So, I successfully redirected everything as required. Now I opened the myflag file, which gave me the flag
```bash
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{onboMLakwwLt0LcnETNkkl0vBFf.QX3YTN0wCMxkjNzEzW}
```

## What I learned
1. Just like standard output, you can also redirect the error channel of commands.
2. A File Descriptor (FD) is a number that describes a communication channel in Linux. 
3. When you redirect process communication, you do it by FD number, though some FD numbers are implicit.
4. 3 types of FD (we know till now)
FD 0: Standard Input
FD 1: Standard Output
FD 2: Standard Error
5. you can redirect multiple file descriptors at the same time
6. Command : hacker@dojo:~$ some_command > output.log 2> errors.log
 - This command will redirect output to output.log and errors to errors.log.

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 5. Redirecting Input 
In this level, we will practice using /challenge/run, which will require you to redirect the PWN file to it and have the PWN file contain the value COLLEGE! To write that value to the PWN file, recall the prior challenge on output redirection from echo!

## My solution
**Flag:** `pwn.college{47ldA5oCJTP5w5QJS7PgPSlUs32.QXwcTN0wCMxkjNzEzW}`

1. First, connect to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, I redirected the message from `/challenge/run` to PWN file and then passed the message COLLEGE into the file PWN 
```bash
hacker@piping~redirecting-input:~$ /challenge/run > PWN
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
```
3. Now, I redirected the message from PWN file to the input /challenge/run command, which in turn gave me the flag.
```bash
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{47ldA5oCJTP5w5QJS7PgPSlUs32.QXwcTN0wCMxkjNzEzW}
```

## what I learned 
1. Just like you can redirect output from programs, you can redirect input to programs.
2. This is done using < 

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 6. Grepping stored results 
In this challenge, we should do :
1. Redirect the output of /challenge/run to /tmp/data.txt.
2. This will result in a hundred thousand lines of text, with one of them being the flag, in /tmp/data.txt.
3. grep that for the flag!

## My solution
**Flag:** `pwn.college{ITGowsSfpQw6Nce8GGcUafrb0CO.QX4EDO0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. By question, first, I redirected the output of /challenge/run to /tmp/data.txt, using the command `/challenge/run > /tmp/data.txt`
```bash
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
```
3. Now, I grepped the txt file to find the file grepping 'pwn', bcz the flags in these challenges start with 'pwn' keyword, whose execution gave me the flag.
```bash
hacker@piping~grepping-stored-results:~$ grep pwn /tmp/data.txt
pwned
pwning
pwns
pwn.college{ITGowsSfpQw6Nce8GGcUafrb0CO.QX4EDO0wCMxkjNzEzW}
pwn
```
## what I learned 
1. This challenge was a revision of the previous concepts like grep, etc 

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 7. Grepping live output
In this challenge, /challenge/run will output a hundred thousand lines of text, including the flag. grep for the flag

## My solution
**Flag:** `pwn.college{wok_P1X8rE4mASrH4yedqEenx5T.QX5EDO0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. From the question, I passed the output (left) command/file is passed to the (right) command/file, by passing the command `/challenge/run | grep pwn`, which on execution gave me the flag.
```bash
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{wok_P1X8rE4mASrH4yedqEenx5T.QX5EDO0wCMxkjNzEzW} --> Flag
pwned
pwn
pwning
pwns
```

## what I learned 
1. It turns out that you can "cut out the middleman" and avoid the need to store results to a file, like you did in the last level
2. You can do this by using the | (pipe) operator.
3. Standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe.

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 8. Grepping errors
In this challenge, use 2>&1 to redirect the error output. 

## My solution
**Flag:** `pwn.college{0ts47l2liUYrEcpNoZuIouUjcFE.QX1ATO0wCMxkjNzEzW}`

1. First, connect to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. By question, We need to redirect the error output directly using the new command `2>&1 ` and then pipe it with grep function. So, I ran the command ` /challenge/run 2>&1 | grep pwn` by simply following the syntax, whose execution gave me the flag.
```bash
hacker@piping~grepping-errors:~$ /challenge/run 2>&1 | grep pwn
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{0ts47l2liUYrEcpNoZuIouUjcFE.QX1ATO0wCMxkjNzEzW}  ---> THE FLAG 
pwning
pwns
pwn
pwned
```

## What I learned
1. If you wanted to grep through errors directly, The shell has a >& operator, which redirects a file descriptor to another file descriptor.

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 9. Filtering with grep -v
In this challenge, /challenge/run will output the flag to stdout, but it will also output over 1000 decoy flags (containing the word DECOY somewhere in the flag) mixed in with the real flag. You'll need to filter out the decoys while keeping the real flag!

## My solution
**Flag:** `pwn.college{wXrLU4XE39rZaPmKzPRFg2HjCXC.0FOxEzNxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. According to the question, we need to use `grep -v DECOY` to remove all the decoy flags and print the original flag. So, I executed `/challenge/run | grep -v DECOY`, which gave me the right flag.
```bash
hacker@piping~filtering-with-grep-v:~$ /challenge/run | grep -v DECOY
pwn.college{wXrLU4XE39rZaPmKzPRFg2HjCXC.0FOxEzNxwCMxkjNzEzW}
```

## What I learned 
1. The grep command has a very useful option: -v (invert match).
2. While normal grep shows lines that MATCH a pattern, grep -v shows lines that do NOT match a pattern


## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 10. Duplicating piped data with tee
This process' /challenge/pwn must be piped into /challenge/college, but you'll need to intercept the data to see what pwn needs from you!

## My solution
**Flag:** `pwn.college{swJ-Ze2Pjqd_LYqtW8ijcyUStLk.QXxITO0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. After reading the question, you understand there will be some secret argument that we need to pass / condition we need to perform in order to successfully run the command. So first, I use tee to find the secret condition by passing the output passed from /challenge/pwn into a file of my choice 
```bash
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee arg | /challenge/college
Processing...
The input to 'college' does not contain the correct secret code! This code
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the
output of 'pwn' and figure out what the code needs to be.
```
3. Now, I open the file that I created to check the info passed 
```bash
hacker@piping~duplicating-piped-data-with-tee:~$ cat arg
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "swJ-Ze2P"
```
4. So, we got what we wanted. Now, I run the command `/challenge/pwn --secret "swJ-Ze2P" | /challenge/college`, which gave me the flag.
```bash
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret "swJ-Ze2P" | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{swJ-Ze2Pjqd_LYqtW8ijcyUStLk.QXxITO0wCMxkjNzEzW}
```

## What I learned 
1. Inorder to see the data as it flows through between your commands to debug unintended outcomes
2. Command: The `tee` command, named after a "T-splitter" from plumbing pipes, duplicates data flowing through your pipes to any number of files provided on the command line.

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 11. Process substitution for input 
In this challenge, you'll `diff` two sets of command outputs: /challenge/print_decoys, which will print a bunch of decoy flags, and /challenge/print_decoys_and_flag which will print those same decoys plus the real flag. Use process substitution with diff to compare the outputs of these two programs and find your flag!

## My solution
**Flag:** `pwn.college{YXWA2szMyc-zdCQzkSDz-7JZPeC.0lNwMDOxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. By question, we need to use diff command to compare the real flag that is present in the 2nd file, with a decoy in the 1st file, outputing the difference by implementing process substitution. So I ran the command, `diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag )`, which gave the flag as output
```bash
hacker@piping~process-substitution-for-input:~$ diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag )
25a26
> pwn.college{YXWA2szMyc-zdCQzkSDz-7JZPeC.0lNwMDOxwCMxkjNzEzW}
```

## What I learned 
1. Linux follows the philosophy that "everything is a file"
2. Interestingly, we can go further, and hook input and output of programs to arguments of commands. This is done using Process Substitution.
3. For reading from a command (input process substitution), use <(command).
4. When you write <(command), bash will run the command and hook up its output to a temporary file that it will create. This isn't a real file, of course, it's what's called a named pipe, in that it has a file name.
5. You can also use <(command) command multiple times.
6. The main point is : process substitution can make command output appear as files for reading with <(command).

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 12. Writing to multiple functions 
In this challenge, we have /challenge/hack, /challenge/the, and /challenge/planet. Run the /challenge/hack command, and duplicate its output as input to both the /challenge/the and the /challenge/planet commands!

## My solution
**Flag:** `pwn.college{Ijl8Kp7AaCHY0jFXVcbr5-Qms60.QXwgDN1wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, we are required to duplicate /challenge/hack output as input to both the /challenge/the and the /challenge/planet commands, implementing >(command) command. So, I ran the command `/challenge/hack | tee >(/challenge/the) >(/challenge/planet )` , which made the shell to reveal the flag
```bash
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) >(/challenge/planet )
This secret data must directly and simultaneously make it to /challenge/the and
/challenge/planet. Don't try to copy-paste it; it changes too fast.
598623990305112681
Congratulations, you have duplicated data into the input of two programs! Here
is your flag:
pwn.college{Ijl8Kp7AaCHY0jFXVcbr5-Qms60.QXwgDN1wCMxkjNzEzW}
```

## What I learned 
1. you can also use process substitution for writing to commands
2. ou just learned that bash can make commands look like files using process substitution
3. For writing to a command (output process substitution), use >(command).

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 13. Split-piping stderr and stdout
In this challenge, you have:

/challenge/hack: this produces data on stdout and stderr
/challenge/the: you must redirect hack's stderr to this program
/challenge/planet: you must redirect hack's stdout to this program. And you cannot mix stderr and stdout. 

## My solution
**Flag:** `pwn.college{8Flc8erPJ1MEzRUbArqvY8eo2Vh.QXxQDM2wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. Inorder to navigate the output from /challenge/hack to stdout and stderr, I use >(), 2>, and | . 
a) > >(/challenge/planet) tells the shell: take the program’s stdout and write it into the named pipe that feeds /challenge/planet
b) 2> >(/challenge/the) tells the shell: take the program’s stderr and write it into the named pipe that feeds /challenge/the
So, the command that I executed was `/challenge/hack > >(/challenge/planet) 2> >(/challenge/the)`, which turned out to be the right command and gave the flag as output
```bash
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack > >(/challenge/planet) 2> >(/challenge/the)
Congratulations, you have learned a redirection technique that even experts
struggle with! Here is your flag:
pwn.college{8Flc8erPJ1MEzRUbArqvY8eo2Vh.QXxQDM2wCMxkjNzEzW}
```

## What I learned 
1. With this challenge, I understood how to implement | and 2>&1 without mixing stderr and stdout. 

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages

# 14. Named pipes
or this challenge you must create a FIFO at /tmp/flag_fifo, have a reader listening on it, and then redirect /challenge/run's stdout into that FIFO. When /challenge/run writes, the reader will receive the flag.

## My solution
**Flag:** `pwn.college{s9f5wCcWPEBg-mxDVZ5TNb-wrF2.01MzMDOxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, we need to make the FIFO . Then, I started a reader in the background that will print whatever comes through the FIFO
```bash
hacker@piping~named-pipes:~$ mkfifo /tmp/flag_fifo
hacker@piping~named-pipes:~$ cat /tmp/flag_fifo &
[1] 141
```
3. Now, transpose /challenge/run's stdout into the FIFO (this will block until the reader is ready), ie when it writes, the flag will appear in the terminal because cat is reading and printing it.
```bash
hacker@piping~named-pipes:~$ /challenge/run > /tmp/flag_fifo
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo!
Bash will now try to open the FIFO for writing, to pass it as the stdout of
/challenge/run. Recall that operations on FIFOs will *block* until both the
read side and the write side is open, so /challenge/run will not actually be
launched until you start reading from the FIFO!
You've correctly redirected /challenge/run's stdout to a FIFO at
/tmp/flag_fifo! Here is your flag:
pwn.college{s9f5wCcWPEBg-mxDVZ5TNb-wrF2.01MzMDOxwCMxkjNzEzW}
[1]+  Done                    cat /tmp/flag_fifo
```

## What I learned 
1. You can also create your own persistent named pipes that stick around on the filesystem.
2. These are called FIFOs, which stands for First (byte) In, First (byte) Out.
3. Command : mkfifo - You create a FIFO using the mkfifo command

## References
-[pwn.college](https://pwn.college/linux-luminarium/piping/) - Practicing Piping resource pages
