
zabbix

dnf install net-snmp-utils-y


!@firewall1k
conf t
 int g1
 ip addr dhcp
 no shut
 end
 show ip int br

!@firewall1k
snmpv2
conf t
access-list 10 permit 208.8.8.133
snmp-server community public RO 10

!@no shut/dc/timeout configuration
conf t
line vty 0 14
exec-timeout 0 0
login local
end

snmpv3
conf t
snmp-server group zabbix v3 priv
snmp-server user admin zabbix v3 auth sha C1sc0123 priv aes 128 C1sc0123

!@zabbix
sudo systemctl restart zabbix-server

**************************************

RADIUS AAA [ shell:priv-lvl=15 ]

!@corebaba
conf t
username admin privilege 15 secret pass
aaa new-model
radius server WINRAD
address ipv4 10.92.1.8 auth-port 1812 acct-port 1813
key aaaaaaaa
aaa group server radius RADGROUP
server name WINRAD
exit
aaa authentication login default group RADGROUP local
aaa authorization exec default group RADGROUP local
line vty 0 14
login authentication default
end

!@run command
diskmgmt.msc


