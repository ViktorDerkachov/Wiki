Welcome to the freeipa wiki!

[Linux Guide and Hints FreeIPA](https://linuxguideandhints.com/el/freeipa.html#requirements)

[Red Hat Identity Management](https://access.redhat.com/products/identity-management#getstarted)

[Fedora 17 FreeIPA: Identity/Policy Management Managing Identity and Authorization Policies for Linux-Based Infrastructures Edition 2.2.0](https://docs.fedoraproject.org/en-US/Fedora/17/pdf/FreeIPA_Guide/Fedora-17-FreeIPA_Guide-en-US.pdf)

[How To Install FreeIPA Server on CentOS 7](https://computingforgeeks.com/install-freeipa-server-centos-7/)


# Oracle Linux 8.5 installation



yum install net-tools
  
// yum -y install epel-release

localectl set-locale LANG=en_US.UTF-8
yum install langpacks-en glibc-all-langpacks
   
yum update -y

[Configure the time for EC2 instances with IPv4 addresses](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-time.html)

less /etc/chrony.conf
systemctl status chronyd
vi  /etc/chrony.conf
service chronyd restart
systemctl restart chronyd
  
systemctl status chronyd
chronyc sources -v
  
hostnamectl set-hostname ipa2.tuton.cf
vi /etc/hosts 
yum module enable idm:DL1
?? yum distro-sync
 
 // yum module install idm:DL1/server
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


