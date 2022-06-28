Welcome to the freeipa wiki!

[Linux Guide and Hints FreeIPA](https://linuxguideandhints.com/el/freeipa.html#requirements)

[Red Hat Identity Management](https://access.redhat.com/products/identity-management#getstarted)

[Fedora 17 FreeIPA: Identity/Policy Management Managing Identity and Authorization Policies for Linux-Based Infrastructures Edition 2.2.0](https://docs.fedoraproject.org/en-US/Fedora/17/pdf/FreeIPA_Guide/Fedora-17-FreeIPA_Guide-en-US.pdf)

[How To Install FreeIPA Server on CentOS 7](https://computingforgeeks.com/install-freeipa-server-centos-7/)


# Oracle Linux 8.5 - IPA installation 



yum install net-tools
  
// yum -y install epel-release

localectl set-locale LANG=en_US.UTF-8

yum install langpacks-en glibc-all-langpacks
   
yum update -y

[Configure the time for EC2 instances with IPv4 addresses](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-time.html)

less /etc/chrony.conf

systemctl status chronyd

vi  /etc/chrony.conf

`server 169.254.169.123 prefer iburst minpoll 4 maxpoll 4`

service chronyd restart

systemctl restart chronyd
  
systemctl status chronyd

chronyc sources -v
  
hostnamectl set-hostname ipa2.tuton.cf

vi /etc/hosts 

yum module enable idm:DL1

yum distro-sync
 
 // yum module install idm:DL1/server
 // yum -y install @idm:client

yum module install idm:DL1/dns

ipa-server-install 

 systemctl stop firewalld

 systemctl disable firewalld

 kinit admin

 klist 

--------------------------------------------------------------------  
less /var/log/ipaserver-install.log
 systemctl start ipa.service

  // 53  ipa-server-install --uninstall
  
  // 55  systemctl  status named-pkcs11.service
  / 57  ls /etc/ipa/dnssec/softhsm2.conf
  // 58  less  /etc/ipa/dnssec/softhsm2.conf
  // 59  export SOFTHSM2_CONF=/etc/ipa/dnssec/softhsm2.conf 
  // 60  export SOFTHSM2_PIN="$(cat /var/lib/ipa/dnssec/softhsm_pin)"
  // 61  softhsm2-util --show-slots  
  // 62  pkcs11-list -p "${SOFTHSM2_PIN}" -s "337811534"
  // 63  pkcs11-list -p "${SOFTHSM2_PIN}" -s "1685181299"
  // 64  pkcs11-tokens 
  // 65  pkcs11-list -p "${SOFTHSM2_PIN}" -l "ipaDNSSEC"
  // 66  rpm -q bind bind-dyndb-ldap bind-pkcs11
  // 67  dnf -yq downgrade bind
  // 68  dnf install bind-9.11.26-4.el8_4
  // 69  systemctl edit named-pkcs11
  // 70  systemctl status named-pkcs11
 
  // 76  vi /etc/resolv.conf 
  
   78  dnf install bind-9.11.26-4.el8_4
   79  systemctl edit named-pkcs11
   
   [Service]
ExecStart=
ExecStart=/usr/sbin/named-pkcs11 -u named -E libsofthsm2.so -c ${NAMEDCONF} $OPTIONS
   
   80  vi /etc/resolv.conf 
   
   82  ipa-server-upgrade
   86  systemctl start ipa
 


**Oracle Linux 8.5 error after yum update command**


named-pkcs11.service: Failed with result 'exit-code'. апр 26 09:58:10 ipa2.tuton.cf systemd[1]:
Failed to start Berkeley Internet Name Domain (DNS) with native PKCS#11

**recovery**

https://community.oracle.com/tech/apps-infra/discussion/4491429/ipa-server-crash-after-upgrade-to-ol8-5

I was able to fix BIND startup by downgrading the bind and bind-* packages from version 9.11.26-6 to 9.11.26-4. This is only a temporary fix, but it points towards a possible regression. The discussion continues on the FreeIPA bug tracker.
Just as an additional reference, downgrading can be made with: dnf install bind-9.11.26-4.el8_4

After downgrading complete IPA upgrade with: ipa-server-upgrade and finally start IPA: systemctl start ipa.

That done the job for me too.

**recovery**

https://pagure.io/freeipa/issue/9041


 `ipa-client-install --hostname=`hostname -f` \`
`--mkhomedir \`
`--server=ipa.computingforgeeks.com \`
`--domain computingforgeeks.com \`
`--realm COMPUTINGFORGEEKS.COM`

# How To Install FreeIPA Client on CentOS 8 / RHEL 8
[How To Install FreeIPA Client on CentOS 8 / RHEL 8](https://computingforgeeks.com/how-to-install-freeipa-client-on-centos-rhel-8/)


## Ubuntu 20.04 client installation

[Configure FreeIPA Client on Ubuntu 20.04|18.04 / CentOS 7](https://computingforgeeks.com/how-to-configure-freeipa-client-on-ubuntu-centos/)

hostnamectl set-hostname y-jenkins.hopto.org

vi /etc/hosts

`172.31.37.252	y-jenkins.hopto.org`

vi /etc/systemd/resolved.conf 

`[Resolve]`

`DNS=172.30.0.10`

`Domains=~tuton.cf ~buton.cf tuton.cf`

`FallbackDNS=8.8.8.8 8.8.4.4 1.1.1.1 1.0.0.1`

systemctl restart systemd-resolved

yum -y update

apt-get install freeipa-client

apt install chrony
less /etc/chrony/chrony.conf

vi /etc/chrony/chrony.conf    add: server 169.254.169.123 prefer iburst minpoll 4 maxpoll 4

/etc/init.d/chrony restart

ipa-client-install 

kinit admin


vi  /usr/share/pam-configs/mkhomedir

`Name: activate mkhomedir`

`Default: yes`

`Priority: 900`

`Session-Type: Additional`

`Session:`

`required pam_mkhomedir.so umask=0022 skel=/etc/skel`


# Configuring System Authentication

## Oracle make home dir

[Configuring System Authentication](https://docs.oracle.com/cd/F22978_01/8/userauth/F21455.pdf)

[Chapter 6. Enabling Custom Home Directories Using authconfig](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/authconfig-homedirs)

Install the oddjob-mkhomedir package on the system.

This package provides the pam_oddjob_mkhomedir.so library, which the authconfig command uses to create home directories. The pam_oddjob_mkhomedir.so library, unlike the default pam_mkhomedir.so library, can create SELinux labels.

`ls /usr/share/authselect/default/sssd/`

`ls /lib64/security/pam_oddjob_mkhomedir.so`

`authselect current`

`authselect select sssd with-sudo with-mkhomedir`

`systemctl enable oddjobd.service`




# OCSP check

openssl ocsp -CA ./ca.pem -issuer ./ca.pem  -nonce -serial 27  -url  http://ipa-ca.tuton.cf/ca/ocsp

[OCSP_check.sh](https://github.com/OpenVPN/openvpn/blob/master/contrib/OCSP_check/OCSP_check.sh)

[Signer certificate for OCSP responder](https://forums.openvpn.net/viewtopic.php?t=25307)

