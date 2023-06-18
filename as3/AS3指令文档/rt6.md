# rt6
## common
```
sys
sysn rt6
inter g 0/0/0
ip addr 125.3.2.6 24
inter g 0/0/1
ip addr 125.3.3.6 24
inter g 0/0/2
ip addr 125.0.0.246 30
inter l 0
ip addr 3.1.1.6 32
inter l 1
ip addr 192.168.3.6 24
quit
router id 3.1.1.6
ospf
preference ase 200
area 0
network 125.3.2.6 0.0.0.255
network 125.3.3.6 0.0.0.255
network 3.1.1.6 0.0.0.0
network 192.168.3.6 0.0.0.0
import-route bgp
quit
quit
```

## ibgp
```
bgp 3
group as3 internal
peer 3.1.1.7 group as3
peer 3.1.1.8 group as3
peer as3 connect-interface LoopBack 0
peer as3 next-hop-local
```

## ebgp
```
peer 125.0.0.245 as-number 1
network 125.3.16.1 24
network 125.3.17.1 24
network 125.3.18.1 24
network 125.3.19.1 24
aggregate 125.3.16.0 255.255.252.0 detail-suppressed
network 192.168.3.3 32
network 192.168.3.4 32
network 192.168.3.6 32
network 192.168.3.7 32
network 192.168.3.8 32
network 192.168.3.9 32
network 192.168.3.10 32
network 192.168.3.11 32
network 192.168.3.12 32
network 192.168.3.13 32
network 192.168.3.14 32
aggregate 192.168.3.0 24 detail-suppressed
network 125.3.114.1 32
quit
```

### bgp route select

```
ip ip-prefix voice2 p 125.4.125.1 32
route-policy vp2 p n 10
if-match ip-prefix voice2
apply local-pref 200
bgp 3
peer 125.0.0.245 route-policy vp2 import
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
