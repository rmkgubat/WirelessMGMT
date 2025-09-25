
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
Prerequisites  
- Windows Server 2022 VM  
  - Static IP addressing  
    - IP: 10.#$34T#.1.8  
	- Mask: 255.255.255.0  
	- Gateway: None  
	- DNS: 127.0.0.1  
  - DNS Suffix  
    - Suffix: rivanm.com  

- Disabled Firewall  
- Rename Computer  

Restart the Computer to Apply changes  

<br>
---
<br>

### Install the necessary roles and features
1. Active Directory Domains and Services 
  - Promote this server to a domain controller. 
    - Add a new forest: This MUST be your DNS suffix: rivanm.com 
	 - Add a DSRM password: C1sc0123 
	 - Do NOT create DNS delegation 
	 - Allow NetBIOs to resolve the name 
	 - Leave Paths as default 
	
	 - Install

<br>

2. Network Policy Server

<br>

3. Active Directory Certificate Authority
