# Comprehending Commands
This module has 14 challenges. 

# 1. cat: not the pet, but the command!
In this challenge, I will copy the flag to the flag file in your home directory. Use the `cat` to get the flag

## My solution
**Flag:** `pwn.college{MnWwRnpa5DWr1DlGbMowT1ExKkn.QXxcTN0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. Bcz I am currently in the home directory, where the flag file is, I execute the `cat flag` command.
```bash
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{MnWwRnpa5DWr1DlGbMowT1ExKkn.QXxcTN0wCMxkjNzEzW}
```

## What I learned
1. `cat` is most often used for reading out files
2. `cat` will concatenate (hence the name) multiple files if provided multiple arguments
3. If you give no arguments at all, `cat` will read from the terminal input and output it.

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - 'cat: not the pet, but the command!' Module pages 

# 2. catting absolute paths
In this challenge to read the flag, use `cat` at its absolute path: `/flag`

## My solution
**Flag:** `pwn.college{wueBlPfRGqRmvmqcLFsQqtKfl6O.QX5ETO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. Execute the command `cat /flag` to get the flag
```bash
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{wueBlPfRGqRmvmqcLFsQqtKfl6O.QX5ETO0wCMxkjNzEzW}
```

## What I learned
1. You can specify cat's arguments as absolute paths.
2. /flag is where the flag always lives in pwn.college, but unlike in this challenge, you typically can't access that file directly.

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - catting absolute paths Module pages

# 3. more catting practice
In this challenge, I'll put the flag in some crazy directory, and I will not allow you to change directories with cd, so no cat flag

## My solution
**Flag:** `pwn.college{IEUVm3Sv26aWqe5Ex_-ogpi6me7.QXwITO0wCMxkjNzEzW}`
1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. Message in the terminal " You can find it in the file /lib/valgrind/flag." To get the flag, I execute `cat /lib/valgrind/flag`.
```bash
hacker@commands~more-catting-practice:~$ cat /lib/valgrind/flag
pwn.college{IEUVm3Sv26aWqe5Ex_-ogpi6me7.QXwITO0wCMxkjNzEzW}
```

## What I learned
1. You can specify all sorts of paths as arguments to commands

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - more catting practice Module pages

# 4. Grepping for a needle in a haystack
In this challenge, I've put a hundred thousand lines of text into the /challenge/data.txt file. grep it for the flag.

## My solution
**Flag:** `pwn.college{AaalvlTb_T04zuQJ2NP4Q3nnvre.QX3EDO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. As there are a hundred thousand lines of text, I used `grep pwn.college /challenge/data.txt` to get the flag.
```bash
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{AaalvlTb_T04zuQJ2NP4Q3nnvre.QX3EDO0wCMxkjNzEzW}
```

## What I learned
1. the grep command to search for the contents we need.

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - grepping for a needle in a haystack Module pages

# 5. comparing files
In this challenge, find the real flag from the second file, as mentioned in the question, by using the command `diff`

## My solution
**Flag:** `pwn.college{cViNxH1e6TX3duhrL42xQBKHS62.01MwMDOxwCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. Now I compare the 2 files, as given in the question, by executing `diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt`, to get the flag
```bash
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
90a91
> pwn.college{cViNxH1e6TX3duhrL42xQBKHS62.01MwMDOxwCMxkjNzEzW}
```

## What I learned
1. diff compares two files line by line and shows you exactly what's different between them.

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - comparing files Module pages

# 6. listing files
In this challenge, we've named /challenge/run with some random name! List the files in /challenge to find it, by using `ls`

## My solution
**Flag:** `pwn.college{MH8CBAIYAaphX2dAjGGpoFJuLra.QX4IDO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. Now I list the files in challenge directory using `ls /challenge`. On getting the required file/suspecious file's name, I execute `/challenge/10832-renamed-run-27557` to get the flag.
```bash
hacker@commands~listing-files:~$ ls /challenge
10832-renamed-run-27557  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/10832-renamed-run-27557
Yahaha, you found me! Here is your flag:
pwn.college{MH8CBAIYAaphX2dAjGGpoFJuLra.QX4IDO0wCMxkjNzEzW}
```

## What I learned 
1. ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided.

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - listing files Module pages

# 7. touching files
In this level, please create two files: /tmp/pwn and /tmp/college, and run /challenge/run to get your flag!

## My solution
**Flag:** `pwn.college{wcpXZEpKRD6_vKWNaRhnpNOU38y.QXwMDO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. I use `touch` to create 2 files and execute `/challenge/run` to get the flag
```bash
hacker@commands~touching-files:~$ touch /tmp/pwn
hacker@commands~touching-files:~$ touch /tmp/college
hacker@commands~touching-files:~$ /challenge/run
Success! Here is your flag:
pwn.college{wcpXZEpKRD6_vKWNaRhnpNOU38y.QXwMDO0wCMxkjNzEzW}
```

## What I learned 
1. You can create a new, blank file by touching it with the touch command

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - touching files Module pages

# 8. removing files
This challenge will create a delete_me file in your home directory! Delete it, then run /challenge/check, which will make sure you've deleted it and then give you the flag!

## My solution
**Flag:** `pwn.college{AGFX2DiBAb0wGo92994EceBGgUP.QX2kDM1wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. I run the command `rm delete_me` to delete the created file and execute `/challenge/check` to get the flag
```bash
hacker@commands~removing-files:~$ ls
delete_me  f
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{AGFX2DiBAb0wGo92994EceBGgUP.QX2kDM1wCMxkjNzEzW}
```
## What I learned 
1. you remove files with the rm command

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - removing files Module pages

# 9. moving files
This challenge wants you to move the /flag file into /tmp/hack-the-planet (do it)! When you're done, run /challenge/check, which will check things out and give the flag to you.

## My solution
**Flag:** `pwn.college{MAPBDEeQkgXkAiutYmi3BIMhS2v.0VOxEzNxwCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. As per qn, I move the files using `mv /flag /tmp/hack-the-planet` and execute `/challenge/check`, to get the flag.
```bash
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{MAPBDEeQkgXkAiutYmi3BIMhS2v.0VOxEzNxwCMxkjNzEzW}
```

## What I learned 
1. You can move files around with the mv command.

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - moving files Module pages

# 10. hidden files
In this challenge, Go find the flag, hidden as a dot-prepended file in /.

## My solution
**Flag:** `pwn.college{IdlYyy7_imkicgW3vZR79_0z7Hg.QXwUDO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. First, I change the cwd to `/` and then execute `ls -a` to list all the dotted files. Then, on spotting a suspecious file, I open it using `cat .flag-281771048531869` to get the flag.
```bash
hacker@commands~hidden-files:~$ cd /
hacker@commands~hidden-files:/$ ls -a
.   .dockerenv             bin   challenge  etc   lib    lib64   media  nix  proc  run   srv  tmp  var
..  .flag-281771048531869  boot  dev        home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~hidden-files:/$ cat .flag-281771048531869
pwn.college{IdlYyy7_imkicgW3vZR79_0z7Hg.QXwUDO0wCMxkjNzEzW}
```

## What I learned
1. Interestingly, ls doesn't list all the files by default. 
2. Linux has a convention where files that start with a . don't show up by default in ls and in a few other contexts.
3. To view them with ls, you need to invoke ls with the -a flag. 

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - hidden files Module pages

# 11. An Epic Filesystem quest
In this challenge, implement your knowledge of cd, ls, and cat, to find the flag

## My solution
**Flag:**`pwn.college{4zHGVqVWn4X8rBt9B2G_gVvSXez.QX5IDO0wCMxkjNzEzW}`
1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. And this is what I did, to get the flag
```bash
hacker@commands~an-epic-filesystem-quest:~$ cd /
hacker@commands~an-epic-filesystem-quest:/$ ls
REVELATION  boot       dev  flag  lib    lib64   media  nix  proc  run   srv  tmp  var
bin         challenge  etc  home  lib32  libx32  mnt    opt  root  sbin  sys  usr
hacker@commands~an-epic-filesystem-quest:/$ cat REVELATION
Great sleuthing!
The next clue is in: /usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX/General/Italic

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/$ cd /usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX/General/Italic
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX/General/Italic$ ls -a
.                       ControlPictures.js     GreekItalic.js              LetterlikeSymbols.js  SpacingModLetters.js
..                      CurrencySymbols.js     IPAExtensions.js            Main.js               ij.js
.MESSAGE                Cyrillic.js            Latin1Supplement.js         MathItalic.js
AlphaPresentForms.js    EnclosedAlphanum.js    LatinExtendedA.js           MathOperators.js
BoxDrawing.js           GeneralPunctuation.js  LatinExtendedAdditional.js  MathSSItalic.js
CombDiactForSymbols.js  GreekAndCoptic.js      LatinExtendedB.js           MathScript.js
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX/General/Italic$ cat .MESSAGE
Great sleuthing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/sympy/logic/algorithms/__pycache__

Watch out! The next clue is **trapped**. You'll need to read it out without 'cd'ing into the directory; otherwise, the clue will self destruct!
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX/General/Italic$ cat /usr/local/lib/python3.8/dist-packages/sympy/logic/algorithms/__pycache__
cat: /usr/local/lib/python3.8/dist-packages/sympy/logic/algorithms/__pycache__: Is a directory
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX/General/Italic$ ls /usr/local/lib/python3.8/dist-packages/sympy/logic/algorithms/__pycache__
CLUE-TRAPPED             dpll.cpython-38.pyc   lra_theory.cpython-38.pyc         pycosat_wrapper.cpython-38.pyc
__init__.cpython-38.pyc  dpll2.cpython-38.pyc  minisat22_wrapper.cpython-38.pyc  z3_wrapper.cpython-38.pyc
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX/General/Italic$ cat /usr/local/lib/python3.8/dist-packages/sympy/logic/algorithms/__pycache__/CLUE-TRAPPED
Great sleuthing!
The next clue is in: /opt/pwndbg/docs/commands/misc
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX/General/Italic$ cat /opt/pwndbg/docs/commands/misc
cat: /opt/pwndbg/docs/commands/misc: Is a directory
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/jax/output/HTML-CSS/fonts/STIX/General/Italic$ cd /opt/pwndbg/docs/commands/misc
hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/docs/commands/misc$ ls
SNIPPET  errno_.md  pwndbg_.md
hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/docs/commands/misc$ cat SNIPPET
Congratulations, you found the clue!
The next clue is in: /usr/local/lib/python3.8/dist-packages/numpy/fft/tests

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/pwndbg/docs/commands/misc$ cd /usr/local/lib/python3.8/dist-packages/numpy/fft/tests
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/numpy/fft/tests$ ls -a
.  ..  .WHISPER  __init__.py  __pycache__  test_helper.py  test_pocketfft.py
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/numpy/fft/tests$ cat .WHISPER
Lucky listing!
The next clue is in: /opt/linux/linux-5.4/arch/mips/include/asm/octeon

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/local/lib/python3.8/dist-packages/numpy/fft/tests$ cd /opt/linux/linux-5.4/arch/mips/include/asm/octeon
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/mips/include/asm/octeon$ ls
MEMO                cvmx-bootmem.h    cvmx-dbg-defs.h   cvmx-helper-board.h   cvmx-helper-spi.h   cvmx-l2c-defs.h   cvmx-mixx-defs.h     cvmx-pcsxx-defs.h  cvmx-pko.h       cvmx-spi.h         cvmx-uctlx-defs.h
cvmx-address.h      cvmx-ciu-defs.h   cvmx-dpi-defs.h   cvmx-helper-errata.h  cvmx-helper-util.h  cvmx-l2c.h        cvmx-npei-defs.h     cvmx-pemx-defs.h   cvmx-pow-defs.h  cvmx-spinlock.h    cvmx-wqe.h
cvmx-agl-defs.h     cvmx-ciu2-defs.h  cvmx-fau.h        cvmx-helper-jtag.h    cvmx-helper-xaui.h  cvmx-l2d-defs.h   cvmx-npi-defs.h      cvmx-pescx-defs.h  cvmx-pow.h       cvmx-spxx-defs.h   cvmx.h
cvmx-asm.h          cvmx-ciu3-defs.h  cvmx-fpa-defs.h   cvmx-helper-loop.h    cvmx-helper.h       cvmx-l2t-defs.h   cvmx-packet.h        cvmx-pexp-defs.h   cvmx-rnm-defs.h  cvmx-sriox-defs.h  octeon-feature.h
cvmx-asxx-defs.h    cvmx-cmd-queue.h  cvmx-fpa.h        cvmx-helper-npi.h     cvmx-iob-defs.h     cvmx-led-defs.h   cvmx-pci-defs.h      cvmx-pip-defs.h    cvmx-rst-defs.h  cvmx-srxx-defs.h   octeon-model.h
cvmx-boot-vector.h  cvmx-config.h     cvmx-gmxx-defs.h  cvmx-helper-rgmii.h   cvmx-ipd-defs.h     cvmx-lmcx-defs.h  cvmx-pciercx-defs.h  cvmx-pip.h         cvmx-scratch.h   cvmx-stxx-defs.h   octeon.h
cvmx-bootinfo.h     cvmx-coremask.h   cvmx-gpio-defs.h  cvmx-helper-sgmii.h   cvmx-ipd.h          cvmx-mio-defs.h   cvmx-pcsx-defs.h     cvmx-pko-defs.h    cvmx-sli-defs.h  cvmx-sysinfo.h     pci-octeon.h
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/mips/include/asm/octeon$ cat MEMO
Tubular find!
The next clue is in: /usr/share/doc/libnuma1

The next clue is **hidden** --- its filename starts with a '.' character. You'll need to look for it using special options to 'ls'.
hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/arch/mips/include/asm/octeon$ cd /usr/share/doc/libnuma1
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libnuma1$ ls -a
.  ..  .NUGGET  changelog.Debian.gz  copyright
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libnuma1$ cat .NUGGET
Great sleuthing!
The next clue is in: /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Neo-Euler/Normal/Regular
hacker@commands~an-epic-filesystem-quest:/usr/share/doc/libnuma1$ cd /usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Neo-Euler/Normal/Regular
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Neo-Euler/Normal/Regular$ ls
INFO  Main.js
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Neo-Euler/Normal/Regular$ cat INFO
Lucky listing!
The next clue is in: /usr/share/emacs/26.3/etc/images/icons/hicolor

The next clue is **delayed** --- it will not become readable until you enter the directory with 'cd'.
hacker@commands~an-epic-filesystem-quest:/usr/share/javascript/mathjax/unpacked/jax/output/SVG/fonts/Neo-Euler/Normal/Regular$ cd /usr/share/emacs/26.3/etc/images/icons/hicolor
hacker@commands~an-epic-filesystem-quest:/usr/share/emacs/26.3/etc/images/icons/hicolor$ ls
128x128  16x16  24x24  32x32  48x48  EVIDENCE  scalable
hacker@commands~an-epic-filesystem-quest:/usr/share/emacs/26.3/etc/images/icons/hicolor$ cat EVIDENCE
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!
It is: pwn.college{4zHGVqVWn4X8rBt9B2G_gVvSXez.QX5IDO0wCMxkjNzEzW}
```

## What I learned 
1. To have preseverance, even if the decoding is no lengthy

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - previous Module pages

# 12. making directories
In this challenge, create a /tmp/pwn directory and make a college file in it! Then run /challenge/run, which will check your solution and give you the flag.

## My solution
**Flag:**`pwn.college{s_5s3XUqw44t1ULv_-pSR6t-KxG.QXxMDO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. As per the question, I changed my directory to `/tmp` and then created a new directory `/tmp/pwn`
```bash
hacker@commands~making-directories:~$ cd /tmp
hacker@commands~making-directories:/tmp$ mkdir pwn
hacker@commands~making-directories:/tmp$ ls
bin  hsperfdata_root  pwn  tmp.TpSOPGOVKK
```
3. Now, I changed my directory to `/tmp/pwn` and then created a file college, using `touch` command. Then, on exwcuting `/challenge/run`, I got the flag 
```bash
hacker@commands~making-directories:/tmp$ cd pwn
hacker@commands~making-directories:/tmp/pwn$ touch college
hacker@commands~making-directories:/tmp/pwn$ ls /tmp/pwn
college
hacker@commands~making-directories:/tmp/pwn$ /challenge/run
Success! Here is your flag:
pwn.college{s_5s3XUqw44t1ULv_-pSR6t-KxG.QXxMDO0wCMxkjNzEzW}
```

## What I learned 
1. You make directories using the `mkdir` command.

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - making directory Module page

# 13. finding files
In this challenge, there is a flag hidden in a file name flag. Use the command `find` to find the flag.

## My solution
**Flag:**`pwn.college{I8xS9mA4q7_wBlO0ENgl-cboV74.QXyMDO0wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. First, I ran the `find / -name flag` command and got this
```bash
hacker@commands~finding-files:~$ find / -name flag
find: ‘/root’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
find: ‘/tmp/tmp.TpSOPGOVKK’: Permission denied
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/opt/linux/linux-5.4/drivers/vme/boards/flag
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/nix/store/7ns27apnvn4qj4q5c82x0z1lzixrz47p-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/5z3sjp9r463i3siif58hq5wj5jmy5m98-python3.12-pwntools-4.13.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/5n5lp1m8gilgrsriv1f2z0jdjk50ypcn-rizin-0.7.3/share/rizin/flag
/nix/store/bnlabj2vsbljhp597ir29l51nrqhm89w-rizin-0.7.4/share/rizin/flag
/nix/store/s8b49lb0pqwvw0c6kgjbxdwxcv2bp0x4-radare2-5.9.8/share/radare2/5.9.8/flag
/nix/store/1hyxipvwpdpcxw90l5pq1nvd6s6jdi5m-python3.12-pwntools-4.14.1/lib/python3.12/site-packages/pwnlib/flag
/nix/store/h88mxp2mbgyj06vypwmqpy05idhwimnp-python3.13-pwntools-4.14.1/lib/python3.13/site-packages/pwnlib/flag
/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag
```
3. Now, I started checking the files/directories randomly and ended up finding the flag.
```bash
hacker@commands~finding-files:~$ cat /usr/local/lib/python3.8/dist-packages/pwnlib/flag
cat: /usr/local/lib/python3.8/dist-packages/pwnlib/flag: Is a directory
hacker@commands~finding-files:~$ cd /usr/local/lib/python3.8/dist-packages/pwnlib/flag
hacker@commands~finding-files:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ ls
__init__.py  __pycache__  flag.py
hacker@commands~finding-files:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cat flag.py
"""Describes a way to submit a key to a key server.
"""
from __future__ import absolute_import
from __future__ import division

import os

from pwnlib.args import args
from pwnlib.log import getLogger
from pwnlib.tubes.remote import remote

env_server  = args.get('FLAG_HOST', 'flag-submission-server').strip()
env_port    = args.get('FLAG_PORT', '31337').strip()
env_file    = args.get('FLAG_FILE', '/does/not/exist').strip()
env_exploit_name = args.get('EXPLOIT_NAME', 'unnamed-exploit').strip()
env_target_host  = args.get('TARGET_HOST', 'unknown-target').strip()
env_team_name    = args.get('TEAM_NAME', 'unknown-team').strip()

log = getLogger(__name__)

def submit_flag(flag,
                exploit=env_exploit_name,
                target=env_target_host,
                server=env_server,
                port=env_port,
                team=env_team_name):
    """
    Submits a flag to the game server

    Arguments:
        flag(str): The flag to submit.
        exploit(str): Exploit identifier, optional
        target(str): Target identifier, optional
        server(str): Flag server host name, optional
        port(int): Flag server port, optional
        team(str): Team identifier, optional

    Optional arguments are inferred from the environment,
    or omitted if none is set.

    Returns:
        A string indicating the status of the key submission,
        or an error code.

    Doctest:

        >>> l = listen()
        >>> _ = submit_flag('flag', server='localhost', port=l.lport)
        >>> c = l.wait_for_connection()
        >>> c.recvall().split()
        [b'flag', b'unnamed-exploit', b'unknown-target', b'unknown-team']
    """
    flag = flag.strip()

    log.success("Flag: %r" % flag)

    data = "\n".join([flag,
                      exploit,
                      target,
                      team,
                      '']).encode('ascii')

    if os.path.exists(env_file):
        write(env_file, data)
        return

    try:
        with remote(server, int(port)) as r:
            r.send(data)
            return r.recvall(timeout=1)
    except Exception:
        log.warn("Could not submit flag %r to %s:%s", flag, server, port)
hacker@commands~finding-files:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cd /nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag
hacker@commands~finding-files:/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag$ ls
__init__.py  __pycache__  flag.py
hacker@commands~finding-files:/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag$ grep pwn flag.py
from pwnlib.args import args
from pwnlib.log import getLogger
from pwnlib.tubes.remote import remote
hacker@commands~finding-files:/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag$ cd /opt/linux/linux-5.4/drivers/vme/boards/flag
bash: cd: /opt/linux/linux-5.4/drivers/vme/boards/flag: Not a directory
hacker@commands~finding-files:/nix/store/5qz6hgb1qzpvjrsw20wyiylx5zw8b9bk-pwntools-4.14.0/lib/python3.13/site-packages/pwnlib/flag$ cat /opt/linux/linux-5.4/drivers/vme/boards/flag
pwn.college{I8xS9mA4q7_wBlO0ENgl-cboV74.QXyMDO0wCMxkjNzEzW}
```

## What I learned 
1. We use the find command, to find the location of files.
2. If no path is given, find uses the current directory (.) as the starting point.
3. The find command takes optional arguments describing the search criteria and the search location.

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - finding files Module pages

# 14. linking files
In this challenge, the flag is, as always, in /flag, but /challenge/catflag will instead read out /home/hacker/not-the-flag.

## My solution
**Flag:**`pwn.college{grHBrx0F8JzFg1wj8SEUEA8Dcrn.QX5ETN1wCMxkjNzEzW}`

1. I connected the dojo host using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. The shell is now connected to the dojo. First, I ran the `ln -sf /flag /home/hacker/not-the-flag` command, followed by `/challenge/catflag`, to get the flag
```bash
hacker@commands~linking-files:~$ ln -sf /flag /home/hacker/not-the-flag
hacker@commands~linking-files:~$ /challenge/catflag
About to read out the /home/hacker/not-the-flag file!
pwn.college{grHBrx0F8JzFg1wj8SEUEA8Dcrn.QX5ETN1wCMxkjNzEzW}
```


## What I learned 
1. In programs usually you want two programs to access the same data, but the programs expect that data to be in two different locations. Luckily, Linux provides a solution to this quandary: links.
2. Links come in two flavors: hard and soft (also known as symbolic) links.
3. Hard links sound simpler to most people, but they have various downsides and implementation gotchas that make soft/symbolic links, by far, the more popular alternative.
4. Command 1 : ln -s _ _ - for soft links 
5. Command 2 : file - to which takes a filename and tells you what type of file it is. It can also recognize symlinks 

## References 
-[pwn.college](https://pwn.college/linux-luminarium/commands/) - linking files Module pages