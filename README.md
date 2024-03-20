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
