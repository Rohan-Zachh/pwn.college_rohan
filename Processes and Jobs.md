# Processes and Jobs 
Computers execute software to get stuff done. In modern computing, this software is split into two categories: 
 a. operating system kernels (about which we will learn much later in system security)
 b. processes, which we will discuss here

When Linux starts up, it launches an init (short for initializer) process that, in turn, launches a bunch of other processes which launch more processes until, eventually, you are looking at your command line shell, which is also a process! The shell, of course, launches processes in response to the commands you enter.

Process is basically a task being executed. In this module, we will learn to view and interact with processes in a number of exciting ways!

# 1. Listing Processes
In this level, I have once again renamed /challenge/run to a random filename, and this time made it so that you cannot ls the /challenge directory! But I also launched it, so you can find it in the running process list, figure out the filename, and relaunch it directly for the flag!

## My solution
**Flag:** `pwn.college{oj9Z1qQLSkAbmg1eMyHP9dfK1Rj.QX4MDO0wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, the challenge wants us to find the filename/location of the renamed /challenge/run directory. And it is given that it is launched , so you can find it in the running process list. So I run the command `ps aux` to list all the running processes and figure out the fileaname. 
```bash
hacker@processes~listing-processes:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.2  0.0   1056   640 ?        Ss   20:28   0:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           7  0.2  0.0 231708  2560 ?        S    20:28   0:00 /run/dojo/bin/sleep 6h
root         132  0.0  0.0   4132  2560 ?        S    20:28   0:00 /challenge/6452-run-11538
root         135  0.0  0.0   2744  1600 ?        S    20:28   0:00 sleep 6h
hacker       137  0.2  0.0 231576  3520 pts/0    Ss   20:28   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p37/bin/bash /run/dojo/bin/ssh-entrypoint
hacker       143  0.0  0.0 231940  4160 pts/0    S    20:28   0:00 /run/dojo/bin/bash --login
hacker       152  0.0  0.0 233600  3840 pts/0    R+   20:28   0:00 ps aux
```
3. For me, I found the process `/challenge/6452-run-11538` suspecious, bcz it was quite similar to the original name. So, as given in the question, I ran the command `/challenge/6452-run-11538` `directly`, which outputted the flag.
```bash
hacker@processes~listing-processes:~$ /challenge/6452-run-11538
Yahaha, you found me! Here is your flag:
pwn.college{oj9Z1qQLSkAbmg1eMyHP9dfK1Rj.QX4MDO0wCMxkjNzEzW}
Now I will sleep for a while (so that you could find me with 'ps').
```

## what I learned 
1. ps command - This command is used to list currently running commands/processes in the terminal. 
2. Each process has a numerical identifier (the Process ID, or PID), which is a number that uniquely identifies every running process in a Linux environment.
3. We also see the terminal on which the commands are running (TTY).
4. The total amount of cpu time that the process has eaten up so far.
5. But these info aren't that useful. Inorder to make them useful, we need to pass some arguments.
6. There are two ways to specify arguments:
  a) Standard Syntax :
        i) -e to list "every" process .
        ii) -f for a "full format" output, including arguments.
        iii) These can be combined into a single argument -ef.
  b) BSD Syntax :
        i)  a to list processes for all users.
        ii) x to list processes that aren't running in a terminal.
        iii) and u for a "user-readable" output.
        iv) These can be combined into a single argument aux.

Therefore, These two methods are : ps -ef and ps aux
7. There are many commonalities between ps -ef and ps aux: both display the user (USER column), the PID, the TTY, the start time of the process (STIME/START), the total utilized CPU time (TIME), and the command (CMD/COMMAND).
8. ps -ef additionally outputs the Parent Process ID (PPID), which is the PID of the process that launched the one in question, while ps aux outputs the percentage of total system CPU and Memory that the process is utilizing.
9. you can pass the w option twice (e.g., ps -efww or ps auxww) to disable the truncation, which occurs when you're not in full screen mode.

## References
-[pwn.college](https://pwn.college/linux-luminarium/processes/) -  Processes and Jobs manual pages 

# 2. Killing Processes
In this challenge, /challenge/run will refuse to run while /challenge/dont_run is running! You must find the dont_run process and kill it.

## My solution
**Flag:** `pwn.college{QK9PT2-qc9eB9i9lP8Y4BD5HwWL.QXyQDO0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, as per question, we need to kill the process `/challenge/dont_run`. Inorder to do so, we need to PID no of the process. For that, I execute `ps aux`.
```bash
hacker@processes~killing-processes:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.0   1056   640 ?        Ss   20:50   0:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           7  0.0  0.0 231708  2560 ?        S    20:50   0:00 /run/dojo/bin/sleep 6h
root         135  0.0  0.0   5204  3520 ?        S    20:50   0:00 su -c /challenge/.launcher hacker
hacker       136  0.0  0.0 231576  3520 ?        Ss   20:50   0:00 /challenge/dont_run
hacker       137  0.0  0.0 231708  2560 ?        S    20:50   0:00 sleep 6h
hacker       139  0.0  0.0 231576  3520 pts/0    Ss   20:50   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p37/bin/bash /run/dojo/bin/ssh-entrypoint
hacker       145  0.0  0.0 231940  4160 pts/0    S    20:50   0:00 /run/dojo/bin/bash --login
hacker       154  0.0  0.0 233600  3840 pts/0    R+   20:51   0:00 ps aux
```
3. From that, we got PID = 136. Now, I run the kill command. And for clarification, I run another command `ps aux | grep dont_run` as shown
```bash
hacker@processes~killing-processes:~$ kill 136
hacker@processes~killing-processes:~$ ps aux | grep dont_run
hacker       158  0.0  0.0 230696  2560 pts/0    S+   20:54   0:00 grep --color=auto dont_run
```
4. This confirms that /challenge/dont_run has been killed. Now, I ran `/challenge/run`, whose execution gave me the flag!!
```bash
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{QK9PT2-qc9eB9i9lP8Y4BD5HwWL.QXyQDO0wCMxkjNzEzW}
```

## What I learned 
1. kill command: In Linux, to terminate a process, you use the kill command.
2. With default options (which is all we'll cover in this level), kill will terminate a process in a way that gives it a chance to get its affairs in order before ceasing to exist.
3. sleep command : sleep is a program that simply stops for the number of seconds specified on the commandline.
4. Inorder, to execute the kill command, we need the PID of the process, which we get from ps.

## References
-[pwn.college](https://pwn.college/linux-luminarium/processes/) -  Processes and Jobs manual pages 

# 3. Interrupting Processes
In this challenge, /challenge/run will refuse to give you the flag until you interrupt it.

## My solution
**Flag:** `pwn.college{g2xCb13iKgRxDhtAP7QqN1p1RmC.QXzQDO0wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I run the command `/challenge/run` to see how the output shows up
```bash
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember,
you can force me to exit with Ctrl-C. Try it now!
```
3. Then, as per the message displayed in the terminal, I hold down Ctrl-C, whose execution gave the flag!!
```bash
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{g2xCb13iKgRxDhtAP7QqN1p1RmC.QXzQDO0wCMxkjNzEzW}
```

## What I learned 
1. Sometimes you just want to get rid of the process that's clogging up your terminal. terminals have a hotkey for this: Ctrl-C (e.g., holding down the Ctrl key and pressing C) sends an "interrupt" to whatever application is waiting on input from the terminal and, typically, this causes the application to cleanly exit.

## References
-[pwn.college](https://pwn.college/linux-luminarium/processes/) -  Processes and Jobs manual pages 

# 4. Killing Misbehaving Processes
In this challenge, there's a decoy process that's hogging a critical resource - a named pipe (FIFO) at /tmp/flag_fifo into which (like in the Practicing Piping FIFO challenge) /challenge/run wants to write your flag. You need to kill this process.

## My solution
**Flag:** `pwn.college{kvv2xQhru1eROhrJGynI9CN68PU.0FNzMDOxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, to check which processes are running, I run the command : `ps aux` to see all the processes.
```bash
hacker@processes~killing-misbehaving-processes:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.0   1056   640 ?        Ss   16:05   0:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-worksroot           7  0.0  0.0 231708  2560 ?        S    16:05   0:00 /run/dojo/bin/sleep 6h
root         137  0.0  0.0   4132  1280 ?        S    16:05   0:00 /bin/bash /challenge/.init
root         138  0.0  0.0   4132  1280 ?        S    16:05   0:00 /bin/bash /challenge/.init
root         139  0.0  0.0   5204  3520 ?        S    16:05   0:00 su -c exec /challenge/decoy > /tmp/flag_fifo hacker
root         140  0.0  0.0   2744  1600 ?        S    16:05   0:00 sleep 6h
root         141  0.0  0.0   2744  1600 ?        S    16:05   0:00 sleep 6h
hacker       142  0.1  0.0  13516  9280 ?        Ss   16:05   0:00 /usr/bin/python /challenge/decoy
hacker       144  0.0  0.0 231576  3520 pts/0    Ss   16:05   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-intehacker       150  0.0  0.0 231972  4160 pts/0    S+   16:05   0:00 /run/dojo/bin/bash --login
hacker       159  0.5  0.0 231576  3520 pts/1    Ss   16:06   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-intehacker       166  0.0  0.0 231972  4160 pts/1    S    16:06   0:00 /run/dojo/bin/bash --login
hacker       175  0.0  0.0 233600  3840 pts/1    R+   16:06   0:00 ps aux
```
3. As per question, we need to kill the file `/challenge/decoy`, for which we got the PID no of the process which is 142. After killing it, I run `/challenge/run` to try and see if I can get the flag. 
```bash
hacker@processes~killing-misbehaving-processes:~$ kill 142
hacker@processes~killing-misbehaving-processes:~$ /challenge/run
Sending the flag to /tmp/flag_fifo!
```
4. Seeing this message, I run `cat /tmp/flag_fifo`, to try and get the flag. But as per the concept, we need to wait/flush the decoy data out of the FIFO file or else decoy values will get outputted. And this is what happened with me. 
```bash
hacker@processes~killing-misbehaving-processes:~$ cat /tmp/flag_fifo
pwn.college{zwCYgMc8Iz9QrAtxZ39j2D4whaunXmi8ENCbBYY5CsJHw8.}
pwn.college{ZNkxulD0QVerCRBJ647DzViwaQtutWjpfORtns9uHrTo1B7}
pwn.college{s3EHSVdRrp3N3UotGOTBlTiJtSBxSLCn6nj4qOiNsC6FgN5}
pwn.college{RUjiQW2uqPHYrnBUTtZpiOl6XzlETt1Uvqdcx-0bR2-TpQ6}
pwn.college{D3uGtUDuVh6juocumQXkqds96.x1xawC0a4M13GUykGam3z}
pwn.college{QncTQUhS.JMsgcpD6VTHbiNsgiWZYzfjxWm2Ga3UlKoVsdH}
pwn.college{g.wBKzHVWpHgWXlsLrL1JUH.FUfjHlGxwZ-Hx935WwTfIAU}
pwn.college{lig4.ed4OrSSBoZ6f.AThsUIpeeFBJCWvqV7M.MYLP7vx0z}
pwn.college{.jbVcoT7UGSxidaA98kmM4l05qctVrEgwYxrot6lhlbUe9U}
pwn.college{itwH.aFm29ju80l36WZbyp8WuoGl.vMshPPqFuMSjyHawX8}
pwn.college{azdP2deWahpOvSTOiph0Lgs8cMnf14Ek--ZSQltjgkpLbtV}
pwn.college{3l9IL2CvgICiCwc0UIy3zJ8qIcL8fKPSWJ8sN6kX0czEznk}
pwn.college{whhx-nzV9w2i.s9pqEZ5.OGHaxTn1VqDG2kgDTZwToC.WET}
pwn.college{bzZwi.WqhILyj4GQCkYFAEGVJfj8tjy8tPnhPp2yIZpNMR0}
pwn.college{K1SOW4JuD3DlIyBvXfUvZtZPAxsMRXCHsOLFMqZAVqUnSJz}
pwn.college{9UFAvGWNalxVinrz0CXlcUe9ut3.CzSuvVVvn30EhUE4VhX}
pwn.college{ViG0FLckc2rsrmsp2eBh55b1djfRO2aa3vkly7n6f4ucOBD}
pwn.college{OckZRfWHUxZpT4VhZwzKOTiwBcSxTzXbXExo5gtGaC.UOB9}
pwn.college{tcHLSjxos17QsslVGuvvqhaIy6zb2E6IYrjXwbmpPH3aIHM}
pwn.college{IciYF6M27TxAHSh2cTgUGkTCG0mrK1bhuFZY7xJrhzRHK.s}
pwn.college{nxcK.Y7w1c5bN-Xnh5P.pOBefykWmiKFhO8u.zGZdUsZtEw}
pwn.college{pvjro7tUvhU8xpAAcj6MlywqEEdDiIFnP-J.Kjl7QGzyDNo}
pwn.college{Vq56fXQVsz2mWIN5lZrECw1RQHgUt.Z78AoKbXM03Wsm0sZ}
pwn.college{dRpJr-GV3AGrIin..oUFr4Ru3jifOoGWx8UAjuW6UmGQDRp}
pwn.college{VUHFIB0bAS93rg-61f33CI3A.McvJRyQRwHs7Sgbk9mvWFv}
pwn.college{31f-RiSbSV-kJtof67U8qcwJEJoTSC2n6IeSLo6hFSQC-uF}
pwn.college{kIpAUzN66NF2KV7BvKkxQIJ6vnxNpnvn2BiobXgUtiGj5eR}
pwn.college{xAfQxo1eXRZrkxjZxPLrFxFCI6wfWjwUQ7uKv7q8WFOYQF9}
pwn.college{KSzs6bNhZiLkqQQIDZvZaIpm2F.gNn6ylbWH3EA1sgLJ3jc}
pwn.college{5F3B.QHajX1wifUdvW7kQCKOUx8WuDWPwIP5fEpDblyVKXe}
pwn.college{mJiZcUfi2tZ5rsCTZzFHZXptMq6HM0XPU-KYPVs4q6Pa2Rv}
pwn.college{820LoI6my3ywKC5MqMtbfGI34F0zTUHSDhxVp41ks0FV.4u}
pwn.college{-yq0.8bwSq-ksUWyN2WdI9s7dohikociDbeyDIXXmLgRoO7}
pwn.college{T21htNg1bzIlvnmwHiGfEweo6bPo8gRqzPbxUJuNkO8SQ3O}
pwn.college{sHtP4bwNEdB8RYsyYq1pqvyxcUaYSjH1oH5.f0OdD.iB.4D}
pwn.college{kY85yBGIlF1NJSiNeQKvV81VPlPWWp-YInlYq.h7RpRH8Bj}
pwn.college{9BUkZp.tOhqqeRGpxDXT24UQoAU3AEVcqMhMWq-qF37OGRh}
pwn.college{PmonqzPCzdg2fI5e8tM1x3t9Ld5ID2lBHtQrtmLxXzgCyVW}
pwn.college{XrYJpf6Ddk-mFcck3Kil8C1rMhq2A1hPWRnrultVmU3ef7w}
pwn.college{ltMZD.MSWD62eriH4Ri3iwY39PmXetct3NN3xk-8cM0.NIr}
pwn.college{4bC1Vw.UOXE1SrbqAANtjtYuAETizM7vABMd42vRJyKl7y5}
pwn.college{tc6DSdMI77kc8YRqMHpiX2Xh436osNf3OvZjBshI79HsOca}
pwn.college{CFyiw12YbIBpKtCdJOClXmHOAlf0k0Sk5Y5wXZgb0UN1nC-}
pwn.college{LetMg9XodSLlUfHpdKDKmGOXJdLYLlJG08HLEhjJgat-S7M}
pwn.college{Sf8ICxp5vvIxNjCw7SWGdMt2IUYGjumKd94DFZ.WxRNFJx1}
pwn.college{Wdjz2LpXJgif8k-VHW0QQrg-BFu.KiUkxsQSqqrnTEg8zfJ}
pwn.college{Cse9MhotN5KgIBYYqw3c0Ll1kTaklfQJ37rsSGoZ8JUxMVS}
pwn.college{x5STMzFP6Oqp5roS4.UYLmuP-Gi8Z7WwD0.pDe-gSJgme5E}
pwn.college{iAuK4Jo0T7R0BnLRdaByhndHOIGuJWuB9X8hX3c8RBMIcob}
pwn.college{I-w81COp83YaA3ay.fFQA3bd9HJ50vvKxDr0noeaQ-v4rTZ}
pwn.college{2O9WwiYqUN45Ho0mCKLgbve8xVeH0ix1rqCPKrk82ZyRur6}
pwn.college{GndNtYl3Gdn8coTHLrLZYZYZsclXBLvUkWNudGGA1qFApBl}
pwn.college{FrJW00yXn0olDWtGOH-G0tp9w3qg2M4qKXzFlurWfZfuksQ}
pwn.college{XJ5QCAOpFcZSgnNHVx8h97HE9gCM2XlpneX4oSnbzRzZSaT}
pwn.college{J4HUtidASr0PZ9kZSpDwLezCA359UtIP8c5j0Mrzj69jtSG}
pwn.college{qSgwJZkOuPA3znv3yVg5Ybmsh6vwYXw0p4R5v2btDxmn2w4}
pwn.college{WEuD8e66GV9bXDvxWlmKxzZ9qMHgEYCVxeJGQyygWEsACiF}
pwn.college{Dqtg4TH64Wu7G6je3llb3a9ulWCM47gjyKp.eRpTVdO.pQm}
pwn.college{eclVrASFCygaZlLa9YAgklhzUQ4nVQe2cN5dL4WHyRiaIit}
pwn.college{Cb6vLPsdZUXokGT4YV8D9u7h9cQQEaHNAoDTA3GtFGSUrQg}
pwn.college{e57GqeVec5QQBSNzSX3zjOMP-iAOpwKnPEahgH0QGkWh8yL}
pwn.college{3agLd1wyqosaEbOnq7gI5GB86k8-ZiW14WFqtrw9uxuQigg}
pwn.college{I6pK9QYqHKQdK0lI2uipwEclEhE4-YmRYKdUyFehz6xZKXj}
pwn.college{5wKlwmOcieHlGMis234Y4lsjjSQkzJPXqw3hcbtZtrmQTd3}
pwn.college{ysUG520IYPmjH-KbAHEJuYwN-R-fFJsfAXNKzPK90IOsbiW}
pwn.college{I8dtNt7-XobClCJrDmOqqiTW4-kXg8iAe4H6rci7itGl42G}
pwn.college{Tv1F6UwqqDFsHsJhhJE1OTkrqyFeCqWluxVVmaGvHjgVw.C}
pwn.college{rjjjSIpwXSGQTt3kO1pa1W2a-4DnVWvJnf3GU.VVWH4v5jn}
pwn.college{kSeOa1IWGC278XDYGqLUJJvED2A9jvRKw7KxIQLwxZWvNkT}
pwn.college{4eTuC8-Ypmf3xUdPsPOPR-humT2RRSAHoFnjq3XpRO8eAkO}
pwn.college{eD7I4AMo7csFZYfeXQBeJ2LCu343stDXIY0x3emz6D8kLMk}
pwn.college{xJWOi-9vUk0ZA.d6KLYrIuDbSeQ49xrWXHoAHXQvNIXPC92}
pwn.college{EDxjaR4aDW.-KYhnjzOPCxePc25fup5..9glDWx2KCSIvzF}
pwn.college{2i.ftwMFk7inm24zCEik6a.mUhoBzjco-LB2Qg2GFeAzbQz}
pwn.college{CLnwUad3Z4q6kX7.IL1L-ozoQDLpvVJmUskIAOYd1-EYdFF}
pwn.college{3LwuhvgcSuZCZV6p.q3AXdNp10hP8rYlh9DNBN2h6fjrWKY}
pwn.college{ckN.QeUYtNWKoz2Y6CR4vlZGElGucQOh.cBnRXkEbGwDxj0}
pwn.college{585Eg.JPwDcc6XAJ2N7EhPMC56tjzs80q.1qGzsHOD7x5jL}
pwn.college{bsoi.23CJ8Es5-eOiOl42WGBPbCex-FBYHy5TCB2T980HCo}
pwn.college{YO8NHoNnXBkWhmUzmaq0pGBrUL6kwQga57tX.kBEpTSOgwf}
pwn.college{FMxLr48gBt3Qox850GYViI5NODIBVzCWbv7dMaYC7jvT-gE}
pwn.college{Ar-JMQD.XEMsGsyHDjH6RJh2cAY5gj1zKpypPUmAc4D3d9Z}
pwn.college{3AQNx3I6W4PnMDf1crc8DDmv.kyKjBFTXXXymbel.Mfh0-M}
pwn.college{6jOQk9tcGmrlmqa1TwoeZYat90woqTESHDLP3MZgZpQbXJ5}
pwn.college{zKyOBTvVbGstHZNS97foHiu-gOWNeb6Xv-Uf.M2OplqrCVd}
pwn.college{zZybAgW-Uy2zbsq2SqlASAh4nUcHtpluei884vIdPw0AwbB}
pwn.college{JL9AdH45vMpPkmxt0mLM74JfaOpavB.HAle7xyKgzXeVJVS}
pwn.college{Q9jDPvcAiquD-nDlUEpIWfFgjsm05BF09gcIUOQmZAgLrMu}
pwn.college{.GJYSYdNeOQXW9-XVozf7Ifk7c27FAkUOKIKCq8BNeCotS2}
pwn.college{0WzC.uV8zG51k0eDsg..n.LqrMEfQHSILvSo3oyWQDda7wN}
pwn.college{Y-gjBzI3No1HfBnjI0jvk828FWpDrp32O3H8L-ZrwEISZw9}
pwn.college{kvc9SxaGA4z3OObbZ5GQluU1aAn2KT4LgDWLG.lSHXnWbEg}
pwn.college{RSdmWMby5MhF34ZJdNkFHx6JbDB-0lFf7lcCUo4xNfPWN6C}
pwn.college{YaJkGT0DHHXAyVlZffHeKaC2r0Lp1DGCu.BOcba570DswwE}
pwn.college{N6gNrhTjirOHS5x2L0FyQAaeG0.Zup0BCBzfO-mETevSUsk}
pwn.college{hG530ahP3YfHc5d0U8q3L7SyHDXmQDLeChPeTGnmGKA4yWT}
pwn.college{-1fG57CQj53mv09gPTJxmcysEVh7BTJTQAkV9799HRF9J4z}
pwn.college{tHFtW3DxxPmJ8iTW610hFAcV1YNF8nGjf1.C21yk.n5vDLZ}
pwn.college{bR1XvnDjbue-exNEBtwZQ0sOmt5eV7t6zNtOoOXjQnWftP5}
pwn.college{qAp4hoB2Kcdevii5xEdghLOStxATfLEe7Tn4SYOY7ss1DSS}
pwn.college{ZZN8ZLEBiPlPIWgHJPJZGGlsvz4G-xKrdswSWNoOv1w9jrv}
pwn.college{-xVUsizW7ZUIjqCAGgoBVqRemIPzGGzUS4F-l97KOJpiE6s}
pwn.college{wI-H0cqT57m8D4L3fBTP68ofHZWMnLdbqImrnaSNbuyjQk2}
pwn.college{hxYrp1Kq31TzS8f.X.AcJf4bhyaSvH9KzpSbZmuCDy.G4FF}
pwn.college{sGoGnAgQRH9ZVgmBLxVM5.ccQjQ3Fxm.l9ENrlVa7hlYe6q}
pwn.college{dKSsbuqPcJK-wHRw3lh5nlqDsnTfcy2bl07r3cQgNAFTr5k}
pwn.college{pEbxqEb.65RlNbAr8Z3QJ9Z.id804P7cVfrBlAcYL07O2vo}
pwn.college{cOJ4yJRBneamazKA1O9UVPludokArXarkXF1neqh7wQA2e-}
pwn.college{jStBLmr3yJZhVrUjsi2vVTJ-gMmR8FaZn9zW114OJUwZ7ay}
pwn.college{y1Y6LurHc8OmwGZHjyYZ3g7xNqJv-E5nlWUCgYuKmNbefJg}
pwn.college{uRjgt.DHDJMjDC9sXmIkNdoHIbI5OT.fsp32ISbWO6Bmvk.}
pwn.college{IZ5tWGYewBBfjlMXtV1uu5APeElC5B0oDJZEa56bZU6liH9}
pwn.college{yzfJD.tZbLQ6bdVQ0vxmuV3C.Uq5mMpRUaJCPNUQb.vpFuR}
pwn.college{01bs4AJu0eZHtS5zL0ee52pklWjbVcCTr-u14bel7RMfhx2}
pwn.college{usW0vPIKA86OuZhsFNGrpANqtQYA.lVM9EeoojCVIt6c7AR}
pwn.college{3n1YuSliI8pFFrdxwE-EbhWjTiczjRaPN8CsFpB7YxaB1Yi}
pwn.college{w4l8Xy6NUfxiU-4i.CX6ZcyqPHzUtCHMgLS1QmGStaM4nY6}
pwn.college{hPE1rF4ZHSS5kMQ.gs5ZVV6Jl1Fob2UIY3k94On8dIkHLg8}
pwn.college{zlXF9X2F7qH8dbAavutqoaqjLm8WA2brQWMI5y10d3CEhYz}
pwn.college{5T-30dWaxRirpF7HwneSEaBxT0rcNZFei1tqvo1.HeMxTd7}
pwn.college{eJj7iH9A2cQOWmNMNu9uxhF55gzuEx6mYDMBiGgJNdLCFIa}
pwn.college{LgFQnmQiYlFvUf3wIFZxuoQS8PtTOC92.hGunU0uO4RL8x7}
pwn.college{BvEIJF0AygflBrHnNk2wyrvv7W8e58OCNXdlJFOlGC7nc4S}
pwn.college{CA40JG9tW1rxBw4RBxuu3KOfBSuk5RKN4PkXZvSSKxGh7up}
pwn.college{gdQ9GcAGhiYw.f5-7n1D2QYtVdZ3h0-RNnHi4y8geBNeSM6}
pwn.college{2wITcYKmKOyJ17lspuWI4CjX2Fz6mNq.SRJTfkR4Wkx3Zp2}
pwn.college{zFWnCvHDfRjnwZNWAUuM0kR32GyEjd.5d2mjUrhV.4DFpB4}
pwn.college{Vn4x9RtEuUwCxHaSEsBYI.W9iOh-EtVM9XS2UbgGh-zrjMS}
pwn.college{GbZYDHIEpz6hB1KBKMESNcXfdehOkJQmL.7kst76KUjrEBu}
pwn.college{ACLK-exiSj6bHqaegbmddEgvd-hOh-EhOVZSxRbc0krpamD}
pwn.college{-uwAuVrjWY9AR14FrBMnK8pb.oAwHBtbG5A.hSVJr4g6wWF}
pwn.college{o.bJ1Hov7QhZPinX6wEP56YyZauxuqvkDrOcaZjO0JfPlHt}
pwn.college{pDXb18EYrT5iZUZgiWIens0y9QMqWI5.h4c9wrIkCikOTCt}
pwn.college{hTC912hgoHZl2K5YQGbiHldhVL65ind6tiI4ldIDULT9lT0}
```
5. Now, as this didn't work out, I went back to the Practicing Piping question. From there I got an indea to pass the info of /challenge/run to /tmp/flag_fifo using > operator. On doing that :
```bash
hacker@processes~killing-misbehaving-processes:~$ cat /challenge/run > /tmp/flag_fifo
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo!
Bash will now try to open the FIFO for writing, to pass it as the stdout of
/challenge/run. Recall that operations on FIFOs will *block* until both the
read side and the write side is open, so /challenge/run will not actually be
launched until you start reading from the FIFO!
```
6. From the message, I felt like I should open up the `/tmp/flag_fifo` file and see if the real flag got passed into it. So, I run the the command `cat /tmp/flag_fifo` and this led to the execution of the real flag!!
```bash
hacker@processes~killing-misbehaving-processes:~$ cat /tmp/flag_fifo
Sending the flag to /tmp/flag_fifo!
pwn.college{kvv2xQhru1eROhrJGynI9CN68PU.0FNzMDOxwCMxkjNzEzW}
```
## What I learned 
1. A FIFO can “hold” data temporarily (buffered). Even after killing the writer, the data already in the buffer will still flow to the reader (that’s why you saw decoy outputs for a bit). Waiting or flushing lets the “bad data” clear out, after which we can get the flag from the real flag file. 

## References
-[pwn.college](https://pwn.college/linux-luminarium/processes/) -  Processes and Jobs manual pages 

# 5. Suspending Processes
This level's run wants to see another copy of itself running and using the same terminal. How? Use the terminal to launch it, then suspend it, then launch another copy while the first is suspended!

## My solution
**Flag:** `pwn.college{g6L8Fv6pxyBp6PVAKbEq1CL7zsW.QX1QDO0wCMxkjNzEzW}`
1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I run the command `/challenge/run` inorder to run the command in the terminal for the 1st time. 
```bash
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         138     129  0 19:30 pts/0    00:00:00 bash /challenge/run
root         140     138  0 19:30 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can
background me with Ctrl-Z or, if you're not ready to do that for whatever
reason, just hit Enter and I'll exit!
```
3. In order to introduce a second copy of the command, we need to suspend the currently running identical command. So, in order to do that, I use Ctrl-Z, whose execution suspends the 1st identical command. Now, I run `/challenge/run` again, so that 2 copies of the same command is now present in the current terminal. Such that the condition of the challenge is satified and it should output the flag on execution, which it did !!
```bash
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root         138     129  0 19:30 pts/0    00:00:00 bash /challenge/run
root         145     129  0 19:31 pts/0    00:00:00 bash /challenge/run
root         147     145  0 19:31 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{g6L8Fv6pxyBp6PVAKbEq1CL7zsW.QX1QDO0wCMxkjNzEzW}
```

## What I learned 
1. You can suspend processes to the background with Ctrl-Z

## References
-[pwn.college](https://pwn.college/linux-luminarium/processes/) -  Processes and Jobs manual pages 


# 6. Resuming Processes
This challenge's run needs you to suspend it, then resume it.

## My solution
**Flag:** `pwn.college{wQiD0v5rYkpAAIIsyAzwn8efCSh.QX2QDO0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I run the command `/challenge/run` to invoke it to carry out the challenge. Then, I am asked to susped the process, which I do by executing Ctrl-Z. And by question, I need to resume it to get the flag. So, I execute the command `fg`, whose execution outputted the flag.
```bash
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{wQiD0v5rYkpAAIIsyAzwn8efCSh.QX2QDO0wCMxkjNzEzW}
```

## what I learned 
1. Inorder to resume the command that you had suspended, your shell provides the fg command, a builtin that takes the suspended process, resumes it, and puts it back in the foreground of your terminal.

## References
-[pwn.college](https://pwn.college/linux-luminarium/processes/) -  Processes and Jobs manual pages 

# 7. Backgrounding Processes
This level's run wants to see another copy of itself running, not suspended, and using the same terminal. How? Use the terminal to launch it, then suspend it, then background it with bg and launch another copy while the first is running in the background.

## My solution
**Flag:** `pwn.college{kiN80b_oF8UupeNrreEImipa3q1.QX3QDO0wCMxkjNzEzW}`
1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. I execute the command, `/challenge/run` to get things started, which gave me the message, as shown below:
```bash
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         138 S+   bash /challenge/run
root         140 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the
background, and then launch a new version of me! You can background me with
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to
do that for whatever reason, just hit Enter and I'll exit!
```
3. As per question, we need to suspend the process and then resume it in the background. For that, I execute Ctrl-Z and bg respectively.
```bash
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~backgrounding-processes:~$


Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out.
```
4. Now, I ran the command `/challenge/run`, whose executino gave me the flag, bcz we have satisfied every condition as given in the question.
```bash
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root         138 S    bash /challenge/run
root         148 S    sleep 6h
root         149 S+   bash /challenge/run
root         151 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{kiN80b_oF8UupeNrreEImipa3q1.QX3QDO0wCMxkjNzEzW}
```

## What I learned 
1. You can also resume processes in the background with the `bg` command.
2.  This will allow the process to keep running, while giving you your shell back to invoke more commands in the meantime.

## References
-[pwn.college](https://pwn.college/linux-luminarium/processes/) -  Processes and Jobs manual pages

# 8. Foregrounding Processes
In this level, you will walk through - you can foreground a backgrounded process with fg just like you foreground a suspended process.

## My solution
**Flag:** `pwn.college{8TYdaopMOKPZ20Y3lBfTO_3s3sN.QX4QDO0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I ran `/challenge/run` command, to see what pops up. For that, the output is :
```bash
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the
background, and *then* foreground it without re-suspending it! You can
background me with Ctrl-Z (and resume me in the background with 'bg') or, if
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
```
3. As per the instructions, I run Ctrl-Z and then execute bg to run the process in the background, whose execution gave a message.
```bash
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:~$ bg
[1]+ /challenge/run &
hacker@processes~foregrounding-processes:~$


Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out. After that, resume me into the foreground with 'fg';
I'll wait.
fg
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!
pwn.college{8TYdaopMOKPZ20Y3lBfTO_3s3sN.QX4QDO0wCMxkjNzEzW}
 
```
## What I learned 
1. You can foreground a backgrounded process with fg just like you foreground a suspended process

## References
-[pwn.college](https://pwn.college/linux-luminarium/processes/) -  Processes and Jobs manual pages


# 9. Starting Background processes 
In this challenge, Launch /challenge/run backgrounded for the flag

## My solution
**Flag:** `pwn.college{oVbQImie5C0fZRI6X46tA1QaBkc.QX5QDO0wCMxkjNzEzW}`
1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. For backgrounding the required commmand, I follow the syntax of directly backgrounding, ie by passing the command `/challenge/run &`, whose execution gave me the flag.
```bash
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 138
hacker@processes~starting-backgrounded-processes:~$

Yay, you started me in the background! Because of that, this text will probably
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{oVbQImie5C0fZRI6X46tA1QaBkc.QX5QDO0wCMxkjNzEzW}
```

## What I learned 
1. You can background a process, directly (without using suspending process and all), by just appending a `&` to end of the command.

## References
-[pwn.college](https://pwn.college/linux-luminarium/processes/) -  Processes and Jobs manual pages


# 10. Process exit commands
In this challenge, you must retrieve the exit code returned by /challenge/get-code and then run /challenge/submit-code with that error code as an argument.

## My solution
**Flag:** `pwn.college{gphkLIrdSSg0LVDSEznscGP2uQJ.QX5YDO1wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, in order to retrieve the exit code returned by /challenge/get-code, I run the command : `echo /challenge/get-code $?` to get the code:
```bash
hacker@processes~process-exit-codes:~$ echo /challenge/get-code $?
/challenge/get-code 125
```
3. Then, I ran /challenge/submit-code with that error code as an argument, as given in the question (code=125), whose execution outputted the flag!!
```bash
hacker@processes~process-exit-codes:~$ /challenge/submit-code 125
CORRECT! Here is your flag:
pwn.college{gphkLIrdSSg0LVDSEznscGP2uQJ.QX5YDO1wCMxkjNzEzW}
```

## What I learned 
1. Every shell command, including every program and every builtin, exits with an exit code when it finishes running and terminates.
2. You can access the exit code of the most recently-terminated command using the special ? variable (don't forget to prepend it with $ to read its value!)

## References
-[pwn.college](https://pwn.college/linux-luminarium/processes/) -  Processes and Jobs manual pages
