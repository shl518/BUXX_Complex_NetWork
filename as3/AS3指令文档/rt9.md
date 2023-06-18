# rt9

## common
```
sys
sysn rt9
inter g 0/0/0
ip addr 125.3.8.9 24
inter g 0/0/1
ip addr 125.3.9.9 24
ospf cost 5
router id 3.1.1.9
inter l 1
ip addr 192.168.3.9 32
ospf
area 0
network 125.3.8.9 0.0.0.255
network 125.3.9.9 0.0.0.255
network 125.3.12.253 0.0.0.3
network 125.3.13.249 0.0.0.3
network 192.168.3.9 0.0.0.0
quit
quit
```

## ppp
```
aaa
local-user oto password cipher abracadabra
local-user oto service-type ppp
local-user oto priviledge level 8
quit
inter s 4/0/0
link-protocol ppp
ppp authentication-mode chap
ppp chap user oto
ip addr 125.3.12.253 30
inter s 4/0/1
link-protocol ppp
ppp authentication-mode chap
ppp chap user oto
ip addr 125.3.13.249 30
```

## smnp
```
snmp-agent trap source loop 1
snmp-agent group v3 buaa authentication
snmp-agent usm-user v3 oto buaa authentication-mode sha abaracadabra
snmp-agent target-host trap-hostname nym address 192.168.0.1 trap-paramsname buaa
snmp-agent trap enable
```
