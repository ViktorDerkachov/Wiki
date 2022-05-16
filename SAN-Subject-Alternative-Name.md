Subject Alternative Name

[Subject Alternative Name](https://www.alvestrand.no/objectid/2.5.29.17.html)

OID value: 2.5.29.17

OID description:
id-ce-subjectAltName

This extension contains one or more alternative names, using any of a variety of name forms, for the entity that is bound by the CA to the certified public key.

This extension may, at the option of the certificate issuer, be either critical or non-critical. An implementation which supports this extension is not required to be able to process all name forms. If the extension is flagged critical, at least one of the name forms that is present shall be recognized and processed, otherwise the certificate shall be considered invalid.

subjectAltName EXTENSION ::= {

	SYNTAX GeneralNames

	IDENTIFIED BY id-ce-subjectAltName

}

GeneralNames ::= SEQUENCE SIZE (1..MAX) OF GeneralName

GeneralName ::= CHOICE {

	`otherName	[0] INSTANCE OF OTHER-NAME,`

	`rfc822Name	[1] IA5String,`

	`dNSName		[2] IA5String,`

	`x400Address	[3] ORAddress,`

	`directoryName	[4] Name,`

	`ediPartyName	[5] EDIPartyName,`

	`uniformResourceIdentifier [6] IA5String,`

	`IPAddress	[7] OCTET STRING,`

	`registeredID	[8] OBJECT IDENTIFIER`

}

OTHER-NAME ::= TYPE-IDENTIFIER

EDIPartyName ::= SEQUENCE {
	nameAssigner [0] DirectoryString {ub-name} OPTIONAL,
	partyName [1] DirectoryString {ub-name}
}


[Reference record for OID 2.5.29.17](https://oidref.com/2.5.29.17)


[Add support for SubjectAltNames (SAN) to IPA service certificates](https://pagure.io/freeipa/issue/3977)

[root@ipa-server ~]# ipa-getcert request -k /root/test.key -f /root/test.crt -N "cn=ipa-server.test.com" -D "cn=auth.test.com" -D "blah.test.com" -D "blah" -D "auth" -K ldap/ipa-server.test.com

i.e: generate a new service certificate for a service which includes a subject alternative name. This prevents load balanced IPA operation for SSL traffic.

Although DNS SRV records can be used for some applications (such as sssd) - many applications don't work with SRV records, and/or only allow one ldap service be specified.

There are two ways to allow user supplied SAN extension:

A. use the userExtensionDefault profile plugin, which I think Dogtag currently supports:
https://access.redhat.com/site/documentation//en-US/Red_Hat_Certificate_System/8.1/html/Admin_Guide/Certificate_and_CRL_Extensions.html#User_Supplied_Extension_Default
make sure you read the Warning and the Note so you know what you are getting into.

B. I have in some limited CS8.1 beta releases "out of band" solution. It involves a modified profile default plugin and a new input plugin. This solution allows one to specify multiple SAN's along with the CSR (READ: outside of the CSR, but along with the url to the CA as part of the HTTP request). This requires that the client of the CA to be trusted.
Again, this is not currently available in Dogtag.

This is how I would imagine that dogtag would behave:

If subjectAltNames user extension is present in the certificate request (and passes IPA checks), dogtag adds the subjectAltNames to certificate
If the subjectAltName user extension is not specified in the request, it is not added to certificate
Any other user certificate extension is ignored
Can dogtag be configured that way or am I misunderstanding the configuration? Also adding awnuk to CC as he is now involved in IPA/PKI integration.
Identifier: Subject Alternative Name - 2.5.29.17
Critical: no
Value:
DNSName: client.example.com

It's correct that there is currently no SAN constraint as far as I know. Yes if you need it, RFE can be filed.
For configuration. The userExtOID already sets the constraint for the allowed OID.
So, in my test example, I have
policyset.otherCertSet.10.default.params.userExtOID=2.5.29.17
which is already limiting the allowed user supplied OID to be SAN.
However, to further setting constraint for the actual content of the SAN, you will need to write a constraint plugin as I suggested earlier.
