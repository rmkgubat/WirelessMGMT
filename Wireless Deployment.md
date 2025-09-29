
<!-- Monitor Number = #$34T# -->

### Exercise 01: Design and implement a network for SOC-GROUP with a maximum of 45 users.
- Use the available network address 10.#$34T#.11.0/24  
- Reserve the first 10 IPs  
- Use VLAN 11 for the network.  
- Make sure clients can connect from both wired, and wireless devices.  
- Verify by connecting on mobile and checking if you got the correct IP from the DHCP Server.  

<br>

<details>
<summary>Show Answer</summary>

C: 45 users = 6 bits  
S: 32 - 6 = /26 (4th, 64i)  
I:  
  - 10.#$34T#.11.0 255.255.255.192  
  - 10.#$34T#.11.64 255.255.255.192   

<br>

__NETWORK ADDRESS: `10.#$34T#.11.0 255.255.255.192`__  

<br>

~~~
!@CoreBABA
conf t
 vlan 11
  name SOC-GROUP
  exit
 int vlan 11
  description SOC-GROUP
  ip add 10.#$34T#.11.4 255.255.255.192
  ip ospf 1 area 0
  no shut
 !
 ip dhcp excluded-address 10.#$34T#.11.1 10.#$34T#.11.10
 ip dhcp pool SOC-GROUP
  network 10.#$34T#.11.0 255.255.255.192
  default-router 10.#$34T#.11.4
  domain-name SOC-GROUP.COM
  dns-server 10.#$34T#.1.10
  end
~~~
	
</details>

<br>
<br>

---
&nbsp;

### Exercise 02: Design and implement a network for NOC-GROUP with a maximum of 27 users.
- Use the available network address 10.#$34T#.12.0/24  
- Reserve the first 10 IPs  
- Use VLAN 12 for the network.  
- Make sure clients can connect from both wired, and wireless devices.  
- Verify by connecting on mobile and checking if you got the correct IP from the DHCP Server.  

<br>

<details>
<summary>Show Answer</summary>

C: 27 users = 5 bits  
S: 32 - 5 = /27 (4th, 32i)  
I:  
  - 10.#$34T#.12.0 255.255.255.224  
  - 10.#$34T#.12.32 255.255.255.224  

<br>

__NETWORK ADDRESS: `10.#$34T#.12.0 255.255.255.224`__  

<br>

~~~
!@CoreBABA
conf t
 vlan 11
  name NOC-GROUP
  exit
 int vlan 11
  description NOC-GROUP
  ip add 10.#$34T#.12.4 255.255.255.224
  ip ospf 1 area 0
  no shut
 !
 ip dhcp excluded-address 10.#$34T#.12.1 10.#$34T#.12.10
 ip dhcp pool NOC-GROUP
  network 10.#$34T#.12.0 255.255.255.224
  default-router 10.#$34T#.12.4
  domain-name NOC-GROUP.COM
  dns-server 10.#$34T#.1.10
  end
~~~
	
</details>

<br>
<br>

---
&nbsp;

### Exercise 04: Modify `SOC-TEAM` Wifi for `Port-Based Authentication (802.1x)`
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

&nbsp;
---
&nbsp;

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
