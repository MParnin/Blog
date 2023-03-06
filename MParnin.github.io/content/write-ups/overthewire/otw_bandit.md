---
title: "Bandit"
date: 2023-03-03
weight: 10
hideSummary: true
---

## Background
The Bandit wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames as well as the basics of the Linux command line.

## sshpass Command
```
sshpass -p `cat bandit0` ssh bandit0@bandit.labs.overthewire.org -p 2220
```

---

## Levels 0 thru 4

Bandit 0 (https://overthewire.org/wargames/bandit/bandit0.html)

```Level Goal
The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.
```

Navigate to your bandit working directory:
`cd ~/Documents/overthewire/bandit`

We are going to store the SSH credentials for each level in seperate files within the directory that we just navigated to and use sshpass to manage our credentials.  The title of the file is the username and the password is entered on the first line of the file.

Install sshpass with the following on debian-based distros:

`sudo apt install sshpass`

Enter the following command:
`nano bandit0`

Enter the provided password:
`bandit0`

Begin to exit nano by hitting `Ctrl + x` 

Nano will ask "Save modified buffer?"
`y`

Nano will ask "File Name to Write: bandit0", hit `enter`

---

Bandit 0 --> 1 (https://overthewire.org/wargames/bandit/bandit1.html)

```Level Goal
The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.
```

Connect to the Bandit 0 level with sshpass:

```
sshpass -p `cat bandit0` ssh bandit0@bandit.labs.overthewire.org -p 2220
```

`ls -la`

`cat readme`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 1 --> 2 (https://overthewire.org/wargames/bandit/bandit2.html)

```Level Goal
The password for the next level is stored in a file called - located in the home directory
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  For example:

```
sshpass -p `cat bandit1` ssh bandit1@bandit.labs.overthewire.org -p 2220
```

Note how bandit0 has changed to bandit1 for the next level.  Connect to the level.

`ls -la`

`cat ./-`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 2 --> 3 (https://overthewire.org/wargames/bandit/bandit3.html)

```Level Goal
The password for the next level is stored in a file called spaces in this filename located in the home directory
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`ls -la`

`cat 'spaces in this filename'`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 3 --> 4 (https://overthewire.org/wargames/bandit/bandit4.html)

```Level Goal
The password for the next level is stored in a hidden file in the inhere directory.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`ls -la`

`cd inhere`

`ls -la`

`cat '.hidden'`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

## Levels 5 thru 9

Bandit 4 --> 5 (https://overthewire.org/wargames/bandit/bandit5.html)

```Level Goal
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`ls -la`

`cd inhere`

`file ./*` #all files but list 'data' except -file07 lists 'ASCII text'

`strings ./*` #prints strings of all files.  doesnt specify file per line though

`cat ./-file00`

`cat ./-file01`

`cat ./-file02`

`cat ./-file03`

`cat ./-file04`

`cat ./-file05`

`cat ./-file06`

`cat ./-file07`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 5 --> 6 (https://overthewire.org/wargames/bandit/bandit6.html)

```Level Goal
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

    human-readable
    1033 bytes in size
    not executable
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`ls -la`

`cd inhere`

`ls -lR` #Recursively list files in all folders

`find \! -executable -size 1033c`

`cat ./maybehere07/.file2`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 6 --> 7 (https://overthewire.org/wargames/bandit/bandit7.html)

```Level Goal
The password for the next level is stored somewhere on the server and has all of the following properties:

    owned by user bandit7
    owned by group bandit6
    33 bytes in size
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`ls -la`

`find / -size 33c -user bandit7 -group bandit6`

`find / -size 33c -user bandit7 -group bandit6 2>/dev/null` #redirect stderror output to trash

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 7 --> 8 (https://overthewire.org/wargames/bandit/bandit8.html)

```Level Goal
The password for the next level is stored in the file data.txt next to the word millionth
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`ls -la`

`cat data.txt`

`cat data.txt | grep millionth`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 8 --> 9 (https://overthewire.org/wargames/bandit/bandit9.html)

```Level Goal
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`cat data.txt`

`cat data.txt | sort | uniq -c | grep -v "10"`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

## Levels 10 thru 14

Bandit 9 --> 10 (https://overthewire.org/wargames/bandit/bandit10.html)

```Level Goal
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`cat data.txt`

`cat data.txt | strings | grep "===="`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 10 --> 11 (https://overthewire.org/wargames/bandit/bandit11.html)

```Level Goal
The password for the next level is stored in the file data.txt, which contains base64 encoded data
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`cat data.txt | base64 -d`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 11 --> 12 (https://overthewire.org/wargames/bandit/bandit12.html)

```Level Goal
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`cat data.txt`

`echo "echo "Gur cnffjbeq vf WIAOOSFzMjXXBC0KoSKBbJ8puQm5lIEi" | rot13"`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 12 --> 13 (https://overthewire.org/wargames/bandit/bandit13.html)

```Level Goal
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`mkdir /tmp/t0nberry`

`cp data.txt /tmp/t0nberry`

`cd /tmp/t0nberry`

`xxd -reverse data.txt > reverse`

`file reverse` gzip compressed data

`mv reverse reverse.gz`

`gunzip reverse.gz`

`file reverse` bzip2 compressed data

`bunzip2 reverse`

`file reverse.out` gzip compressed data

`mv reverse.out reverse.gz`

`gunzip reverse.gz`

`file reverse` tar archive

`tar xf reverse`

`file *` data5.bin is tar

`tar xvf data5.bin`

`file *`

`bunzip2 data6.bin`

`file *`

`tar xvf data6.bin.out`

`file *`

`mv data8.bin data8.gz`

`gunzip data8.gz`

`cat data8`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 13 --> 14 (https://overthewire.org/wargames/bandit/bandit14.html)

```Level Goal
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`ls -la`

`ssh -i sshkey.private bandit14@localhost -p 2220`

---

## Levels 15 thru 19

Bandit 14 --> 15 (https://overthewire.org/wargames/bandit/bandit15.html)

```Level Goal
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`cat /etc/bandit_pass/bandit14 | nc localhost 30000`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 15 --> 16 (https://overthewire.org/wargames/bandit/bandit16.html)

```Level Goal
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`cat /etc/bandit_pass/bandit15`

`cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001`

`cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -ign_eof`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 16 --> 17 (https://overthewire.org/wargames/bandit/bandit17.html)

```Level Goal
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`nmap localhost -p31000-32000`

```
Starting Nmap 7.80 ( https://nmap.org ) at 2022-09-18 13:55 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00017s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown
```

`cat /etc/bandit_pass/bandit16`

`cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:31046`

`cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:31518 -ign_eof`

`cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:31691 -ign_eof`

`cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:31790 -ign_eof`

```
-----BEGIN RSA PRIVATE KEY-----
[redacted]
-----END RSA PRIVATE KEY-----
```

`ssh -i bandit17 bandit17@bandit.labs.overthewire.org -p 2220`

---

Bandit 17 --> 18 (https://overthewire.org/wargames/bandit/bandit18.html)

```Level Goal
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`cat passwords.old`

`cat passwords.new`

`diff passwords.old passwords.new`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 18 --> 19 (https://overthewire.org/wargames/bandit/bandit19.html)

```Level Goal
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

sshpass -p `cat bandit18` ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"

---

## Levels 20 thru 24

Bandit 19 --> 20 (https://overthewire.org/wargames/bandit/bandit20.html)

```Level Goal
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`ls -la`

`./bandit20-do cat /etc/bandit_pass/bandit20`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 20 --> 21 (https://overthewire.org/wargames/bandit/bandit21.html)

```Level Goal
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: Try connecting to your own network daemon to see if it works as you think
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`nc -lvp 8888`

`./suconnect 8888` supply bandit20 pass in listener window after connecting to receive bandit21 pass

---

Bandit 21 --> 22 (https://overthewire.org/wargames/bandit/bandit22.html)

```Level Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`cd /etc/cron.d`

`cat cronjob_bandit22`

`cat /usr/bin/cronjob_bandit22.sh`

`cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 22 --> 23 (https://overthewire.org/wargames/bandit/bandit23.html)

```Level Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`cd /etc/cron.d`

`cat cronjob_bandit23`

`echo I am user bandit23 | md5sum | cut -d ' ' -f 1`

`cat /tmp/8ca319486bfbbc3663ea0fbe81326349`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 23 --> 24 (https://overthewire.org/wargames/bandit/bandit24.html)

```Level Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`cd /etc/cron.d`

`ls -la`

`cat cronjob_bandit24`

`cat /usr/bin/cronjob_bandit24.sh`

`myname=bandit24`

`cd /var/spool/bandit24/foo`

`mkdir /tmp/t0nberry2`

`chmod 777 /tmp/t0nberry2`

`nano getpass.sh`

```
#!/bin/bash

touch /tmp/t0nberry2/bandit24
cat /etc/bandit_pass/bandit24 > /tmp/t0nberry2/bandit24

```

`chmod +x getpass.sh`

`cat /tmp/t0nberry2/bandit24`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

## Levels 25 thru 29

Bandit 24 --> 25 (https://overthewire.org/wargames/bandit/bandit25.html)

```Level Goal
A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`cat /etc/bandit_pass/bandit24`

`nc localhost 30002`

`mkdir /tmp/t0nberry3`

`cd /tmp/t0nberry3`

```
#!/bin/bash

for i in {000..9999}
do
    echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar" $i >> combinations.txt
done
```

`chmod +x index.sh`

`./brute.sh`

`cat combinations.txt | nc localhost 30002 >> result.txt`

`sort result.txt | uniq -u`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 25 --> 26 (https://overthewire.org/wargames/bandit/bandit26.html)

```Level Goal
Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

shrink screen small

`ssh -i bandit26.sshkey bandit26@localhost -p 2220`

press v to enter vim

`:r /etc/bandit_pass/bandit26`

---

Bandit 26 --> 27 (https://overthewire.org/wargames/bandit/bandit27.html)

```Level Goal
Good job getting a shell! Now hurry and grab the password for bandit27!
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

shrink screen small

`ssh -i bandit26.sshkey bandit26@localhost -p 2220`

press v to enter vim

`:set shell=/bin/bash`

`:shell`

`cat /etc/bandit_pass/bandit27`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 27 --> 28 (https://overthewire.org/wargames/bandit/bandit28.html)

```Level Goal
There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo. The password for the user bandit27-git is the same as for the user bandit27.

Clone the repository and find the password for the next level.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`mkdir /tmp/t0nberry4`

`cd /tmp/t0nberry4`

`git clone "ssh://bandit27-git@localhost:2220/home/bandit27-git/repo"`

`ls`

`cd repo`

`cat README`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 28 --> 29 (https://overthewire.org/wargames/bandit/bandit29.html)

```Level Goal
There is a git repository at ssh://bandit28-git@localhost/home/bandit28-git/repo. The password for the user bandit28-git is the same as for the user bandit28.

Clone the repository and find the password for the next level.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`mkdir /tmp/t0nberry5`

`cd /tmp/t0nberry5`

`git clone "ssh://bandit28-git@localhost:2220/home/bandit28-git/repo"`

`cd repo`

`cat README.md`

`git log`

`git show bdf3099fb1fb05faa29e80ea79d9db1e29d6c9b9` #change history shows password

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

## Levels 30 thru 34

Bandit 29 --> 30 (https://overthewire.org/wargames/bandit/bandit30.html)

```Level Goal
There is a git repository at ssh://bandit29-git@localhost/home/bandit29-git/repo. The password for the user bandit29-git is the same as for the user bandit29.

Clone the repository and find the password for the next level.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`mkdir /tmp/t0nberry6`

`cd /tmp/t0nberry6`

`git clone "ssh://bandit29-git@localhost:2220/home/bandit29-git/repo"`

`cd repo`

`ls`

`cat README.md`

`git branch -a`

`git checkout remotes/origin/dev`

`git log`

`git show 2b1395f00cfb986163082c50100be5be8f249f64` #log for dev commit

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 30 --> 31 (https://overthewire.org/wargames/bandit/bandit31.html)

```Level Goal
There is a git repository at ssh://bandit30-git@localhost/home/bandit30-git/repo. The password for the user bandit30-git is the same as for the user bandit30.

Clone the repository and find the password for the next level.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`mkdir /tmp/t0nberry7`

`cd /tmp/t0nberry7`

`cd repo`

`cat README.md`

`ls -la`

`cd .git`

`cat packed-refs`

`git show 831aac2e2341f009e40e46392a4f5dd318483019`

`git show-ref` #will also show the secret branch containing the key

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 31 --> 32 (https://overthewire.org/wargames/bandit/bandit32.html)

```Level Goal
There is a git repository at ssh://bandit31-git@localhost/home/bandit31-git/repo. The password for the user bandit31-git is the same as for the user bandit31.

Clone the repository and find the password for the next level.
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`mkdir /tmp/t0nberry8`

`cd /tmp/t0nberry8`

`cd repo`

`cat README.md`

`nano key.txt` #May I come in? added

`git add .`

`git commit` #key.txt was ignored

`git add key.txt` #notes .gitignore ignores .txt files.  use -f to override ignore.

`git add key.txt -f`

`git commit`

`Added file` #to commit message

`git push`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 32 --> 33 (https://overthewire.org/wargames/bandit/bandit33.html)

```Level Goal
After all this git stuff its time for another escape. Good luck!
```

Arrow up to get to retrieve your previously entered sshpass command and increment bandit by one.  Connect to the ssh server.

`$0`

`cat /etc/bandit_pass/bandit33`

Highlight and copy the returned password 

Break the ssh connection by typing `logout` or hitting `Ctrl + d`

Enter `nano bandit1`, paste the copied password, save & exit (`Ctrl + x`, `y`, `enter`)

---

Bandit 33 --> 34 (https://overthewire.org/wargames/bandit/bandit34.html)

```Level Goal
At this moment, level 34 does not exist yet.
```

---