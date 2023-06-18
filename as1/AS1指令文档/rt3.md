# rt3
## common
```
sys
sysn rt3
inter g 0/0/0
ip addr 125.1.2.3 24
inter g 0/0/1
ip addr 125.1.3.3 24
inter g 0/0/2
ip addr 125.0.0.245 30
inter loop 0
ip addr 1.1.1.3 32
inter loop 1
ip addr 192.168.1.2 32
quit
router id 1.1.1.3
ospf
preference ase 200
area 0
network 125.1.2.3 0.0.0.255
network 125.1.3.3 0.0.0.255
network 1.1.1.3 0.0.0.0
network 192.168.1.3 0.0.0.0
import-route bgp
quit
quit
```

## ibgp
```
bgp 1
group as1 internal
peer 1.1.1.1 group as1
peer 1.1.1.2 group as1
peer 1.1.1.4 group as1
peer 1.1.1.5 group as1
peer as1 connect-interface LoopBack 0
peer as1 next-hop-local
preference 255 110 110 
```

## ebgp
```
peer 125.0.0.246 as-number 3
network 172.16.1.2 24
```

### bgp route select

这里原来写的200.0.0.250？？rt5  peer也不是这个啊

```
ip ip-prefix voice2 p 125.4.125.1 32
route-policy vp2 p n 10
if-match ip-prefix voice2
apply local-pref 200
bgp 1
peer 125.0.0.246 route-policy vp2 import
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

