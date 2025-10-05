# Untangling Users
1. There are MANY users on a typical Linux system! The full list of users on a Linux system is specified in the /etc/passwd file (named so for historical reasons --- it doesn't actually hold passwords anymore)
2. Each user info contains, separated by :s, the username, an x as a placeholder for where the password used to be, the numerical user ID, the numerical default group ID, long-form user details, the home directory, and the default shell.
3. One important user is root: the system administrator.

In this module, we will learn the intended ways to switch users to administer the system, and have fun along the way. 

# 1. Becoming root with su
THIS challenge (and only this challenge) does have a root password. That password is hack-the-planet, and you must provide it to su to become root! Go do that, and read the flag

## My solution
**Flag:** `pwn.college{cVGAGOdbOISYB_weryJfA8dTvkV.QX1UDN1wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, I execute the su command and enter the password as given in the question. Now running as the root, I `ls` to check the files in this directory. On doing so, the not-the-flag file is highlighted, which made me to choose to for the execution. On executing it, I got the flag !!!
```bash
hacker@users~becoming-root-with-su:~$ su
Password:
root@users~becoming-root-with-su:/home/hacker# ls
'?1'   COLLEGE   PWN   arg   f   foo.1x.dvi   foo.1x.flag   instructions   myflag   not-the-flag   stdout   the-flag
root@users~becoming-root-with-su:/home/hacker# cat not-the-flag
pwn.college{cVGAGOdbOISYB_weryJfA8dTvkV.QX1UDN1wCMxkjNzEzW}
```

## What I learned 
1. Oftentimes, you, as the owner of your computer, need to use root access to administer it and and there are two utilities that exist for this purpose: su and sudo.
2. In this challenge, we will cover the older one, su (the substitute user command). This is not typically used to elevate to root access anymore, but it is an elegant utility from a more civilized time, and we'll cover it first.
3. Because it has the SUID bit set, su runs as root. Running as root, it can start a root shell.
4. Of course, su is discerning: before allowing the user to elevate privileges to root, it checks to make sure that the user knows the root password
5. Modern systems very rarely have root passwords, and different mechanisms (that we will learn later) are used to grant administrative access.


## References
-[pwn.college](https://pwn.college/linux-luminarium/users/) -  Untangling Users manual pages 

# 2. Other users with su
In this level, you must switch to the zardus user and then run /challenge/run. Zardus' password is dont-hack-me. 

## My solution
**Flag:** `pwn.college{Y8N24TZLoZ6CkzOJiVaXNLtr21o.QX2UDN1wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. Following what the question wants us to do, First I su into the user id zardus, entering the password, as given in the question. Then, I ran `/challenge/run`, whose execution gave me the flag!!
```bash
hacker@users~other-users-with-su:~$ su zardus
Password:
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{Y8N24TZLoZ6CkzOJiVaXNLtr21o.QX2UDN1wCMxkjNzEzW}
```

## What I learned
1. With no arguments, su will start a root shell (after authenticating with root's password)
2. With argument, ie, you can also give a username as an argument to switch to that user instead of root.


## References
-[pwn.college](https://pwn.college/linux-luminarium/users/) -  Untangling Users manual pages 

# 3. Cracking passwords
This level simulates this story, giving you a leak of /etc/shadow (in /challenge/shadow-leak). Crack it (this could take a few minutes), su to zardus, and run /challenge/run to get the flag.

## My solution
**Flag:** `pwn.college{4CedTSytaDCMIHUaBCnpXNKLW2g.QX3UDN1wCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. By question, we need to enter into the zardus user id. For that, we don't need the password as of right now. For that, I first get the hash value of the password for zardus from the `/challenge/shadow-leak`, by running the command `cat /challenge/shadow-leak`
```bash
hacker@users~cracking-passwords:~$ cat /challenge/shadow-leak
root:*:20182:0:99999:7:::
daemon:*:20182:0:99999:7:::
bin:*:20182:0:99999:7:::
sys:*:20182:0:99999:7:::
sync:*:20182:0:99999:7:::
games:*:20182:0:99999:7:::
man:*:20182:0:99999:7:::
lp:*:20182:0:99999:7:::
mail:*:20182:0:99999:7:::
news:*:20182:0:99999:7:::
uucp:*:20182:0:99999:7:::
proxy:*:20182:0:99999:7:::
www-data:*:20182:0:99999:7:::
backup:*:20182:0:99999:7:::
list:*:20182:0:99999:7:::
irc:*:20182:0:99999:7:::
gnats:*:20182:0:99999:7:::
nobody:*:20182:0:99999:7:::
_apt:*:20182:0:99999:7:::
systemd-timesync:*:20357:0:99999:7:::
systemd-network:*:20357:0:99999:7:::
systemd-resolve:*:20357:0:99999:7:::
mysql:!:20357:0:99999:7:::
messagebus:*:20357:0:99999:7:::
sshd:*:20357:0:99999:7:::
hacker::20357:0:99999:7:::
zardus:$6$EbGSVREkxBCLL2n6$dmihhi/1O9WtC0HyeXl4wCWLts7iksWXQVQyFRg9wAcvnu.c3nhZai6BxO/WCCViwOynCDvsmJ7J2aHYoNxIC1:20366:0:99999:7::: ---> REQUIRED !!!
```
3. But we need to decrypt the hashed value of the password for entering the user id. For that, I run the 'John the Ripper' syntax command  : `john /challenge/shadow-leak` and then enter the hashed value of the password, which outputs the decryted/original form of the password.
```bash
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Created directory: /home/hacker/.john
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:16 0% 2/3 0g/s 282.0p/s 282.0c/s 282.0C/s national..rocket1
aardvark         (zardus)                                         -------> THE ORIGINAL PASSWORD
1g 0:00:00:20 100% 2/3 0.04849g/s 282.3p/s 282.3c/s 282.3C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```
4. Now, I enter into the zardus user id using the password and then run `/challenge/run`, whose execution gave me the flag!!!
```bash
hacker@users~cracking-passwords:~$ su zardus
Password:
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{4CedTSytaDCMIHUaBCnpXNKLW2g.QX3UDN1wCMxkjNzEzW}
```

## what I learned
1. Password hashes used to be in /etc/passwd, but that file is readable by anyone — so Linux moved real password hashes to /etc/shadow and only root can read it
2. If /etc/shadow leaks, an attacker can try to crack the hashes offline and recover passwords.
3. In creacking of a password, attackers take the hash of the password and start guessing. For each guess they run the same hash function. If it matches, they found the password.
4. Tools like John the Ripper automate this process of repetition involved in guessing. 

## References
-[pwn.college](https://pwn.college/linux-luminarium/users/) -  Untangling Users manual pages 


# 4. Using sudo
In this level, we will give you sudo access, and you will use it to read the flag.

## My solution
**Flag:** `pwn.college{8oxeadUoBwEpkK1ufXpfJ0FKuU0.QX4UDN1wCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. By question, we are told to use sudo to find the flag. But where is not given in the question. So, I run `sudo ls` to check all the files in the root directory and check and see any suspicious files that might contain the flag. 
```bash
hacker@users~using-sudo:~$ sudo ls
'?1'   COLLEGE   PWN   arg   f   foo.1x.dvi   foo.1x.flag   instructions   myflag   not-the-flag   stdout   the-flag
```
3. I found the `not-the-flag` suspicious. So I ran opened the file using `sudo`, whose execution gave me the flag.
```bash
hacker@users~using-sudo:~$ sudo cat not-the-flag
pwn.college{8oxeadUoBwEpkK1ufXpfJ0FKuU0.QX4UDN1wCMxkjNzEzW}
```

## What I learned 
1. In the olden days, a typical Linux system had a root password that administrators would use to su to root (after logging into their account with their normal account password). But root passwords are a pain to maintain, they (or their hashes!) can leak, and they don't lend themselves well to larger environments.
2. In order to address this, the world has moved from administration via su to administration via sudo (the current meaning of sudo is "substitute user, do")
3. Unlike su, which defaults to launching a shell as a specified user, sudo defaults to running a command as root.
4. So basically, sudo - run commands as an admin temporarily and /etc/sudoers = rulebook that defines who can use sudo and what they can do.

## References
-[pwn.college](https://pwn.college/linux-luminarium/users/) -  Untangling Users manual pages 

