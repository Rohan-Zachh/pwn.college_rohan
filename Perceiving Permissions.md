# Perceiving Permissions
In Linux, files have different permissions. You can check out the permissions of a file or directory using ls -l. 

The key take aways from the output of ls -l are  : 
1. File type : For a directory, it starts with a `d` & For a normal file, it starts with a `-`
2. The permissions : They come in 3 groups of 3 characters:
                     [owner][group][others] — each group shows r, w, x: 
                     r = read (look inside or view file)
                     w = write (change the file or add/remove files in a folder)
                     x = execute (run the file as a program, or enter a directory)
3. Ownership Information : There are two columns showing the onwer and the group related to the file/directory 

# 1. Changing File Ownership
In this level, we will practice changing the owner of the /flag file to the hacker user, and then read the flag.

## My solution
**Flag:** `pwn.college{Mb6bQTWMC_jG8i2NQDzXZydU3Dd.QXxEjN0wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First of all, we need to change the ownership of file /flag from the root to hacker user. For that I use the `chown` command : `chown hacker /flag`and then execute the /flag file using `cat /flag`, on executing, gave me the flag.
```bash
hacker@permissions~changing-file-ownership:~$ chown hacker /flag
hacker@permissions~changing-file-ownership:~$ cat /flag
pwn.college{Mb6bQTWMC_jG8i2NQDzXZydU3Dd.QXxEjN0wCMxkjNzEzW}
```

## What I learned 
1. chown command : For changing the ownership of a file, we can use the `chown` command 

## References
-[pwn.college](https://pwn.college/linux-luminarium/permissions/) -  Perceiving Permissions manual pages 

# 2. Groups and Files
In this level, I have made the flag readable by whatever group owns it, but this group is currently root. Luckily, I have also made it possible for you to invoke chgrp as the hacker user! Change the group ownership of the flag file, and read the flag!

## My solution
**Flag:** `pwn.college{IKweWtRB7AeNfxzN23LV5Z2YohX.QXxcjM1wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. I changed the group of /flag from root to hacker and then I ran the /flag file, which gave me the flag.
```bash
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ ls -l /flag
-r--r----- 1 root hacker 60 Oct  5 19:24 /flag
hacker@permissions~groups-and-files:~$ cat /flag
pwn.college{IKweWtRB7AeNfxzN23LV5Z2YohX.QXxcjM1wCMxkjNzEzW}
```

## What I learned
1. Files have both an owning user and group. A group can have multiple users in it, and a user can be a member of multiple groups.
2. You can check what groups you are part of with the id command.
3. The most common use-case for groups is to control access to different system resources.

## References
-[pwn.college](https://pwn.college/linux-luminarium/permissions/) -  Perceiving Permissions manual pages 

# 3. Fun with Group Names
In this challenge, I'll still allow you to use chgrp, but I have randomized the name of the group that your user is in. You will need to use the id command to figure that name out, then chgrp to victory!

## My solution
**Flag:** `pwn.college{UJgR7RGgIJAHwLQKZHURDtgnSXB.QXycjM1wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I used the id command to figure out the name of the group to which I needed to change the current group section to. On doing so, I understood it was `grp2654`. Then, as per question, I changed the group of the `/flag` and then opened the `/flag` file, which outputted the flag.
```bash
hacker@permissions~fun-with-groups-names:~$ id
uid=1000(hacker) gid=1000(grp2654) groups=1000(grp2654)
hacker@permissions~fun-with-groups-names:~$ chgrp grp2654 /flag
hacker@permissions~fun-with-groups-names:~$ ls -l /flag
-r--r----- 1 root grp2654 60 Oct  5 10:35 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{UJgR7RGgIJAHwLQKZHURDtgnSXB.QXycjM1wCMxkjNzEzW}
```

## What I learned
1. Usually, There is a convention in Linux that every user has their own group, but this does not have to be the case.

## References
-[pwn.college](https://pwn.college/linux-luminarium/permissions/) -  Perceiving Permissions manual pages

# 4. Changing Permissions
In this challenge, you must change the permissions of the /flag file to read it! Typically, you need to have write access to the file in order to change its permissions, but I have made the chmod command all-powerful for this level, and you can chmod anything you want even though you are the hacker user. This is an ultimate power. The /flag file is owned by root, and you can't change that, but you can make it readable.

## My solution
**Flag:** `pwn.college{YABQkXQqGLrgxHbFehoKSnFCLUg.QXzcjM1wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I executed `ls -l /flag` to know the current permission of /flag file. 
```bash
hacker@permissions~changing-permissions:~$ ls -l /flag
-r-------- 1 root root 60 Oct  5 12:13 /flag
```
3. Now, inorder to execute the /flag file, we need to have executing power. For that, I run the command `chmod ugo+rwx /flag` and then I ran /flag file, which revealed the flag as the output.
```bash
hacker@permissions~changing-permissions:~$ chmod ugo+rwx /flag
hacker@permissions~changing-permissions:~$ /flag
/flag: line 1: pwn.college{YABQkXQqGLrgxHbFehoKSnFCLUg.QXzcjM1wCMxkjNzEzW}
```

## What I learned 
1. The permissions : They come in 3 groups of 3 characters:
                     [owner][group][others] — each group shows r, w, x: 
                     r = read (look inside or view file)
                     w = write (change the file or add/remove files in a folder)
                     x = execute (run the file as a program, or enter a directory)
                     - = nothing 
2. chmod ( change mode ) command : Just like ownership, file permissions can also be changed. 
3. In the syntax : chmod [OPTIONS] MODE FILE, You can specify the MODE in two ways: as a modification of the existing permissions mode, or as a completely new mode to overwrite the old one.
4. In this level, we will cover the former: modifying an existing mode. chmod allows you to tweak permissions with the mode format of WHO+/-WHAT, where WHO is user/group/other and WHAT is read/write/execute.
5. When * is used in the FILE position in the syntax of the chmod command, you apply the changes made to all the files in the current directory .
6. Typically, you need to have write access to the file in order to change its permissions.

## References
-[pwn.college](https://pwn.college/linux-luminarium/permissions/) -  Perceiving Permissions manual pages

# 5. Executable Files 
In this challenge, the /challenge/run program will give you the flag, but you must first make it executable! Remember your chmod, and get /challenge/run to tell you the flag

## My solution
**Flag:** `pwn.college{sYXs6P7FZeSmCFTOdVqQy2pUXkm.QXyEjN0wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I run `ls -l /challenge/run` to know the current permission of the file. 
```bash
hacker@permissions~executable-files:~$ ls -l /challenge/run
-r--r--r-- 1 hacker hacker 32 Jan 14  2025 /challenge/run
```
3. From this, I understood that the executable permission is absent in the user,group and other setting. Inorder to invoke the executable permission, I run `chmod ugo+x /challenge/run` and run the command `/challenge/run`, which gave the flag as the output.
```bash
hacker@permissions~executable-files:~$ chmod ugo+x /challenge/run
hacker@permissions~executable-files:~$ /challenge/run
Successful execution! Here is your flag:
pwn.college{sYXs6P7FZeSmCFTOdVqQy2pUXkm.QXyEjN0wCMxkjNzEzW}
```

## What I learned 
1. Linux will only actually execute it if you have execute-access to the program file.

## References
-[pwn.college](https://pwn.college/linux-luminarium/permissions/) -  Perceiving Permissions manual pages

# 6. Permission Tweaking Practice 
This challenge will ask you to change the permissions of the /challenge/pwn file in specific ways a few times in a row. If you get the permissions wrong, the game will reset and you can try again. If you get the permissions right eight times in a row, the challenge will let you chmod /flag to make it readable for yourself :- Launch /challenge/run to get started.

## My solution
**Flag:** `pwn.college{ARM8PRDjbBY3e1KcFDj8QUbeckt.QXwEjN0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. By question, first I must execute `/challenge/run` to start the challenge
```bash
hacker@permissions~permission-tweaking-practice:~$ /challenge/run
Round 1 of 8!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxr-xr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
```
3. According to the instruction, we need to make all the permission classes executable 
```bash
hacker@permissions~permission-tweaking-practice:~$ chmod ugo+x /challenge/pwn
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": rwxr-xr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rwxrwxr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
```
4. In round 2, we need to make the group class writable 
```bash
hacker@permissions~permission-tweaking-practice:~$ chmod g+w /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": rwxrwxr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rwxrwx---
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
5. In round 3, we need to remove the option of reading and execution from other permission file 
```bash
hacker@permissions~permission-tweaking-practice:~$ chmod o-rx /challenge/pwn
You set the correct permissions!
Round 4 of 8!

Current permissions of "/challenge/pwn": rwxrwx---
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w--w----
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
6. In the round 4, we need to remove the option of read and execution 
```bash
hacker@permissions~permission-tweaking-practice:~$ chmod ug-rx /challenge/pwn
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": -w--w----
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w-rw----
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
7. IN round 5, we need to add read option to the group permission file 
```bash
hacker@permissions~permission-tweaking-practice:~$ chmod g+r /challenge/pwn
You set the correct permissions!
Round 6 of 8!

Current permissions of "/challenge/pwn": -w-rw----
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxrw----
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
8. In round 6, we need to add read and execution in the user file 
```bash
hacker@permissions~permission-tweaking-practice:~$ chmod u+rx /challenge/pwn
You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": rwxrw----
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxr-----
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
9. In round 7, we need to remoce the write option from the group section 
```bash
hacker@permissions~permission-tweaking-practice:~$ chmod g-w /challenge/pwn
You set the correct permissions!
Round 8 of 8!

Current permissions of "/challenge/pwn": rwxr-----
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwxrwx---
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
10. In the 8th round, we need to add write and execution option for group permission file 
```bash
hacker@permissions~permission-tweaking-practice:~$ chmod g+wx /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
11. Inorder to make the /flag readable with chmod, I execute the command `chmod ugo+rwx /flag` and then execute /flag, which gave me the flag as output !!!
```bash
hacker@permissions~permission-tweaking-practice:~$ chmod ugo+rwx /flag
hacker@permissions~permission-tweaking-practice:~$ /flag
/flag: line 1: pwn.college{ARM8PRDjbBY3e1KcFDj8QUbeckt.QXwEjN0wCMxkjNzEzW}:
```

## What I learned 
1. I learned how to fully use the command chmod, till what was taught till now, by practicing this module.

## References
-[pwn.college](https://pwn.college/linux-luminarium/permissions/) -  Perceiving Permissions manual pages

# 7. Permissions Setting Practice 
This level extends the previous level by requesting more radical permission changes, which you will need = and ,-chaining to achieve.

## My solution
**Flag:** `pwn.college{sBJi5XuOvN24yaoayIsQ5f3Nrfb.QXzETO0wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. This challenge is basically same as the previous challenge, but we use = in place of +/- and comma intead of grouping all the permission files. I just followed what the challenge wanted me to do at each round and in the end, I changed the permission of /flag to open it/make it readable, which gave me the flag as the output.
```bash
hacker@permissions~permissions-setting-practice:~$ /challenge/run
Round 1 of 8!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": ---r----x
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=-,g=r,o=x /challenge/pwn
You set the correct permissions!
Round 2 of 8!

Current permissions of "/challenge/pwn": ---r----x
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": -w-rwx-w-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=w,g=rwx,o=w /challenge/pwn
You set the correct permissions!
Round 3 of 8!

Current permissions of "/challenge/pwn": -w-rwx-w-
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rw-r-x-w-
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rw,g=rx,o=w /challenge/pwn
You set the correct permissions!
Round 4 of 8!

Current permissions of "/challenge/pwn": rw-r-x-w-
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r-x-w---x
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rx,g=w,o=x /challenge/pwn
You set the correct permissions!
Round 5 of 8!

Current permissions of "/challenge/pwn": r-x-w---x
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": -wx----wx
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
* the world does have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=wx,g=-,o=wx /challenge/pwn
You set the correct permissions!
Round 6 of 8!

Current permissions of "/challenge/pwn": -wx----wx
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": -wxr----x
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=wx,g=r,o=x /challenge/pwn
You set the correct permissions!
Round 7 of 8!

Current permissions of "/challenge/pwn": -wxr----x
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rwx--xr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=x,o=rx /challenge/pwn
You set the correct permissions!
Round 8 of 8!

Current permissions of "/challenge/pwn": rwx--xr-x
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": rwxrw-rwx
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=rw,o=rwx /challenge/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
hacker@permissions~permissions-setting-practice:~$ chmod ugo=rwx /flag
hacker@permissions~permissions-setting-practice:~$ /flag
/flag: line 1: pwn.college{sBJi5XuOvN24yaoayIsQ5f3Nrfb.QXzETO0wCMxkjNzEzW} ---> THE FLAG!!!
```

## What I learned 
1. chmod can also simply set permissions altogether, overwriting the old ones. This is done by using = instead of - or +.
2. You can achieve different ways of setting up permissions by chaining multiple modes to chmod with ,!

## References
-[pwn.college](https://pwn.college/linux-luminarium/permissions/) -  Perceiving Permissions manual pages

# 8. The SUID BIT 
IN this level, we are going to let you add the SUID bit to the /challenge/getroot program in order to spawn a root shell for you to cat the flag yourself. 

## My solution
**Flag:** `pwn.college{Ap3zjHRM-n2YzuiLB6cy9KPIgid.QXzEjN0wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I needed to set the permission bit of the file to SUID. For that I run the command : `chmod u+s /challenge/getroot`. Then I run the command `/challenge/getroot` to finalize the setup of SUID 
```bash
hacker@permissions~the-suid-bit:~$ /challenge/getroot
SUCCESS! You have set the suid bit on this program, and it is running as root!
Here is your shell...
```
3. Now, I run `cat /flag`, whose execution revealed the flag !!
```bash
root@permissions~the-suid-bit:~# cat /flag
pwn.college{Ap3zjHRM-n2YzuiLB6cy9KPIgid.QXzEjN0wCMxkjNzEzW}
```

## What I learned 
1. In some cases where the user wants to do a task, which only root/sudoers can do. For that, the "Set User ID" (SUID) permissions bit allows the user to run a program as the owner of that program's file.
2. The permissions of a file with SUID has a s part in place of the executable bit means that the program is executable with SUID. 
3. chmod u+s [program] - This command sets the SUID bit on a program.

## References
-[pwn.college](https://pwn.college/linux-luminarium/permissions/) -  Perceiving Permissions manual pages

