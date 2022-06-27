[root@ipa2 ~]# ipa-server-upgrade 
Upgrading IPA:. Estimated time: 1 minute 30 seconds
  [1/11]: stopping directory server
  [2/11]: saving configuration
  [3/11]: disabling listeners
  [4/11]: enabling DS global lock
  [5/11]: disabling Schema Compat
  [6/11]: starting directory server
  [7/11]: updating schema
  [8/11]: upgrading server
  [9/11]: stopping directory server
  [10/11]: restoring configuration
  [11/11]: starting directory server
Done.
Update complete
Upgrading IPA services
Upgrading the configuration of the IPA services
Disabled p11-kit-proxy
[Verifying that root certificate is published]
[Migrate CRL publish directory]
CRL tree already moved
[Ensuring ephemeralRequest is enabled in KRA]
ephemeralRequest is already enabled
[Verifying that KDC configuration is using ipa-kdb backend]
[Fix DS schema file syntax]
Syntax already fixed
[Removing RA cert from DS NSS database]
RA cert already removed
[Enable sidgen and extdom plugins by default]
[Updating HTTPD service IPA configuration]
[Updating HTTPD service IPA WSGI configuration]
Nothing to do for configure_httpd_wsgi_conf
[Migrating from mod_nss to mod_ssl]
Already migrated to mod_ssl
[Moving HTTPD service keytab to gssproxy]
[Removing self-signed CA]
[Removing Dogtag 9 CA]
[Checking for deprecated KDC configuration files]
[Checking for deprecated backups of Samba configuration files]
dnssec-validation yes
[Add missing CA DNS records]
IPA CA DNS records already processed
created backup /etc/named.conf.ipa-backup
created new /etc/named.conf
named user config '/etc/named/ipa-ext.conf' already exists
named user config '/etc/named/ipa-options-ext.conf' already exists
named user config '/etc/named/ipa-logging-ext.conf' already exists
named.conf has been modified, restarting named
[Upgrading CA schema]
CA schema update complete
[Update certmonger certificate renewal configuration]
Certmonger certificate renewal configuration already up-to-date
[Enable PKIX certificate path discovery and validation]
PKIX already enabled
[Authorizing RA Agent to modify profiles]
[Authorizing RA Agent to manage lightweight CAs]
[Ensuring Lightweight CAs container exists in Dogtag database]
[Adding default OCSP URI configuration]
[Disabling cert publishing]
pki-tomcat configuration changed, restart pki-tomcat
[Ensuring CA is using LDAPProfileSubsystem]
[Migrating certificate profiles to LDAP]
[Ensuring presence of included profiles]
[Add default CA ACL]
Default CA ACL already added
[Updating ACME configuration]
[Migrating to authselect profile]
Already migrated to authselect profile
[Create systemd-user hbac service and rule]
hbac service systemd-user already exists
[Add root@TUTON.CF alias to admin account]
Alias already exists
[Setup SPAKE]
[Setup PKINIT]
[Enable server krb5.conf snippet]
[Adding ipa-ca alias to HTTP certificate]
Certificate is OK; nothing to do
The IPA services were upgraded
The ipa-server-upgrade command was successful
[root@ipa2 ~]# 


[Upgrade](https://www.freeipa.org/page/Upgrade)

[ipa-server-upgrade ](https://www.mankier.com/1/ipa-server-upgrade)


## Recovery

after ipa-server upgrade  i've got
free ipa update initializing DST: PKCS#11 initialization failed

что-то похожее:
[#5104 F20-F21 update and crashing bind-pkcs11](https://pagure.io/freeipa/issue/5104)
[[Freeipa-users] named-pkcs11 doesn't start after bind update](https://www.mail-archive.com/freeipa-users@redhat.com/msg23018.html)

Worked Recovery:
[IPA server crash after upgrade to OL8.5](https://community.oracle.com/tech/apps-infra/discussion/4491429/ipa-server-crash-after-upgrade-to-ol8-5)

In relation to this topic, the fix for this (on OL8.5 at least) is, according to the FreeIPA Bug Tracker:

1 - Edit the /etc/sysconfig/named file, add a line with: OPTIONS="-E libsofthsm2.so"

2 - Perform the update (I did a yum update, updating all the server packages). When ipa-server package got update, it was able to automatically do the IPA upgrade and properly start the named-pkcs11.service.

3 - Check ipa service with ipactl status and ipa-healthcheck. I just had some warning about log permissions and the ipa-ca DNS record (somehow, the ipa-ca DNS registry only had the second node IP). I just added the IP of my first node in the DNS registry.

Regards.

That worked like a charm. The only thing I have left is some errors regarding "{nickname} certificate in NSS DB {dbdir} does not match entry in LDAP" when running ipa-healthcheck.

------- more detaled -----

[ 4.9.6 upgrade failure on Oracle Linux 8.5 (BIND error: PKCS#11 initialization failed)](https://pagure.io/freeipa/issue/9041)

Yes. You need to pass the name of the PKCS#11 provider library (libsofthsm2.so) to BIND explicitly with a command-line argument. Just override the named-pkcs11 systemd unit file:

$ sudo systemctl edit named-pkcs11
Then paste the following lines, which add the -E argument to the command responsible for starting the service :



[Service]
ExecStart=
ExecStart=/usr/sbin/named-pkcs11 -u named -E libsofthsm2.so -c ${NAMEDCONF} $OPTIONS
Then update BIND to the latest version and restart the service; it should be OK.

[root@ipa2 ~]# cat  /etc/sysconfig/named 

# BIND named process options
# ~~~~~~~~~~~~~~~~~~~~~~~~~~
#
# OPTIONS="whatever"     --  These additional options will be passed to named
#                            at startup. Don't add -t here, enable proper
#                            -chroot.service unit file.
#
# NAMEDCONF=/etc/named/alternate.conf
#                        --  Don't use -c to change configuration file.
#                            Extend systemd named.service instead or use this
#                            variable.
#
# DISABLE_ZONE_CHECKING  --  By default, service file calls named-checkzone
#                            utility for every zone to ensure all zones are
#                            valid before named starts. If you set this option
#                            to 'yes' then service file doesn't perform those
#                            checks.

SOFTHSM2_CONF=/etc/ipa/dnssec/softhsm2.conf

OPTIONS="-E libsofthsm2.so"

# Creating the Replica
[4.5. Creating the Replica: Introduction](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/linux_domain_identity_authentication_and_policy_guide/creating-the-replica#replica-install-otp)

[2.4. Setting up FreeIPA Replicas](https://docs.fedoraproject.org/en-US/Fedora/18/html/FreeIPA_Guide/Setting_up_IPA_Replicas.html)


[Howto/Migration](https://www.freeipa.org/page/Howto/Migration#Migrating_from_other_FreeIPA_to_FreeIPA)


