
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



