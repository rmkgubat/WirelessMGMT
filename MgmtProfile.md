
### Exercise 01: Create WLANs for SOC-TEAM on VLAN 11. Verify by connecting on mobile and checking if you got the correct IP from the DHCP Server.
NETWORK ADDRESS: 10.92.11.0/24

~~~
!@CoreBABA
conf t
 vlan 11
  name SOC-TEAM
  exit
 int vlan 11
  description SOC-TEAM-GW
  ip add 10.92.11.4 255.255.255.0
  ip ospf 1 area 0
  no shut
 !
 ip dhcp excluded-address 10.92.11.1 10.92.11.100
 ip dhcp pool SOCPOOL
  network 10.92.11.0 255.255.255.0
  default-router 10.92.11.4 255.255.255.0
  domain-name SOC-TEAM.COM
  dns-server 10.92.1.10
  end
~~~

<br>
---
<br>

### Exercise 02: Create WLANs for THREAT-HUNTERS on VLAN 12. Using the network address 10.92.12.0/24

~~~
!@CoreBABA
conf t
 vlan 12
  name THREAT-HUNTERS
  exit
 int vlan 12
  description THREAT-HUNTERS-GW
  ip add 10.92.12.4 255.255.255.0
  ip ospf 1 area 0
  no shut
 !
 ip dhcp excluded-address 10.92.12.1 10.92.12.100
 ip dhcp pool THUNTPOOL
  network 10.92.12.0 255.255.255.0
  default-router 10.92.12.4 255.255.255.0
  domain-name THUNT.COM
  dns-server 10.92.1.10
  end
~~~

### Exercise 03: Modify SOC-TEAM Wifi for Port-Based Authentication (802.1x)

