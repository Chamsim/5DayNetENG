Corebaba
10.41.1.4
CallManager
10.41.100.8

meraki dashboard
rivancybersec2@outlook.com
C1sc0123


D1#show ip route !@show IP Route@!  
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area 
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       + - replicated route, % - next hop override
Gateway of last resort is not set
      10.0.0.0/8 is variably subnetted, 6 subnets, 3 masks
C        10.1.4.4/30 is directly connected, Ethernet1/1
L        10.1.4.6/32 is directly connected, Ethernet1/1
C        10.2.1.0/24 is directly connected, Vlan10
L        10.2.1.1/32 is directly connected, Vlan10
C        10.2.2.0/24 is directly connected, Vlan20
L        10.2.2.1/32 is directly connected, Vlan20
      192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.1.128/27 is directly connected, Vlan200
L        192.168.1.129/32 is directly connected, Vlan200



@@VPN Configuration@@
@JP
config t
no logging console
no ip domain lookup
ip route 0.0.0.0 0.0.0.0 200.0.0.20

int gi1
ip add 200.0.0.10 255.255.255.0
no shut
int gi3
ip add 10.10.10.1 255.255.255.0
no shut

@PH
config t
no logging console
no ip domain lookup
ip route 0.0.0.0 0.0.0.0 200.0.0.10

int gi1
ip add 200.0.0.20 255.255.255.0
no shut
int gi3
ip add 10.20.20.1 255.255.255.0
no shut

git clone https://github.com/rivan16/sshansible


task 2: most important day for all 5 hands on lab exam

q1 give internet to your vpn router using 192.168.108.2 as gate way and 108.8 as you Gi 1 ip add

@vpnPH:
conf t
int Gi 1
no shut 
ip add 192.168.108.8 255.255.255.0
ip route 0.0.0.0 0.0.0.0 192.168.108.2
ip route 0.0.0.0 0.0.0.0 192.168.108.4 20


q2 give your vpnph a domain name and dns server 8.8.8.8

conf t
ip domain name ccna.com
ip name-server 8.8.8.8 1.1.1.1


q3 create a standard access-list (1-99)
create a layer 3(network: ip address) fw to block top 3 porn sites

ping pornhub.com 66.254.114
ping faketaxi.com 66.254.114
ping bangbros.com 66.254.114
ping pornhat.com 172.67.74
ping cumloader.com 172.67.74
ping porntube.com 104.23.135
ping pornburst.com 104.21.235.97

conf t 
no access-list 1
access-list 1 deny 66.254.0.0 0.0.255.255
access-list 1 deny 172.67.0.0 0.0.255.255
access-list 1 deny 104.23.0.0 0.0.255.255
access-list 1 deny 104.21.0.0 0.0.255.255
access-list 1 permit any
do sh ip access-list NOPORN

conf t 
no IP access-list standard NOPORN
IP access-list standard NOPORN
deny 66.254.0.0 0.0.255.255
deny 172.67.0.0 0.0.255.255
deny 104.23.0.0 0.0.255.255
deny 104.21.0.0 0.0.255.255
permit any
do sh ip access-list

how to lock a interface using ACL
conf t 
int gi 1
ip access-group NOPORN in 
do sh ru int gi 1

q4 using network using network address translation give internet to BLDGPH1 and BLDGPH2

what is NAT: 
3 steps to NAT:
give static address to buildings
@VPNPH
conf t 
int gi 2 
no shut
ip add 192.168.102.8 255.255.255.0

@bldgph1
sudo ifconfig eth0 192.168.102.11 netmask 255.255.255.0 up
sudo route add default gw 192.168.102.8

@bldgph 2
sudo ifconfig eth0 192.168.102.12 netmask 255.255.255.0 up
sudo route add default gw 192.168.102.8


how to implement real world NAT

conf t 
int gi 1
ip NAT outside
int gi 2
ip NAT inside
!@create ACL to permit all 192.168.102.x
access-list 2 permit 192.168.102.0 0.0.0.255
!@create a static NAT pool for .11 and .12
ip nat inside source static 192.168.102.11 192.168.108.69
ip nat inside source static 192.168.102.12 192.168.108.88
ip nat inside source list 2 int gi 1 overload
!@para sa ibang future bldg 

do sh ip nat translation


config t
no IP access-list standard NOSKUL
ip access-list standard NOSKUL
deny 110.34.0.0 0.0.255.255
deny 162.241.0.0 0.0.255.255
deny 166.62.0.0 0.0.255.255
deny 208.97.0.0 0.0.255.255
permit any
do sh ip access-list NOPORN
int gi 1
no ip access-group NOPORNPORN in 
ip access-group NOSKUL in


EXAM Q3: Protect your website and app with firewall

how to be a Cybersecurity Analyst
1. master OSI layer
2. learn hacking tools: NMAP, nessus, Metasploit, AirCrack, etc.
3. join capture the flags
config t 
ip host www.web8.com 192.168.102.8
ip host www.web9.com 192.168.102.9
int gi 2
 ip add 192.168.102.9 255.255.255.0 Secondary
service finger
service tcp-small-servers
service udp-small-servers
ip dns server
ip http server
ip http secure-server
end


ex4 create a firewall policy to protect web8 and web9 with these condition
web8 is a web and secureweb server
web9 is an ssh and dns server
solution:use extended ACL 100-199
@VPN: protocol Hacker Victom Port
config t
no access-list 100 
access-list 100 permit tcp any host www.web8.com eq 80
access-list 100 permit tcp any host www.web8.com eq 443
access-list 100 permit tcp any host www.web8.com eq 23
access-list 100 permit tcp any host www.web9.com eq 80
access-list 100 permit tcp any host www.web9.com eq 22
access-list 100 permit tcp any host www.web9.com eq 53
!!!access-list 100 deny ip any any matic na yan, Tanga
int gi 2
ip access-group 100 in
do sh ip access-list 100

another method
config t
no ip access-list extended FWPOLICY1
ip access-list extended FWPOLICY1
permit tcp any host www.web8.com eq 80
permit tcp any host www.web8.com eq 443
permit tcp any host www.web9.com eq 22
permit tcp any host www.web9.com eq 53
int gi 2
ip access-group FWPOLICY1 in
advance level: softwareCracking.

ex 2 create a FWPOLICY2 to allow these conditions
open ping, dns, https on web 8 = 3 line
open everything on web 9 = 1 line
config t 
no ip access-list extended FWPOLICY2
ip access-list extended FWPOLICY2
permit icmp any host www.web8.com 
permit tcp any host www.web8.com eq 53
permit tcp any host www.web8.com eq 443
permit ip any host www.web9.com 
int gi 1
ip access-group FWPOLICY2 in
do sh ip access-list FWPOLICY2
