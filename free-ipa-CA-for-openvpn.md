
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

