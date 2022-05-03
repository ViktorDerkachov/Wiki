
[[Freeipa-users] Openvpn and Certificates](https://freeipa-users.redhat.narkive.com/kf51FYgc/openvpn-and-certificates)

`I understand from previous discussions that client certificates are not yet`
`supported in FreeIPA, instead I understand one can use "service`
`certificates". From an OpenVPN standpoint I'm guessing this is fine because`
`a vpn client can be entered in Freeipa as a client and a certificate`
`generated for it. This might actually be a preferred model for VPN.`

`My OVPN server config looks like this:`
`ca ca.crt`
`cert server.crt`
`key server.key`
`# Diffie hellman parameters.`
`dh dh2048.pem`

`I guess I can use the`
`"ipa-getcert request -f /path/to/server.crt -k /path/to/private.key -r"`
`command to generate the server.crt and private.key and I know where to find`
`ca.crt however:`
`- How about the Diffie hellman parameters?`
`- Is dh2048.pem just a bunch of shared primes that enable the two parties`
`to establish encryption together?`
`- Is it bad If this file is compromised?`

` **in the docs** of optionally requiring that a peer`
`certificate include a particular value in its **nsCertType extension**`
`(support for that's not currently planned AFAIK), or a particular value`
`in its **extendedKeyUsage (EKU)** extension (there's a ticket [1] for`
`supporting that), but you're not setting such a requirement above.`

`ipa service-add-host --hosts ipa.domain.de client/andrews-macbook-air.local.domain.de`

`ipa-getcert request -f`
`/var/lib/certmonger/requests/Andrews-MacBook-Air.local.crt -k`
`/var/lib/certmonger/requests/Andrews-MacBook-Air.local.key -N CN=`
`andrews-macbook-air.local.domain.de -D andrews-macbook-air.local.domain.de`
`-K client/andrews-macbook-***@DOMAIN.DE`

`-- Then shuffle the keys and certs around --`

`-- Restart OpenVPN --`

`And et voila! It works! Although it does feel a bit hacky :)`



[ipa-getcert does not allow setting specific EKU on certificates](https://pagure.io/freeipa/issue/2915)

Using **ipa-getcert -U id-kp-serverAuth** as shown in documentation, the certificate is created with **EKU** for both "TLS Web Server Authentication" and "TLS Web Client Authentication".
OpenVPN, for example, is one application that suggests setting the server's certificate to only specify "**TLS Web Server Authentication**": http://openvpn.net/index.php/open-source/documentation/howto.html#mitm

With the current **/var/lib/pki-ca/profiles/ca/caIPAserviceCert.cfg** and **ipa-getcert**, it _doesn't seem possible to override the default for specific cases, though the -U option to ipa-getcert _seems to indicate that specific EKU's can be requested.

This will be possible when IPA would support multiple certificate profiles.

This can now be achieved with different (custom) profiles.

Whilst that is not what is specifically asked for in the ticket, **accepting**
**user-specified (in CSR) EKU in default profile** would require c**reating a new**
**Dogtag profile policy** default that does something along the lines of:

**use intersection of CSR EKU and default EKU when CSR contains**
**EKU request extension**
use default EKU when CSR does not contain EKU request extension
And the default profile would have to be updated to use this new component.

I think specifying a profile with the exact EKU that is appropriate for
a given use case is the most sensible approach (and it is now supported).
Therefore I propose closing this ticket and, if necessary, updating
guides and documentation that refer to getcert '-U' option to indicate
that this is not the intended way to get a particular EKU with FreeIPA.

