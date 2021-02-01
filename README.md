# DDNS-DHCP

Acheiving Dynamic DNS on linux requires the following components:
- named (bind server)
- DHCP
- generated keys and configuration between both DNS & DHCP for Dynamic DNS to function

This repo has example configuration for DNS and DHCP
these configurations have been defined against Centos7 

to generate a new key to be used between NAMED and DHCPD, run:

dnssec-keygen -a HMAC-MD5 -b 128 -r /dev/urandom -n USER DDNS_UPDATE

the above command will generate the key in your home directory path. e.g:
[root@netservices ~]# pwd
/root
[root@netservices ~]# ll
total 16
-rw-------. 1 root root   53 Jan 31 20:55 Kddns_update.+157+50689.key
-rw-------. 1 root root  165 Jan 31 20:55 Kddns_update.+157+50689.private
drwxr-xr-x. 2 root root   39 Jan 30 21:43 tmp

