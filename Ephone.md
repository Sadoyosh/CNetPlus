Para sa TELUSPETRON
config t
vlan 13
 name TELUSPETRON.com
 exit
Int vlan 13
 IP OSPF 1 AREA 0
 no shut
 ip add 10.0.32.1 255.255.224.0
ip dhcp excluded-add 10.0.32.1 10.0.32.100
ip dhcp pool TELUSPETRON.com
 network 10.0.32.0 255.255.224.0
 default-router 10.0.32.1
 domain-name TELUSPETRON.com
 dns-server 10.92.1.10
 option 150 ip 10.92.100.8
 Int Fa 0/5
  swi Voice vlan 13
  do sh ip dhcp binding

Para sa Meralco:
config t
vlan 12
 name HAYOPMERALCO.com
 exit
Int vlan 12
 IP OSPF 1 AREA 0
 no shut
 ip add 10.0.16.1 255.255.240.0
ip dhcp excluded-add 10.0.16.1 10.0.16.100
ip dhcp pool HAYOPMERALCO.com
 network 10.0.16.0 255.255.240.0
 default-router 10.0.16.1
 domain-name HAYOPMERALCO.com
 dns-server 10.92.1.10
 option 150 ip 10.92.100.8
 Int Fa 0/7
  swi Voice vlan 12
  do sh ip dhcp binding

