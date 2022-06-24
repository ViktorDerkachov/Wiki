ovpn2
nmcli connection add type ip-tunnel ip-tunnel.mode ipip con-name tun10 ifname tun10 remote 172.31.6.183 local 172.30.0.100
nmcli connection modify tun10 ipv4.addresses '10.0.0.1/30'
nmcli connection modify tun10 ipv4.method manual
nmcli connection modify tun10 +ipv4.routes "172.27.0.0/16 10.0.0.2"
nmcli connection modify tun10 +ipv4.routes "172.28.0.0/16 10.0.0.2"
nmcli connection up tun10

ov.hopto.org
nmcli connection add type ip-tunnel ip-tunnel.mode ipip con-name tun10 ifname tun10 local 172.31.6.183 remote 172.30.0.100 
nmcli connection modify tun10 ipv4.addresses '10.0.0.2/30'
nmcli connection modify tun10 ipv4.method manual
nmcli connection modify tun10 +ipv4.routes "172.30.1.0/24 10.0.0.1"
nmcli connection up tun10


nmcli connection modify tun10 +ipv4.routes "10.150.0.0/16 10.0.0.1"
nmcli connection modify tun10 +ipv4.routes "10.144.0.0/12 10.0.0.1"
nmcli connection modify tun10 +ipv4.routes "10.128.0.0/12 10.0.0.1"
nmcli connection modify tun10 +ipv4.routes "10.10.0.0/16 10.0.0.1"

ipa2
route add 172.16.0.0 255.240.0.0 gw 172.30.1.100

Chapter 16. Configuring IP tunnels

[Chapter 16. Configuring IP tunnels](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/configuring_and_managing_networking/configuring-ip-tunnels_configuring-and-managing-networking)


# An introduction to Linux virtual interfaces: Tunnels
[An introduction to Linux virtual interfaces: Tunnels](https://developers.redhat.com/blog/2019/05/17/an-introduction-to-linux-virtual-interfaces-tunnels#)

[How to create VTI interface for IPsec Site-To-Site in OpenWrt?](https://forum.openwrt.org/t/solved-how-to-create-vti-interface-for-ipsec-site-to-site-in-openwrt/67981?page=2)