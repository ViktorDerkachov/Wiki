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




# Mobile device

[Mobile device only](https://forums.openvpn.net/viewtopic.php?t=25460)

[Configure OpenVPN to block clients by OS?](https://serverfault.com/questions/834826/configure-openvpn-to-block-clients-by-os)

