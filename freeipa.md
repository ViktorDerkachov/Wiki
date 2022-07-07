[ Alexander Bokovoy](https://github.com/abbra)

# freeipa-workshop
[freeipa-workshop](https://github.com/abbra/freeipa-workshop)

# IDVIEW
[Using an ID view](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_identity_management/using-an-id-view-to-override-a-user-attribute-value-on-an-idm-client_configuring-and-managing-idm)

[ Using (Free)IPA ID-Views with LDAP for your legacy servers](https://blog.delouw.ch/2016/04/15/using-freeipa-id-views-with-ldap-for-your-legacy-servers/)

[V4/Migrating existing environments to Trust](https://www.freeipa.org/page/V4/Migrating_existing_environments_to_Trust)

# Logging Audit Logs

[Logging](https://linuxguideandhints.com/el/freeipa.html#logging)


# Extending FreeIPA

[Extending the FreeIPA Server](https://www.freeipa.org/images/5/5b/FreeIPA33-extending-freeipa.pdf)

[FreeIPA33-extending-freeipa.pdf](https://github.com/yar145/freeipa/files/8749456/FreeIPA33-extending-freeipa.pdf)

[Extending FreeIPA LDAP schema and UI (By example for Owncloud/Nextcloud)](https://github.com/radiorabe/freeipa-extending-ldap-schema-and-ui)

[Extending FreeIPA](https://abbra.fedorapeople.org/freeipa-extensibility.html#sec-6)

[A user status plugin example for freeIPA](https://github.com/abbra/freeipa-userstatus-plugin)

[V3/WebUI plugins](https://www.freeipa.org/page/V3/WebUI_plugins)

# Modification certificate profiles for ipa 

ipa certprofile-mod  OpenVPNUserCertMobile --file=/root/ipa-profiles/OpenVPNUserCertMobile.cfg --store=TRUE --desc="OpenVPN mobile user enrollment profile"
in **OpenVPNUserCertMobile.cfg**:
policyset.serverCertSet.7.default.params.exKeyUsageOIDs=1.3.6.1.5.5.7.3.2
policyset.serverCertSet.1.default.params.name=CN=$request.req_subject_name.cn$, O=TUTON.CF, generationQualifier=mobile




## **Ammendment for certificate view to reflect generationQualifier attribute  in app.js**

file app.js at /usr/share/ipa/ui/js/freeipa/

saved as app.js.original and replaced by app.js.purpose

Main changes:
that.cert_subject=$('<div />',{style:'font-weight: bold;',text:''}).appendTo(that.container);
that.table_layout=that.create_layout().appendTo(that.container);

**var tr=that.create_row().appendTo(that.table_layout);**
**that.create_header_cell('Purpose',':').appendTo(tr);**
**that.cert_generationqualifier=that.create_cell('','','cert-value').appendTo(tr);**

that.create_row().appendTo(that.table_layout);
that.create_header_cell('@i18n:objects.cert.serial_number',':').appendTo(tr);
that.cert_sn=                 that.create_cell('','','cert-value').appendTo(tr);

tr=that.create_row().appendTo(that.table_layout);
that.create_header_cell('@i18n:objects.cert.issued_by',':').appendTo(tr);
that.cert_issuer=that.create_cell('','','cert-value').appendTo(tr);

tr=that.create_row().appendTo(that.table_layout);
that.create_header_cell('@i18n:objects.cert.valid_from',':').appendTo(tr);
that.cert_valid_from=that.create_cell('','','cert-value').appendTo(tr);

tr=that.create_row().appendTo(that.table_layout);
that.create_header_cell('@i18n:objects.cert.valid_to',':').appendTo(tr);
that.cert_valid_to=that.create_cell('','','cert-value').appendTo(tr);
----------------------
if(cert){that.cert_subject.text(IPA.cert.parse_dn(cert.subject).cn);
 ---> inserted **that.cert_generationqualifier.text(IPA.cert.parse_dn(cert.subject).generationqualifier);**  <------
that.cert_sn.text(cert.serial_number);



less /usr/lib/python3.6/site-packages/asn1crypto/x509.py

dn_qualifier



## FeeIPA migration
[V4/FreeIPA to FreeIPA Migration](https://www.freeipa.org/page/V4/FreeIPA_to_FreeIPA_Migration)

[[Freeipa-users] export users/groups from one ipa server to another](https://listman.redhat.com/archives/freeipa-users/2014-January/010658.html)

ipa migrate-ds --user-container=cn=users,cn=accounts --group-container=cn=groups,cn=accounts --with-compat ldap://dr-ipa.mydomain.com:389


# DNS
[Backup DNS Zones](https://lists.fedorahosted.org/archives/list/freeipa-users@lists.fedorahosted.org/thread/DPC5BELJXA6YIMJNG5GLKDNCDY6EI2UT/)

[[Freeipa-users] Export DNS to external](https://listman.redhat.com/archives/freeipa-users/2014-January/msg00291.html)

# Export
[[Freeipa-users] Export user and host list to a csv or text file](https://freeipa-users.redhat.narkive.com/s8GMtC3S/export-user-and-host-list-to-a-csv-or-text-file)

Forward zones

[V4/Forward zones](https://www.freeipa.org/page/V4/Forward_zones)

[Recursive DNS and FreeIPA](https://adam.younglogic.com/2018/04/recursive-dns-and-freeipa/)

[FreeIPA (IdM) integrated DNS server denies recursive query from client networks](https://access.redhat.com/solutions/5753431)

[freeipa DNS issues with resolving](https://lists.fedoraproject.org/archives/list/freeipa-users@lists.fedorahosted.org/thread/NP2LMUA4M54XAV2PRNTCGCTKFQKSQILD/)

[Troubleshooting/DNS](https://www.freeipa.org/page/Troubleshooting/DNS)

[Set allow-recursion by default in IPA DNS](https://pagure.io/freeipa/issue/1335)
 "allow-recursion { any; };"

[Is IPA's DNS working as a recursive DNS server for internal + external requests](https://lists.fedorahosted.org/archives/list/freeipa-users@lists.fedorahosted.org/thread/HEMQW24AW3JW6BDCINZDBIQ5BVONOVOU/)

[IPA DNS DNSSEC causes Global Forwarding to not function](https://access.redhat.com/solutions/1400113)
Edit /etc/named.conf 
`dnssec-enable no;`
`dnssec-validation no;`
`# systemctl restart named-pkcs11`


## FreeIPA password 

[FreeIPA self-service password reset](https://github.com/larrabee/freeipa-password-reset)

[change default freeipa settings for password change/expire and otp timeout](https://lists.fedorahosted.org/archives/list/freeipa-users@lists.fedorahosted.org/thread/RENDPMEIXUWFGI2IBFAAC6WBVKNZCI7P/)


# Web App Authentication
[Web App Authentication](https://www.freeipa.org/page/Web_App_Authentication#SAML)
[Web App Authentication/Namespace separation](https://www.freeipa.org/page/Web_App_Authentication/Namespace_separation)


## DNS Autodiscovery

[Explain how autodiscovery works in ipa-client-install man pages](https://bugzilla.redhat.com/show_bug.cgi?id=910546)
 DNS Autodiscovery
       Client  installer  by  default  tries to search for _ldap._tcp.DOMAIN DNS SRV records for all
       domains that are parent to its hostname. For example, if a  client  machine  has  a  hostname
       'client1.lab.example.com',  the  installer  will  try to retrieve an IPA server hostname from
       _ldap._tcp.lab.example.com,  _ldap._tcp.example.com  and  _ldap._tcp.com  DNS  SRV   records,
       respectively.  The  discovered  domain is then used to configure client components (e.g. SSSD
       and Kerberos 5 configuration) on the machine.

       When the client machine hostname is not in a subdomain of an IPA server, its  domain  can  be
       passed  with --domain option. In that case, both SSSD and Kerberos components have the domain
       set in the configuration files and will use it to autodiscover IPA servers.

       Client machine can also be configured without a DNS autodiscovery at all. When both  --server
       and  --domain  options  are  used,  client installer will use the specified server and domain
       directly. --server option accepts multiple server hostnames which can be  used  for  failover
       mechanism.  Without  DNS  autodiscovery,  Kerberos is configured with a fixed list of KDC and
       Admin servers. SSSD is still configured to either try to read domain's  SRV  records  or  the
       specified  fixed list of servers. When --fixed-primary option is specified, SSSD will not try
       to read DNS SRV record at all (see sssd-ipa(5) for details).

[For FreeIPA autodiscovery to work, what SRV records must exist on the DNS server?](https://serverfault.com/questions/996099/for-freeipa-autodiscovery-to-work-what-srv-records-must-exist-on-the-dns-server)

ipa dns-update-system-records --dry-run