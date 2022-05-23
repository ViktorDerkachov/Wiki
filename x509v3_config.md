
[x509v3_config](https://www.openssl.org/docs/manmaster/man5/x509v3_config.html)

Several OpenSSL commands can add extensions to a certificate or certificate request based on the contents of a configuration file and CLI options such as **-addext**. 

[Example OpenSSL Configuration File](http://webservices.itcs.umich.edu/mediawiki/radmind/index.php/Example_OpenSSL_Configuration_File)


[Manually Generate a Certificate Signing Request (CSR) Using OpenSSL](https://www.ssl.com/how-to/manually-generate-a-certificate-signing-request-csr-using-openssl/)

# Manipulating ssl certificates

[Manipulating ssl certificates](https://bgstack15.wordpress.com/2016/06/30/manipulating-ssl-certificates/)

`Testing ssl cert from server`

`To find out if the https or other ssl-enabled service is serving the right certificate, you can use openssl as a client and pull down the ssl `
`cert.`

`printf '\n' | openssl s_client -connect ipa.example.com:443`

`And observe the output for the certificate information.`

`To test SNI, add the parameter -servername myurl.example.com.`

`Reference: weblink 6 https://major.io/2012/02/07/using-openssls-s_client-command-with-web-servers-using-server-name-indication-sni/`


[Certificate subject X.509](https://stackoverflow.com/questions/6464129/certificate-subject-x-509)
IETF PKIX (latest version RFC 5280) is a well accepted profile for certificates. From section 4.1.2.4, the following fields must be supported (I've added between parenthesis is the OpenSSL long and optional short name):

country (countryName, C),

organization (organizationName, O),

organizational unit (organizationalUnitName, OU),

distinguished name qualifier (dnQualifier),

state or province name (stateOrProvinceName, ST),

common name (commonName, CN) and

serial number (serialNumber).

There's also a list of element that should be supported:

locality (locality, L),

title (title),

surname (surName, SN),

given name (givenName, GN),

initials (initials),

pseudonym (pseudonym) and

generation qualifier (generationQualifier).

[LDAP schema](http://www-lor.int-evry.fr/~michel/LDAP/Classes/Attributes-G.html)

**generationQualifier**

The generationQualifier attribute contains the part of the name which typically is the suffix, as in "IIIrd".

 

attributetype ( 2.5.4.44

NAME 'generationQualifier'
DESC 'RFC2256: name qualifier indicating a generation'
SUP name )

[LDAP schema](http://www-lor.int-evry.fr/~michel/LDAP/Classes/Attributes-D.html)

**dnQualifier**

The dnQualifier attribute type specifies disambiguating information to add to the relative distinguished name of an entry. It is intended for use when merging data from multiple sources in order to prevent conflicts between entries which would otherwise have the same name. It is recommended that the value of the dnQualifier attribute be the same for all entries from a particular source.



attributetype ( 2.5.4.46

NAME 'dnQualifier'

DESC 'RFC2256: DN qualifier'

EQUALITY caseIgnoreMatch

ORDERING caseIgnoreOrderingMatch

SUBSTR caseIgnoreSubstringsMatch

SYNTAX 1.3.6.1.4.1.1466.115.121.1.44 )


