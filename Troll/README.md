--------------------------------
# Author Shubham Ranpise
--------------------------------

# 21/december/2022

# Troll

----------------------------------------------------------------
# nmap scan ()
----------------------------------------------------------------
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.2
22/tcp open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.7 ((Ubuntu))


from pcap file from 38 tcp stream we got
/sup3rs3cr3tdirlol on website
got bin file ,if we string that got this addres /0x0856BF  worked on website
from this directory got userlist and password

hydra -L which_one_lol.txt -p Pass.txt ssh://10.0.2.17
the Pass.txt is password not the password list
overfloe:Pass.txt
----------------------------------------------------------------
# privilege escalation
----------------------------------------------------------------
vulnerable kernel version
https://www.exploit-db.com/exploits/37292
uname -r
3.13.0-32-generic

----------------------------------------------------------------
# flag
----------------------------------------------------------------
# cat proof.txt
Good job, you did it! 


702a8c18d29c6f3ca0d99ef5712bfbdc
