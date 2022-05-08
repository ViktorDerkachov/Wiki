
# insufficient capabilities

oracle linux 8.5

`root@ov ~]#  vi /usr/lib/systemd/system/openvpn-server@.service`

`CapabilityBoundingSet=CAP_IPC_LOCK CAP_NET_ADMIN CAP_NET_BIND_SERVICE CAP_NET_RAW CAP_SETGID CAP_SETUID CAP_SYS_CHROOT CAP_DAC_OVERRIDE CAP_AUDIT_WRITE** CAP_DAC_READ_SEARCH CAP_AUDIT_READ**`


openvpn-server@ systemd unit has insufficient capabilities

[Can't get pam authentication to work](https://forums.openvpn.net/viewtopic.php?t=24497)

[openvpn-server@ systemd unit has insufficient capabilities](https://community.openvpn.net/openvpn/ticket/918)

[How to find out what linux capabilities a process requires to work?](https://stackoverflow.com/questions/35469038/how-to-find-out-what-linux-capabilities-a-process-requires-to-work)