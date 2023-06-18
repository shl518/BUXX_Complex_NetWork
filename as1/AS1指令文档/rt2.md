# rt2
## common
```
sys
sysn rt2
vlan 10
port g 1/0/1
port g 1/0/13
port g 1/0/14
port g 1/0/2

inter vlan 10
ip add 125.1.2.2 24

vlan 20
port g 1/0/24

inter vlan 20
ip add 125.0.0.249 30

inter loop 0
ip add 1.1.1.2 32

inter loop 1
ip add 192.168.1.2 32

quit

router id 1.1.1.2

undo stp global enable

ospf
preference ase 200
area 0
network 125.1.2.2 0.0.0.255
network 125.1.3.2 0.0.0.255
network 1.1.1.2 0.0.0.0
network 192.168.1.2 0.0.0.0
import-route bgp
quit
```

## ibgp
```
bgp 1
group as1 internal
peer 1.1.1.1 group as1
peer 1.1.1.3 group as1
peer 1.1.1.4 group as1
peer 1.1.1.5 group as1
peer as1 connect-interface LoopBack 0
peer 125.0.0.250 as-number 2
address-family ipv4 unicast
peer as1 enable
peer as1 next-hop-local
peer 125.0.0.250 enable
```

## ebgp
```
bgp1
network 172.16.1.2 24
network 172.16.1.2 24
network 192.168.1.2 32
network 192.168.1.4 32
network 192.168.1.5 32
network 192.168.1.100 32
network 192.168.1.129 32
network 192.168.1.130 32
aggregate 192.168.1.0 24 detail-suppressed
network 125.3.114.1 32
preference 255 110 110 
quit
```

### bgp route select

优先选择rt2，local-pref越大越优先作为出口

```
ip ip-prefix voice2 p 125.4.125.1 32
route-policy vp2 p n 10
if-match ip-prefix voice2
apply local-pref 200
bgp 1
peer 125.0.0.250 route-policy vp2 import
quit
```

## smnp
```
snmp-agent trap source loop 1
snmp-agent group v3 buaa authentication
snmp-agent usm-user v3 oto buaa authentication-mode sha abaracadabra
snmp-agent target-host trap-hostname nym address 192.168.0.1 trap-paramsname buaa
snmp-agent trap enable
```
