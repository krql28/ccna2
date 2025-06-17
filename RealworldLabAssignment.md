Design and configure realworld lab for this diagram:

![image](https://github.com/user-attachments/assets/53e9a9a8-18a7-4c07-b13b-02460f26a0bf)

Task1: For ARMY.MIL.PH
10.0.0.0 subnet to 4500:
c: 4500 is 13bits
s:/32 - /13 = /19; 3rd octet, 32i
i:ipasok si 32i sa  3RD octet
ARMY: 10.0.32.0 /19
1st: 10.0.32.1 last: 10.0.63.255
Not ARMY: 10.0.64.0 /19

##CoreDelta1
config t
vlan 21
 name ARMY.MIL.PH
 exit
Int vlan 21
 IP ospf 1 area 0
 no shut
 ip add 10.0.32.1 255.255.224.0
ip dhcp excluded-add 10.0.32.1 10.0.32.100
ip dhcp pool ARMY.MIL.PH
 network 10.0.32.0 255.255.224.0
 default-router 10.0.32.1
 domain-name ARMY.MIL.PH
 dns-server 10.41.1.10
 option 150 ip 10.41.100.8
( Int Fa 0/5
  swi Voice vlan 11
  do sh ip dhcp binding) ##include if this is set up with physically

  AlacessSW:
  conf t
  int e0/0
  switchport mode access
  switchport access vlan 21
  end
  show vlan brief
  @P1:
  conf t 
  int e0/0
  no shut
  ip address dhcp
  do bp

Task2: For PNP.GOV.PH
10.0.0.0 subnet to 350:
c: 350 is 9bits
s:/32 - /9 = /23; 3rd octet, 2i
i:ipasok si 2i sa  3RD octet
PNP: 10.0.2.0 /23
1st: 10.0.2.1 last: 10.0.3.255
Not PNP: 10.0.4.0 /23

  ##CoreDelta2
config t
vlan 22
 name PNP.GOV.PH
 exit
Int vlan 22
 IP ospf 1 area 0
 no shut
 ip add 10.0.2.1 255.255.254.0
ip dhcp excluded-add 10.0.2.1 10.0.2.100
ip dhcp pool PNP.GOV.PH
 network 10.0.2.0 255.255.254.0
 default-router 10.0.2.1
 domain-name PNP.GOV.PH
 dns-server 10.41.1.10
 option 150 ip 10.41.100.8
 
  AlacessSW:
  conf t
  int e1/0
  switchport mode access
  switchport access vlan 22
  end
  show vlan brief
  @P2:
  conf t 
  int e1/0
  no shut
  ip address dhcp
  do bp
  
