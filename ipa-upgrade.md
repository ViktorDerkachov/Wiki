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