# Pondering Paths 
This module contains 9 challenges 

# 1. The Root 
To find the flag, from the /pwn location

## My solution
**Flag:** `pwn.college{sMOKRMrV3u2T8sLlroz00172p-N.QX4cTO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. On typing `/pwn`, I will get the flag 
```bash
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{sMOKRMrV3u2T8sLlroz00172p-N.QX4cTO0wCMxkjNzEzW}
```

## What I learned
1. the filesystem starts at `/` . 
2. Under the `/` , there are other directories, configuration files, programs, and, most importantly, flags.
3. This style of path, one that starts with the root directory, is referred to as an "absolute path".

## References 
-[pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering paths / The Root Module pages 

# 2. Program and Absolute paths
This challenge requires you to execute the run file, that is in the challenge directory that is, in turn, in the / directory.

## My solution 
**Flag:** `pwn.college{YeWUCQSSLm5YWMW34DCd9DD1qzI.QX1QTN0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. On typing `/challenge/run`, I will get the flag 
```bash
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{YeWUCQSSLm5YWMW34DCd9DD1qzI.QX1QTN0wCMxkjNzEzW}
```

## What I learned 
1. Filesystem structure basics, the challenge reinforces how files and directories are organized under / and how a program can live in a subdirectory /challenge

## References 
-[pwn.college](https://pwn.college/linux-luminarium/paths/) - Pondering paths / Program and Absolute paths Module Pages 

# 3. Position thy self
This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program.

## My solution 
**Flag:** `pwn.college{kRd36EGlNeR5KJTkzEUNzhu9Tnz.QX2QTN0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. On typing `/challenge/run`, I am given a message 
```bash
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /var directory.
Please use the `cd` utility to change directory appropriately.
```
3. Now, bcz I have changed my current required directory, on typing `/challenge/run`, I will get the flag
```bash
hacker@paths~position-thy-self:~$ cd /var
hacker@paths~position-thy-self:/var$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{kRd36EGlNeR5KJTkzEUNzhu9Tnz.QX2QTN0wCMxkjNzEzW}
```

## What I learned 
1. The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument
2. ~ represents your home directory.
3. For absolute paths, it really doesn't matter what directory you are in

## References 
-[pwn.college](https://pwn.college/linux-luminarium/paths/) - Position thy self Module Pages

# 4. Position elsewhere
This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program.

## My solution 
**Flag:** `pwn.college{YtG-mkzqukA5xUdPeC1i3um25uP.QX3QTN0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. On typing `/challenge/run`, I am given a message 
```bash
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
```
3. Now, bcz I have changed my current required directory, on typing `/challenge/run`, I will get the flag
```bash
hacker@paths~position-elsewhere:~$ cd /
hacker@paths~position-elsewhere:/$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{YtG-mkzqukA5xUdPeC1i3um25uP.QX3QTN0wCMxkjNzEzW}
```

## What I learned 
1. The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument
2. ~ represents your home directory.
3. For absolute paths, it really doesn't matter what directory you are in

## References
-[pwn.college](https://pwn.college/linux-luminarium/paths/) - Position elsewhere Module Pages

# 5. Position yet elsewhere
This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program.

## My solution 
**Flag:** `pwn.college{QPm3HXwLsxjtWA9awj9A5M0n0Au.QX4QTN0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. On typing `/challenge/run`, I am given a message 
```bash
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /var/log directory.
Please use the `cd` utility to change directory appropriately.
```
3. Now, bcz I have changed my current required directory, on typing `/challenge/run`, I will get the flag
```bash
hacker@paths~position-yet-elsewhere:~$ cd /var/log
hacker@paths~position-yet-elsewhere:/var/log$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{QPm3HXwLsxjtWA9awj9A5M0n0Au.QX4QTN0wCMxkjNzEzW}
```
## What I learned 
1. The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument
2. ~ represents your home directory.
3. For absolute paths, it really doesn't matter what directory you are in

## References
-[pwn.college](https://pwn.college/linux-luminarium/paths/) - Position yet elsewhere Module Pages

# 6. Implicit Relative paths, from /
For this challenge, You'll need to run /challenge/run using a relative path while having a current working directory of /.

## My solution 
**Flag:** `pwn.college{oCikf92s4GvHb6mWhnj1WttWKCN.QX5QTN0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. I need to change my current working directory to `/`. So, on typing `cd /` and then executing `challenge/run`, as per the hint given in the question (I'll give you a hint. Your relative path starts with the letter c ) and I got the flag
```bash
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{oCikf92s4GvHb6mWhnj1WttWKCN.QX5QTN0wCMxkjNzEzW}
```

## what I learned 
1. For absolute paths, it really doesn't matter what directory you are in, as you likely found out in the previous three challenges.
2. However, the current working directory does matter for relative paths.
3. Relative path properties:
    a) A relative path is any path that does not start at root (i.e., it does not start with /).
    b) A relative path is interpreted relative to your current working directory (cwd).
    c) Your cwd is the directory that your prompt is currently located at.
4. The .. refers to the parent directory.

## References
-[pwn.college](https://pwn.college/linux-luminarium/paths/) - Implicit relative paths Module pages 

# 7.Explicit Relative Paths, from /
This challenge wants you to run the /challenge/run command implimenting . , in the relative path

## My solution 
**Flag:** `pwn.college{8qMESHlespjAyE94AoNIaVQlFyZ.QXwUTN0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. I need to change my current working directory to `/`. Then I used the relative path `./challenge/run` to get the flag
```bash
hacker@paths~explicit-relative-paths-from-:/challenge$ cd /
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{8qMESHlespjAyE94AoNIaVQlFyZ.QXwUTN0wCMxkjNzEzW}
```

## What I learned 
1. `.`, refers right to the same directory

## References 
-[pwn.college](https://pwn.college/linux-luminarium/paths/) - Explicit relative path Module pages 

# 8. Implicit Relative path
This challenge wants you to explicitly use relative paths to launch run 

## My solution 
**Flag:** `pwn.college{kbju7zlkzQnNJdTRGpALtN3bFr3.QXxUTN0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. I changed my curent diectory to `/challenge` directory. Then I ran `./run` command to get the flag
```bash
hacker@paths~implicit-relative-path:~$ cd /
hacker@paths~implicit-relative-path:/$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{kbju7zlkzQnNJdTRGpALtN3bFr3.QXxUTN0wCMxkjNzEzW}
```

## What I learned 
1. Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path. 
2. This is actually a safety measure: if Linux searched the current directory for programs every time you entered a naked path, you could accidentally execute programs in your current directory that happened to have the same names as core system utilities.

## References 
-[pwn.college](https://pwn.college/linux-luminarium/paths/) - Implicit relative path Module pages 

# 9. home sweet home
In this challenge, /challenge/run will write a copy of the flag to any file you specify as an argument on the commandline, with some contraints as given. You need to refer to the home directory as well

## My solution 
**Flag:** `pwn.college{I1mGZAL17zuQdizT2mGgI2Uoybb.QXzMDO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. Now, I need to copy the flag from `/challenge/run` to a file in the home directory. So, I execute `/challenge/run ~/f` and I get the flag.
```bash
hacker@paths~home-sweet-home:~$ /challenge/run ~/f
Writing the file to /home/hacker/f!
... and reading it back to you:
pwn.college{I1mGZAL17zuQdizT2mGgI2Uoybb.QXzMDO0wCMxkjNzEzW}
```

## What I learned
1. Every user has a home directory, typically under /home in the filesystem.
2. The home directory is typically where users store most of their personal files.
3. ~ is the shorthand for /home/user directory.
4. cd will use your home directory as the default destination.

## References 
-[pwn.college](https://pwn.college/linux-luminarium/paths/) - home sweet home Module pages