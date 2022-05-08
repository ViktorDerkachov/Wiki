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

ipa2
route add 172.16.0.0 255.240.0.0 gw 172.30.1.100
