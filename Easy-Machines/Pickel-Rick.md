nmap: 

nmap -sS -A -p- -T4 -oN PRnmap.txt 10.48.151.64

Ports:

22/tcp open  ssh
80/tcp open  http

Vuln:

login bypass 

Exploit:

 gobuster dir -u [http://10.48.151.64](http://10.48.151.64/) -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,txt,js,py,html

gobuster findings  - 

index.html           (Status: 200) [Size: 1062]
login.php            (Status: 200) [Size: 882]
assets               (Status: 301) [Size: 313] [--> http://10.48.151.64/assets/]
portal.php           (Status: 302) [Size: 0] [--> /login.php]
robots.txt           (Status: 200) [Size: 17]

PrivEsc:

find the password in /robots.txt 
`Wubbalubbadubdub`

less Sup3rS3cretPickl3Ingred.txt
`mr. meeseek hair`

less /home/rick/'second ingredients'
`1 jerry tear`

sudo ls /root/
`3rd.txt`

sudo less /root/3rd.txt

3rd ingredients: fleeb juice
