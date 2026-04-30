Day 2 Warm Up Exercise - Find +1 & - 1

	Pera/Pesos		ipv4			ipv6
	0-9			0-255			0-f
-1	4999			4.255.255.255		:4fff:
	5000			5.0.0.0			:5000:
+1	5001			5.0.0.1			:5001:

-1	2999			2.255.255.255		:2fff:
	3000			3.0.0.0			:3000:
+1	3001			3.0.0.1			:3001:

-1	7908			7.255.0.254		:7f0e:
	7909			7.255.0.255		:7f0f:
+1	7910			7.255.1.0		:7f10:

-1	6098			6.0.255.254		:60fe:
	6099			6.0.255.255		:60ff:
+1	6100			6.1.0.0			:6100:


petron: 4500 agents
meralco: 2500 agents
		Petron			Meralco
Convert:	13 Bits			12 bits
subtract32-: 	/19			/20
		3rd,32i			3rd,16i
subnet:		10.0.32.0/19		10.0.16.0/20
1st:		10.0.32.1		10.0.16.1

BC:		10.0.63.255		10.0.31.255
Not Urs:	10.0.64.0/19		10.0.32.0/20

!@CoreBABA
conf t
 int fa0/9
  no sw
  ip add 192.168.69.45 255.255.255.224
  no shut
  end

!@CUCM
conf t
int vlan 1
 ip add 192.168.69.100 255.255.255.224
 no shut
 end

192.168.69.45 / 27
192.168.69.100 /27

Find the Network:

Step 1- Get the Rivan Format nung /
/27 (4th, 32i)

Step 2 -

192.168.69.45 /27
           0
           32 Final answer = 192.168.69.32 /27
           64

192.168.69.100 /27
	   0
           32
           64
           96 Final answer = 192.168.69.96 /27
           128

Example:

1. 172.16.200.82 /30

/30 (4th, 4i)

Final = 172.16.200.80

!@CoreBaba
conf t
 int loopback 1
 ip add 172.16.200.82 255.255.255.252
 end
show ip route | inc C

Exercise:
1.172.16.2.200 /26
/26 (4th, 64i)
172.16.2.192 /26 255.255.255.192

2. 192.168.70.122 /28
/28 (4th, 16i)
192.168.70.112 /28 255.255.255.240

!@cmd
nslookup -type=NS com 170.247.170.2

-DNS Heirarchy

root servers- tldserver
tldserver (.com .net .ph)

A RECORD

CUCM cm.netm.com 10.92.100.8
EDGE ed.netm.com 10.92.92.1
Cam1 c6.netm.com 10.92.50.6
Cam2 c8.netm.com 10.92.50.8
