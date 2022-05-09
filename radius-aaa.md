
[FreeRADIUS / pam_radius](https://github.com/FreeRADIUS/pam_radius)

[PAM to RADIUS Authentication Module](https://www.beyondtrust.com/docs/privilege-management/unix-linux/admin/overview/pam-to-radius-auth-module.htm)

/etc/pam.d/pbul_pam_radius:
#task control module
auth required pam_radius_auth.so
account required pam_radius_auth.so
password required pam_radius_auth.so

/etc/pam.d/pbul_pam_radius:
auth required pam_radius_auth.so conf=<filepathname>
Edit the pam_radius_auth configuration file and add a line that represents your RADIUS server using this format:

server[:port] shared_secret [timeout]


