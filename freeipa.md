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


