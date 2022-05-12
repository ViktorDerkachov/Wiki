# OpenVPN authentication against FreeIPA, SSSD

[OpenVPN authentication against FreeIPA, SSSD](https://forums.openvpn.net/viewtopic.php?t=23667)

[Configure OpenVPN LDAP Based Authentication](https://kifarunix.com/configure-openvpn-ldap-based-authentication/)

How to Create OpenLDAP Member Groups
`Therefore, to enable group membership authentication, set the value of the RequireGroup option to true and edit the group section such that you configuration may look like;`

`<LDAP>`
	`URL		ldap://ldapmaster.kifarunix-demo.com`
	`BindDN		cn=readonly,ou=system,dc=ldapmaster,dc=kifarunix-demo,dc=com`
	`Password	P@ssW0rd`
	`Timeout		15`
	`TLSEnable	no`
	`FollowReferrals no`
`</LDAP>`
`<Authorization>`
	`BaseDN		"ou=people,dc=ldapmaster,dc=kifarunix-demo,dc=com"`
	`SearchFilter	"(uid=%u)"`
	`RequireGroup	true`
	`<Group>`
		`BaseDN		"ou=groups,dc=ldapmaster,dc=kifarunix-demo,dc=com"`
		`SearchFilter	"memberOf=cn=vpnonly,ou=groups,dc=ldapmaster,dc=kifarunix-demo,dc=com"`
		`MemberAttribute	uniqueMember`
	`</Group>`
`</Authorization>`

[FreeIPA CA -- user certificates for OpenVPN server](https://forums.fedoraforum.org/showthread.php?321605-FreeIPA-CA-user-certificates-for-OpenVPN-server)

[Настройка сервиса OpenVPN + LDAP аутентификация](https://habr.com/ru/company/icl_services/blog/301554/)


# Instlallation OPENVPN

from here

[How to Install OpenVPN Server and Client with Easy-RSA 3 on CentOS 8](https://www.howtoforge.com/tutorial/how-to-install-openvpn-server-and-client-with-easy-rsa-3-on-centos-8/)

[How To Set Up and Configure an OpenVPN Server on CentOS 8](https://www.digitalocean.com/community/tutorials/how-to-configure-a-freeipa-client-on-ubuntu-16-04)

[How To Set Up and Configure an OpenVPN Server on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-and-configure-an-openvpn-server-on-ubuntu-22-04)

[OpenVPN](https://wiki.archlinux.org/title/OpenVPN)

[OpenVPN - Getting started How-To](https://community.openvpn.net/openvpn/wiki/GettingStartedwithOVPN)

[Ubuntu/OpenVPN Server ( PAM  and more )](https://charlesreid1.com/wiki/Ubuntu/OpenVPN_Server)

[Install and Configure OpenVPN Server on RHEL 8 / CentOS 8](https://computingforgeeks.com/install-and-configure-openvpn-server-on-rhel-centos-8/)

[2x HOW TO](https://openvpn.net/community-resources/how-to/)


2.3.1.9 Disabling Source/Dest Checking (Recommended)
If your VPN setup consists of a site-to-site setup between your cloud instances and your
machines on-premises, you will need to disable source destination check protection on Amazon,
otherwise routing will not function properly. To do this, right click on the VPN instance,
select Change Source/Dest. Check and make sure the status is Disabled. This setting must also
be used if for for example want traffic from your VPC to go directly to the IP addresses of your
VPN clients in the VPN client subnet or this security feature will block the traffic.
2.3.1.10 Setup static routes
By default, the OpenVPN Access Server gives VPN clients access to your VPC by using the
NAT method (Network Address Translation). Using this method, traffic originating from the
VPN clients will appear to be coming from the local IP address of the Access Server. For that
reason, routing is not necessary and is much easier to implement. However, one drawback of
using such method is that traffic from the VPC itself cannot directly access a VPN client as the
NAT engine prevents such direct contact. In order to allow a VPN client to be directly
addressable via the VPC, you will need to configure the Access Server to use the routing method
instead of NAT. Once that is done, the source IP address of packets coming from the VPN 
27
clients is kept intact, and direct access from the VPC network to the VPN client subnet is then
possible. However, because the VPC does not automatically recognize the VPN subnet within
the VPN instance, it does not know how to send the return traffic back to the instance. To correct
this problem, you will need to add a static route in the Amazon routing table for your VPC so
that the return traffic flows properly. To learn how to do this see this document on Amazon AWS
VPC routing:
https://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Route_Tables.html


# Mobile device

[Mobile device only](https://forums.openvpn.net/viewtopic.php?t=25460)

[Configure OpenVPN to block clients by OS?](https://serverfault.com/questions/834826/configure-openvpn-to-block-clients-by-os)


## Особенности конфигурирования openvpn 

**# auth-user-pass-verify**

`script-security 2`

`auth-user-pass-verify /etc/openvpn/server/envprinter via-env`

`# does not work with uncommented`

`_#user nobody_`

`_#group nobody_`

cat **envprinter **

`#!/bin/bash`

`echo "common name is: ${common_name}"`

`echo "username is: ${username}"`

`set`

`exit 0`


log from server

`common name is: yaruser`

`username is: `

`_='username is: '`

`common_name=yaruser`

`config=server.conf`

`daemon=0`
`daemon_log_redirect=1`
`daemon_pid=3533`
`daemon_start_time=1652358974`
`dev=tun0`
`dev_type=tun`
`ifconfig_local=172.28.0.1`
`ifconfig_remote=172.28.0.2`
`link_mtu=1621`
`local_port_1=1194`
`proto_1=udp`
`redirect_gateway=0`
`remote_port_1=1194`
`route_gateway_1=172.28.0.2`
`route_net_gateway=172.31.0.1`
`route_netmask_1=255.255.255.0`
`route_network_1=172.28.0.0`
`route_vpn_gateway=172.28.0.2`
`script_context=init`
`script_type=user-pass-verify`
`tls_digest_0=37:17:48:ce:f3:fe:64:ee:fa:4d:f8:e4:01:45:a3:e0:8b:bf:49:42`
`tls_digest_1=43:53:a6:37:c9:9a:02:0c:30:de:4c:80:37:b0:78:7b:e7:1a:90:51`
`tls_digest_sha256_0=aa:16:2b:40:9a:f7:ab:3a:6e:69:7c:18:46:a3:19:84:67:25:98:58:eb:c9:20:5d:97:24:32:2f:93:bb:f8:17`
`tls_digest_sha256_1=8e:95:43:b2:84:ac:36:13:ec:d1:ec:aa:68:e4:18:3e:9f:6a:99:ca:81:07:fc:ed:e2:e7:b3:6f:0f:ae:22:1c`
`tls_id_0='O=TUTON.CF, CN=yaruser'`
`tls_id_1='O=TUTON.CF, CN=Certificate Authority'`
`tls_serial_0=19`
`tls_serial_1=1`
`tls_serial_hex_0=13`
`tls_serial_hex_1=01`
`tun_mtu=1500`
`untrusted_ip=91.203.114.1`
`untrusted_port=43832`
`username=`
`verb=4`

**Интересные параметры:**

--push-peer-info  на стороне клиента
            peer info: IV_HWADDR=10:51:07:60:43:f2   
            peer info: IV_PLAT=linux
--duplicate-cn
              Allow  multiple  clients with the same common name to concurrently connect.  In the absence of this option,
              OpenVPN will disconnect a client instance upon connection of a new client having the same common name.
--auth --tls-verify cmd
              Run  command  cmd  to  verify the X509 name of a pending TLS connection that has otherwise passed all other
              tests of certification (except for revocation via --crl-verify directive; the revocation test occurs  after
 --x509-username-field [ext:]fieldname
              Field  in the X.509 certificate subject to be used as the username (default=CN).  Typically, this option is
              specified with fieldname as either of the following:

              --x509-username-field emailAddress
              --x509-username-field ext:subjectAltName
            the --tls-verify test).-user-pass-verify cmd method
 --x509-track attribute
              Save  peer  X509 attribute value in environment for use by plugins and management interface.  Prepend a '+'
              to   attribute   to   save   values   from   full   cert   chain.     Values    will    be    encoded    as
              X509_<depth>_<attribute>=<value>.    Multiple  --x509-track  options  can  be  defined  to  track  multiple
              attributes.
 --remote-cert-tls client|server
 --remote-cert-eku oid
              Require that peer certificate was signed with an explicit extended key usage.
 --crl-verify crl ['dir']
              Check peer certificate against the file crl in PEM format





