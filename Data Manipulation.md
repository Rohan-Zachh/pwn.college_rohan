# Data Manipulation
In this module, you'll learn a number of commands for manipulating data that will help you achieve great results on the shell.

# 1. Translating Characters
 In this level, /challenge/run will print the flag but will swap the casing of all characters (e.g., A will become a and vice-versa). You need to undo it with tr and get the flag

## My solution
**Flag:** `pwn.college{Eowti-HvQwkPwywXT3BSHOv4TIX.01MxEzNxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. First, I opened ran the /challenge/run command, to see if it directly gave the flag, but case swapped, as given in question 
```bash
hacker@data~translating-characters:~$ /challenge/run
Your case-swapped flag:
PWN.COLLEGE{eOWTI-hVqWKpWYWxt3bshoV4tix.01mXeZnXWcmXKJnZeZw}
```
3. So, this flag is currently case swapped. To convert it back to its original case, I follow the syntax : tr '[:lower:][:upper:]' '[:upper:][:lower:]' for tr command and I run the command `/challenge/run | tr 'A-Za-z' 'a-zA-Z'`, which in turn gave me the flag with the corrected case.
```bash
hacker@data~translating-characters:~$ /challenge/run | tr 'A-Za-z' 'a-zA-Z'
yOUR CASE-SWAPPED FLAG:
pwn.college{Eowti-HvQwkPwywXT3BSHOv4TIX.01MxEzNxwCMxkjNzEzW}
```

## What I learned 
1. One of the purposes of piping data is to modify it.
2. In its most basic usage, tr translates the character provided in its first argument to the character provided in its second argument.
Ex : hacker@dojo:~$ echo OWN | tr O P  -->  PWN

3. It can also handle multiple characters, with the characters in different positions of the first argument replaced with associated characters in the second argument.
Ex : hacker@dojo:~$ echo PWM.COLLAGE | tr MA NE  -->  PWN.COLLEGE

## References
-[pwn.college](https://pwn.college/linux-luminarium/data/) -  Data Manipulation resource pages 
- https://stackoverflow.com/questions/23178769/unix-tr-command-to-convert-lower-case-to-upper-and-upper-to-lower-case - For the syntax to convert lowercase to uppercase and vice versa using tr command .

# 2. Deleting Characters
In this challenge, you need to delete the decoy characters (specifically: ^ and %) among the flag characters. Use tr -d to remove them!

## My solution
**Flag:** `pwn.college{E4Ri3hayf8Tp2bJ1Au1kdzUEQ73.0FNxEzNxwCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, we need to delete the characters ^ and % from the flag. In order to do that, I run a command following the syntax of deleting characters by using `tr -d 'characters'`, which is  `/challenge/run | tr -d ^% `, whose execution, revealed the flag.
```bash
hacker@data~deleting-characters:~$ /challenge/run | tr -d ^%
Your character-stuffed flag:
pwn.college{E4Ri3hayf8Tp2bJ1Au1kdzUEQ73.0FNxEzNxwCMxkjNzEzW}
```

## What I learned 
1. tr can also translate characters to nothing (i.e., delete them).
2. This is done via a -d flag and an argument of what characters to delete.

## References
-[pwn.college](https://pwn.college/linux-luminarium/data/) -  Data Manipulation resource pages 


# 3.Deleting newlines
In this challenge, we'll inject a bunch of newlines into the flag. Delete them with tr's -d flag and the escaped newline specification!

## My solution
**Flag:** `pwn.college{0BsBDVYoZHS8bLwVAvOPwP_fpL7.0VNxEzNxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. As per question, we need to delete the newline characters in the flag. So, on following the newline character deletion syntax, I execute the command, `/challenge/run | tr -d '\n'` to delete the newline characters, whose execution gave me the flag in a single line .
```bash
hacker@data~deleting-newlines:~$ /challenge/run | tr -d '\n'
Your line-split flag: pwn.college{0BsBDVYoZHS8bLwVAvOPwP_fpL7.0VNxEzNxwCMxkjNzEzW}
```

## What I learned 
1. If you want to convert the newlines in your output and convert it into a continuous line, you can use `tr -d '\n'` to delete newline characters from the stream.
2. In tr, you often write '\n' (inside quotes) as a stand-in for the newline character, because you cannot literally hit “Enter” there.
3. EXTRA TRICK: if you ever want to deal with a backslash character \ itself (not as escape), you must escape it (i.e. write \\) so tr sees it as a literal backslash.

## References
-[pwn.college](https://pwn.college/linux-luminarium/data/) -  Data Manipulation resource pages 

# 4. Extracting the first lines with head
This challenge's /challenge/pwn outputs a bunch of data, and you'll need to pipe it through head to grab just the first 7 lines and then pipe them onwards to /challenge/college, which will give you the flag if you do this right! Your solution will be a long composite command with two pipes connecting three commands

## My solution
**Flag:** `pwn.college{EzI8n44DXaGVd4KVVfdaMFG5RmA.0lNxEzNxwCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. So, by question, inorder to pipe the first 7 lines of the output of the file /challenge/pwn to /challenge/college, I execute the command `/challenge/pwn | head -n 7 | /challenge/college`, following each commands syntax, whose execution outputted the flag.
```bash
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{EzI8n44DXaGVd4KVVfdaMFG5RmA.0lNxEzNxwCMxkjNzEzW}
```

## What I learned 
1. The head command is used to display the first few lines of its input.
2. head commands shows the first 10 lines, but you can control this with the -n option.

## References
-[pwn.college](https://pwn.college/linux-luminarium/data/) -  Data Manipulation resource pages 

# 5. Extracting specific sections of text 
In this challenge, the /challenge/run program will give you a bunch of lines with random numbers and single characters (characters of the flag) as columns. Use cut to extract the flag characters, then pipe them to tr -d "\n" (like the previous level!) to join them together into a single line. Your solution will look something like /challenge/run | cut ??? | tr ???, with the ??? filled out.

## My solution
**Flag:** `pwn.college{kUMgYXl5kvR7YhC7o4uY8aEEEGH.01NxEzNxwCMxkjNzEzW}`

1. Connecting the dojo host into the wsl using SSH command.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. According to the question, the file `/challenge/run ` is having its flag value in column order and we need to group it together inorder to get the flag in the correct order. So, I open the `/challenge/run` to see which column is the flag's value at, inorder to construct the correct `cut` part of the command.
```bash
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run
17121 p
22661 w
16638 n
4523 .
30450 c
11864 o
9310 l
20975 l
16752 e
13236 g
31249 e
7249 {
16405 k
9561 U
715 M
1853 g
29367 Y
329 X
30523 l
27683 5
29410 k
21419 v
51 R
6763 7
32609 Y
17407 h
16400 C
25404 7
11843 o
23634 4
17459 u
1066 Y
26041 8
3896 a
24132 E
22522 E
27780 E
31077 G
28012 H
30600 .
6031 0
23631 1
18391 N
11413 x
8454 E
18487 z
11196 N
22239 x
27476 w
4508 C
9741 M
14628 x
5758 k
17788 j
2652 N
9435 z
24167 E
25837 z
3287 W
14044 }
```
3. Now, I know that the flag's value is in the 2nd column. Now, I use the cut part of the command to cut out the 2nd column and then, use the tr part of the command to group the elements in the column in a single line. So, I execute the command `/challenge/run | cut -d " " -f 2 | tr -d '\n'`, whose execution gave me the flag!!
```bash
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d " " -f 2 | tr -d '\n'
pwn.college{kUMgYXl5kvR7YhC7o4uY8aEEEGH.01NxEzNxwCMxkjNzEzW}
```


## What I learned 
1. In some cases, if you want to extract the data of some specific columns in a file, you use the command `cut`
2. The -d argument specifies the column delimiter (how columns are separated).
3. The -f argument specifies the field number (which column to extract).

## References
-[pwn.college](https://pwn.college/linux-luminarium/data/) -  Data Manipulation resource pages 

# 6. Sorting Data 
In this challenge, there's a file at /challenge/flags.txt containing 100 fake flags, with the real flag mixed among them. When sorted alphabetically, the real flag will be at the end (we made sure of this when generating fake flags).

## My solution
**Flag:** `pwn.college{8VhJrfXBD0N_pFk1d2vVTmJgZwe.0FM0MDOxwCMxkjNzEzW}`

1. Connected the wsl to the dojo.
```bash
rozakk@DESKTOP-JPQGP4K:~$ ssh -i key hacker@dojo.pwn.college
Connected!
```
2. Because, the question says that to sort alphabetically, we don't need to pass any arguments in this command. So, we simple sort the data in the file `/challenge/flags.txt` by passing the command `sort /challenge/flags.txt`, whose execution outputs a list of flags. But, as it is mentioned in the question, the real flag will be at the end of the list. So, we have successfully found the flag!!
```bash
ovm.bollegd{8VgIrfXAD0M_oEj0d2vUSmJfZve.0EM0MDNxwCMxkiMyEzW}
ovn.cnklefe{8VhJreWAD0M_oEj1d2vVSmIfYve.0FL0LCOxwCMxkjNzEzW}
ovn.cnlkege{8UgIqfXBD0N_oFk1c1uVTlJfYwe.0EM0MDOxvCMxkjNzEzW}
ovn.cnlldge{8VhIqfXBD0N_pFj1d2uVTmJfZwe.0FL0LCNxwCMxjiNyEyW}
ovn.cokldge{8UgJrfXBD0N_pFk1c2vVTmJfZwe.0FM0MDNwvCLxkjNyEyV}
ovn.coklegd{7VgJqfXBC0N_pFj1d2uVSmIgZwd.0EM0MCOxwBMxkjNyEyV}
ovn.colkefe{8UhIrfWBC0N_pEj1c2vVTmIfZve.0FM0MDNxvCLwkjMyDyW}
ovn.colkege{8VgIrfXBD0N_oEk1d2vVTmJgZwe.0FM0LDOxwCMxkiNzEzW}
owm.boklegd{8VhIrfWAD0M_oFk1c1vUTmJgZve.0FL0MCOxvCLxjjNzDzW}
owm.bollefe{8VgJqeXBD0N_oFj0d2vUTmJfYvd.0FM0MDNxwBMxjjNyEyW}
owm.cnlkege{8UhJrfXBC0N_pFj1d1vVTmJgZwe.0FM0MDOwwCLxkjMzEzW}
owm.cokkdge{8VgIrfXAC0N_oFj0c2vVTmJgYve.0EM0MDNwwBMxkjNyDyV}
owm.college{7VhJreXBD0N_pFk1d2vVTmJgZwe.0FM0LDNwwCMxkjMyEzW}
owm.college{8VhJrfXBD0N_pFk1d2vVTmJgYwe.0FL0MDOwvCMxkjNyEzV}
own.boklege{8VhIqfXBD0M_oFj0d2uUTmJgZwd.0EM0MCOxwBMxkjNzEzV}
own.bolldgd{8UhIrfXBC0M_oFk1d2vUTmJfZve.0FM0LDNxwCLxkjNzEzV}
own.bolldge{7UhJreXBD0N_oFj0d2vUTmJgZwe.0FM0MDOwwCLwjjMzEzW}
own.bollege{7VhJrfWBC0N_pFk0d2vVTlJgZwd.0FM0MDOxvCLxkjMzDyW}
own.colldge{8VhJrfXBD0N_pEk1d2vVTlJgZwe.0FM0LCOxwCMxkjNzEzV}
own.collefe{8VhJrfXBD0N_pFk1d2vVTmJgZwe.0FM0MDOxwCMxkjNzDzW}
own.college{8VhIrfXBD0N_pFk1d2uUSmJgYwe.0FL0MDOxwBMxkjNyEzV}
pvm.boklegd{8VhIqeXBD0M_oFj1c1vVTmJgZve.0FM0MDNxwCLwkjNzEzV}
pvm.cnlkege{8VhJrfXBD0N_pFk1d2vVTmJgZwd.0FM0MCOxwBMxkjNzEzW}
pvm.college{8VgJrfXBD0N_pFk0d2uVTmJfZve.0FL0MCNwwCMxkiNzEzW}
pvn.bnklege{7VhIrfXBC0N_pFk1c2vVTlJgZve.0FM0MCNwwCMxkjMzDyW}
pvn.bnllefe{8VhJreWBD0N_pEj1c2uUTlIgZve.0FL0MCOwwCLxkiNyDyV}
pvn.bokkefe{8VgJqfXBD0N_pEk0d2vUSlIfZwe.0FM0MDNxwBMwkjNyEzV}
pvn.bollegd{8VhJreWBC0N_oEk0d2vVSlJgYwe.0FM0LDOxvCMwjjNyEzV}
pvn.bollege{8UhIreXAD0N_pFk1d2vVSmIgZvd.0FL0MCNxwCMxkjNzDyV}
pvn.cnlkefe{8UhJrfWBD0N_pFk0d2uVSmJfZwd.0FM0MCOxvBMwkiMyEyW}
pvn.cnllege{8VhJqeWBD0M_pFk0d2vVSlJgZwd.0EM0LDOxwCMxkjMzEyW}
pvn.cnllege{8VhJqfXBC0N_pFk1d2vVTmJgZwe.0FL0MDNxwBMxkiMzEyW}
pvn.coklegd{8VhJqfXBD0M_oFk1d2uVTlIgZvd.0EM0MCOwvCMxkiNyEzW}
pvn.colkdfe{8VgIqfXBC0M_pEk0d1vVTmJfYwd.0FM0MDOxwBMxjiNzEzV}
pvn.college{8UgJrfWBD0N_pFk1c2vVTmJgYwd.0FM0MDOxwCMwkiMzEzW}
pvn.college{8VhJrfXBD0N_pFk1d2vVTmJgZwe.0FM0MDOxwCMxkjNzEzW}
pwm.bnllefd{7VhJrfWBD0M_pEk1c1vUTlJfYve.0EM0LCOwwBLxkjNzEzW}
pwm.bollege{8VhJreXAD0N_oFk0c1uVSmIfYwd.0EM0MDOwvBMwkjMzDzW}
pwm.bollege{8VhJrfXBC0N_pFk1d2vVTmJgZwe.0FM0MDOxwCMxkjNzEyW}
pwm.cnkkege{8VhJrfXAC0N_pEj1d2vVTmJfZwd.0FL0LDOxwBMwkjNyEzW}
pwm.cnlkege{8VgJrfXBC0N_oFj0d2vUSlIgZwd.0EM0LDOxwCLxkjNzEyW}
pwm.cokldgd{8VhJqfXBD0M_pFk1d2vVTmJgZve.0EM0MDOxwCMwkjNyEzW}
pwm.colkegd{8VhJrfXBD0N_pEk1d2vVTmJgZwe.0FM0MDOxwBMxjjNzEzV}
pwm.college{7VgJrfWBD0N_pFk1d2uVSmIgZwe.0EM0LDNwwCMxkiNzEyW}
pwm.college{7VhJrfXBD0M_pEk0d2vVTmJgZwe.0FM0MDOxwCMxkjNzEyV}
pwm.college{8UhJrfXBD0N_pEj1d2vVSmJfZwd.0FM0LDOxwCMwkjNzEyW}
pwm.college{8VhJrfXBC0N_pFk1c2uVTmJfYwe.0FM0MDOxwCMxkjNzEzW}
pwm.college{8VhJrfXBD0M_pFk1d2vVTmIgZwe.0EM0MDOxwCMxkjNzEzV}
pwn.bnlkdgd{8VgJrfXBC0N_pFk1c2vVTlJfYwd.0FM0MDOxwCLxkjNzEzW}
pwn.bnllege{7UgJreXBD0N_oFk1d2vVTmJgZve.0EM0MDNxwCMxkjNyDzW}
pwn.bnllege{7VhJreXAD0M_pEj1c1vUTmIfZve.0EM0LDOxwCLwkjMzEyV}
pwn.boklegd{8VhJreXAD0N_pEk1d2vVTlJfZwe.0FM0MCOxwCMwkjNzEzW}
pwn.boklege{7VgJreXBD0M_pEk0d1vVTmJfZwe.0EM0MCNxwBLxkjMzEzW}
pwn.bolldfe{7VhIrfXBD0M_pEj1c2vVTlJgYwe.0FM0MCOwwBMxkiNzEzW}
pwn.bolldge{8VgIqeXBD0M_pFj1c2uVTmJgYwe.0FM0MCNwwCMwjjNyEzW}
pwn.bollefe{8VhJqfWBD0N_pEk0d1uVSmJfZwe.0FM0MDOwwCMxkiNyEzW}
pwn.bollegd{8VhIreXAC0N_pFk1d2uUSlIgYwe.0EM0MCNwvBMxjjNyEzW}
pwn.bollege{8UgJrfWBD0N_oFk1d1vVTmJgYwe.0FM0MDOxwCLwkjNyDzW}
pwn.bollege{8UhJqfXBD0M_oFj0d1uVTmJfZwd.0FM0MDNxwCMwjiMzEyW}
pwn.cnklegd{8VhIreXBD0N_pEk1d2uVSmJfZwe.0FM0LDOxwCMxkjNzEzV}
pwn.cnlkefe{8VhJrfXBD0N_pFk1d2vVTmJfZwe.0FM0MDOwwCMxjjNzEzW}
pwn.cnlkege{8VhJreXBD0N_pFk1d2vVTmJgZwe.0FM0MCOxwCMxkjNzEzW}
pwn.cnllegd{8VhJrfWBD0N_oFk1d2vVSmIgZwe.0FM0MDNxwCMxkiNyEyW}
pwn.cnllege{7VhJrfXBD0N_pFk1d2vVTmJgZwe.0FL0MCOxwCMxkjNzEzW}
pwn.cnllege{8VgIrfXBC0N_pEk1d2vUTmJgZwe.0FL0MDOxwCMxkiNyEzV}
pwn.cnllege{8VhJrfWBD0N_pFk1d2vVTmJgZwe.0FM0MDOxwCMxkjNzEzW}
pwn.cokldfd{8VgJqfXAD0N_oEk0d2vVTmJfZwd.0FM0LCOxwCLxkiMzDzW}
pwn.cokldge{7VhJrfXBD0N_pEk1d2vUTmJgZwe.0FM0MDOxwCMxkjNzDzW}
pwn.coklefd{8VhJrfWBD0N_pEk0d2uVTmIgZwe.0FM0LDNxwCMxkjNzDzW}
pwn.coklegd{7VhJqeXBD0N_oFj1d2vUTmJgYwe.0FM0MCOxwCLxjjNzDzV}
pwn.colkdge{8VhJreWAD0N_oFj0d2vVTmIfZwe.0FM0LDNwvBMxkjNzEzW}
pwn.colkege{8VhIreWAD0N_pEj1c2vUSlIgZwe.0FL0LDOxwCMwkjMzEzW}
pwn.colkege{8VhJrfXAD0N_oFj1c1vVTlJgZwd.0FL0MCOxwCMxkiNzEzW}
pwn.colldgd{7VhIrfXBD0N_pEk1c2vVSmJgZwe.0FM0MCOxwCMxjiNzEzW}
pwn.colldge{7VhIqfXBD0M_pEk1d2uVTmJgYwe.0EL0MCOxwCMxkiNzEzW}
pwn.colldge{7VhIrfXBD0N_pFk0d2vVTmJgZve.0FM0MDOxwCMwkjNzEzW}
pwn.colldge{8UhJrfWAD0M_oFk1d2vUTlIgZvd.0FM0MCOxwCMxkjNzEzW}
pwn.colldge{8VgJqeXBD0N_pFj1d1vVTlJgZwe.0FL0MDOxwCMxkjNzEzV}
pwn.colldge{8VhIrfWBD0N_pFk1d2vVSmJgZwe.0FM0MDOxwCMxkjNzEzW}
pwn.colldge{8VhJrfXAD0M_pFk1d1vVTmIgZwe.0FL0MDOxwCLxkjNyDzV}
pwn.colldge{8VhJrfXBD0N_pFk0d1vVTmJgZwd.0FM0MCNxwBMwkjNzEzW}
pwn.collefd{7UhJrfXAD0M_pFk0c2vUTmIgZve.0EM0MCOxvCMwkiNzEzW}
pwn.collefd{7VhJrfWBD0M_oFk1c2vVSmJgZwd.0EL0MDOxvCMxkjNzEzW}
pwn.collefe{8VhJreXBC0N_pFj0d2uVTlJfZwe.0FM0MDOxwCMxkjNzDyW}
pwn.collegd{8VhJrfXBD0N_pFj1d1vVTmIgZwe.0FM0LDOxwCMxjjNzDzW}
pwn.collegd{8VhJrfXBD0N_pFk1d2vUTmJgZwe.0FM0MDOxwCMxkjNyEzW}
pwn.college{8UhIrfXBC0N_pFj1c2vVTmIfYwd.0FM0LCOwwCMxkiMzEzW}
pwn.college{8VgIrfXBD0N_oFk1d2vVTmJgZwe.0EM0MDOxvCMxkjMzDyW}
pwn.college{8VgJrfXBD0N_pFk1d2vVTmJgZwe.0FM0MDOxwCMxkjNzEzW}
pwn.college{8VhJreXAD0M_pFk1d2uVTmJgZwd.0EM0LDOwwBMxkjNzEyW}
pwn.college{8VhJreXBD0N_pFk1d2vVTmJgZwe.0FM0MDOxwCMxkjNzEzW}
pwn.college{8VhJrfXBC0N_pFk1d2vUTmJgZwd.0FM0MDOxwCMxkjNzEzW}
pwn.college{8VhJrfXBD0N_oFk1c1vVTmIgZwe.0FM0MDOxwCMxjjNzEyW}
pwn.college{8VhJrfXBD0N_pFj1d2vVTmJfZwe.0FM0MDOxwCMxjjMzEzW}
pwn.college{8VhJrfXBD0N_pFk1c2vVTmJgZwe.0FM0MDOxwCMxkjNzEzW}
pwn.college{8VhJrfXBD0N_pFk1d2uUTmIgZwe.0FM0LDOxwCMxkjNzEzW}
pwn.college{8VhJrfXBD0N_pFk1d2vVTmIgZwe.0FM0MDOwwCMxkjNzEzW}
pwn.college{8VhJrfXBD0N_pFk1d2vVTmJgZwe.0FM0MDOwwCMxkjNzEzW}
pwn.college{8VhJrfXBD0N_pFk1d2vVTmJgZwe.0FM0MDOxwCMxkjNzEyW}
pwn.college{8VhJrfXBD0N_pFk1d2vVTmJgZwe.0FM0MDOxwCMxkjNzEzV}
pwn.college{8VhJrfXBD0N_pFk1d2vVTmJgZwe.0FM0MDOxwCMxkjNzEzW} ---> THE REAL FLAG !!!
```

## what I learned 
1. Because, the data in a file in not always sorted, The `sort` command helps you organize data. It reads lines from input (or files) and outputs them in sorted order.
2. By default, sort orders lines alphabetically.
3. Arguments can change this, like :
    
a)   -r: reverse order (Z to A)
b)   -n: numeric sort (for numbers)
c)   -u: unique lines only (remove duplicates)
d)   -R: random order!


## References
-[pwn.college](https://pwn.college/linux-luminarium/data/) -  Data Manipulation resource pages 
