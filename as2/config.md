## LSW7

```shell
sys
sysn ls7

inter vlan 1
ip addr 125.2.2.254 24
quit

router id 2.2.1.7
inter loop 1
ip addr 192.168.2.135 32
ospf
area 0
network 125.2.2.254 0.0.0.255
network 192.168.2.135 0.0.0.0
```

```
snmp-agent group v3 buaa authentication
snmp-agent usm-user v3 oto buaa authentication-mode sha abaracadabra
snmp-agent trap source loop 1
snmp-agent target-host trap address udp-domain 192.168.0.1 params securityname buaa
snmp-agent trap enable
```



## LSW8

```shell
sys
sysn ls8

inter vlan 1
ip addr 125.2.3.254 24

inter g 0/0/4
port link-type access

vlan 2
port g 0/0/4
inter vlan2
ip addr 192.168.0.1 24
quit
inter loop 1
ip addr 192.168.2.136 32

router id 2.2.1.8
ospf
area 0
network 192.168.0.1 0.0.0.255
network 125.2.3.254 0.0.0.255
network 192.168.2.136 0.0.0.255
```

```
snmp-agent group v3 buaa authentication
snmp-agent usm-user v3 oto buaa authentication-mode sha abaracadabra
snmp-agent trap source loop 1
snmp-agent target-host trap address udp-domain 192.168.0.1 params securityname buaa
snmp-agent trap enable
```

## AR17

```shell
sys
sysn rt17

inter g 0/0/0
ip addr 125.2.2.17 24

inter g 0/0/1
ip addr 125.2.3.17 24

inter g 4/0/0
ip addr 125.0.0.233 24

inter loop 0
ip addr 2.1.1.17 32

inter loop 1
ip addr 192.168.2.17 32
quit

router id 2.1.1.17

ospf
preference ase 200
area 0
network 125.2.2.17 0.0.0.255
network 125.2.3.17 0.0.0.255
network 2.1.1.17  0.0.0.0
network 192.168.2.17 0.0.0.0
import-route bgp
quit

bgp 2
group as2 internal
peer 2.1.1.15 group as2
peer 2.1.1.16 group as2
peer 2.1.1.18 group as2
peer as2 connect-interface LoopBack 0
peer as2 next-hop-local
preference 255 110 110 


peer 125.0.0.234 as-number 4
network 192.168.0.1 24
```

```
snmp-agent trap source loop 1
snmp-agent group v3 buaa authentication
snmp-agent usm-user v3 oto buaa authentication-mode sha abaracadabra
snmp-agent target-host trap-hostname nym address 192.168.0.1 trap-paramsname buaa
snmp-agent trap enable
```



## AR18

```shell
sys
sysn rt18

inter g 0/0/0
ip addr 125.2.3.18 24

inter g 0/0/1
ip addr 125.2.2.18 24

inter g 4/0/0
ip addr 125.0.0.229 24

inter loop 0
ip addr 2.1.1.18 32

inter loop 1
ip addr 192.168.2.18 32
quit

router id 2.1.1.18
ospf
preference ase 200
area 0
network 125.2.2.18 0.0.0.255
network 125.2.3.18 0.0.0.255
network 2.1.1.18 0.0.0.0
network 192.168.2.18 0.0.0.0
import-route bgp
quit


bgp 2
group as2 internal
peer 2.2.1.15 group as2
peer 2.1.1.16 group as2
peer 2.1.1.17 group as2
peer as2 connect-interface LoopBack 0
peer as1 next-hop-local
preference 255 110 110 

peer 125.0.0.230 as-number 4
network 192.168.0.1 24
```

```
snmp-agent trap source loop 1
snmp-agent group v3 buaa authentication
snmp-agent usm-user v3 oto buaa authentication-mode sha abaracadabra
snmp-agent target-host trap-hostname nym address 192.168.0.1 trap-paramsname buaa
snmp-agent trap enable
```

