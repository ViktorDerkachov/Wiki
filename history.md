[root@ipa2 ~]# history 

    1  less /etc/resolv.conf 
    2  localectl set-locale LANG=en_US.UTF-8
    3  yum install langpacks-en glibc-all-langpacks
    4  yum update -y
    5  yum install net-tools
    6  yum install mc
    7  systemctl status chronyd
    8  chronyc sources -v
    9  vi  /etc/chrony.conf
   10  systemctl restart chronyd
   11  chronyc sources -v
   12  hostnamectl set-hostname  --static  ipa1.core.idenon.com
   13  vi /etc/hosts 
   14  yum module enable idm:DL1
   15  yum distro-sync
   16  yum module install idm:DL1/dns
   17  sync
   18  exit
   19  hostnamectl set-hostname ipa2.core.idenon.com
   20  bash
   21  vi /etc/hosts
   22  less /etc/chrony.conf 
   23  history 
   24  chronyc sources -v
   25  vi /etc/resolv.conf 
   26  nslookup io.com 
   27  ping 172.16.0.8
   28  netstat -nr
   29  ping 172.16.8.1
   30  ping 172.16.0.1
   31  ssh  172.16.0.8
   32  ping 172.16.0/8
   33  ping 172.16.0.8
   34  nslookup io.com 
   35  exit
   36  less /etc/hosts 
   37  nslookup 172.16.8.8 172.16.0.8
   38  nslookup 172.16.0.8 172.16.0.8
   39  nslookup 172.16.8.8 172.16.0.8
   40  less /etc/resolv.conf 
   41  ifconfig 
   42  nslookup io.com 172.16.8.2
   43  nslookup io.com 8.8.8.8
   44  nslookup io.com 172.16.8.2
   45  nslookup io.com 172.16.8.1
   46  nslookup io.com 172.16.8.3
   47  nslookup io.com 172.16.8.4
   48  nslookup io.com 172.16.0.8
   49  ssh -i "itdep.pem" ubuntu@172.16.8.10
   50  exit
   51  ipa-replica-install --principal admin --admin-password
   52  ipa-replica-install --principal admin --admin-password key4admin
   53  systemctl 
   54  systemctl stop firewalld
   55  systemctl disable firewalld
   56  ipa-replica-install --principal admin --admin-password key4admin
   57  ipa-replica-install --help
   58  ipa-ca-install --help
   59  ipa-ca-install
   60  top
   61  ipa-kra-install 
   62  ipa-dns-install --help
   63  ipa-dns-install 
   64  ipa-dns-install --help
   65  ipa-kra-install --help
   66  ipa-server-install --help
   67  exit
   68  ipa-server-install --uninstall 
   69  less /etc/resolv.conf 
   70  vi  /etc/resolv.conf 
   71  nslookup ipa1.core.idenon.com
   72  nslookup idenon.com
   73  ipa-server-install --help
   74  ipa-replica-install --help
   75  history 
   76  ipa-replica-install --principal admin --admin-password key4admin --setup-ca --setup-kra --setup-dns 
   77  ipa-replica-install --principal admin --admin-password key4admin --setup-ca --setup-kra --setup-dns  --forwarder
   78  ipa-replica-install --principal admin --admin-password key4admin --setup-ca --setup-kra 
   79  systemctl 
   80  systemctl stop iptables
   81  systemctl disable  iptables
   82  ipa-replica-install --principal admin --admin-password key4admin --setup-ca --setup-kra 
   83  less /etc/resolv.conf 
   84  ipa-dns-install --help
   85  ipa-dns-install 
   86  ipa-dns-install --ip-address=172.16.0.8
   87  less /etc/resolv.conf 
   88  less /etc/named.conf
   89  nslookup www.cisco.com 
   90  less /etc/resolv.conf 
   91  ipa-server-install --uninstall
   92  ipa-replica-manage --help
   93  kinit admin
   94  kinit 
   95  ipa
   96  ipa 
   97  ipa-replica-manage --help
   98  ipa-replica-manage
   99  ipa-replica-manage list
  100  exit
  101  history 





