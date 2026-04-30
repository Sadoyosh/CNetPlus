Golden Rule of Network: Mali ko, Kasalanan mo!

Task1: Hardware and Software

compmgmt.msc

vmdk - virtual disk

Credentials IR-ElasticSys:

ElasticS: localhost:5601
 User: admin
 Pass: C1sc0123

OTRS Admin: 192.168.102.133/otrs/index.pl
 User: admin
 Pass: C1sc0123

OTRS User: 192.168.102.133/otrs/customer.pl
 User: user1
 Pass: C1sc0123

Cisco:
ss 	sh start
sr 	sh run
siib 	sh ip int brief
svb 	sh vlan brief

git clone https://github.com/rivancorp/ccna2

create 4 VLANs:
conf t
vlan 10 
name wifivlan
vlan 50
name ipcameravlan
vlan 100
name voicevlan
end
sh vlan brief

HOW TO USE 7 OSI LAYER TO CONFIGURE A CALLCENTER:

L1:PHYSICAL: 802.3AT OR 802.3AF POE (Standard)
L2: MAC ADDRESS: + VOICEVLAN = 100
L3: IP ADDRESS:
L4: session initiation protocol: sip: 5060
    skinny client control protocol: 2000

L5:RTP: real time transport protocol
L6: codec: g711, g729, h323
L7: CISCO UNIFIED CALLmanager: APP

creating/config IVRS: Interactive voice response system:

Sample voice:
"welcome to team rivan, the best IT training in the universe, press 1 for sales, press 2 to enroll, press 3 for reception or stay on the line."

step1: .wav[phon to .au[cisco]

use IAC to automate:

IAC-AP-12# --> WIFIAP-92
SSID---------> SOLAIREWIFI-92
CHANNEL------> "1-13"

how to master ipv4/ipv6:

Pera/Pesos 	ipv4		ipv6
0-9		0-255		0-f

4999		4.255.255.255	:4fff:
5000		5.0.0.0		:5000:	
5001		5.0.0.1		:5001:

2999		2.255.255.255	:2fff:
3000		3.0.0.0		:3000:
3001		3.0.0.1		:3001:

finalboss:

7908		7.255.0.254	:7f0e:
7909		7.255.0.255	:7f0f:
7910		7.255.1.0	:7f10:

superfinalboss:

6098		6.0.255.254	:60fe:
6099	     	6.0.255.255	:60ff:
6100		6.1.0.0		:6100:

