
[OpenVPN Authentication Using PAM and Duo Security](https://blog.403labs.com/post/18387939648/openvpn-authentication-using-pam-and-duo-security)

OpenVPN Authentication Using PAM and Duo Security
It’s possible to configure OpenVPN with two-factor authentication utilizing PAM and Duo Security’s phone authentication on Ubuntu 10.04 LTS.

You just need to think like a hacker… By using password concatenation with OpenVPN’s PAM plugin and Duo Security’s plugin, your password will be comma-delimited, supporting both a PAM integrated password and Duo Security’s phone authentication.

Summary
I wasn’t satisfied with OpenVPN’s options for two-factor authentication. I configured OpenVPN with client certificates and Active Directory password integration via pam_winbind, but I wanted better security.

Knowing that it’s possible for an attacker on a compromised workstation to grab both the certificate and the user’s password (by keylogging or, depending on the OpenVPN configuration, memory scraping), I felt I needed a second out-of-band factor.

This is where Duo Security comes into play. Duo has made phone authentication simple to set up, use, and manage. They’ve created an OpenVPN plugin and, for most users, it’s all you need.

But since the Duo Security’s OpenVPN plugin utilizes the password field to input your method of authentication, this poses a problem to your existing PAM integration. The problem is, OpenVPN sends the same password to both plugins. Therefore, simply using your existing PAM plugin with Duo’s plugin isn’t an option.

…unless we make some modifications.

Why you’d want to do this
Why? Because…

You don’t want the workstation to be the single point of compromise (for both factors when using certificates and passwords).
You don’t want to password-protect your certificates because that would be a static password.
You want to use your existing password policies and lockouts with AD or some form of LDAP.
Duo Security has made phone authentication easy, powerful and slick.
Prerequisites
No reason to rehash steps for which there are already good tutorials. Make sure you have the following steps completed and working before moving on:

Get password authentication working with pam_winbind (we will force OpenVPN to use this PAM module later).
Install OpenVPN and create user certificates (Note: the CN field in the user certificate MUST equal the username for the user). Your clients should be able to authenticate with certificates only at this point.
Set up your Duo Security account with OpenVPN integration and users.
Patching the plugins
Both plugins need minor patching to split the concatenated password. The following patches will split based on the rightmost comma.

Patch OpenVPN’s auth-pam plugin
Download OpenVPN source and extract
Download the auth-pam patch
Patch and compile auth-pam.c
Patch Duo Security’s OpenVPN plugin
Download the Duo OpenVPN plugin
Download the duo_openvpn patch
Patch and compile duo_openvpn
Follow the remainder of duo_openvpn installation starting at ‘Configure the server config’ and stopping when you come to 'Test your step’
Setup a PAM configuration for OpenVPN
Place your PAM configuration in the following location: /etc/pam.d/openvpn

I use pam_winbind and my configuration is below. It allows only users that are in the 'vpnusers’ group defined in Active Directory. You can really use any PAM module if it is configured correctly. I haven’t tested with pam_ldap, but it should work without any problems.

auth [success=1 default=ignore] pam_winbind.so krb5_auth krb5_ccache_type=FILE cached_login try_first_pass require_membership_of=DOMAIN\vpnusersauth requisite pam_deny.soauth required pam_permit.so
Configure OpenVPN
Add the following lines in your OpenVPN server config/s (`IKEY`, `SKEY` and `HOST` are assigned by Duo Security in the admin interface when you setup an 'integration’)
Restart OpenVPN
Test your configuration
OpenVPN will defer authentication while Duo calls the phone that is provisioned for that user to then accept the connection.

You can also test other methods. Scroll to the bottom of Duo Security’s OpenVPN documentation page to see the supported factor identifiers.

Troubleshooting
If you are having troubles authenticating and it’s not obvious in either server or client logs, start by disabling the Duo plugin and making sure your client can connect with just certificates and the PAM authentication.

It’s also best to increase the verbosity in the server-side logs by adding 'verb 7’ in the server configuration. This will help with displaying the debug output of the plugins.

A successful PAM authentication in the OpenVPN server logs will return a status=0. A status=1 is a failure. This plugin call output will looks like this:

PLUGIN_CALL: POST /usr/lib/openvpn/openvpn-auth-pam.so/PLUGIN_AUTH_USER_PASS_VERIFY status=0
If you are successfully connected and your tunnel re-keys every hour, make sure your server config and client configs have matching reneg-sec statements. Otherwise, re-keying will happen with whichever one is the lowest. A non-defined reneg-sec statement defaults to one hour.



[Add support for "composite" password The plugin provided by Duo Security is intended to](https://www.netmeister.org/blog/duo-openvpn.html)

Add support for "composite" password
The plugin provided by Duo Security is intended to be combined with certificates to authenticate. However, we briefly considered combining it with regular password authentication via LDAP, but that solution is not currently supported by the plugin. However, there are ways around that. This blog entry explains in detail what needs to be done to make this happen.

After reading those instructions, I updated the duo_openvpn plugin to optionally support this as well. Those changes are also available in my fork on GitHub, but it should be noted that there are a few usability concerns: the two plugins are executed independently from each other, meaning that if one fails, the other is still attempted. This can lead to confusion when the user enters their password wrong, but still gets a Duo notification (which naturally takes a bit longer).

In the end, we decided that the user interface of these "composite passwords" is rather suboptimal: asking the user to enter their (hopefully complex) password (which we expect many users to have stored in 1Password and would have to copy from there), followed by a comma, followed by the Duo token seems prone to errors. Either way, the code is there, if you're interested.

[jschauma / duo_openvpn](https://github.com/jschauma/duo_openvpn)

having some trouble with openvpn using an auth plugin for DuoSecurity MFA.
https://github.com/duosecurity/duo_openvpn
[Discussion: [Openvpn-users] username-as-common-name not setting username as common_name for plugin](https://openvpn-users.narkive.com/MkNsB9Be/username-as-common-name-not-setting-username-as-common-name-for-plugin)

[Integrating Duo 2FA with OpenVPN](https://www.netmeister.org/blog/duo-openvpn.html)
