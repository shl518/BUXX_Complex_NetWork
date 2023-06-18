# rt1
## common
```
sys
sysn rt1
inter g 0/0
ip addr 125.1.2.1 24
inter g 0/1
ip addr 125.1.3.1 24
inter se 1/0
ip addr 125.0.0.253 30
inter loop 0
ip addr 1.1.1.1 32
inter loop 1
ip addr 192.168.1.1 32
quit
router id 1.1.1.1
ospf
preference ase 200
area 0
network 125.1.2.1 0.0.0.255
network 125.1.3.1 0.0.0.255
network 1.1.1.1 0.0.0.0
network 192.168.1.1 0.0.0.0
import-route bgp
quit
```

## ibgp
```
bgp 1
group as1 internal
peer 1.1.1.2 group as1
peer 1.1.1.3 group as1
peer 1.1.1.4 group as1
peer 1.1.1.5 group as1
peer as1 connect-interface LoopBack 0
peer 125.0.0.254 as-number 2
address-family ipv4 unicast
peer as1 next-hop-local
peer as1 enable
peer 125.0.0.254 enable
```

## ebgp
```
bgp 1
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

## smnp
```
snmp-agent trap source loop 1
snmp-agent group v3 buaa authentication
snmp-agent usm-user v3 oto buaa authentication-mode sha abaracadabra
snmp-agent target-host trap-hostname nym address 192.168.0.1 trap-paramsname buaa
snmp-agent trap enable
```