**Libreswan as an IPsec VPN implementation**

[Chapter 4. Configuring a VPN with IPsec](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/securing_networks/configuring-a-vpn-with-ipsec_securing-networks)

**Install the libreswan packages**:

# yum install libreswan
If you are re-installing Libreswan, remove its old database files and create a new database:

# systemctl stop ipsec
# rm /etc/ipsec.d/*db
# ipsec initnss
Start the ipsec service, and enable the service to be started automatically on boot:

# systemctl enable ipsec --now
Configure the firewall to allow 500 and 4500/UDP ports for the IKE, ESP, and AH protocols by adding the ipsec service:

# firewall-cmd --add-service="ipsec"
# firewall-cmd --runtime-to-permanent

