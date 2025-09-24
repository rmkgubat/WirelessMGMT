
IP Addresses:
 C9800-CL = 10.92.1.7
 Azure-CL = 10.92.1.8
 
<br>
<br>

### Setup L3 Switch

~~~
!@CSwitch
conf t
 hostname CSwitch-92
 enable secret pass
 service password-encryption
 no logging console
 no ip domain lookup
 line cons 0
  password pass
  no login
  exec-timeout 0 0
  logging synchronous
 line vty 0 14
  password pass
  login
  exec-timeout 0 0
 !
 !
 vlan 10
  name WIRELESS
  exit
 int vlan 1
  ip add 10.92.1.4 255.255.255.0
  no shut
 int vlan 10
  ip add 10.92.10.4 255.255.255.0
  no shut
 !
 !
 int range fa0/2,fa0/4
  switchport mode access
  switchport access vlan 10
  exit
 !
 !
 ip routing
 !
 !
 ip dhcp excluded-address 10.92.1.1 10.92.1.100
 ip dhcp excluded-address 10.92.10.1 10.92.10.100
 ip dhcp pool MGMTPOOL
  network 10.92.1.0 255.255.255.0
  default-router 10.92.1.4 255.255.255.0
  dns-server 10.92.1.10
  domain-name MGMT.COM
 ip dhcp pool WIFIPOOL
  network 10.92.10.0 255.255.255.0
  default-router 10.92.10.4 255.255.255.0
  dns-server 10.92.1.10
  domain-name WIFI.COM 
  option 43 ip 10.92.1.7
  end
~~~

<br>
<br>

---
&nbsp;

### Setup C9800-Cloud

1. Open the VM: C9800-CL-universalk9_vga.17.15.03.ovf

![01](img/01.JPG)

&nbsp;
---
&nbsp;

2. Set the Name

![02](img/02.JPG)

&nbsp;
---
&nbsp;

3. Specify deployment size

![03](img/03.JPG)

&nbsp;
---
&nbsp;
