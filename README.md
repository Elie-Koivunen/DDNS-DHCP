# DDNS-DHCP

These configuration files serve as an example on how to setup DNS on a linux box along with DHCP.
These configuration files would result in DHCPD updating DNS entries into DNS and thus automatically
update DNS records dynamically as DHCPD updates its own records.

Do note that to see a listing of dynamically registered records, you need to read the journal and 
not the self created dns zone files. for example:

named-journalprint /var/named/lab.scape.zone.jnl |egrep -i add|egrep -i 300|egrep -v TXT |sed -e 's/add //g'

Dynamic entries are maintained in a binary format in zone files that end with ".jnl". original zone files
are not modified!


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

