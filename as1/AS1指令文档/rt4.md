# rt4
## common
```
sys
sysn rt4
inter g 0/0/0
ip addr 125.1.2.4 24
inter g 0/0/1
ip addr 125.1.3.4 24
inter g 0/0/2
ip addr 125.0.0.241 30
inter loop 0
ip addr 1.1.1.4 32
inter loop 1
ip addr 192.168.1.4 32
quit
router id 1.1.1.4
ospf
preference ase 200
area 0
network 125.1.2.4 0.0.0.255
network 125.1.3.4 0.0.0.255
network 1.1.1.4 0.0.0.0
network 192.168.1.4 0.0.0.0
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
peer 1.1.1.3 group as1
peer 1.1.1.5 group as1
peer as1 connect-interface LoopBack 0
peer as1 next-hop-local
preference 255 110 110 
```

## ebgp
```
peer 125.0.0.242 as-number 3
network 172.16.1.2 24
```

## smnp
```
snmp-agent trap source loop 1
snmp-agent group v3 buaa authentication
snmp-agent usm-user v3 oto buaa authentication-mode sha abaracadabra
snmp-agent target-host trap-hostname nym address 192.168.0.1 trap-paramsname buaa
snmp-agent trap enable
```
