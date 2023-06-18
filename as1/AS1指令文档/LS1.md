# ls1
## common
```
sys
sysn ls1
inter g 0/0/1
inter vlan 1
ip addr 125.1.2.254 24
router id 1.1.2.1
inter loop 1
ip addr 192.168.1.129 32
ospf
area 0
network 125.1.2.254 0.0.0.255
network 192.168.1.129 0.0.0.0
```

## smnp
```
snmp-agent group v3 buaa authentication
snmp-agent usm-user v3 oto buaa authentication-mode sha abaracadabra
snmp-agent trap source loop 1
snmp-agent target-host trap address udp-domain 192.168.0.1 params securityname buaa
snmp-agent trap enable
```

