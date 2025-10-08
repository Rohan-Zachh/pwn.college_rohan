# Terminal Multiplexing 
In this module, we have 6 challenges

# 1. Launching Screen
For this challenge, we've hooked things up so that just launching screen will get you the flag.

## My solution
**Flag:** `pwn.college{Q-slMDGEncwTFWSzTeqGTk25vnF.0VN4IDOxwCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. By question, you just need to launch the screen, on doing so, the flag was revealed 
```bash
Congratulations! You're inside a screen session!
Here's your flag:
pwn.college{Q-slMDGEncwTFWSzTeqGTk25vnF.0VN4IDOxwCMxkjNzEzW}
```

## What I learned 
1. screen command : screen is a program that creates virtual terminals inside your terminal. It's somewhat like having multiple browser tabs, but for your command line.
2. Syntax : just 'screen'
3. When you're done with your command line, type exit or press Ctrl-D to leave the screen session. Then screen will terminate and return you to your original shell.

## References
-[pwn.college](https://pwn.college/linux-luminarium/terminal-multiplexing/) -  Chaining Commands manual pages 

# 2. Detaching and Attaching 
For this challenge, you'll need to:

1. Launch screen
2. Detach from it.
3. Run /challenge/run (this will secretly send the flag to your detached session!)
4. Reattach to see your prize

## My solution
**Flag:** `pwn.college{w_heLE9F2EUL51YDJ1-y_oFTKfe.0lN4IDOxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, First launch screen and then detach from it using Ctrl + A and then press d 
```bash
hacker@terminal-multiplexing~launching-screen:~$ screen
[detached from 154.pts-1.terminal-multiplexing~detaching-and-attaching]
```
3. Now, by question, run /challenge/run, which sends the flag to the screen, so I run `screen -r` to reattach to the screen and get the flag!!
```bash
hacker@terminal-multiplexing~detaching-and-attaching:~$ /challenge/run
Found detached screen session: 154.pts-1.terminal-multiplexing~detaching-and-attaching
Sending flag to your screen session...

Flag sent! Now reattach to your screen session with:

  screen -r

You'll find the flag waiting for you there!
hacker@terminal-multiplexing~detaching-and-attaching:~$ screen -r 
hacker@terminal-multiplexing~detaching-and-attaching:~$ echo Yes! Flag is: pwn.college{w_heLE9F2EUL51YDJ1-y_oFTKfe.0lN4IDOxwCMxkjNzEzW}
Yes! Flag is: pwn.college{w_heLE9F2EUL51YDJ1-y_oFTKfe.0lN4IDOxwCMxkjNzEzW}
```

## What I learned
1. Imagine you're working on something important over a remote connection, and your connection drops. With a normal terminal (outside of this awesome dojo environment), everything's gone. With screen, your work keeps running, and you can reattach later.
2. You detach by pressing Ctrl-A, followed by d - for detach.
3. This leaves your session running in the background while you return to your normal terminal.
4. To reattach, you can use the -r argument to screen : ie, screen -r
5. Ctrl-A is screen's activation key for all of its shortcuts in its default configuration. All screen functionality is activated by some command combination starting with Ctrl-A.

## References
-[pwn.college](https://pwn.college/linux-luminarium/terminal-multiplexing/) -  Chaining Commands manual pages 

# 3. Finding Sessions
In this challenge, we've created three screen sessions for you. One of them contains the flag. The other two are decoys.

## My solution
**Flag:** `pwn.college{Q8k5VIBzI8hWdqKmPQeT5C4q2y4.01N4IDOxwCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. I need to look into 3 detached sessions and find which one has the flag. For that I first run `screen -ls`, to see all the sessions which are detached and get their names/PID, to invoke them 
```bash
hacker@terminal-multiplexing~finding-sessions:~$ screen -ls
There are screens on:
        150.pts-0.terminal-multiplexing~launching-screen        (Remote or dead)
        154.pts-1.terminal-multiplexing~detaching-and-attaching (Remote or dead)
        144.session_be6b430cd658cbc5    (Detached)
        147.session_fe49c4a0d2f3d7ae    (Detached)
        150.session_19adbbd89d5d4e16    (Detached)
5 Sockets in /home/hacker/.screen.
```
3. Now, I run all the detached sessions and eventually I got the flag, by executing one of the sessions.
```bash
hacker@terminal-multiplexing~finding-sessions:~$ screen -r 144
[detached from 144.session_be6b430cd658cbc5]
hacker@terminal-multiplexing~finding-sessions:~$ screen -r 147
[detached from 147.session_fe49c4a0d2f3d7ae]
hacker@terminal-multiplexing~finding-sessions:~$ screen -r 150
hacker@terminal-multiplexing~finding-sessions:~$  echo 'Congratulations! You found the right session!'
Congratulations! You found the right session!
hacker@terminal-multiplexing~finding-sessions:~$  echo pwn.college{Q8k5VIBzI8hWdqKmPQeT5C4q2y4.01N4IDOxwCMxkjNzEzW}
pwn.college{Q8k5VIBzI8hWdqKmPQeT5C4q2y4.01N4IDOxwCMxkjNzEzW}
```

## what I learned
1. If you end up with multiple sessions running, and you wanna find the right one to reattach to, use `screen -ls` command, which lists all the current running sessions.
2. The identifiers of the sessions are the PID of each respective screen process, a dot, and the name of the screen session.
3. To attach to a specific one, you use `its name or its PID` by giving it as an argument to screen -r.

## References
-[pwn.college](https://pwn.college/linux-luminarium/terminal-multiplexing/) -  Chaining Commands manual pages 

# 4. Switching Windows
For this challenge, we've set up a screen session with two windows:

Window 0 has... well, you'll have to switch there to find out!
Window 1 has a welcome message
Attach to the session with screen -r, then use one of the key combinations above to switch to Window 1. 

## My solution
**Flag:** `pwn.college{giNDRK6wAQCLXo4Osm7Z7erX9LO.0FO4IDOxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I ran `screen -ls` to know what all sessions are detached. 
```bash
hacker@terminal-multiplexing~switching-windows:~$ screen -ls
There are screens on:
        150.pts-0.terminal-multiplexing~launching-screen        (Remote or dead)
        154.pts-1.terminal-multiplexing~detaching-and-attaching (Remote or dead)
        144.session_be6b430cd658cbc5    (Remote or dead)
        147.session_fe49c4a0d2f3d7ae    (Remote or dead)
        150.session_19adbbd89d5d4e16    (Remote or dead)
        135.challenge_session   (Detached)
        189.pts-2.terminal-multiplexing~switching-windows       (Detached)
7 Sockets in /home/hacker/.screen.
```
2. Then I ran `screen -r 189`, bcz it has the same name as the challenge, but it was of no use, bcz I was just going in circles in that session. Then I ran `screen -r 135 `, which was the right session. On execution , it gave :
```bash
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Welcome to the window switching challenge!
> You are currently in window 1.
> The flag is hidden in window 0.
> Use Ctrl-A 0 to switch to window 0!
> MSG
```
3. Following the message as given above, I got into the window 0, using `Ctrl+A 0`, which revealed the flag
```bash
hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{giNDRK6wAQCLXo4Osm7Z7erX9LO.0FO4IDOxwCMxkjNzEzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{giNDRK6wAQCLXo4Osm7Z7erX9LO.0FO4IDOxwCMxkjNzEzW}
```

## What I learned 
1. Inside a single screen session, you can have multiple windows, like your browser has multiple tabs. This can be super handy for organizing different tasks.
2. These windows are handled with different keyboard shortcuts, all starting with Ctrl-A:

a) Ctrl-A c - Create a new window
b) Ctrl-A n - Next window
c) Ctrl-A p - Previous window
d) Ctrl-A 0 through Ctrl-A 9 - Jump directly to window 0-9
e) Ctrl-A " - bring up a selection menu of all of the windows

## References
-[pwn.college](https://pwn.college/linux-luminarium/terminal-multiplexing/) -  Chaining Commands manual pages 

# 5. Detaching and Attaching (tmux)
For this challenge:

a) Launch tmux
b) Detach from it.
c) Run /challenge/run (this will send the flag to your detached session!)
d) Reattach to see your prize 

## My solution
**Flag:** `pwn.college{cz7Ks4aeoDOV6UnFDnwrDvsAHZ7.0VO4IDOxwCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. By question, I run `tmux` to open the screen and then detach from it using `Ctrl-B d`, then I run `/challenge/run` and reattach to tmux using :`tmux attach`
```bash
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ tmux
[detached (from session 0)]
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ /challenge/run
Found detached tmux session: 0
Sending flag to your tmux session...

Flag sent! Now reattach to your tmux session with:
  tmux attach

You'll find the flag waiting for you there!
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$  echo Congratulations, here is your flag: pwn.college{cz7Ks4aeoDOV6UnFDnwrDvsAHZ7.0VO4IDOxwCMxkjNzEzW}
Congratulations, here is your flag: pwn.college{cz7Ks4aeoDOV6UnFDnwrDvsAHZ7.0VO4IDOxwCMxkjNzEzW}
```

## what I learned 
1. tmux: tmux (terminal multiplexer) is screen's younger, more modern cousin. It does all the same things but with some different key bindings. To invoke screen : just `tmux`
2. Instead of Ctrl-A, tmux uses `Ctrl-B` as its command prefix.
3. to detach from tmux - you press `Ctrl-B + d`.
4. `tmux ls` - List sessions
5. `tmux attach or tmux a` - Reattach to session

## References
-[pwn.college](https://pwn.college/linux-luminarium/terminal-multiplexing/) -  Chaining Commands manual pages 

# 6. Switching Windows 
In this level, We've created a tmux session with two windows:

a) Window 0 has the flag!
b) Window 1 has your warm welcome.

## My solution
**Flag:** `pwn.college{4BTVrsAVuUNTC3LN5x704mGCgg5.0FM5IDOxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I search for the detached session having 2 windows by running `tmux ls`
```bash
hacker@terminal-multiplexing~switching-windows-tmux:~$ tmux ls
1: 1 windows (created Wed Oct  8 19:08:43 2025)
challenge_session: 2 windows (created Wed Oct  8 19:07:29 2025) --> REQUIRED SESSION
```
3. To enter this session, I run `tmux a -t challenge_session`, where I enter into window 1
```bash
hacker@terminal-multiplexing~switching-windows-tmux:~$  cat <<MSG
> Welcome to the tmux window switching challenge!
> You are currently in window 1.
> The flag is hidden in window 0.
> Use Ctrl-B 0 to switch to window 0!
> MSG
Welcome to the tmux window switching challenge!
You are currently in window 1.
The flag is hidden in window 0.
Use Ctrl-B 0 to switch to window 0!
```
4. According to what is told, I need to enter window 0, to get the flag, so I execute `Ctrl-B + 0`, which reveals the flag!!
```bash
hacker@terminal-multiplexing~switching-windows-tmux:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{4BTVrsAVuUNTC3LN5x704mGCgg5.0FM5IDOxwCMxkjNzEzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{4BTVrsAVuUNTC3LN5x704mGCgg5.0FM5IDOxwCMxkjNzEzW}
```

## What I learned 
1. Just like screen, tmux has windows.
2. The key combos are different, but the concept is the same:

a) Ctrl-B c - Create a new window
b) Ctrl-B n - Next window
c) Ctrl-B p - Previous window
d) Ctrl-B 0 through Ctrl-B 9 - Jump to window 0-9
e) Ctrl-B w - See a nice window picker

3. Tmux shows your windows at the bottom in a status bar.

## References
-[pwn.college](https://pwn.college/linux-luminarium/terminal-multiplexing/) -  Chaining Commands manual pages 