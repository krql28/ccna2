Design and configure realworld lab for this diagram:

![image](https://github.com/user-attachments/assets/53e9a9a8-18a7-4c07-b13b-02460f26a0bf)

Task1:
10.0.0.0 subnet to 700:
c: 700 is 10bits
s:/32 - /10 = /22; 3rd octet, 4i
i:ipasok si 4i sa 3rd octet
sykes: 10.0.4.0 /22
1st: 10.0.4.1 last: 10.0.7.255
Not sykes: 10.0.8.0 /22

##CoreDelta1
config t
vlan 11
 name SKYESasia.COM
 exit
Int vlan 11
 IP ospf 1 area 0
 no shut
 ip add 10.0.4.1 255.255.252.0
ip dhcp excluded-add 10.0.4.1 10.0.4.100
ip dhcp pool SKYESasia.COM
 network 10.0.4.0 255.255.252.0
 default-router 10.0.4.1
 domain-name SKYESasia.COM
 dns-server 10.41.1.10
 option 150 ip 10.41.100.8
( Int Fa 0/5
  swi Voice vlan 11
  do sh ip dhcp binding) ##include if this is set up with physically

  AlacessSW:
  conf t
  int e0/0
  switchport mode access
  switchport access vlan 11
  end
  show vlan brief
  @P1:
  conf t 
  int e0/0
  no shut
  ip address dhcp
  do bp

For 2900 TELUS

  ##CoreDelta2
config t
vlan 12
 name TELUS.COM
 exit
Int vlan 12
 IP ospf 1 area 0
 no shut
 ip add 10.0.16.1 255.255.240.0
ip dhcp excluded-add 10.0.16.1 10.0.16.100
ip dhcp pool TELUS.COM
 network 10.0.16.0 255.255.240.0
 default-router 10.0.16.1
 domain-name TELUS.COM
 dns-server 10.41.1.10
 option 150 ip 10.41.100.8
 
  AlacessSW:
  conf t
  int e1/0
  switchport mode access
  switchport access vlan 12
  end
  show vlan brief
  @P2:
  conf t 
  int e1/0
  no shut
  ip address dhcp
  do bp
  
