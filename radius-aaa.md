
[FreeRADIUS / pam_radius](https://github.com/FreeRADIUS/pam_radius)

[PAM to RADIUS Authentication Module](https://www.beyondtrust.com/docs/privilege-management/unix-linux/admin/overview/pam-to-radius-auth-module.htm)

/etc/pam.d/pbul_pam_radius:

#task control module

`auth required pam_radius_auth.so`

`account required pam_radius_auth.so`

`password required pam_radius_auth.so`

/etc/pam.d/pbul_pam_radius:

`auth required pam_radius_auth.so conf=<filepathname>`

Edit the pam_radius_auth configuration file and add a line that represents your RADIUS server using this format:

server[:port] shared_secret [timeout]

[OpenVPN steps to configure only username/password authentication](https://serverfault.com/questions/751700/openvpn-steps-to-configure-only-username-password-authentication)

`username-as-common-name`

`client-cert-not-required`

`plugin /usr/lib64/openvpn/plugins/openvpn-plugin-auth-pam.so openvpn`

You would also need to create a PAM config for **openvpn** (e.g. /etc/pam.d/openvpn).

If you were using RADIUS to authenticate users, then your PAM config might look like:


`account         required        pam_radius_auth.so`

`account         required        pam_radius_auth.so`

`auth            required        pam_radius_auth.so no_warn try_first_pass`


[2x HOW TO Introduction](https://openvpn.net/community-resources/how-to/)

**alternative someone's plugin**
[openvpn-auth-radius](https://github.com/brainly/openvpn-auth-radius)

--------------------------

yum install pam_radius

Installed:
  pam_radius-1.4.0-15.el8.x86_64

less /usr/share/doc/pam_radius/USAGE

ovpn server.conf
`plugin /usr/lib64/openvpn/plugins/openvpn-plugin-auth-pam.so opvpn-radius`


[root@ov server]# cat /etc/pam.d/opvpn-radius

`auth required pam_radius_auth.so `

`account required pam_radius_auth.so`

`password required pam_radius_auth.so` 

cat /etc/pam_radius.conf 

`# server[:port]	shared_secret      timeout (s)`

`172.31.6.183	secret		30`


**wget https://rublon.com/download/rublonauthproxy-latest.tgz  --no-check-certificate**

tar -xzvf rublonauthproxy-latest.tgz ./rublonauthproxy/
make
cp  rublon.service /lib/systemd/system
cp examples/config.min.example.json config.json

yum install openldap-clients
ldapsearch -h 172.30.0.10 -b dc=tuton,dc=cf -D uid=ovpn,cn=users,cn=accounts,dc=tuton,dc=cf -w secret


[root@ov config]# cat /usr/local/src/rublonauthproxy/config/config.json
{
  "PROXY": {
    "RADIUS_SECRET": "secret",
    "RUBLON_API": "https://core.rublon.net",
    "SERVERS": [
      {
        "IP": "0.0.0.0",
        "PORT": 1812,
        "MODE": "standard",
        "AUTH_SOURCE": "LDAP",
        "RUBLON_TOKEN": "ABF8D57AFA7A44F49143E61AC2823D6F",
        "RUBLON_SECRET": "4d2b4d4d90fe7024803702aee1ac07",
        "AUTH_METHOD": "push"
      }
    ]
  },
  "LDAP": {
    "HOST": "172.30.0.10",
    "SEARCH_DN": "dc=tuton,dc=cf",
    "USERNAME_ATTRIBUTE": "uid",
    "ACCESS_USER_DN": "uid=ovpn,cn=users,cn=accounts,dc=tuton,dc=cf",
    "ACCESS_USER_PASSWORD": "secret"
  }


