Physical Layer (L1)
-Voltage
-Interface
 -Copper
 -Laser
 -RF(Radio Frequency)
-Transmission

Data Link Layer (L2)
MAC Address - SRC MAC, and DEST. MAC (Ethernet Frames)
-CSMA/CD (Collision Detection)
-CSMA/CA (Collision Avoidance) - Wifi

Network Layer (L3)
SRC IP, DEST IP
-Packets De-encapsulation

Transport Layer (L4)
TFTP UDP (port 69)
     TCP (Port 2000 or 5060(SiP))

Session Layer (L5)
RTP

Presentation Layer (L6)
File Formats (jpeg, txt, png and etc.)
Codecs:
G711
G729
H323

Application Layer (L7)
Voice or Picture You see or hear

!@Corebaba (Port mirroring config)
conf t
 monitor session 1 source int fa0/3,fa0/5,fa0/7
 monitor session 1 dest int fa0/1,fa0/9
 end

clear ip nat trans *
conf t
no ip nat inside source static 192.168.103.21 208.8.8.51
no ip nat inside source static 192.168.103.22 208.8.8.52
end

config t
no access-list 8
access-list 8 permit any
Int Gi 3
 ip nat Inside
Int gi 1
 ip nat Outside
IP Nat inside source static tcp 192.168.103.21 80 208.8.8.100 8080
IP Nat inside source static tcp 192.168.103.21 443 208.8.8.100 8443
IP Nat inside source static tcp 192.168.103.22 80 208.8.8.100 80
IP Nat inside source static tcp 192.168.103.22 443 208.8.8.100 443
IP nat inside source list 8 int gi 1 Overload
end
show ip nat translation

!@WEBS-1,WEBS-2,WEBS-3
sudo su

conf t
 IP Nat inside source static tcp 192.168.103.21 22 208.8.8.100 2222
 IP Nat inside source static tcp 192.168.103.22 22 208.8.8.100 6969
 end

conf t
 IP Nat inside source static tcp 192.168.103.23 80 208.8.8.200  4567
 IP Nat inside source static tcp 192.168.103.23 443 208.8.8.200 1234
 IP Nat inside source static tcp 192.168.103.23 22 208.8.8.200 8022
 end

Exercise

192.168.103.23 80 > 208.8.8.200
192.168.103.23 443 > 1234
192.168.103.23 22 > 

Site-Site VPN

!@BLDG-PH
sudo su
ifconfig eth0 10.11.11.101 netmask 255.255.255.224 up
route add default gw 10.11.11.113
ping 10.11.11.113

!@BLDG-JP
sudo su
ifconfig eth0 10.21.21.211 netmask 255.255.255.240 up
route add default gw 10.21.21.213
ping 10.21.21.213

UTM-PH = 192.168.102.11
UTM-JP = 192.168.102.12

VPN - CIA Tria
-Confidentiality
-Integrity (hash values)
 -sha-256
 -merkle tree
-Availability


Create Priv and Pub Key

!@UTM-PH
conf t
 ip domain name net.com
 crypto key generate rsa modulus 2048 label puki exportable
 ip ssh version 2
 crypto key export rsa puki
 end

!@UTM-JP
conf t
 ip domain name net.com
 crypto key generate rsa modulus 2048 label puki exportable
 ip ssh version 2
 crypto key export rsa puki
 end


Find the Network:
10.11.11.101 /27
1. /27 (4th, 32i)


For Network MONITORING
http://208.8.8.133:5601

!@UTM-PH,JP
conf t
 no int tunnel1
 !
 no ip route 10.21.21.208 255.255.255.240 Tunnel1
 
conf t
 no int tunnel1
 !
 no ip route 10.11.11.96 255.255.255.224 Tunnel1

*************************
conf t
NO IP access-list Extended FWP1
IP access-list Extended FWP1
 Permit tcp Any host www.web310.com eq 80 log
 Permit tcp Any host www.web310.com eq 443 log
 Permit icmp Any host www.web310.com log
 Permit tcp Any host www.web311.com eq 53 log
 Permit tcp Any host www.web311.com eq 443 log
 Permit tcp Any host www.web311.com eq 22 log
 Int Gi 3
  ip access-group FWP1 in


conf t
NO IP access-list Extended WAF2
IP access-list Extended WAF2
 Permit udp Any host www.web310.com eq 123 log
 Permit tcp Any host www.web310.com eq 22 log
 Permit tcp Any host www.web310.com eq 53 log
 Permit tcp Any host www.web310.com eq 80 log
 Permit tcp Any host www.web310.com eq 25 log
 Permit icmp Any host www.web311.com log
 Permit tcp Any host www.web311.com eq 23 log
 Permit tcp Any host www.web311.com eq 22 log
 Permit tcp Any host www.web311.com eq 443 log
 Int Gi 3
  ip access-group WAF2 in

LOGGING
!@UTM-PH
conf t
 logging host 192.168.102.133 transport udp port 9001
 logging source-interface g2
 logging on

conf t
 service timestamps log datetime msec
 service sequence-numbers
 archive
 log config
 notify syslog
 end
